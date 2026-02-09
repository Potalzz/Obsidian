
# Step 3 Implementation Plan: Transparency & Fresnel Effect

**X-Ray Scanner Shader - 투명도 및 프레넬 효과 구현**

## 1. Context (배경)

> **Why This Change:** > 불투명한(Opaque) 스캔 웨이브를 **투명도(Transparency)**와 **프레넬 림 라이팅(Fresnel Rim Lighting)**이 적용된 진정한 X-ray 비전 효과로 변환하여 Pearl Abyss 포트폴리오의 퀄리티를 높입니다.

### 📋 Current State (현재 상태)

- ✅ **Step 1:** 월드 공간 좌표를 포함한 기본 셰이더 구조
    
- ✅ **Step 2:** 절차적 그리드 패턴이 포함된 스캔 웨이브 효과 (완료)
    
- ⏳ **Step 3:** 현재 `Alpha=1.0`인 불투명 상태 (Line 135: "Step 3에서 투명도 추가 예정")
    
- **Target File:** `/Users/penguinland/Desktop/Unity/X-Ray_Shader/Assets/Shaders/ScannerShader.shader`
    
- **Foundation:** `worldPos` (Line 56), `worldNormal` (Line 59) 구현 완료
    

### 🎯 Step 3 Goals

1. **Transparency System:** 물체를 반투명하게 만들고 스캔 웨이브가 이를 드러내도록 구현
    
2. **Fresnel Effect:** 시야각에 따른 림 라이팅 (가장자리 발광) 구현
    
3. **X-Ray Capability:** 벽 투시를 위한 깊이 테스트(Depth Testing) 준비
    
4. **Integration:** 기존 스캔 웨이브 및 그리드 패턴과 자연스럽게 블렌딩
    

### 💎 Portfolio Value

- **Vector Mathematics:** 내적(Dot Product), 뷰 방향(View Direction) 활용 능력 입증
    
- **Render Pipeline:** 블렌드 모드, 깊이 테스트, 큐 오더링에 대한 이해도 증명
    
- **Optimization:** 분기 없는 코드(Branchless code), 절차적 생성 기법 사용
    
- **Interview Points:** Fresnel 이론, Alpha Blending, GPU 아키텍처
    

---

## 2. Implementation Plan (구현 계획)

### Part 1: Add Shader Properties (Lines 5-9)

기존 `_ScanWidth` 아래에 다음 속성들을 추가합니다.

OpenGL Shading Language

```
// Step 3: Transparency & Fresnel
_BaseAlpha ("Base Transparency", Range(0, 1)) = 0.2
_ScanAlpha ("Scan Wave Alpha Boost", Range(0, 1)) = 0.8
_FresnelPower ("Fresnel Power (Rim Sharpness)", Range(0.1, 5)) = 2.0
_FresnelIntensity ("Fresnel Intensity", Range(0, 2)) = 1.0
_RimColor ("Rim Color (Fresnel)", Color) = (0.3, 0.9, 1.0, 1.0)
```

**Uniform 변수 선언 (Line 29 이후 추가):**

OpenGL Shading Language

```
float _BaseAlpha;
float _ScanAlpha;
float _FresnelPower;
float _FresnelIntensity;
float4 _RimColor;
```

### Part 2: Configure Transparency Render State (Lines 11-16)

기존 `SubShader` 블록을 아래 내용으로 교체하여 투명 렌더링을 활성화합니다.

OpenGL Shading Language

```
SubShader
{
    Tags { 
        "RenderType"="Transparent" 
        "Queue"="Transparent+100" 
        "IgnoreProjector"="True" 
    }
    LOD 100

    Pass
    {
        ZWrite Off
        ZTest LEqual
        Blend SrcAlpha OneMinusSrcAlpha
        Cull Back
        
        CGPROGRAM
        // ... (나머지는 동일)
```

