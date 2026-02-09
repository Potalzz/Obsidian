# X-Ray Scanner Shader: GPU 기반 실시간 스캔 이펙트

**지원 직군**: Technical Artist
**지원 회사**: Pearl Abyss
**작성자**: [이름]
**연락처**: [이메일 / 전화번호]
**작성일**: 2026년 2월

---

## 1. 프로젝트 개요

텍스처 없이 순수 수학 함수만으로 렌더링되는 실시간 X-Ray 스캔 이펙트입니다. `distance()`, `smoothstep()`, `frac()`, `pow()` 등 HLSL 내장 함수의 조합으로 스캔 웨이브, 프로시저럴 그리드, 프레넬 림 라이팅을 구현하며, 마우스 클릭 지점에서 동심원이 확장되는 인터랙티브 시스템을 포함합니다.

![[Pasted image 20260210045803.png]]

| 지표 | 수치 |
|------|------|
| Fragment Shader 명령어 수 | ~35-40 instructions |
| 텍스처 페치 | 0회 |
| 분기문 (if/branch) | 0개 |
| 메모리 대역폭 | 레지스터만 사용 |
| 좌표 공간 | World Space (씬 전역 일관성) |

---

## 2. 기술적 설계 철학

이 섹션에서는 각 설계 결정의 **이유**를 GPU 아키텍처 관점에서 설명합니다. 모든 원리는 HLSL/GLSL 범용 지식이며, Unity뿐 아니라 프로프라이어터리 엔진(BlackSpace Engine 등)에서도 동일하게 적용됩니다.

### 2.1 왜 World Space인가

| 좌표 공간 | 원점 | 특성 | 적합 용도 |
|-----------|------|------|-----------|
| Object Space | 모델 중심 | 오브젝트별 독립 | 캐릭터 애니메이션, 로컬 이펙트 |
| **World Space** | **씬 원점** | **씬 전역 일관성** | **전역 이펙트, 날씨, 스캔** |
| View Space | 카메라 위치 | 카메라 종속 | 포스트 프로세싱, DOF |
| Clip Space | NDC (-1~1) | 투영 후 정규화 | 래스터라이제이션 |

**선택 이유**: 스캔 이펙트는 씬 내 모든 오브젝트에 동일한 원형 파동이 통과해야 합니다. Object Space를 사용하면 각 오브젝트가 자체 좌표를 기준으로 거리를 계산하므로, 오브젝트마다 별도의 링이 생성되어 시각적 일관성이 깨집니다. World Space에서는 하나의 `_ScannerCenter` 좌표로부터 씬 전체에 걸친 단일 파동이 형성됩니다.

```hlsl
// Vertex Shader: Object Space → World Space 변환
// unity_ObjectToWorld = Model Matrix (엔진 비종속: mul(ModelMatrix, vertex))
o.worldPos = mul(unity_ObjectToWorld, v.vertex).xyz;
```

이 변환은 DirectX의 `mul(World, position)`, OpenGL의 `modelMatrix * position`과 동일한 연산입니다. 엔진이 제공하는 행렬 이름만 다를 뿐, 4x4 행렬 곱셈이라는 본질은 변하지 않습니다.

### 2.2 왜 브랜치리스(Branchless)인가

GPU는 **SIMD(Single Instruction, Multiple Data)** 아키텍처로 동작합니다. 픽셀들은 32개(NVIDIA Warp) 또는 64개(AMD Wavefront) 단위로 묶여 **동일한 명령어**를 동시에 실행합니다.

**if문이 발생시키는 문제 — Warp Divergence**:

```
// 위험: if문 사용 시
if (distance < radius)  // Warp 내 16개는 true, 16개는 false
    color = scanColor;  // → true 그룹 실행, false 그룹 대기
else
    color = black;      // → false 그룹 실행, true 그룹 대기
// 결과: 순차 실행 = 50% 성능 손실
```

**본 프로젝트의 해결책 — smoothstep()**:

