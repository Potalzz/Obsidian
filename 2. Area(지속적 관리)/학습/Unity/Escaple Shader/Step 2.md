 Step 2 Implementation Plan: Scan Wave Effect                                                                                                                                    
                                                                               
 X-Ray Scanner Shader - 스캔 파동 구현

 ---
 Context (배경)

 목표: Unity HLSL 셰이더로 Vision Pro 스타일의 스캔 웨이브 효과 구현

 현재 상태:
 - ✅ Step 1 완료: 기본 셰이더 골격 및 월드 좌표 시스템 구축
 - ✅ Properties 정의: _ScannerCenter, _ScanRadius, _ScanWidth
 - ✅ Vertex Shader: Object Space → World Space 변환 완료
 - ⏳ Fragment Shader: 현재 디버그 패턴만 출력 (frac(worldPos * 0.1))

 Step 2의 목표:
 1. 거리 기반 스캔 웨이브 시각화
 2. smoothstep으로 부드러운 링 경계 생성
 3. frac()로 사이버펑크 격자 패턴 추가
 4. 파란색/시안색 계열의 스캔 색상 적용
 5. Material Inspector에서 수동 테스트

 왜 이 프로젝트가 펄어비스 포트폴리오로 적합한가:
 - 상용 엔진(Unity) 깊은 이해 증명
 - 수학적 원리(distance, smoothstep, 좌표계 변환) 활용
 - 성능 최적화(if문 제거, branchless 코드)
 - 그래픽스 이론과 실무 능력 결합

 ---
 Mathematical Foundation (수학적 기초 - 면접 대비)

 1. Distance-Based Rendering (거리 기반 렌더링)

 개념: 스캔 중심점으로부터의 거리를 계산하여 구형 파동 생성

 수학 공식:
 float dist = distance(pixelPos, scannerCenter);
 // 내부 동작: sqrt((x-cx)² + (y-cy)² + (z-cz)²)

 면접 답변 (초보자용):
 "distance() 함수는 3D 공간에서 두 점 사이의 직선 거리를 계산합니다. 피타고라스 정리를 3차원으로 확장한 것이고, GPU에 최적화된 내장 함수라서 매우 빠릅니다. 이를 사용하면 스캐너
  중심에서 모든 방향으로 균등하게 확산되는 구형 파동을 만들 수 있습니다."

 면접 답변 (기술적):
 "distance()는 HLSL intrinsic function으로 length(A-B)와 동일하며, GPU의 벡터 연산 유닛에서 병렬로 처리됩니다. 내부적으로 dot product와 sqrt를 사용하며, World Space에서
 계산하므로 오브젝트의 Transform과 무관하게 일관된 효과를 보장합니다."

 왜 World Space를 사용하는가:
 - Object Space는 오브젝트마다 다른 좌표계 (중심이 다름)
 - World Space는 씬 전체에서 동일한 기준점 사용
 - 여러 오브젝트에 같은 스캔 효과를 동시 적용 가능
 - 오브젝트를 회전/이동해도 스캔 방향이 일정

 ---
 2. Smoothstep Function (부드러운 경계)

 수학 공식:
 smoothstep(edge0, edge1, x) =
     t = saturate((x - edge0) / (edge1 - edge0))
     return t * t * (3 - 2 * t)  // Hermite interpolation

 시각적 비교:
 if문 사용 (계단식):        smoothstep 사용 (곡선):
     1|    ┌───                 1|      ╭───
      |    │                      |    ╱
      |    │                      |  ╱
     0|────┘                    0|─╯
       edge0 edge1                edge0  edge1
       ![[Pasted image 20260209172153.png]]

 면접 답변 (초보자용):
 "if문을 사용하면 경계가 각지고, GPU가 서로 다른 분기를 실행하는 픽셀들을 따로 처리해야 합니다. smoothstep은 모든 픽셀이 같은 수식을 계산하고, 결과도 부드러워서 앨리어싱이
 줄어듭니다. 게임에서는 if문 대신 수학 함수를 사용하는 것이 훨씬 빠릅니다."

 면접 답변 (기술적):
 "GPU는 SIMD 아키텍처로 warp 단위로 픽셀을 동시 처리합니다. if문은 warp divergence를 유발하여 서로 다른 분기의 픽셀들을 순차 실행해야 하므로 성능이 절반 이하로 떨어질 수
 있습니다. smoothstep은 branchless 알고리즘으로 모든 레인이 동일한 명령어를 실행하여 vectorization 효율을 극대화합니다."

 스캔 링 생성 원리:
 // 두 개의 smoothstep을 곱하여 링 생성
 float wave1 = smoothstep(innerEdge, _ScanRadius, dist);  // 안쪽: 0→1
 float wave2 = smoothstep(outerEdge, _ScanRadius, dist);  // 바깥: 1→0
 float ring = wave1 * wave2;  // 중앙(radius)에서만 1.0

 ---
 3. Grid Pattern with frac() (격자 패턴)

 수학 공식:
 frac(x) = x - floor(x)  // 소수 부분만 추출 (0~1 반복)

 시각적 설명:
 worldPos.x:  0.0  1.0  2.0  3.0  4.0  5.0
 frac(x):     0.0→1.0→0.0→1.0→0.0→1.0
                  ↓    ↓    ↓    ↓
             주기적으로 반복되는 패턴 생성

 면접 답변 (초보자용):
 "frac()는 소수점 부분만 남기는 함수입니다. 월드 좌표에 주파수를 곱하면 0에서 1로 반복되는 패턴이 만들어집니다. 이를 활용하면 텍스처 없이도 격자 무늬를 만들 수 있어서 메모리를
 절약할 수 있습니다."

 면접 답변 (기술적):
 "frac()는 프로시저럴 패턴 생성의 기본입니다. sin/cos보다 ALU 연산량이 적고, 텍스처 샘플링 대비 메모리 대역폭을 절약합니다. 3축의 frac 값을 평균하면 3D 공간에서 균등한 격자를
 얻을 수 있으며, pow()로 대비를 조정하여 선명도를 제어할 수 있습니다."

 ---
 4. Coordinate Systems (좌표계 이해)
