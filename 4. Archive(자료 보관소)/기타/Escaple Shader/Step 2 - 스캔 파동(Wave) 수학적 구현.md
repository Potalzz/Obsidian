# Step 2 Implementation Plan: Scan Wave Effect

## X-Ray Scanner Shader - 스캔 파동 구현

---

## 1. Context (배경)

**목표:** Unity HLSL 셰이더로 Vision Pro 스타일의 스캔 웨이브 효과 구현

**현재 상태:**

- ✅ **Step 1 완료:** 기본 셰이더 골격 및 월드 좌표 시스템 구축
    
- ✅ **Properties 정의:** `_ScannerCenter`, `_ScanRadius`, `_ScanWidth`
    
- ✅ **Vertex Shader:** Object Space → World Space 변환 완료
    
- ⏳ **Fragment Shader:** 현재 디버그 패턴만 출력 (`frac(worldPos * 0.1)`)
    

**Step 2의 목표:**

1. 거리 기반 스캔 웨이브 시각화
    
2. `smoothstep`으로 부드러운 링 경계 생성
    
3. `frac()`로 사이버펑크 격자 패턴 추가
    
4. 파란색/시안색 계열의 스캔 색상 적용
    
5. Material Inspector에서 수동 테스트
    

**왜 이 프로젝트가 펄어비스 포트폴리오로 적합한가:**

- **상용 엔진(Unity) 깊은 이해 증명:** 셰이더 구조 및 파이프라인 이해
    
- **수학적 원리 활용:** Distance, Smoothstep, 좌표계 변환 등 그래픽스 기초
    
- **성능 최적화:** `if`문 제거, Branchless 코드 작성
    
- **이론과 실무의 결합:** 그래픽스 이론을 실제 비주얼로 구현
    

---

## 2. Mathematical Foundation (수학적 기초 - 면접 대비)

### A. Distance-Based Rendering (거리 기반 렌더링)

**개념:** 스캔 중심점으로부터의 거리를 계산하여 구형 파동 생성

**수학 공식:**

$$\text{dist} = \text{distance}(\text{pixelPos}, \text{scannerCenter})$$

$$\text{Internal Logic: } \sqrt{(x-c_x)^2 + (y-c_y)^2 + (z-c_z)^2}$$

**면접 답변 가이드:**

> **초보자용 답변:**
> 
> "distance() 함수는 3D 공간에서 두 점 사이의 직선 거리를 계산합니다. 피타고라스 정리를 3차원으로 확장한 것이고, GPU에 최적화된 내장 함수라서 매우 빠릅니다. 이를 사용하면 스캐너 중심에서 모든 방향으로 균등하게 확산되는 구형 파동을 만들 수 있습니다."

> **기술적 답변:**
> 
> "distance()는 HLSL intrinsic function으로 length(A-B)와 동일하며, GPU의 벡터 연산 유닛에서 병렬로 처리됩니다. 내부적으로 dot product와 sqrt를 사용하며, World Space에서 계산하므로 오브젝트의 Transform(회전/스케일)과 무관하게 일관된 효과를 보장합니다."

**왜 World Space를 사용하는가:**

- **Object Space:** 오브젝트마다 좌표계 중심이 달라 효과가 개별적으로 적용됨.
    
- **World Space:** 씬 전체에서 동일한 기준점을 사용하여, 여러 오브젝트에 같은 스캔 효과를 동시에 적용 가능하며 회전/이동 시에도 스캔 방향이 일정함.
    
![[../../../assets/images/Pasted image 20260209172153.png]]
### B. Smoothstep Function (부드러운 경계)

**수학 공식:**

$$\text{smoothstep}(e_0, e_1, x) = t^2 \cdot (3 - 2t) \quad (\text{where } t = \text{saturate}(\frac{x - e_0}{e_1 - e_0}))$$

**시각적 비교:**

- **if문 사용 (계단식):** 경계가 끊어짐 (Aliasing 발생)
    
- **smoothstep 사용 (곡선):** Hermite interpolation을 통한 부드러운 보간
    



**면접 답변 가이드:**

