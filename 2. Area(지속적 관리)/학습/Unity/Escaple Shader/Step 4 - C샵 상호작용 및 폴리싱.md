# 구현 내용
## ✅ 3단계 구현 완료: 투명도 및 프레넬(Fresnel) 효과

X-Ray 스캐너 셰이더를 위한 **투명도** 및 **프레넬 림 라이팅(Rim Lighting)** 시스템 구현을 성공적으로 마쳤습니다. 달성된 주요 내용은 다음과 같습니다.

### 🛠 변경 사항 (Changes Made)

#### 1. 새로운 셰이더 속성 (10-15행)

OpenGL Shading Language

```
_BaseAlpha ("Base Transparency", Range(0, 1)) = 0.2       // 기본 투명도
_ScanAlpha ("Scan Wave Alpha Boost", Range(0, 1)) = 0.8   // 스캔 파동 시 알파 강조
_FresnelPower ("Fresnel Power (Rim Sharpness)", Range(0.1, 5)) = 2.0 // 프레넬 강도 (림 선명도)
_FresnelIntensity ("Fresnel Intensity", Range(0, 2)) = 1.0 // 프레넬 세기
_RimColor ("Rim Color (Fresnel)", Color) = (0.3, 0.9, 1.0, 1.0) // 림 색상
```

#### 2. 투명도 렌더 파이프라인 설정 (20-32행)

OpenGL Shading Language

```
Tags { "RenderType"="Transparent" "Queue"="Transparent+100" }
ZWrite Off                      // 깊이 버퍼 쓰기 끄기 (투명 객체 겹침 처리)
ZTest LEqual                    // 깊이 테스트: 같거나 가까우면 그리기
Blend SrcAlpha OneMinusSrcAlpha // 표준 알파 블렌딩
Cull Back                       // 후면 컬링
```

#### 3. 프레넬(Fresnel) 계산 (88-106행)

표면의 노멀(법선)과 시선 방향 사이의 각도를 기반으로 시선 의존적 조명을 계산합니다.

OpenGL Shading Language

```
float3 viewDir = normalize(_WorldSpaceCameraPos - i.worldPos);
float3 normalDir = normalize(i.worldNormal);
float NdotV = saturate(dot(normalDir, viewDir));
// 각도가 클수록(가장자리일수록) 더 밝게 처리
float fresnel = pow(1.0 - NdotV, _FresnelPower) * _FresnelIntensity;
```

#### 4. 림 컬러(Rim Color) 통합 (171행)

OpenGL Shading Language

```
float3 rimEffect = _RimColor.rgb * fresnel * scanWave;
```

#### 5. 레이어드 알파 시스템 (177-196행)

OpenGL Shading Language

```
float alpha = _BaseAlpha;                   // 1. 기본 20% 가시성
alpha += scanWave * _ScanAlpha;             // 2. 스캔 링 내부에서 80% 강조
alpha += fresnel * scanWave * 0.5;          // 3. 림(Rim) 기여도 추가
alpha = saturate(alpha);                    // 4. [0,1] 범위로 클램핑
```

---

### 🖼 시각적 결과 (Visual Results)

`Assets/Screenshots/Step3_Fresnel_Transparency.png` 스크린샷에서 확인 가능:

- ✅ **반투명 구체:** 오브젝트를 통해 배경이 비쳐 보임
    
- ✅ **밝은 청록색 스캔 링:** 스캔 파동 위치에서 드러나는 효과(Reveal effect)
    
- ✅ **절차적 그리드 패턴:** 스캔 영역 내부에서만 패턴이 보임
    
- ✅ **프레넬 림 라이팅:** 구체의 실루엣(외곽선)을 따라 밝게 빛나는 가장자리
    

---

### 💡 기술적 주요 사항 (Technical Highlights)

**성능 (Performance):**

- 약 35-40개의 프래그먼트 셰이더 명령어 사용 (2단계 대비 약 8개 증가)
    
- 여전히 **100% 분기 없음(Branchless)** (if 문 미사용)
    
- 텍스처 페치(Texture fetch) 0회 (전체 절차적 생성)
    
- 모바일 친화적 아키텍처 유지
    

**GPU 아키텍처 이해도:**

- **픽셀 단위 프레넬:** 곡면에서 부드러운 그라디언트 보장
    
- **알파 블렌딩:** 표준 공식 사용 (`SrcAlpha * src + (1-SrcAlpha) * dst`)
    
- **ZWrite Off:** 투명 오브젝트의 올바른 레이어링(겹침) 허용
    
- **Queue=Transparent+100:** 올바른 렌더링 순서 보장
    

---

### 🎛 재질 속성 - 추천 조정 값 (Recommended Tuning)

인스펙터 창에서 다음 값들을 조절해 보세요:

|**속성 (Property)**|**기본값**|**효과 (Effect)**|
|---|---|---|
|**_FresnelPower**|2.0|높을수록 림이 얇아짐, 낮을수록 림이 넓어짐|
|**_FresnelIntensity**|1.0|전체적인 림의 밝기 조절|
|**_BaseAlpha**|0.2|스캔 영역 밖의 가시성 (유령/잔상 효과)|
|**_ScanAlpha**|0.8|스캔 링 내부의 불투명도 증가량|
|**_RimColor**|Cyan|프레넬 림이 빛나는 색상|

---

### 🗣 면접 핵심 포인트 (Interview Talking Points)

1. **프레넬 이론:** 슐릭(Schlick) 근사에 기반함 - 물체를 스치듯(grazing angle) 볼 때 가장자리가 더 밝게 보이는 광학 현상 구현.
    
2. **렌더 파이프라인:** 블렌드 모드, 깊이 테스트(Depth Test), 렌더 큐(Render Queue) 순서에 대한 이해 입증.
    
3. **벡터 수학:** 노멀(Normal)과 뷰 방향(View Direction) 간의 내적(Dot Product)을 사용하여 시야각 감지.
    
4. **최적화:** 분기 없는(Branchless) 코드, 절차적 생성, 픽셀 단위의 정확성과 성능 간의 균형.
    

---

### 📂 업데이트된 파일

- `Assets/Shaders/ScannerShader.shader`: 투명도 + 프레넬 추가 (총 200줄)
    
- `memory/MEMORY.md`: 프로젝트 문서 업데이트
    
- `Assets/Screenshots/Step3_Fresnel_Transparency.png`: 시각적 검증 이미지
    

### ✅ 컴파일 오류 없음

유니티 콘솔 깨끗함 - 셰이더가 첫 시도에 성공적으로 컴파일됨!

---

### 🔜 다음 단계: Step 4 - C# 스크립트 상호작용

- 마우스 클릭으로 스캔 트리거
    
- 자동 반경 확장을 위한 코루틴(Coroutine)
    
- 동적 스캐너 위치 선정을 위한 레이캐스트(Raycast)
    
- 스크립트에서 재질(Material) 속성 업데이트