```hlsl
// 안전: smoothstep은 수학 함수 (FMAD 명령어)
float wave1 = smoothstep(innerEdge, _ScanRadius, distanceFromCenter);
float wave2 = smoothstep(outerEdge, _ScanRadius, distanceFromCenter);
float scanWave = wave1 * wave2;
// → 모든 픽셀이 동일 명령어 실행 = 100% Warp 효율
```

`smoothstep(a, b, x)`는 Hermite 보간 함수로, 내부적으로 `t*t*(3-2t)` 다항식을 계산합니다. 결과는 `[a, b]` 범위 밖에서 0 또는 1로 자연스럽게 수렴하므로, 조건 분기 없이도 영역 안/밖을 구분할 수 있습니다. 또한 1차 도함수가 연속(C1 continuous)이므로 경계에서 앨리어싱이 발생하지 않습니다.

이 원리는 **어떤 셰이딩 언어에서든 동일**합니다. GPU의 SIMD 실행 모델은 하드웨어 수준의 제약이므로, 자체 엔진이든 상용 엔진이든 브랜치리스 설계가 성능에 미치는 영향은 같습니다.

### 2.3 왜 프로시저럴(Procedural)인가

셰이더의 병목은 크게 **ALU(산술 연산)**와 **TEX(텍스처 페치)**로 나뉩니다.

| 항목 | 텍스처 기반 | 프로시저럴 (본 프로젝트) |
|------|------------|----------------------|
| 메모리 대역폭 | 텍스처 캐시 사용 (L1/L2 miss 시 수백 사이클) | **대역폭 0** |
| 해상도 독립성 | 텍스처 해상도에 종속 | **무한 해상도** |
| 연산 비용 | 1 TEX fetch = ~4-8 ALU | `frac()` + `pow()` = ~3-4 ALU |
| Occupancy | 레지스터 + 텍스처 유닛 점유 | **레지스터만 사용 → 높은 Occupancy** |

```hlsl
// 프로시저럴 그리드: 텍스처 없이 수학만으로 격자 생성
float3 gridPattern = frac(i.worldPos * gridFrequency);  // 0~1 반복 패턴
float gridValue = (gridPattern.x + gridPattern.y + gridPattern.z) / 3.0;
float gridLines = pow(1.0 - gridValue, 3.0);  // 대비 증가
```

`frac(x) = x - floor(x)`는 입력값의 소수 부분만 추출하여 0~1이 무한 반복되는 패턴을 생성합니다. 이후 `pow()`로 값 분포를 비선형 변환하면 격자선의 대비가 증가합니다. 전체 과정이 ALU 연산(FMAD + SFU)으로만 이루어지므로 텍스처 유닛을 전혀 사용하지 않습니다.

프로시저럴 패턴은 **텍스처 에셋에 종속되지 않으므로** 엔진 간 포팅이 즉시 가능합니다. 에셋 파이프라인의 차이와 무관하게 `frac()`, `pow()` 함수만 있으면 동일한 결과를 재현할 수 있습니다.

---

## 3. 셰이더 아키텍처 상세

전체 렌더링 파이프라인의 흐름:

```
Vertex Shader (per-vertex, ~10K회):
├── Object Space → Clip Space (래스터라이제이션용)
├── Object Space → World Space (이펙트 계산용)
└── Normal → World Normal (프레넬 계산용)

하드웨어 보간기 (Interpolator):
└── worldPos, worldNormal을 프래그먼트별로 선형 보간

Fragment Shader (per-pixel, ~1M회):
├── Fresnel: normalize + dot + pow          [3-4 instr]
├── Distance: 1x sqrt via distance()        [1 instr]
├── Scan Ring: 2x smoothstep                [2 instr]
├── Grid: frac + pow                        [3-4 instr]
├── Color: wave + grid + rim (additive)     [3 instr]
└── Alpha: base + scan + fresnel + saturate [4 instr]
```

### 3.1 버텍스 셰이더 — 좌표 변환과 보간기 설계