> **초보자용 답변:**
> 
> "if문을 사용하면 경계가 각지고, GPU가 서로 다른 분기를 실행하는 픽셀들을 따로 처리해야 합니다. smoothstep은 모든 픽셀이 같은 수식을 계산하고, 결과도 부드러워서 앨리어싱이 줄어듭니다."

> **기술적 답변:**
> 
> "GPU는 SIMD 아키텍처로 Warp 단위로 픽셀을 동시 처리합니다. if문은 Warp Divergence를 유발하여 성능 저하를 일으킬 수 있습니다. smoothstep은 Branchless 알고리즘으로 모든 레인이 동일한 명령어를 실행하여 Vectorization 효율을 극대화합니다."

**스캔 링 생성 원리:**

High-level shader language

```
// 두 개의 smoothstep을 곱하여 링 생성
float wave1 = smoothstep(innerEdge, _ScanRadius, dist); // 안쪽: 0 → 1
float wave2 = smoothstep(outerEdge, _ScanRadius, dist); // 바깥: 1 → 0
float ring = wave1 * wave2; // 중앙(radius)에서만 1.0 (교집합)
```

### C. Grid Pattern with frac() (격자 패턴)

**수학 공식:**

$$\text{frac}(x) = x - \text{floor}(x) \quad (\text{소수 부분 추출, } 0 \sim 1 \text{ 반복})$$

**면접 답변 가이드:**

> **초보자용 답변:**
> 
> "frac()는 소수점 부분만 남기는 함수입니다. 월드 좌표에 주파수를 곱하면 0에서 1로 반복되는 패턴이 만들어집니다. 텍스처 없이도 격자 무늬를 만들 수 있어 메모리를 절약할 수 있습니다."

> **기술적 답변:**
> 
> "frac()는 프로시저럴 패턴 생성의 기본입니다. sin/cos보다 ALU 연산량이 적고, 텍스처 샘플링(Memory Fetch) 대비 메모리 대역폭을 절약합니다. 3축의 frac 값을 평균하여 3D 격자를 만들고 pow()로 선명도를 제어합니다."

### D. Coordinate Systems (좌표계 이해)

![[../../../assets/images/Pasted image 20260209172214.png]]

**변환 과정:**

High-level shader language

```
// Vertex Shader에서 한 번 변환, Fragment에서 보간 사용
o.worldPos = mul(unity_ObjectToWorld, v.vertex).xyz;
```

**면접 질문:** "왜 Fragment Shader가 아닌 Vertex Shader에서 변환하나요?"

> **답변:** "버텍스 셰이더는 정점당 1회, 프래그먼트 셰이더는 픽셀당 수백만 번 실행됩니다. 월드 좌표 변환은 정점에서 한 번만 하고 보간된 값을 픽셀에서 사용하면 연산량이 획기적으로 줄어듭니다. (예: 1만 정점 vs 100만 픽셀)"

---

## 3. Complete Fragment Shader Code (구현부)

- **파일:** `/Assets/Shaders/ScannerShader.shader`
    
- **수정 위치:** Fragment Shader (Lines 65-71)
    

High-level shader language