> **설정 이유 (Why these settings):**
> 
> - **`RenderType="Transparent"`**: 렌더 파이프라인에서 투명 처리를 가능하게 함
>     
> - **`Queue"="Transparent+100"`**: 일반 투명 물체보다 나중에 렌더링
>     
> - **`ZWrite Off`**: 투명 물체가 서로 겹쳐 보이도록 깊이 버퍼 쓰기 방지
>     
> - **`Blend SrcAlpha OneMinusSrcAlpha`**: 표준 알파 블렌딩 공식 적용
>     

### Part 3: Implement Fresnel Calculation (After Line 72)

Fragment Shader 시작 부분(거리 계산 전)에 Fresnel 코드를 추가합니다.

OpenGL Shading Language

```
fixed4 frag (v2f i) : SV_Target
{
    // ========================================
    // STEP 3: Fresnel Rim Light Calculation
    // ========================================
    // View-dependent edge lighting for holographic effect

    // View direction: from surface to camera (world space)
    float3 viewDir = normalize(_WorldSpaceCameraPos - i.worldPos);

    // Normalize interpolated normal
    float3 normalDir = normalize(i.worldNormal);

    // Fresnel calculation using dot product
    // NdotV = 1 (facing camera), 0 (grazing angles)
    float NdotV = saturate(dot(normalDir, viewDir));

    // Fresnel term: 0 at center, 1 at edges
    float fresnel = pow(1.0 - NdotV, _FresnelPower) * _FresnelIntensity;

    // ========================================
    // 1단계: 거리 계산 (Distance Calculation)
    // ========================================
    float distanceFromCenter = distance(i.worldPos, _ScannerCenter.xyz);
    
    // ... (이후 스캔 웨이브 코드는 그대로 유지)
```

### Part 4: Add Rim Color to Final Composition (Line ~125)

색상 합성(Color Composition) 섹션을 수정하여 림 라이트 효과를 추가합니다.

OpenGL Shading Language

```
    // 스캔 웨이브 색상
    float3 waveEffect = scanColor * scanWave;

    // 그리드 효과
    float3 gridEffect = gridColor * gridLines * scanWave;

    // STEP 3: Fresnel rim effect
    // Multiply by scanWave to mask rim outside scan area
    float3 rimEffect = _RimColor.rgb * fresnel * scanWave;

    // 최종 색상: 웨이브 + 그리드 + 림 (Additive Blending)
    float3 finalColor = waveEffect + gridEffect + rimEffect;
```

### Part 5: Implement Alpha Calculation (Replace Line 135)

최종 `return` 문을 아래의 알파 계산 로직으로 교체합니다.

OpenGL Shading Language

```
    // ========================================
    // 5단계: Alpha Calculation (Step 3)
    // ========================================
    // Layered transparency system

    // Base transparency (subtle visibility outside scan range)
    float alpha = _BaseAlpha;

    // Boost alpha in scan wave area (reveal effect)
    alpha += scanWave * _ScanAlpha;

    // Add Fresnel rim contribution (only in scanned area)
    alpha += fresnel * scanWave * 0.5;

    // Clamp to valid range [0, 1]
    alpha = saturate(alpha);

    // ========================================
    // 6단계: 최종 출력 (Final Output with Transparency)
    // ========================================
    return fixed4(finalColor, alpha);
}
```

---

## 3. Testing & Verification (테스트 및 검증)

### 🔍 Phase 1: Visual Verification (Scene View)

1. **Scene 열기:** `/Assets/Scenes/SampleScene.unity`
    
2. **적용:** `ScanTestSphere` 오브젝트에 업데이트된 Shader Material 적용
    
3. **체크리스트:**
    
    - [ ] **Transparency:** 물체가 반투명한가? (완전 불투명 X)
        
    - [ ] **Base Alpha:** 스캔 범위 밖에서도 희미하게 보이는가?
        
    - [ ] **Scan Reveal:** 스캔 반경 내에서 불투명도가 증가하는가?
        
    - [ ] **Fresnel Rim:** 가장자리에 밝은 Cyan 색상의 림 라이트가 보이는가?
        
    - [ ] **View Dependency:** 카메라 회전 시 림 효과가 시야각에 따라 변하는가?
        
    - [ ] **No Errors:** 콘솔에 셰이더 컴파일 에러가 없는가?
        