```hlsl
v2f vert (appdata v)
{
    v2f o;
    o.vertex = UnityObjectToClipPos(v.vertex);      // → mul(MVP, position)
    o.worldPos = mul(unity_ObjectToWorld, v.vertex).xyz;  // → mul(M, position)
    o.worldNormal = UnityObjectToWorldNormal(v.normal);   // → mul((M^-1)^T, n)
    return o;
}
```

![[Pasted image 20260210045824.png]]

**설계 의도**: 모든 좌표 변환을 버텍스 셰이더에서 수행하고, 결과를 보간기(Interpolator)를 통해 프래그먼트로 전달합니다. 프래그먼트에서 행렬 곱셈을 하면 픽셀당 4x4 MUL이 실행되므로 비용이 급증합니다. 버텍스에서 한 번만 계산하고 하드웨어가 자동으로 보간하는 것이 효율적입니다.

노멀 벡터의 월드 변환에는 **역전치 행렬(Inverse Transpose)**을 사용합니다. 비균등 스케일이 적용된 오브젝트에서 단순 모델 행렬로 노멀을 변환하면 방향이 왜곡되기 때문입니다. 이는 `UnityObjectToWorldNormal()`이 내부적으로 처리하며, DirectX/커스텀 엔진에서는 `mul((float3x3)transpose(InverseModel), normal)`로 동일하게 구현합니다.

### 3.2 스캔 웨이브 — Dual Smoothstep 링

스캔 링은 `_ScanRadius`를 중심으로 `_ScanWidth` 범위에서만 밝아지는 동심원입니다.

```hlsl
float distanceFromCenter = distance(i.worldPos, _ScannerCenter.xyz);

float innerEdge = _ScanRadius - _ScanWidth;
float outerEdge = _ScanRadius + _ScanWidth;

float wave1 = smoothstep(innerEdge, _ScanRadius, distanceFromCenter);  // 0→1
float wave2 = smoothstep(outerEdge, _ScanRadius, distanceFromCenter);  // 1→0
float scanWave = wave1 * wave2;  // 중앙에서만 1.0
```

![[Pasted image 20260210045835.png]]

**수학적 분석**: `distance()` 함수는 내부적으로 `sqrt(dot(a-b, a-b))`를 수행합니다. `sqrt`는 SFU(Special Function Unit)에서 처리되며 1사이클에 완료됩니다. 두 개의 `smoothstep`은 각각 Hermite 다항식 `3t² - 2t³`을 계산하는데, 이는 FMAD(Fused Multiply-Add) 명령어 체인으로 변환되어 처리량(throughput)이 높습니다.

두 smoothstep의 곱은 `innerEdge`에서 `outerEdge` 사이에서만 양수 값을 가지며, 정확히 `_ScanRadius` 지점에서 최대값 1.0이 됩니다. 이 패턴은 if문 없이 "특정 거리 범위 안에서만 활성화"라는 조건을 수학적으로 표현합니다.

### 3.3 프로시저럴 그리드 — frac() + pow() 패턴

```hlsl
float3 gridPattern = frac(i.worldPos * 5.0);  // 5.0 = 격자 밀도
float gridValue = (gridPattern.x + gridPattern.y + gridPattern.z) / 3.0;
float gridLines = pow(1.0 - gridValue, 3.0);
```

3축(X, Y, Z) 각각에 `frac()`를 적용하면 월드 좌표에 따라 0→1이 반복되는 톱니파(sawtooth wave)가 생성됩니다. 3축 평균을 구한 후 `pow(1-x, 3)`으로 감마 커브를 적용하면, 격자선(값이 0에 가까운 경계)이 밝게 강조됩니다. `pow`의 지수 3.0은 대비(contrast)를 제어하며, 값이 클수록 격자선이 가늘고 선명해집니다.

### 3.4 프레넬 림 라이팅 — 물리 기반 시선 의존 효과

