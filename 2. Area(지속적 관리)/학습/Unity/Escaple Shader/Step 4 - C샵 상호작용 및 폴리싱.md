
# X-Ray Scanner Shader - 마우스 클릭 스캔 트리거 구현

## 1. Context (배경)

**변경 이유 (Why This Change):**

런타임 상호작용(Runtime Interactivity)을 추가합니다. 화면의 아무 곳이나 클릭하면 해당 지점에서 바깥쪽으로 퍼져나가는 스캔 웨이브를 트리거하도록 만듭니다. 이를 통해 정적인 셰이더 데모를 동적이고 상호작용 가능한 X-ray 스캐닝 경험으로 전환합니다.

**현재 상태 (Current State):**

- ✅ **1-3단계 완료:** 월드 공간 스캔 링, 절차적 그리드, 프레넬 투명도가 적용된 셰이더 구현 완료
    
- 현재는 **재질 인스펙터(Material Inspector)**를 통해서만 제어 가능 (런타임 상호작용 없음)
    
- `Assets/Scripts/` 폴더는 존재하지만 비어 있음 (아직 C# 스크립트 없음)
    
- **씬 구성:** ScanTestSphere (크기 10), Wall, HiddenItem, Floor (콜라이더 포함), Main Camera, Directional Light
    
- 모든 3개의 스캔 객체가 `ScannerMaterial`을 공유함 (동일한 재질 자산 사용 = 한 번의 업데이트로 모두 적용됨)
    

**C#에서 제어할 셰이더 속성:**

- `_ScannerCenter` (Vector4) — 스캔 시작점의 월드 좌표
    
- `_ScanRadius` (Float) — 중심으로부터의 링 거리 (이 값을 애니메이션화)
    
- `_ScanWidth` (Float) — 링 두께
    

---

## 2. Implementation Plan (구현 계획)

### Part 1: ScannerController.cs 생성

**파일:** `Assets/Scripts/ScannerController.cs`

**아키텍처 구조:**

코드 스니펫

```
classDiagram
    class ScannerController {
        +Material scannerMaterial
        +float maxScanRadius
        +float scanSpeed
        -Start()
        -Update()
        -StartScan()
        -AnimateScan()
        -OnDisable()
    }
```

- `ScannerController : MonoBehaviour`
    
    - `[SerializeField] Material scannerMaterial` : 인스펙터에서 ScannerMaterial 드래그 앤 드롭
        
    - `[SerializeField] float maxScanRadius = 20f` : 최대 확장 거리
        
    - `[SerializeField] float scanSpeed = 10f` : 초당 이동 단위 (Unit/sec)
        
    - **메서드 흐름:**
        
        - `Start()` → `Camera.main` 캐싱, `_ScanRadius`를 0으로 초기화
            
        - `Update()` → `Input.GetMouseButtonDown(0)` → 레이캐스트(Raycast) → `StartScan()` 호출
            
        - `StartScan()` → `_ScannerCenter` 벡터 설정, 코루틴 시작
            
        - `AnimateScan()` → 코루틴: `_ScanRadius`를 0에서 max까지 보간(Lerp) 후 초기화
            
        - `OnDisable()` → 에디터 변경 사항이 영구적으로 남지 않도록 재질 초기화
            

**주요 설계 결정 사항 (Key Design Decisions):**

1. **[SerializeField] Material:** `ScannerMaterial.mat` 자산을 직접 참조합니다. 3개의 객체(ScanTestSphere, Wall, HiddenItem)가 이 재질을 공유하므로, 한 번의 `SetFloat` 호출로 씬 전체가 동시에 업데이트됩니다. 이는 전역 스캔 효과를 위해 의도된 동작입니다.
    
2. **애니메이션을 위한 코루틴:** 매 프레임 `yield return null`을 반환하며 `scanSpeed * Time.deltaTime`만큼 반지름을 증가시킵니다. 이는 프레임 독립적인 애니메이션 구현 능력을 보여줍니다.
    
3. **새 클릭 시 이전 스캔 중단:** 새로운 클릭이 발생하면 `StopCoroutine()`을 호출하여 이전 애니메이션과 겹치는 것을 방지합니다.
    
4. **OnDisable 정리(Cleanup):** 플레이 모드 종료 시 `_ScanRadius`를 0으로 리셋하여, 에디터 상에 변경된 재질 값이 영구적으로 남는 것을 방지합니다.
    
5. **Physics.Raycast:** 월드 공간의 충돌 지점(hit point)을 가져옵니다. 바닥(MeshCollider), 벽(BoxCollider), 구체(SphereCollider) 모두 레이캐스트의 대상이 됩니다.
    

### Part 2: 씬에 스크립트 부착

**옵션:** `ScannerController`를 **Main Camera**에 부착합니다 (카메라는 이미 존재하며, 스크립트에서 어차피 Camera 참조가 필요합니다).

**인스펙터 설정 (Inspector Setup):**

- `Assets/Materials/ScannerMaterial.mat`을 `scannerMaterial` 필드에 드래그
    
- `maxScanRadius`: **20** (크기 10인 구체를 덮기에 충분한 크기)
    
- `scanSpeed`: **10** (최대 크기 도달까지 약 2초 소요)
    

### Part 3: 셰이더 변경 필요 없음

셰이더에는 이미 필요한 속성들(`_ScannerCenter`, `_ScanRadius`)이 구현되어 있습니다. C# 스크립트는 단지 `Material.SetFloat()`와 `Material.SetVector()`를 호출하여 값을 전달하기만 하면 됩니다.

---

## 3. Critical Files (주요 파일 및 작업)

|**파일 (File)**|**작업 (Action)**|
|---|---|
|`Assets/Scripts/ScannerController.cs`|**생성 (CREATE)** — 새로운 C# MonoBehaviour|
|`Assets/Shaders/ScannerShader.shader`|**변경 없음 (No changes)**|
|`Assets/Scenes/SampleScene.unity`|Main Camera에 스크립트 부착 (MCP 이용)|

---

## 4. Verification (검증)

1. **컴파일 확인:** 스크립트 생성 후 콘솔(console)에 에러가 없는지 확인
    
2. **컴포넌트 부착:** `manage_components`를 통해 Main Camera에 `ScannerController` 추가
    
3. **재질 참조:** `scannerMaterial` 필드에 `ScannerMaterial.mat` 할당
    
4. **플레이 모드 테스트:** 플레이 모드 진입 → 씬(Scene) 클릭 → 클릭한 지점부터 스캔 웨이브가 퍼져나가는지 확인
    
5. **스크린샷:** 결과를 `Assets/Screenshots/Step4_Interactive_Scan.png`에 캡처 및 저장



# 구현 내용
## 4단계 완료: 작업 요약

⏺ **Step 4: C# 스크립트 상호작용 - 완료 (Step 4: C# Script Interaction - Complete)**

### 📂 생성된 파일: `Assets/Scripts/ScannerController.cs`

- **마우스 클릭:** `Physics.Raycast`를 통해 월드 공간의 충돌 지점(hit point)을 감지
    
- **`StartScan()`:** `_ScannerCenter`를 클릭한 위치로 설정하고 코루틴(Coroutine) 시작
    
- **`AnimateScan()`:** `_ScanRadius`를 0에서 20까지 초당 10단위 속도로 확장 (전체 스캔에 2초 소요)
    
- **`StopCoroutine()`:** 빠르게 연속 클릭할 경우 스캔 애니메이션이 겹치는 현상 방지
    
- **`OnDisable()`:** 에디터 상에서 재질(Material) 값이 영구적으로 변경된 채 남지 않도록 반경을 0으로 초기화
    

### 🛠 구현 중 주요 수정 사항 (Key Fix)

이 프로젝트는 레거시 `UnityEngine.Input` 대신 **New Input System** 패키지를 사용하고 있습니다. 이에 따라 입력 감지 코드를 다음과 같이 업데이트했습니다:

- 변경 전: `Input.GetMouseButtonDown(0)`
    
- 변경 후: `Mouse.current.leftButton.wasPressedThisFrame`
    

### 🎬 씬(Scene) 설정

- `ScannerController`가 **Main Camera**에 부착됨
    
- `scannerMaterial` 필드는 `Assets/Materials/ScannerMaterial.mat`을 참조
    
- 3개의 객체(ScanTestSphere, Wall, HiddenItem)가 모두 **동일한 재질을 공유** → 단 한 번의 `SetFloat` 호출로 모든 객체가 동시에 업데이트됨
    

### ✅ 검증 (Verification)

- 컴파일 에러 0건
    
- Play 모드 런타임 에러 0건
    
- 스크린샷 저장 완료: `Assets/Screenshots/Step4_Interactive_Scan-1.png`