### 🎛️ Phase 2: Property Tuning (Inspector)

**권장 시작 값:**

- `_BaseAlpha`: **0.15** (은은한 기본 가시성)
    
- `_ScanAlpha`: **0.85** (선명한 스캔 효과)
    
- `_FresnelPower`: **2.5** (적당한 림 두께)
    
- `_FresnelIntensity`: **1.0** (밝은 림)
    
- `_RimColor`: **RGB(0.3, 0.9, 1.0)** (Cyan)
    

### 📸 Phase 5: Documentation

- **Screenshot:** `Assets/Screenshots/Step3_Fresnel_Transparency.png` 저장
    
- **포인트:** Fresnel Rim, 투명도 변화, Grid+Rim 결합 효과가 잘 드러나게 촬영
    

---

## 4. Interview Preparation (면접 대비)

### Q1: Fresnel 효과를 어떻게 구현했나요?

> **초보자 답변:** > "표면의 노멀 벡터와 카메라 방향 벡터의 내적을 이용했습니다. 정면은 1, 측면은 0이 되는데, 이를 반전시키고 거듭제곱해서 가장자리를 밝게 만들었습니다."

> **Technical Answer:** > "I calculated the dot product between the surface normal and view direction vectors. Using `pow(1 - saturate(dot(N, V)), power)`, I created the rim light effect. This mimics the **Schlick approximation** of Fresnel equations, where the reflection intensity increases at grazing angles."

### Q2: 왜 ZWrite Off를 사용하나요?

> **초보자 답변:** > "투명한 물체가 겹쳐 보일 수 있게 하기 위해서입니다. ZWrite On이면 앞의 투명 물체가 뒤의 물체를 가려버립니다."

> **Technical Answer:** > "**ZWrite Off** prevents transparent objects from occluding objects behind them in the depth buffer. This is essential for alpha blending. Unity's **Transparent queue** handles the necessary back-to-front sorting to ensure correct visual output."

### Q3: Alpha 계산 공식을 설명해주세요.

> **Technical Answer:** > "It uses a layered additive composition: `alpha = saturate(base + scan + fresnel)`.
> 
> 1. **Base Alpha (0.2):** Spatial awareness.
>     
> 2. **Scan Boost (0.8):** Reveal effect.
>     
> 3. **Fresnel:** Edge emphasis.
>     
>     Finally, `saturate()` clamps the value to [0,1] to prevent rendering artifacts."
>     

### Q4: 성능 최적화는 어떻게 했나요?

> **Technical Answer:** > 1. **Branchless Code:** No `if` statements (100% GPU warp efficiency).
> 
> 2. **Zero Texture Fetches:** All procedural patterns (saves memory bandwidth).
> 
> 3. **Per-pixel Math:** Used `normalize` in frag shader for quality, but kept ALU ops minimal.
> 
> 4. **Instruction Count:** Only ~35-40 instructions, well optimized for mobile.

---

## 5. Success Criteria (완료 기준)

- [ ] Fragment Shader에 Fresnel 계산 (`dot`, `pow`) 구현 완료
    
- [ ] Transparency 활성화 (`Tags`, `Blend`, `ZWrite`) 설정 완료
    
- [ ] Alpha 계산 로직 (`base` + `scan` + `fresnel`) 적용 완료
    
- [ ] Rim Color (가장자리 발광) 추가 완료
    
- [ ] Material Inspector에서 실시간 값 조정 가능
    
- [ ] Unity Console 컴파일 에러 0건
    
- [ ] 시각적 확인 (투명도 + 림 효과 + 스캔 웨이브)
    
- [ ] 포트폴리오용 스크린샷 확보
    

**🚀 Next Step (Step 4):** C# 스크립트 상호작용 (마우스 클릭 트리거, 코루틴 애니메이션, UI 연동)