```hlsl
float3 viewDir = normalize(_WorldSpaceCameraPos - i.worldPos);
float3 normalDir = normalize(i.worldNormal);
float NdotV = saturate(dot(normalDir, viewDir));
float fresnel = pow(1.0 - NdotV, _FresnelPower) * _FresnelIntensity;
```

![[Pasted image 20260210045846.png]]

**물리적 원리**: `dot(N, V)`는 표면 노멀과 시선 벡터 사이 각도의 코사인입니다. 카메라를 정면으로 향하는 표면에서는 1.0(프레넬 기여 0), 가장자리(grazing angle)에서는 0에 가까워져(프레넬 기여 최대) 림 글로우가 발생합니다. 이는 Schlick 근사의 단순화된 형태로, 실제 물리 기반 렌더링에서 사용되는 Fresnel-Schlick 공식 `F0 + (1-F0)(1-cosθ)^5`와 같은 원리입니다.

**Per-Pixel vs Per-Vertex 선택**: 프레넬을 버텍스 셰이더에서 계산하면 저폴리 메시에서 면(facet) 단위로 보간되어 부자연스러운 밴딩이 발생합니다. 프래그먼트에서 `normalize()`를 다시 수행하는 비용(~3-4 instructions)은 시각적 품질 향상 대비 미미합니다. 특히 곡면 오브젝트(구체)에서는 per-pixel 계산이 필수적입니다.

### 3.5 투명도 파이프라인 — 블렌딩 수학

```hlsl
// Render State 설정
ZWrite Off                          // 깊이 버퍼 쓰기 비활성화
Blend SrcAlpha OneMinusSrcAlpha     // Porter-Duff Over 연산

// Alpha 합성
float alpha = _BaseAlpha;                    // 기본 투명도 (0.2)
alpha += scanWave * _ScanAlpha;              // 스캔 영역 강조 (+0.8)
alpha += fresnel * scanWave * 0.5;           // 프레넬 기여 (가장자리 강조)
alpha = saturate(alpha);                     // [0, 1] 클램핑
```

**블렌딩 수학**: `Blend SrcAlpha OneMinusSrcAlpha`는 프레임버퍼에 이미 존재하는 색상(Dst)과 셰이더 출력(Src)을 다음과 같이 합성합니다:

```
최종 색상 = Src.rgb × Src.a + Dst.rgb × (1 - Src.a)
```

이것은 Porter-Duff의 **Over** 연산이며, 실시간 렌더링에서 반투명 오브젝트의 표준 합성 방식입니다.

**ZWrite Off의 필요성**: 투명 오브젝트가 깊이 버퍼에 쓰면, 뒤에 있는 불투명 오브젝트가 깊이 테스트(ZTest)에서 실패하여 렌더링되지 않습니다. 이는 "투명한 물체 뒤가 안 보이는" 시각적 결함을 초래합니다. 따라서 투명 오브젝트는 깊이를 읽기만 하고(`ZTest LEqual`) 쓰지 않아야(`ZWrite Off`) 합니다.

**렌더 큐**: `Queue="Transparent+100"`으로 설정하여 불투명 오브젝트(Geometry 큐, 2000)가 먼저 렌더링된 후 투명 오브젝트가 후순위로 그려지도록 합니다. 이는 올바른 블렌딩의 전제 조건이며, 모든 렌더링 엔진에서 동일한 원칙이 적용됩니다.

---

## 4. 성능 분석

### 명령어 비용 분석

| 연산 | HLSL 함수 | GPU 유닛 | 추정 비용 |
|------|----------|---------|----------|
| 유클리드 거리 | `distance()` | SFU (sqrt) | 1 cycle |
| Hermite 보간 (x2) | `smoothstep()` | ALU (FMAD) | 2-3 FMAD each |
| 소수 추출 (x3) | `frac()` | ALU | 1 FMAD each |
| 거듭제곱 (x2) | `pow()` | SFU | 1 cycle each |
| 정규화 (x2) | `normalize()` | SFU (rsqrt) | 1 cycle each |
| 내적 | `dot()` | ALU (FMAD) | 1 FMAD |
| 클램핑 | `saturate()` | Free (modifier) | 0 cycle |
| **총 추정** | | | **~35-40 instructions** |