```
// Fragment Shader - Step 2: Scan Wave Implementation
fixed4 frag (v2f i) : SV_Target
{
    // ========================================
    // 1단계: 거리 계산 (Distance Calculation)
    // ========================================
    // 현재 픽셀의 월드 좌표와 스캐너 중심 간의 유클리드 거리
    float distanceFromCenter = distance(i.worldPos, _ScannerCenter.xyz);

    // ========================================
    // 2단계: 스캔 링 생성 (Scan Ring with Smoothstep)
    // ========================================
    // 내부 경계: 스캔 반경 - 폭 (링의 안쪽 시작점)
    float innerEdge = _ScanRadius - _ScanWidth;

    // 외부 경계: 스캔 반경 + 폭 (링의 바깥쪽 끝점)
    float outerEdge = _ScanRadius + _ScanWidth;

    // 안쪽에서 밝아지는 그라디언트 (0→1)
    float wave1 = smoothstep(innerEdge, _ScanRadius, distanceFromCenter);
    // 바깥쪽에서 어두워지는 그라디언트 (1→0) (순서 주의: 큰 값 -> 작은 값 아님, 로직으로 처리)
    // *수정 노트: smoothstep(a, b, t)에서 t가 b보다 크면 1입니다. 
    // 보통 링을 만들 땐 (1 - smoothstep(...))을 쓰거나 범위를 조정합니다. 
    // 여기서는 wave1 * (1 - smoothstep(radius, outer, dist)) 형태가 일반적이나,
    // 원본 코드의 의도(wave1 * wave2)를 살려 구현합니다.
    
    // *수정 제안 코드 (더 명확한 링 형태)*
    float wave2 = 1.0 - smoothstep(_ScanRadius, outerEdge, distanceFromCenter); 
    
    // 두 그라디언트를 곱하면 중앙(_ScanRadius) 부근에서 높은 값
    float scanWave = wave1 * wave2;

    // ========================================
    // 3단계: 격자 패턴 생성 (Grid Pattern)
    // ========================================
    float gridFrequency = 5.0;  // 격자 밀도

    // 각 축(X, Y, Z)에 대해 frac() 적용하여 0~1 반복 패턴
    float3 gridPattern = frac(i.worldPos * gridFrequency);

    // 3축 패턴을 평균하여 단일 값으로 합침
    float gridValue = (gridPattern.x + gridPattern.y + gridPattern.z) / 3.0;

    // 대비 증가: pow()로 0 근처 값 강조 (격자선이 선명해짐)
    float gridLines = pow(1.0 - gridValue, 3.0);

    // ========================================
    // 4단계: 색상 합성 (Color Composition)
    // ========================================
    float3 scanColor = float3(0.2, 0.8, 1.0);  // 밝은 시안 (주 스캔 링)
    float3 gridColor = float3(0.1, 0.4, 0.8);  // 어두운 파랑 (격자선)

    // 스캔 웨이브 색상
    float3 waveEffect = scanColor * scanWave;

    // 그리드 효과: 스캔 영역(scanWave) 내에서만 격자 표시
    float3 gridEffect = gridColor * gridLines * scanWave;

    // 최종 색상: Additive Blending
    float3 finalColor = waveEffect + gridEffect;

    // ========================================
    // 5단계: 최종 출력
    // ========================================
    return fixed4(finalColor, 1.0);
}
```

---

## 4. Step-by-Step Implementation (단계별 구현)

### Phase 1: Distance Visualization Test

- **목적:** `distance()` 함수 작동 확인
    
- **코드:** `return fixed4(dist/10.0, dist/10.0, dist/10.0, 1);`
    
- **테스트:** Sphere(Scale 10) 생성 후 적용. 중심이 검고 외곽이 흰 그라디언트 확인.
    

### Phase 2: Scan Ring Implementation

- **목적:** `smoothstep`으로 링 모양 생성
    
- **코드:** `return fixed4(scanWave, scanWave, scanWave, 1);`
    
- **테스트:** `_ScanRadius`를 조절하며 링이 확장되는지, 경계가 부드러운지 확인.
    

### Phase 3: Grid Pattern Addition

- **목적:** `frac()`로 격자 오버레이
    
- **코드:** `scanWave * (1.0 + gridLines * 0.5)`
    
- **테스트:** `gridFrequency` 변경 (2, 5, 10)에 따른 격자 밀도 확인.
    

### Phase 4: Cyberpunk Color Application

- **목적:** 최종 사이버펑크 스타일 완성
    
- **테스트:** 최종 코드로 교체 후 Scene View에서 시각적 확인 (Play Mode 불필요).
    

---

## 5. Testing & Verification (테스트 및 검증)

### ✅ Test Case 1: Static Visualization

1. Sphere 생성 (Scale: 10, 10, 10) 및 Material 적용.
    
2. `_ScanRadius: 3.0`, `_ScanWidth: 0.5` 설정.
    
3. **결과 확인:** 반경 3.0에 시안색 링, 0.5 폭, 격자 패턴 확인.
    

### ✅ Test Case 2: Dynamic Radius

1. `_ScanRadius`를 1.0 → 8.0으로 변경.
    
2. **결과 확인:** 링이 부드럽게 확장됨 (앨리어싱 없음). 월드 기준 격자 크기 유지.
    

### ✅ Test Case 3: Multiple Objects

1. Cube, Sphere, Cylinder에 모두 같은 Material 적용.
    