![[Pasted image 20260209172214.png]]

 변환 과정:
 // Vertex Shader에서 한 번 변환, Fragment에서 보간 사용
 o.worldPos = mul(unity_ObjectToWorld, v.vertex).xyz;

 면접 질문: "왜 Fragment Shader가 아닌 Vertex Shader에서 변환하나요?"

 답변:
 "버텍스 세이더는 정점당 1회, 프래그먼트 세이더는 픽셀당 수백만 번 실행됩니다. 월드 좌표 변환은 정점에서 한 번만 하고 보간된 값을 픽셀에서 사용하면 연산량이 엄청나게
 줄어듭니다. 예를 들어 10,000개 정점의 오브젝트가 100만 픽셀을 차지하면, 버텍스에서 하면 10,000번, 프래그먼트에서 하면 1,000,000번 계산해야 합니다."

 ---
 Complete Fragment Shader Code (완전한 구현 코드)

 Implementation (구현부)

 파일: /Users/penguinland/Desktop/Unity/X-Ray_Shader/Assets/Shaders/ScannerShader.shader

 수정 위치: Fragment Shader (Lines 65-71)

 현재 코드 (Step 1):
 fixed4 frag (v2f i) : SV_Target
 {
     // 테스트: 월드 좌표를 색상으로 출력
     fixed4 col = fixed4(frac(i.worldPos * 0.1), 1);
     return col;
 }

 새 코드 (Step 2 - 완전한 스캔 웨이브):
 // Fragment Shader - Step 2: Scan Wave Implementation
 fixed4 frag (v2f i) : SV_Target
 {
     // ========================================
     // 1단계: 거리 계산 (Distance Calculation)
     // ========================================
     // 현재 픽셀의 월드 좌표와 스캐너 중심 간의 유클리드 거리
     // distance(A, B) = sqrt((Ax-Bx)² + (Ay-By)² + (Az-Bz)²)
     float distanceFromCenter = distance(i.worldPos, _ScannerCenter.xyz);

     // ========================================
     // 2단계: 스캔 링 생성 (Scan Ring with Smoothstep)
     // ========================================
     // 부드러운 경계를 가진 링 효과 생성
     // smoothstep(a, b, x)는 x가 a에서 b로 이동할 때 0→1로 부드럽게 변화

     // 내부 경계: 스캔 반경 - 폭 (링의 안쪽 시작점)
     float innerEdge = _ScanRadius - _ScanWidth;

     // 외부 경계: 스캔 반경 + 폭 (링의 바깥쪽 끝점)
     float outerEdge = _ScanRadius + _ScanWidth;

     // 안쪽에서 밝아지는 그라디언트 (0→1)
     float wave1 = smoothstep(innerEdge, _ScanRadius, distanceFromCenter);

     // 바깥쪽에서 어두워지는 그라디언트 (1→0)
     float wave2 = smoothstep(outerEdge, _ScanRadius, distanceFromCenter);

     // 두 그라디언트를 곱하면 중앙(_ScanRadius)에서만 1.0인 링 생성
     // 결과: innerEdge < dist < outerEdge 범위에서만 밝음
     float scanWave = wave1 * wave2;

     // ========================================
     // 3단계: 격자 패턴 생성 (Grid Pattern)
     // ========================================
     // frac() 함수로 반복되는 격자 무늬 생성 (텍스처 불필요)

     float gridFrequency = 5.0;  // 격자 밀도 (높을수록 촘촘)

     // 각 축(X, Y, Z)에 대해 frac() 적용하여 0~1 반복 패턴
     float3 gridPattern = frac(i.worldPos * gridFrequency);

     // 3축 패턴을 평균하여 단일 값으로 합침
     float gridValue = (gridPattern.x + gridPattern.y + gridPattern.z) / 3.0;

     // 대비 증가: pow()로 0 근처 값 강조 (격자선이 선명해짐)
     // pow(1-x, 3)은 x가 0일 때 1, x가 1일 때 0
     float gridLines = pow(1.0 - gridValue, 3.0);

     // ========================================
     // 4단계: 색상 합성 (Color Composition)
     // ========================================
     // 사이버펑크 스타일 파란색/시안색 팔레트

     float3 scanColor = float3(0.2, 0.8, 1.0);  // 밝은 시안 (주 스캔 링)
     float3 gridColor = float3(0.1, 0.4, 0.8);  // 어두운 파랑 (격자선)

     // 스캔 웨이브 색상: scanWave 강도만큼 시안색 적용
     float3 waveEffect = scanColor * scanWave;

     // 그리드 효과: 격자선에 파란색 적용, 스캔 영역에서만 표시
     // scanWave를 마스크로 사용하여 링 밖에서는 격자 숨김
     float3 gridEffect = gridColor * gridLines * scanWave;

     // 최종 색상: 웨이브 + 그리드 (Additive Blending)
     float3 finalColor = waveEffect + gridEffect;

     // ========================================
     // 5단계: 최종 출력 (Final Output)
     // ========================================
     // Alpha는 항상 1.0 (완전 불투명, Step 3에서 투명도 추가 예정)
     return fixed4(finalColor, 1.0);
 }

 ---
 Step-by-Step Implementation (단계별 구현)

 Phase 1: Distance Visualization Test (거리 시각화 테스트)

 목적: distance() 함수가 제대로 작동하는지 확인

 코드:
 fixed4 frag (v2f i) : SV_Target
 {
     float dist = distance(i.worldPos, _ScannerCenter.xyz);
     float normalizedDist = dist / 10.0;  // 0~10 거리를 0~1로 정규화
     return fixed4(normalizedDist, normalizedDist, normalizedDist, 1);
 }

 테스트 방법:
 5. Unity에서 Sphere 생성 (Scale: 10, 10, 10)
 6. ScannerMaterial 적용
 7. Material Inspector: _ScannerCenter = (0, 0, 0)
 8. Scene View에서 확인: 중심이 검정, 외곽이 흰색 그라디언트

 예상 결과: 구형 그라디언트 (radial gradient)

 ---
 Phase 2: Scan Ring Implementation (스캔 링 구현)

 목적: smoothstep으로 링 모양 생성

 코드:
 fixed4 frag (v2f i) : SV_Target
 {
     float dist = distance(i.worldPos, _ScannerCenter.xyz);

     float innerEdge = _ScanRadius - _ScanWidth;
     float outerEdge = _ScanRadius + _ScanWidth;

     float wave1 = smoothstep(innerEdge, _ScanRadius, dist);
     float wave2 = smoothstep(outerEdge, _ScanRadius, dist);
     float scanWave = wave1 * wave2;

     return fixed4(scanWave, scanWave, scanWave, 1);  // 흰색 링
 }

 테스트 방법:
 9. Material Inspector 설정:
   - _ScanRadius = 3.0
   - _ScanWidth = 0.5
   - _ScannerCenter = (0, 0, 0)
 2. 반경 3.0 지점에 흰색 링 확인
 3. _ScanRadius를 1.0 → 5.0으로 조정하며 링 확장 관찰

 예상 결과: 부드러운 경계의 흰색 링

 ---
 Phase 3: Grid Pattern Addition (격자 패턴 추가)

 목적: frac()로 격자 무늬 오버레이

 코드 (위의 Phase 2 코드에 추가):
 fixed4 frag (v2f i) : SV_Target
 {
     // ... (Phase 2의 scanWave 계산 코드)

     // 격자 패턴
     float gridFrequency = 5.0;
     float3 gridPattern = frac(i.worldPos * gridFrequency);
     float gridValue = (gridPattern.x + gridPattern.y + gridPattern.z) / 3.0;
     float gridLines = pow(1.0 - gridValue, 3.0);

     // 링 + 격자 결합
     float finalIntensity = scanWave * (1.0 + gridLines * 0.5);

     return fixed4(finalIntensity, finalIntensity, finalIntensity, 1);
 }

 테스트 방법:
 1. gridFrequency를 2.0, 5.0, 10.0으로 변경하며 격자 밀도 확인
 2. 링 위에 격자선이 나타나는지 확인

 예상 결과: 격자 무늬가 있는 흰색 링

 ---
 Phase 4: Cyberpunk Color Application (최종 색상)

 목적: 파란색/시안색으로 사이버펑크 스타일 완성

 코드: 위의 "Complete Fragment Shader Code" 전체 적용

 테스트 방법:
 1. 최종 코드로 교체
 2. Material Inspector:
   - _ScanRadius = 5.0
   - _ScanWidth = 1.0
   - _ScannerCenter = (0, 1, 0)
 3. Play Mode 없이 Scene View에서 시각적 확인

 예상 결과: 밝은 시안색 링 + 파란색 격자

 ---
 Testing & Verification (테스트 및 검증)

 Test Case 1: Static Visualization

 절차:
 4. Hierarchy > Create > Sphere (Scale: 10, 10, 10)
 5. ScannerMaterial을 Sphere에 적용
 6. Material Inspector 설정:
   - _ScanRadius: 3.0
   - _ScanWidth: 0.5
   - _ScannerCenter: (0, 0, 0)

 체크리스트:
 - 반경 3.0 위치에 시안색 링 표시
 - 링의 폭이 _ScanWidth(0.5)와 일치
 - 격자 패턴이 링 위에 보임
 - 색상이 파란색/시안색 계열

 Test Case 2: Dynamic Radius

 절차:
 1. _ScanRadius를 1.0 → 2.0 → 5.0 → 8.0으로 조정
 2. 각 값에서 링 위치 확인

 체크리스트:
 - Radius 증가 시 링이 확장
 - 부드러운 경계 유지 (앨리어싱 없음)
 - 격자 크기는 일정 (월드 공간 기준)

 Test Case 3: Multiple Objects

 절차:
 1. Scene에 Cube, Sphere, Cylinder 생성
 2. 모두 ScannerMaterial 적용
 3. _ScanRadius를 0 → 10으로 증가

 체크리스트:
 - 모든 오브젝트에 동시에 링 표시
 - 링이 구형으로 확산 (오브젝트 모양 무시)
 - 격자가 모든 오브젝트에서 연속적

 ---
 Interview Q&A (면접 예상 질문)

 Q1: 왜 if문 대신 smoothstep을 사용하나요?

 초보자 답변:
 "if문은 GPU가 각 픽셀마다 다른 경로를 실행해야 해서 느립니다. smoothstep은 모든 픽셀이 같은 수식을 계산하므로 GPU의 병렬 처리 능력을 최대한 활용할 수 있습니다. 또한 부드러운
 경계를 만들어서 앨리어싱도 줄어듭니다."

 기술적 답변:
 "GPU는 SIMD 아키텍처로 warp 단위로 픽셀을 동시 처리합니다. if문은 warp divergence를 유발하여 성능이 절반 이하로 떨어질 수 있습니다. smoothstep은 branchless 알고리즘으로 모든
 레인이 동일 명령어를 실행하여 vectorization 효율을 극대화합니다. 또한 Hermite interpolation으로 1차 미분 연속성을 보장하여 시각적으로 부드러운 전환을 제공합니다."

 Q2: Object Space와 World Space의 차이는 무엇인가요?

 초보자 답변:
 "Object Space는 오브젝트의 중심을 기준으로 하는 좌표계입니다. 오브젝트를 회전하면 좌표도 같이 회전합니다. World Space는 씬 전체의 절대 좌표로, 오브젝트가 어떻게 변형되든 항상
 같은 값을 가집니다. 스캔 효과는 씬 전체에 적용되어야 하므로 World Space를 사용합니다."

 기술적 답변:
 "Object Space는 모델의 로컬 좌표계로 TRS(Translation-Rotation-Scale) 행렬에 종속적입니다. World Space 변환은 unity_ObjectToWorld 4x4 행렬을 곱하여 얻으며, 버텍스 세이더에서 한
  번 변환 후 보간된 값을 프래그먼트 세이더에서 사용합니다. 이렇게 하면 백만 픽셀이 있어도 변환은 수천 개의 정점에서만 실행되므로 효율적입니다."

 Q3: frac() 함수로 어떻게 격자를 만드나요?

 초보자 답변:
 "frac()는 소수 부분만 남기는 함수입니다. 월드 좌표에 주파수를 곱하면 0에서 1로 반복되는 패턴이 생깁니다. 예를 들어 frac(5.7) = 0.7이고 frac(6.7) = 0.7이므로 같은 패턴이
 반복됩니다. 이를 활용하면 텍스처 없이도 격자를 만들 수 있습니다."

 기술적 답변:
 "frac(x) = x - floor(x)로 정의되며, 프로시저럴 패턴 생성의 기본입니다. sin/cos 대비 ALU 연산량이 적고, 텍스처 샘플링 없이 수학 함수만으로 패턴을 생성하여 메모리 대역폭을
 절약합니다. 3축의 frac 값을 평균하면 3D 공간에서 균등한 격자를 얻을 수 있으며, pow()로 대비를 조정합니다."

 Q4: 성능 최적화를 위한 고려사항은?

 초보자 답변:
 "이 셰이더는 if문 대신 smoothstep을 사용하고, 텍스처 샘플링 없이 수학 함수만 사용하며, Vertex Shader에서 월드 좌표를 한 번만 계산합니다. Fragment Shader에서는 간단한 산술
 연산만 하므로 매우 빠릅니다."

 기술적 답변:
 "주요 최적화:
 1. Branchless: if문 제거로 warp efficiency 100%
 2. Pre-computation: 버텍스에서 worldPos 계산, 프래그먼트에서 보간만
 3. Bandwidth: 텍스처 fetch 없음, 레지스터 연산만
 4. Math: sqrt 1회(distance), pow 1회, 나머지는 FMAD
 5. Occupancy: 레지스터 사용량 적어 여러 warp 동시 실행 가능"

 Q5: 모바일에서도 사용 가능한가요?

 답변:
 "네, 가능합니다. Built-in Render Pipeline에 최적화되어 있고, branchless 코드라 모바일 GPU에서도 효율적입니다. 다만 격자 밀도(gridFrequency)를 너무 높이면 앨리어싱이 발생할 수
 있으니 3~5 정도가 적절합니다. 필요하다면 fixed/half precision으로 변경하여 모바일 최적화를 더 강화할 수 있습니다."

 ---
 Common Issues & Solutions (흔한 문제 해결)

 Issue 1: 링이 보이지 않음

 증상: 전체가 검정색

 원인:
 - _ScanRadius가 0 또는 오브젝트에서 너무 멀리 설정
 - _ScannerCenter가 잘못된 위치

 해결:
 1. Material Inspector 값 확인
 2. Debug 코드로 테스트:
 return fixed4(scanWave, 0, 0, 1);  // 빨간색으로 웨이브만 확인

 Issue 2: 링이 각지거나 깜빡임

 증상: 경계가 거칠거나 앨리어싱

 원인:
 - _ScanWidth가 너무 작음
 - gridFrequency가 너무 높음

 해결:
 1. _ScanWidth를 0.5 이상으로
 2. gridFrequency를 5 이하로

 Issue 3: 오브젝트마다 다른 효과

 증상: 같은 Material인데 링 위치가 다름

 원인: World Space 변환 누락

 해결:
 // Vertex Shader에서 필수:
 o.worldPos = mul(unity_ObjectToWorld, v.vertex).xyz;

 ---
 Critical Files (핵심 파일)

 수정 필요:

 - /Users/penguinland/Desktop/Unity/X-Ray_Shader/Assets/Shaders/ScannerShader.shader
   - Fragment Shader (Lines 65-71) 교체
   - 위의 "Complete Fragment Shader Code" 전체 적용

 테스트용:

 - /Users/penguinland/Desktop/Unity/X-Ray_Shader/Assets/Materials/ScannerMaterial.mat
   - Material Inspector에서 Property 조정
   - _ScanRadius, _ScanWidth, _ScannerCenter

 씬 구성:

 - Scene에 Sphere/Cube/Cylinder 생성
 - ScannerMaterial 적용하여 시각적 테스트

 ---
 Next Steps (다음 단계 미리보기)

 Step 3 예고: 투시 및 프레넬 효과
 - Blend Mode 추가 (투명도)
 - Fresnel 효과 (각도에 따른 변화)
 - ZTest 설정 (가려진 부분 강조)

 Step 4 예고: C# 스크립트 상호작용
 - 마우스 클릭으로 스캔 트리거
 - Coroutine으로 _ScanRadius 자동 증가
 - Raycast로 스캔 위치 지정

 ---
 Verification Checklist (최종 확인)

 Step 2 완료 기준:
 - Fragment Shader에 distance(), smoothstep(), frac() 구현
 - Material Inspector에서 _ScanRadius 조정 시 링 확장/축소
 - 사이버펑크 색상(시안/파랑) 적용
 - 격자 패턴 표시
 - Unity Console에 컴파일 에러 없음
 - 면접 질문 5개 답변 준비 완료
 - Scene에서 시각적으로 확인 가능

 추정 소요 시간: 30분 - 1시간 (코드 작성 + 테스트)