### 메모리 프로파일

```
텍스처 페치:    0회 (대역폭 비용 완전 제거)
유니폼 읽기:    ~8 float (cbuffer, L1 캐시 상주)
보간기 사용:    3개 (worldPos, worldNormal, uv)
레지스터 사용:  ~12-16 GPR (낮은 사용량 → 높은 Occupancy)
```

**Occupancy 관점**: GPU의 SM(Streaming Multiprocessor)은 제한된 레지스터 파일을 여러 Warp가 공유합니다. 본 셰이더는 레지스터 ~16개, 텍스처 유닛 0개를 사용하므로 SM당 최대 Warp 수에 근접한 높은 Occupancy를 달성할 수 있습니다. 이는 메모리 레이턴시 은닉(latency hiding)에 유리합니다.

### 최적화 가능성

- **half precision 전환**: 모바일 GPU(Mali, Adreno)에서 `float` → `half` 변환 시 ALU 처리량 2배 향상. 본 셰이더의 모든 연산은 16비트 정밀도로 충분합니다.
- **LOD 기반 그리드 밀도**: 카메라 거리에 따라 `gridFrequency`를 조절하면 원거리에서 모아레 현상을 방지하고 연산량을 줄일 수 있습니다.

---

## 5. C# 인터랙션 시스템

CPU에서 GPU로의 실시간 파라미터 전달 시스템입니다.

### CPU-GPU 통신 패턴

```csharp
// Material.SetFloat → DirectX cbuffer 업데이트와 동일 원리
// GPU는 매 드로우콜마다 cbuffer에서 유니폼 값을 읽음
scannerMaterial.SetFloat("_ScanRadius", currentRadius);
scannerMaterial.SetVector("_ScannerCenter", new Vector4(hit.x, hit.y, hit.z, 0));
```

엔진 비종속 관점에서 이것은 **Constant Buffer(cbuffer) 업데이트**입니다. DirectX에서는 `ID3D11DeviceContext::UpdateSubresource()`, Vulkan에서는 Push Constants 또는 UBO 업데이트로 동일한 작업을 수행합니다. CPU 측에서 값을 설정하면 다음 드로우콜부터 GPU 셰이더가 새 값을 참조합니다.

### 레이캐스트 → 셰이더 연결

```csharp
Ray ray = mainCamera.ScreenPointToRay(mousePos);
if (Physics.Raycast(ray, out hit))
{
    StartScan(hit.point);  // 월드 좌표 → _ScannerCenter
}
```

마우스 스크린 좌표를 카메라 역투영(Inverse Projection)으로 월드 레이로 변환하고, 물리 레이캐스트로 교차점을 구합니다. 이 월드 좌표가 셰이더의 `_ScannerCenter`에 전달되면, 클릭 지점을 중심으로 스캔 링이 생성됩니다.

### 코루틴 애니메이션 (프레임 독립)

```csharp
private IEnumerator AnimateScan()
{
    float currentRadius = 0f;
    while (currentRadius < maxScanRadius)
    {
        currentRadius += scanSpeed * Time.deltaTime;  // 프레임 독립
        scannerMaterial.SetFloat("_ScanRadius", currentRadius);
        yield return null;  // 다음 프레임까지 대기
    }
    scannerMaterial.SetFloat("_ScanRadius", 0f);  // 리셋
}
```

`Time.deltaTime`을 곱하여 프레임 레이트에 관계없이 일정한 속도(`scanSpeed` units/sec)로 반경이 확장됩니다. 60fps에서는 프레임당 ~0.167 단위, 30fps에서는 ~0.333 단위씩 증가하여 동일한 결과를 보장합니다.

### 스캔 반경 확장 시퀀스