2. **결과 확인:** 오브젝트 모양과 무관하게 구형으로 퍼지는 링, 연속적인 격자 패턴.
    

---

## 6. Interview Q&A (면접 예상 질문 요약)

|**질문**|**핵심 키워드**|**답변 요약**|
|---|---|---|
|**Q1. 왜 if문 대신 smoothstep?**|SIMD, Branchless, Warp Divergence|if문은 병렬 처리 효율을 떨어뜨림(Warp Divergence). smoothstep은 모든 픽셀이 동일 연산을 수행하여 빠르고, 경계가 부드러움.|
|**Q2. Object vs World Space?**|기준점, 일관성|Object Space는 개체 중심, World Space는 씬 전체 절대 좌표. 스캔 효과는 전역적이어야 하므로 World Space 사용.|
|**Q3. frac()으로 격자 원리?**|Procedural, Memory Bandwidth|소수점만 취해 반복 패턴 생성. 텍스처 메모리 사용 없이 수학적 연산(ALU)만으로 패턴 생성.|
|**Q4. 최적화 고려사항?**|Pre-computation, Math|Vertex에서 좌표 변환, Fragment는 보간값 사용. 텍스처 Fetch 없음. Branchless 코드.|

---

## 7. Common Issues (트러블슈팅)

1. **링이 보이지 않음:**
    
    - 원인: `_ScanRadius`가 너무 크거나 0임, 또는 `_ScannerCenter` 위치 오류.
        
    - 해결: 디버그 코드로 단순 거리값 출력해보기.
        
2. **링이 각지거나 깜빡임:**
    
    - 원인: `_ScanWidth`가 너무 작거나 `gridFrequency`가 너무 높음(앨리어싱).
        
    - 해결: Width 0.5 이상, Freq 5 이하 권장.
        
3. **오브젝트마다 링 위치가 다름:**
    
    - 원인: Vertex Shader에서 World Space 변환 누락.
        
    - 해결: `mul(unity_ObjectToWorld, v.vertex)` 필수 확인.
        

---

## 8. Next Steps (다음 단계)

- **Step 3 예고:** 투시 및 프레넬(Fresnel) 효과, ZTest(가려진 부분 강조)
    
- **Step 4 예고:** C# 스크립트 상호작용 (Raycast로 스캔 트리거, Coroutine 애니메이션)\


# 완료
✅ **2단계 구현 완료! (Step 2 Implementation Complete!)**

### **구현된 내용 (What Was Implemented)**

Unity X-Ray 스캐너 셰이더를 위한 **스캔 웨이브 효과(Scan Wave Effect)** 구현을 성공적으로 마쳤습니다. 달성한 내용은 다음과 같습니다.

**1. 거리 기반 스캔 링 (ScannerShader.shader: 72번째 줄)**

- `distance()` 함수를 사용하여 각 픽셀에서 스캐너 중심까지의 유클리드 거리 계산
    
- 월드 공간(World Space)에서 구형 파동 전파 패턴 생성
    

**2. 부드러운 링 경계 (ScannerShader.shader: 87-94번째 줄)**

- 두 개의 `smoothstep()` 함수를 사용하여 부드러운 가장자리를 가진 링 생성
    
- 분기 없는(Branchless) 알고리즘으로 GPU 효율성 보장 (Warp Divergence 방지)
    
- `wave1`은 안쪽 경계에서 페이드 인(Fade-in), `wave2`는 바깥쪽 경계에서 페이드 아웃(Fade-out)
    
- 두 값을 곱하여 `_ScanRadius`를 중심으로 하는 링 생성
    

**3. 프로시저럴 격자 패턴 (ScannerShader.shader: 104-111번째 줄)**

- `frac()`을 사용하여 X, Y, Z 축에 반복되는 0~1 패턴 생성
    
- 3축 평균을 통해 균일한 3D 격자 생성
    
- `pow(1 - x, 3)`을 사용하여 대비를 높여 격자 선을 선명하게 만듦
    
- 텍스처가 필요 없음 = 메모리 효율적
    

**4. 사이버펑크 색상 테마 (ScannerShader.shader: 118-129번째 줄)**

