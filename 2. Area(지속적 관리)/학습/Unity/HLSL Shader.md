
`float4` = swift로 치면 `SIMD4<float>`와 같음.

자주 사용하는 `fixed`, `half`, `float`를 보자.
`fixed`는 정밀도가 매우 낮아(-2 ~ 2)주로 color에 사용된다.
`half`는 중간 정밀도
`float`는 `float`로 가장 높은 정밀도를 가짐.

정밀도 순서
`float` > `half` > `fixed`


---

`UnityObjectToClipPos()`
>3D 공간의 점을 모니터 화면(클립 공간)으로 좌표게 변환

인자로 받은 값에 MVP(Model, View, Projection) 3개의 행렬을 각각 곱해주는 유니티 내장 메서드

**수학적 의미 (Linear Algebra)**

`UnityObjectToClipPos(v.vertex)`는 선형대수학적으로 **좌표계 변환(Change of Basis)** 을 수행. 3D 공간의 점을 모니터 화면(클립 공간)으로 옮기기 위해 다음 3가지 행렬을 순서대로 곱하는 과정.

$$V_{clip} = M_{projection} \times M_{view} \times M_{model} \times V_{local}$$

이 세 행렬을 미리 하나로 합쳐놓은 것이 바로 **MVP 행렬**(`UNITY_MATRIX_MVP`)이다.

1. **Model Matrix ($M_{model}$):**
    
    - **Local Space → World Space**
        
    - 객체 자신만의 기준(0,0,0)에서 월드 상의 절대 좌표로 이동한다.
        
2. **View Matrix ($V_{view}$):**
    
    - **World Space → View(Camera) Space**
        
    - 월드 전체를 카메라가 원점(0,0,0)이 되도록 이동/회전시킨다. (카메라가 세상을 보는 시점)
        
3. **Projection Matrix ($P_{projection}$):**
    
    - **View Space → Clip Space**
        
    - 3D 공간을 원근법이 적용된 2D 사다리꼴 공간(Frustum)으로 찌그러뜨린다.


## 셰이더의 종류

셰이더는 역할에 따라 총 두가지로 나뉨.

하나는 콘텐츠 셰이더, 하나는 엔진 셰이더

**콘텐츠 셰이더**는 머티리얼 형태로 특정 오브젝트에만 영향을 끼침. 물, 불 등 이펙트를 아티스트가 잘 활용할 수 있게 파라미터화시켜서 셰이더로 만든 것.

**엔진 셰이더**는 엔진 전체에 영향을 끼침. 화면을 어떻게 그리는 지에 대해서 영향을 준다. 엔진 내부 시스템에 적용한다.

- Unity: Shader = 머티리얼용 셰이더
    
- Unreal: Material ≠ Shader (엔진 내부 셰이더 따로 존재)

Unity 기준

|**문서 용어**|**실무적 분류**|
|---|---|
|ShaderLab Shader|Content Shader|
|Shader Graph|Content Shader|
|Custom Render Feature|Engine Shader 성향|
|URP/HDRP 내부 셰이더|Engine Shader|

Unreal 기준

|**문서 용어**|**실무적 분류**|
|---|---|
|Material|Content Shader|
|Material Function|Content Shader|
|Global Shader|Engine Shader|
|Engine .usf|Engine Shader|