| Radius 3.5 | Radius 5.0 |
|:-----------:|:----------:|
| ![Radius 3.5](../Screenshots/Step4_Scan_Radius3.5.png) | ![Radius 5.0](../Screenshots/Step4_Scan_Radius5.png) |

| Radius 8.0 | Radius 12.0 |
|:-----------:|:-----------:|
| ![Radius 8.0](../Screenshots/Step4_Scan_Radius8.png) | ![Radius 12.0](../Screenshots/Step4_Scan_Radius12.png) |

마우스 클릭 지점에서 시작된 스캔 웨이브가 10 units/sec 속도로 확장되며, 동일한 머테리얼을 공유하는 모든 씬 오브젝트(Sphere, Wall, HiddenItem)에 동시에 적용됩니다.

---

## 6. 렌더링 파이프라인 이해도

### 좌표 변환 체인

```
Object Space ──[Model Matrix]──→ World Space ──[View Matrix]──→ View Space
     │                              │
     └── 모델 로컬 좌표              └── 이펙트 계산 (본 프로젝트)

View Space ──[Projection Matrix]──→ Clip Space ──[Perspective Divide]──→ NDC
                                        │
                                        └── 클리핑 & 래스터라이제이션

NDC ──[Viewport Transform]──→ Screen Space
                                   │
                                   └── 최종 픽셀 좌표
```

본 셰이더는 이 체인에서 두 가지 경로를 동시에 사용합니다:
1. **래스터라이제이션 경로**: `Object → Clip` (MVP 변환, `UnityObjectToClipPos` = `mul(MVP, pos)`)
2. **이펙트 계산 경로**: `Object → World` (Model 변환만, 프래그먼트에서 거리/프레넬 계산)

### 투명도 렌더링 순서

올바른 투명도 합성을 위해 렌더 큐 순서가 중요합니다:

```
1. 불투명 패스 (Queue=2000 "Geometry")
   → 깊이 버퍼 쓰기 ON, 앞→뒤 정렬 (Early-Z 최적화)

2. 투명 패스 (Queue=3100 "Transparent+100")
   → 깊이 버퍼 쓰기 OFF, 뒤→앞 정렬 (올바른 블렌딩)
   → SrcAlpha * Src + (1-SrcAlpha) * Dst
```

투명 오브젝트의 뒤→앞(back-to-front) 정렬은 Order-Independent Transparency(OIT)가 아닌 일반적인 알파 블렌딩의 한계입니다. 복잡한 투명 오브젝트 겹침이 필요한 경우 Weighted Blended OIT나 Per-Pixel Linked Lists 같은 고급 기법이 필요합니다.

---

## 7. 확장 가능성

### 7.1 다중 스캔 웨이브

현재 단일 `_ScannerCenter`/`_ScanRadius` 쌍을 사용하지만, 구조화된 버퍼(StructuredBuffer)를 통해 N개의 동시 스캔을 지원할 수 있습니다:

```hlsl
// 확장 설계 (구현 예시)
StructuredBuffer<float4> _ScanCenters;  // xyz = center, w = radius
int _ScanCount;

float totalWave = 0;
for (int i = 0; i < _ScanCount; i++)
{
    float dist = distance(worldPos, _ScanCenters[i].xyz);
    totalWave += dualSmoothstep(dist, _ScanCenters[i].w, _ScanWidth);
}
totalWave = saturate(totalWave);
```

### 7.2 풀스크린 포스트 프로세싱 전환

현재 오브젝트별 머테리얼 방식에서, 깊이 버퍼(Depth Buffer)를 활용한 풀스크린 포스트 프로세싱으로 전환하면 모든 씬 오브젝트에 자동 적용 가능합니다:

```hlsl
// 깊이에서 월드 좌표 복원
float depth = tex2D(_CameraDepthTexture, uv).r;
float3 worldPos = ComputeWorldSpacePosition(uv, depth, InverseVPMatrix);
// → 이후 동일한 scanWave 계산 적용
```

### 7.3 추가 확장 방향