- **스캔 색상:** 메인 링을 위한 밝은 시안색 (0.2, 0.8, 1.0)
    
- **격자 색상:** 격자 선을 위한 어두운 파란색 (0.1, 0.4, 0.8)
    
- 가산 혼합(Additive blending)으로 웨이브와 격자 효과 결합
    

### **시각적 검증 (Visual Verification)**

스크린샷을 통해 효과가 완벽하게 작동함을 확인할 수 있습니다.

- ✅ 구(Sphere) 위에 밝은 시안색 스캔 링이 보임
    
- ✅ 스캔 웨이브 위에 격자 패턴(수직선 등)이 오버레이 됨
    
- ✅ 링 가장자리에 부드러운 그라디언트 적용 (계단 현상 없음)
    
- ✅ 사이버펑크 미학 달성
    

### **테스트 설정 완료 (Testing Setup Created)**

**테스트 오브젝트:** ScanTestSphere

- **위치:** (0, 2, 0)
    
- **크기(Scale):** 10x10x10
    
- **재질(Material):** Step 2 셰이더가 적용된 ScannerMaterial
    

**현재 재질 속성:**

- `_ScanRadius`: 5.0 (이 값을 조정하여 링의 확장/축소 확인)
    
- `_ScanWidth`: 0.5 (링의 두께)
    
- `_ScannerCenter`: (0, 0, 0)
    

### **추가 테스트 방법 (How to Test Further)**

1. **동적 반경 테스트:**
    
    - Project 창에서 `ScannerMaterial` 선택
        
    - Inspector에서 `_ScanRadius`를 1.0 → 10.0으로 조정
        
    - 시안색 링이 밖으로 퍼져 나가는 것을 관찰
        
2. **다중 오브젝트 테스트:**
    
    - 더 많은 오브젝트(Cube, Cylinder 등) 생성
        
    - `ScannerMaterial` 적용
        
    - 모든 오브젝트에 동시에 동일한 스캔 웨이브가 나타나는지 확인
        
3. **격자 밀도 테스트:**
    
    - 셰이더 코드 101번째 줄에서 `gridFrequency`를 5.0에서 변경해보기:
        
        - 2.0 = 듬성듬성한 격자
            
        - 10.0 = 촘촘한 격자
            
    - 패턴 밀도 변화 관찰
        

### **주요 기술적 성과 (Key Technical Achievements)**

✅ **GPU 최적화:**

- Branchless 코드 (if문 없음)
    
- Vertex Shader에서 월드 공간 변환 (정점당 1회 수행)
    
- Fragment Shader는 보간된 값을 사용 (효율적)
    

✅ **수학적 구현:**

- 구형 전파를 위한 `distance()`
    
- 부드러운 링 경계를 위한 이중 `smoothstep()`
    
- 프로시저럴 패턴을 위한 `frac()`
    

✅ **시각적 품질:**

- 부드러운 안티앨리어싱(Anti-aliased) 경계
    
- 사이버펑크 색상 팔레트
    
- 텍스처 샘플링 없는 격자 오버레이
    

### **수정된 파일 (Files Modified)**

- `Assets/Shaders/ScannerShader.shader` (64-136번째 줄)
    
    - 디버그 패턴을 완전한 스캔 웨이브 구현 코드로 교체
        
    - 면접 대비를 위한 상세 주석 추가
        

### **오류 없음 (No Errors)**

Unity 콘솔에 컴파일 오류가 0개입니다. 셰이더는 **Step 3**로 넘어갈 준비가 완료되었습니다.

### **다음 단계 미리보기 (Next Steps Preview)**

**Step 3**에서는 다음이 추가됩니다:

- 투명도 (Blend Mode 수정)
    
- 프레넬 효과 (시야각에 따른 밝기 변화)
    
- ZTest 설정 (가려진 물체를 투시하는 진정한 X-Ray 효과)
    

**Step 4**에서는 C# 스크립팅이 추가됩니다:

- 마우스 클릭으로 스캔 트리거
    
- Coroutine을 통한 반경 자동 확장
    
- Raycast를 통한 동적 위치 지정
    

---

스캔 웨이브 효과가 이제 완전히 작동하며 Unity 에디터에서 수동 테스트할 준비가 되었습니다! 🎉