- **PBR 통합**: Metallic/Roughness 워크플로우와 결합, 스캔 영역 내부에서 물리 기반 셰이딩 적용
- **컴퓨트 셰이더**: 복잡한 프로시저럴 패턴이나 파티클 데이터를 GPU에서 사전 계산
- **순수 HLSL 포팅**: Unity의 `UnityCG.cginc` 의존성을 제거하고 표준 HLSL로 재작성하여 어떤 렌더링 엔진에서든 즉시 사용 가능

---

## 8. 개발 과정

검증 기반(Verification-Driven) 개발 방법론으로, 각 단계에서 시각적 결과를 확인한 후 다음 단계로 진행했습니다.

| 단계 | 내용 | 검증 |
|------|------|------|
| **Step 1** | 셰이더 골격 + World Space 좌표 변환 | 좌표계 디버그 컬러로 검증 |
| | ![Step 1](../Screenshots/step1_worldpos_test.png) | |
| **Step 2** | Dual smoothstep 스캔 링 + frac() 그리드 | 링 형태 및 격자 선명도 확인 |
| | ![Step 2](../Screenshots/Step2_ScanWave_Test.png) | |
| **Step 3** | Fresnel 림 라이팅 + 투명도 파이프라인 | 시선 의존 림 글로우, 블렌딩 동작 확인 |
| | ![Step 3](../Screenshots/Step3_Fresnel_Transparency.png) | |
| **Step 4** | C# 레이캐스트 인터랙션 + 코루틴 애니메이션 | 클릭 → 스캔 확장 → 리셋 사이클 검증 |
| | ![Step 4](../Screenshots/Step4_Scan_Radius5.png) | |

이 방법론은 "모든 코드를 작성한 후 한꺼번에 테스트"하는 것이 아니라, 최소 기능 단위로 구현하고 검증하는 접근입니다. GPU 셰이더는 디버거 사용이 제한적이므로, 시각적 출력 자체를 테스트 수단으로 활용합니다.

---

## 9. 핵심 역량 요약

| Pearl Abyss 요구 역량 | 본 프로젝트에서의 입증 |
|----------------------|---------------------|
| HLSL/셰이더 프로그래밍 | smoothstep, frac, pow, dot 등 HLSL 내장 함수 기반 이펙트 설계 |
| GPU 아키텍처 이해 | Warp divergence 회피, ALU:TEX 비율 최적화, Occupancy 고려 설계 |
| 렌더링 파이프라인 | 좌표 공간 변환 체인, 투명도 렌더 큐, 블렌딩 수학 구현 |
| 성능 최적화 | 브랜치리스 설계, 텍스처 0회, ~35-40 instructions 달성 |
| 수학적 기반 | 유클리드 거리, Hermite 보간, Fresnel 물리 모델 적용 |
| 엔진 비종속 지식 | 모든 기술 결정을 GPU 하드웨어 원리로 설명, Unity API 대신 범용 원리 병기 |
| CPU-GPU 연동 | cbuffer 유니폼 업데이트, 레이캐스트 → 셰이더 파라미터 파이프라인 |
| 문제 해결 | 검증 기반 개발, 단계별 시각적 디버깅 |

---

본 프로젝트에서 사용된 모든 기술적 원리 — World Space 좌표 변환, 브랜치리스 조건 처리, 프로시저럴 패턴 생성, Fresnel 물리 모델, 투명도 블렌딩 수학, GPU 메모리 아키텍처 고려 — 는 **엔진에 종속되지 않는 범용 그래픽스 지식**입니다. Unity의 `UnityObjectToClipPos()`는 `mul(MVP, position)`이고, `Material.SetFloat()`는 cbuffer 업데이트이며, `smoothstep()`은 어떤 셰이딩 언어에서든 동일한 Hermite 다항식입니다.

Pearl Abyss의 자체 엔진 환경에서도 이 지식은 그대로 적용됩니다. 엔진이 제공하는 API 이름은 달라도, GPU 하드웨어가 실행하는 명령어와 그 최적화 원리는 동일하기 때문입니다.
