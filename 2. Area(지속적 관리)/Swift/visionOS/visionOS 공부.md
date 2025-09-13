## TapGesture
![[Pasted image 20250719163815.png]]

해당 코드를 `RealityView {...}`밖에 추가해준다.
`targetedToAnyEntity()`를 통해서 어떤 물체가 선택되었는지 확인할 수 있다.


## Turntable 예제 코드
> https://developer.apple.com/documentation/visionos/creating-immersive-spaces-in-visionos-with-swiftui

**Component**
- 컴포넌트는 데이터를 저장하는 구조체
- Entity에 부착되어 특정한 속성이나 상태를 부여
- 컴포넌트는 일반저긍로 행동은 없고, 값만 갖고 있다.

**System**
- **시스템**은 행동(Behavior)을 정의하는 객체.
- 특정 컴포넌트를 가진 **Eniity**를 찾아서, 그에 따른 로직을 실행
- 시간의 흐름에 따라 컴포넌트가 붙은 Entity를 어떻게 업데이트할지 결정

## ECS(Entity-Component-System) 패턴
> 행위(Behavior)와 데이터(Data)를 분리하는 구조

**ECS 패턴**는 게임 엔진과 실시간 그래픽 환경(예: RealityKit, Unity DOTS 등)에서 자주 사용되는 구조로써, 전통적인 OOP(객체지향 프로그래밍)와는 **전혀 다른 방식**으로 시스템을 구성한다.

![[Pasted image 20250830180401.png]]
ECS의 전체적인 구조

#### Entity (엔티티)
> 컴포넌트를 담는 **틀**이라고 생각하면 된다.

- 고유 ID를 가진 존재
- 자기 자신은 아무 기능도 하지 않음
- 컴포넌트를 붙여야 의미가 생김

> 예: 자동차 엔티티, 캐릭터 엔티티, 사과 엔티티 등
```swift
let car = Entity()
```

#### Component (컴포넌트)
- 순수 데이터만 저장하는 구조체
- Entity에 부착돼서 "이 엔티티는 어떤 속성을 가진다"고 정의
- 행동(로직)은 없음

**Component**는 따로 폴더를 만들어서 추가하는 개념이 아니라, 보통 **Entity**내부에 포함되어 있음.

**Component**는 MVVM 아키텍처의 **Model과 유사**하다.
- 데이터 저장
- 로직이 존재하지 않음
- 상태 표현

하지만 ECS아키텍처 내부에서 사용된다는 점에서, 몇가지 부분이 다르다.

***연결 방식***
- **Component:** Entity에 attach된다.
- **Model:** ViewModel이나 Controller와 연결된다.

***로직 처리 주체***
- **Component:** System에서 처리
- **Model:** Controller 또는 ViewModel에서 처리



> 예: 위치, 속도, 회전축, 체력, 색깔 등
```swift
struc HealthComponent: Component {
	var value: Int
}
```


#### System (시스템)
- 로직과 행위를 담당
- 특정 컴포넌트를 가진 Entity들을 찾아서, 그에 대한 로직을 실행
- 시간 흐름에 따른 업데이트 처리

> 예: 모든 `HealthComponent`가 있는 Entity들의 체력을 감소시킴
```swift
struct HealthSystem: System {
	func update(context: SceneUpdateContext) {
		// 체력 감소 로직 처리
	}
}
```


#### 동작 방식 요약 (예시)

예를 들어, 회전하는 공을 만들고 싶다면:

1. `Entity`를 만든다 → 공 자체
    
2. `TurnTableComponent`를 붙인다 → 공은 회전해야 한다는 속성
    
3. `TurnTableSystem`이 돌아가며 → 그 공을 계속 회전시킴


#### 객체지향과의 차이점

| 항목      | ECS 아키텍처                    | 객체지향 프로그래밍 (OOP)     |
| ------- | --------------------------- | -------------------- |
| 핵심 단위   | Entity + Component + System | Class (객체 자체가 기능 포함) |
| 데이터와 행위 | 분리                          | 결합                   |
| 재사용성    | 매우 높음 (컴포넌트 조합 가능)          | 클래스 상속으로 제한됨         |
| 확장성     | 유연함                         | 상속 깊어질수록 어려워짐        |
| 성능      | 캐시 친화적, 병렬처리 쉬움             | 상대적으로 느림 (특히 실시간 환경) |

#### 현실 예시
|상황|Entity|Component|System|
|---|---|---|---|
|비행기 시뮬레이터|비행기 Entity|위치, 속도, 방향|물리 시스템, 조작 시스템|
|RPG 게임 캐릭터|캐릭터 Entity|체력, 위치, 장비, 애니메이션 상태|전투 시스템, AI 시스템|
|VisionOS에서 회전 오브젝트|큐브 Entity|TurnTableComponent|TurnTableSystem|

#### 그렇다면 MVVM은 쓰지 않는가 ?
ECS아키텍처를 사용한다고 해서 모든 로직까지 해당 아키텍처를 통해 구성하지는 않는다.

SwiftUI 등 UI 레이어에서의 **상태 관리와 뷰 바인딩 등 반복적인 UI 로직**에서는 MVVM을 사용한다.
`(MVVM이라고 예시를 들었지만, 당연히 MVVM만을 고집하는 것은 아님)`

공간상의 3D 객체 동작(물리, 회전, 애니메이션)은 ECS로 처리하고,
UI 상태, 로딩, 네트워크 등은 MVVM으로 처리하는 하이브리드패턴이 보편적으로 사용된다.

##### VisionOS 개발에서의 ECS활용
- **3D 씬, 물리, 애니메이션, 입력, 렌더링 등** 핵심 동작은 ECS 구조로 처리된다.
	
- visionOS용 예제도 대부분 **ECS 기반으로 구현된 코드 위주**
	
- 제로 ECS 구조는 **게임 개발에 적합하고, 복잡한 공간 동작을 모듈형으로 분리하여** 유지보수성과 성능 최적화에 유리함

visionOS의 **공식 권장 방식**이기도 하고, **실제 예제·프로젝트**도 **ECS 기반**이 대부분임.

#### 그래서 결론은 ?
visionOS의 **공간(Scene) 구성과 객체 동작**은 ECS가 표준이고, 대부분 예제 및 실무도 이 구조를 따른다. 반면, SwiftUI 화면과 일반 로직(UI 상태, 모델 데이터, 로딩 등)은 **MVVM 패턴**이 흔하게 병행됨.

#### Entity에 관한 추가 내용
```swift
if let plus = attachments.entity(for: "plus") {
        plus.position = SIMD3(1.6685265, 1.82187057, -0.07426834)
        plus.orientation = simd_quatf(angle: -.pi / 2, axis: SIMD3(0, 1, 0))

        content.add(plus)
      }
```

위 코드는 enity를 생성하는게 아닌, "plus"라는 ID에 해당하는 SwiftUI 뷰가 Attachments에 등록되어있는 것을 불러온다.

`attachments.entity(for: "plus")`를 호출하면,  
`Attachment(id: "plus") { ... }`에서 정의한 SwiftUI 뷰가 **Entity 형태로 반환**됨

```swift
Attachments: {
    Attachment(id: "plus") {
        PlusButtonView {
            print("plus tapped")
        }
    }
}
```

최종적으로 `.add(plus)`로 RealityView에 추가해서 실제로 보여줌




## SIMD
> **한 번의 명령어로 여러 데이터를 동시에 처리**하는 방식. CPU/GPU에서 병렬 연산이 가능해 빠르다.

`realityKit`에서 많이 사용하는 `SIMD3<Float>`는 3차원 벡터를 `Float`타입으로 표현한 구조체이다.
`SIMD3`:  3개의 값을 가진 SIMD벡터 (x, y, z 좌표 등)

### `SIMD3<Float>`를 쓰는 이유

#### 1. 성능 향상
- Swift의 `simd` 모듈은 하드웨어 수준의 SIMD 명령어를 활용
    
- 벡터/행렬 연산을 매우 빠르게 수행 가능  
    (예: 벡터 합, 내적, 외적, 변환 등)

#### 2. 가독성 좋고 직관적
- 3D 좌표, 색상값 등 벡터 표현이 쉬움  
    예: `SIMD3<Float>(r, g, b)`처럼 RGB 색상도 표현 가능

#### 3. 연산 오버로드 제공
- +, -, *, / 같은 연산자 사용이 가능  
    벡터 간 연산도 직관적으로 표현 가능


### 그럼 `SIMD4`는 무엇일까 ?
**SIMD3**까지는 3개의 값 x, y, z 좌표값을 가진 벡터라는 부분이 이해가 간다.
하지만 SIMD는 하나의 좌표가 더 늘어나는 것인데 그럼 4차원인걸까 ?

결론부터 말하면 아니다.

#### SIMD4란 ?
>`4D 벡터(SIMD4<Float>)`는 **4개의 float 값**으로 이루어진 벡터인데, 단순히 차원이 하나 더 많아졌다고만 보기보다는 **3D 그래픽스에서 특정 목적(위치 or 방향)** 으로 추가된 개념이다.

#### 왜 4D 벡터를 사용할까 ?
3D 공간에서의 위치와 방향, 변환을 행렬로 다루기 위해서이다.
이건 **동차 좌표(homogeneous coordinate)** 라는 개념과 연결돼 있음.


#### 동차 좌표란 ?
> 동차 좌표란 w 값이 의미하는 것을 뜻한다

**위치 벡터(w = 1):** `(x, y, z, 1.0)` 3D 공간상의 점
**방향 벡터(w = 0):** `(x, y, z, 0.0)` 3D 공간상의 방향


#### 좌표 변환하기
`SIMD`로 이루어진 값이, 특정 위치에서의 점의 값이라는 것을 알았다.
해당 값을 변환하기 위해서는 `simd_float4x4`라는 **변환 행렬**을 곱해줘서 적용해주어야 한다.

#### 변환 행렬이란 ?
>변환 행렬은 3D공간의 변환을 표현하는 4x4 행렬이다.

##### 행렬 변환을 쓰는 이유
>*"이동, 회전, 스케일 같은 공간 변환을 수학적으로 간단하고 빠르게 처리하고,  
>여러 변환을 하나로 묶어서 한 번에 적용할 수 있기 때문"*

만약에 특정 좌표에 대해 **위치 이동, 회전, 크기 조절**을 각각 x, y, z 좌표 각각 따로 수식으로 계산하려면 매우 복잡할 것이다.

행렬은 이동, 회전, 스케일 변환을 하나의 **4×4 행렬**에 합칠 수 있으므로,
행렬 변환을 통해 변환한다면 **한 번의 곱셈으로 처리가 가능**하다.

##### 행렬은 변환을 결합하기 쉽다
**여러 변환**을 하나의 행렬로 합칠 수 있기 때문에 아래오 같이 한 번만 곱하면 모든 변환이 적용된다.

`이동 → 회전 → 스케일` = `translationMatrix * rotationMatrix * scaleMatrix`

##### 행렬은 방향과 위치를 동시에 다룬다#
3D에서 방향(벡터)과 위치(점)를 구분해야 하는데,  
**동차 좌표(homogeneous coordinate)** + 4×4 행렬을 쓰면  
`w = 1` → 위치는 이동 변환 적용  
`w = 0` → 방향은 이동 변환 무시  
이게 **자동**으로 된다.

**변환 행렬은 변환 공식 압축 파일과도 같다.**

점(1, 0, 0)을 90도 회전, x축으로 5 이동하는 예제를 통해 살펴보자.

**행렬 없이**
```swift
// 회전
let rotatedX = cos(-.pi/2) * 1 - sin(-.pi/2) * 0 // 0
let rotatedY = sin(-.pi/2) * 1 + cos(-.pi/2) * 0 // -1

// 이동
let finalX = rotatedX + 5 // 5
let finalY = rotatedY     // -1
```

**행렬을 통한 계산**
```swift
let rotation = float4x4(rotationZ: -.pi/2)
let translation = float4x4(translation: SIMD3<Float>(5, 0, 0))
let transform = translation * rotation

let point = SIMD4<Float>(1, 0, 0, 1)
let result = transform * point // 자동 계산
```

행렬을 사용하면 4x4행렬에 변환하고 싶은 수치만 넣어서 간편하게 조정할 수 있다



## Spatial Computing을 위한 SwiftUI
https://developer.apple.com/documentation/visionOS/World

**공간 컴퓨팅**에서 **Scene** 레벨은  `Window`, `Volume`, `FullSpace` 총 3가지로 이루어져 있다.
이 화면은 모두 `SwiftUI`로 구성되어 있다.

이 세 가지 **Scene**은 **Space**개념으로 나뉘는데, 
**Shared Space**에는 `Window Scene`, `Volume Scene`두 가지가 포함된다.
**Full Space**에는 `Immersion Style`에 따라서 세 단계로 나뉜다.

여러 개의 앱을 실행시키면 모두 같은 공간에 위치하는데  이 공간이 **Shared Space**.

![[Pasted image 20250830200947.png]]
(Shared Space 공간)

앱에서 `Immersive Space`씬이 표시되면, 앱은 **Full Space** 공간으로 들어감.
그러면 **Shared Space**를 벗어나므로, 해당 공간에 위치한 다른 **Scene**들은 보이지 않게 된다.
`Immersive Space`를 표시한 해당 앱은 사용자가 볼 수 있는 **유일한 앱**이 된다.

![[Pasted image 20250830201038.png]]
(Immersive Space를 보여줘 Full Space공간으로 들어간다)

이 쯤에서 Full Space와 Immerisve Space의 용어가 헷갈릴 수 있기에 짚고 넘어가자면,
**Full Space**는 **개념적인 용어**이고(Shared Space또한 마찬가지)
`Immersive Space`는 **Full Space**개념을 코드로 제어하는 방식이다.

각각의 자세한 내용은 다음과 같다.

- **Full Space (개념)**
    - 사용자의 현실 공간(Shared Space)을 넘어서 **앱이 방 전체를 무대**로 삼아 환경을 완전히 제어하는 모드.
    - 사용자 주변 전체(360°)를 앱이 가상 콘텐츠로 채우거나, 현실을 부분 또는 완전히 차단해서 보여준다.
    - 몰입 수준(완전 몰입, 부분 몰입 등)에 따라 세부 스타일을 적용한다(예: mixed/progressive/full).
        
- **ImmersiveSpace (API/Scene)**
    - SwiftUI에서 `ImmersiveSpace`로 선언하는 **Scene** 타입. 이것이 바로 개발자가 Full Space 경험을 정의하고 제공하는 방식.
    - `ImmersiveSpace` 안에서 뷰/RealityKit 컨텐츠를 작성하고, `immersionStyle` 같은 속성으로 `.mixed`, `.progressive`, `.full` 등을 지정한다.
    - 런타임에서 `openImmersiveSpace(id:)` 같은 API로 진입/퇴장하게 된다.


정리하자면, 앱 하나는 여러 개의 Scene을 가지고 있음.
**Scene**들은 각각 **Shared Space**와 **Full Space**에 위치해 있다.
- **Shared Space**에는 `window`와 `volume`이 **Group**으로 이루어져 있고, **Group**내부에 각 **Scene**의 인스턴스들이 포함되어 있다.
- **Full Space**에는 `Immersive Space`가 위치해 있고, 이는 `Immersion Style`에 따라서 각기 다른 성질을 가진다.

``` swift
App (프로세스)
└─ Scenes (앱이 선언한 여러 Scene)
   ├─ Shared Space 관련 Scenes
   │  ├─ WindowGroup (Scene)
   │  │   └─ Window 인스턴스들 (유저/시스템이 여러 개 생성 가능)
   │  └─ VolumeGroup (Scene)
   │      └─ Volume 인스턴스들 (유저/시스템이 여러 개 배치 가능)
   │
   └─ Full Space 관련 Scenes
      └─ ImmersiveSpace (Scene)  ← (여러 ImmersiveSpace 선언 가능, 보통 동시에 활성화는 1개)
          └─ ImmersionStyle: .mixed / .progressive / .full

```

앱을 실행하면 기본적으로 **Shared Space**로 실행되기 때문에, `window`가 나오게 된다.

>앱 실행과 동시에 `Immersive Space`가 나오게 할 수는 없을까 ?

![[Pasted image 20250830205002.png]]
([wwdc23 Go beyond the window with SwiftUI](https://www.youtube.com/watch?v=U97XS91blI4&ab_channel=AppleDeveloper) 내용 참고)

앱에 대한 Scene 매니페스트를 설정하면 가능하다.

또한 사용자가 `Immersive Space`를 종료하면 앱이 `window`로 돌아가도록 할 수도 있다.



### Window
윈도우에서는 `SwiftUI`에 있는 제스쳐를 사용할 수 있다.
추가로 3D 환경에서의 상호작용을 위해 추가된 제스쳐들도 있다.
![[Pasted image 20250830185400.png]]


### Volume
`Model3D`를 통해서 앱에서 3D 콘텐츠를 간단하게 추가할 수 있다.
![[Pasted image 20250830185611.png]]

`Model3D`는 로딩하는데 시간이 걸리기 때문에 이미지와 달리 비동기적으로 작동한다.


![[Pasted image 20250830185901.png]]
`Model3D`는 또 다른 `SwiftUI` 이므로, `.padding3D()`를 통해서 Z축으로 패딩을 줄 수 있다.


### FullSpace
`FullSpace`에는 총 3개의 `Immersion Style`이 있다.
- `.full`: 100%가상 환경만 보여주는 화면 전체를 에워싸는 몰입형 환경
- `.mixed`: 현실 세계와 가상 컨텐츠가 함께 보이는 모드
- `.progressive`: 기본 상태는 `.mixed`이지만, 몰입도를 단계적으로 `.full`까지 조절할 수 있음.

![[Pasted image 20250830205210.png]]
`passthrough`를 어둡게 설정하여 공간 콘텐츠에 더 집중되도록 만들 수 있다.

`Immersive Space`에서 현실 손을 비활성화하고 가상 손을 띄울 수 있다.

![[Pasted image 20250830205350.png]]
(현실 손을 비활성화 한다)

![[Pasted image 20250830205445.png]]
(가상 손을 불러오고 루트의 자식으로 추가해준다)

![[Pasted image 20250830205731.png]]
(ARKit와 손 추적 API를 사용하고, handTracking시스템을 시작해야 한다)

![[Pasted image 20250830205836.png]]
손 추적 앵커 업데이트를 확인하고 왼손, 오른손을 구분하기 위해 글로브의 트랜스폼과 손의 앵커가 동일한지 확인하고 동일한 조인트 이름을 갖고 있는지 확인한다.
이렇게 하면 올바르게 매핑되고 장갑 엔티티가 자동으로 앵커링된다.

![[Pasted image 20250830210115.png]]
다시 `ImmersiveSpace`로 돌아가서 가상 손을 추가해주면 된다.

![[Pasted image 20250830210244.png]]
실제 손이 가상 글러브로 바뀐 모습



## Hello World 클론 코드
https://developer.apple.com/documentation/visionos/world
해당 프로젝트를 따라 만들어보면서 정리한 내용

### 아키텍처
#### 1. 전체 구조: 기능 중심 아키텍처 (Feature-Based Architecture)

가장 상위 레벨에서는 앱의 구조를 **기능(Feature) 중심**으로 구성했다.
**모듈러 아키텍처**라는 큰 개념을 **기능 중심 폴더 구조**라는 특정한 방식으로 구현한 것.
`Globe`, `Orbit`처럼 기능별로 폴더를 나누고 `Entities`, `Systems`처럼 여러 기능이 공유하는 기술 계층(Layer)으로 분리하는 방식이다.
이는 프로젝트가 커져도 특정 기능을 찾고 수정하기 쉽게 만들어주는 매우 현대적이고 실용적인 구성 방식이다.

---

#### 2. UI 계층: MVVM (Model-View-ViewModel)

사용자에게 보여지는 화면과 상호작용을 처리하는 부분은 **MVVM 패턴**을 따른다.
`ViewModel`의 존재가 이를 증명하며, 이는 SwiftUI 앱에서 UI 로직과 상태를 데이터 로직과 분리하기 위한 표준적인 방식임.

---

#### 3. 3D/시뮬레이션 계층: ECS (Entity Component System)

3D 그래픽 객체를 처리하고 시뮬레이션을 구동하는 핵심적인 부분은 **ECS 패턴**을 사용.
`Entities`와 `Systems` 폴더는 이 패턴을 사용했다는 명백한 증거이며, 이는 RealityKit과 같은 프레임워크에서 성능과 데이터 관리를 최적화하기 위한 최고의 선택.

---

window의 정렬은 `alignmentGuide`를 통해서 커스텀 하여 정렬.

```swift
VStack {
...
메인 텍스트
...
}
.alignmentGuide(.earthGuide) { context in
	context[VerticalAlignment.top]
}

extension VerticalAlignment {
    /// A custom alignment that pins the background image to the title.
	private struct EarthAlignment: AlignmentID {
		static func defaultValue(in context: ViewDimensions) -> CGFloat {
			context[VerticalAlignment.top]
        }
    }
    /// A custom alignment guide that pins the background image to the title.
	fileprivate static let earthGuide = VerticalAlignment(
		EarthAlignment.self
    )
}
```

`NavigationStack`을 통해 네비게이션 컨트롤하고, 자동으로 배경에 **corner rounded glassEffect Background**가 생긴다.

### alignmentGuide
>자신의 어떤 지점을 기준으로 정렬에 참여할 지 재정의하는 모디파이어

- `HStack(alignment: .bottom)`을 '바닥에 그어진 긴 흰색 선'이라고 상상해 본다면,
- HStack은 그 안에 있는 모든 뷰(자식 뷰)들을 가져와서 "각자의 맨 아래(bottom)를 이 흰색 선에 맞추세요"라고 명령한다.
- 이때, 특정 뷰(예: `Circle()`)가 **`.alignmentGuide(.bottom) { ... }`** 를 사용하면, 이 원은 HStack에게 이렇게 말하는 것과 같다.
- "잠시만요, 저는 제 맨 아래(bottom)를 흰색 선에 맞추고 싶지 않아요. 대신 **제 중심(center)을 그 흰색 선에 맞춰주세요**."

**사용 방법**
우선 alignmentGuide는 `Stack`의 마지막에 붙이는 `modifier`이다.
1. 해당 컨테이너가 사용하는 정렬 기준과 일치하는 가이드를 지정한다.
2. 새로운 기준점을 지정해준다.


### Entity 구조
해당 프로젝트의 Entity는 단순히 3D 모델 하나를 의미하는 것이 아니라, 여러 자식 Entity와 데이터 컴포넌트를 조합하여 **하나의 작은 시스템**처럼 동작하도록 설계되어있다.



## BounceBall Project

### 평면 인식하기
ARKit Planedetection Provider로 주변 평면 인식 후, RealityKit으로 보이지 않는 재질(`OcclusionMaterial`)을 입혀서 인식한 현실 공간의 평면 위치에 가상 평면을 렌더링하여 설치함.

#### ARKit 관련
[WWDC 공간 컴퓨팅을 위한 ARKit 알아보기](https://www.youtube.com/watch?v=XHqANANYTyg&ab_channel=AppleDeveloper)

ARKit은 세 종류의 블록으로 구성되어 있다.

**Session**, **DataProvider**, **Anchor**

**Anchor**
현실의 위치와 방향을 나타낸다.
모든 앵커는 고유 `UUID`와, `Transform`을 지닌다.
어떤 유형의 앵커는 추적이 가능하다.
추적 가능한 앵커가 추적이 되지 않는다면, 해당 앵커로 앵커링한 가상 콘텐츠를 숨겨야한다.

**DataProvider**
데이터 공급자는 개별 ARKit기능을 나타낸다.
데이터 공급자의 유형에 따라 제공하는 데이터 유형이 달라진다.

**Session**
세션은 ARKit 기능이 결합된 집합을 나타낸다.

세션을 실행하려면 데이터 공급자 집합을 제공한다.
세션이 실행되면 데이터 공급자가 데이터를 받기 시작한다.

![[Pasted image 20250913191828.png]]
업데이트는 데이터 유형에 따라 다른 주파수에서 비동기적으로 들어온다.


**ARKit에서 카메라로 얻은 데이터는 접근할 수 없다.**
![[Pasted image 20250913184015.png]]

Camera로 얻은 데이터의 경우 ARKit daemon으로 전송되고, Apple 자체 알고리즘으로 변환시켜 clients단에 제공된다. 그렇기 때문에 가공된 데이터만을 받아서 사용할 수 있다.

ARKit에 접근하기 위한 조건.
1. 앱이 반드시 Full Space에 진입해야 한다.
2. 일부 유형의 ARKit 데이터는 접근 권한을 요구한다.
   - ![[Pasted image 20250913184205.png]]

#### Scene understanding

**Plane detection**
주변 환경에서 평면을 감지하고, 감지된 평면은 `PlaneAnchor`의 형태로 제공된다.
`PlaneAnchor`는 컨텐츠를 원할히 배치하는데 사용된다.(ex. 가상 객체를 탁자 위에 배치)
또한, 물리 시뮬레이션에도 사용이 가능하다.

Plane의 종류에 따라서 분류한다.
![[Pasted image 20250913200221.png]]
[표면의 종류] 



**Scene geometry**
![[Pasted image 20250913200341.png]]
[Scene geometry 인식]

Scene geometry는 현실의 모양을 추정하는 다각형 메시가 있는 앵커를 제공하는데,
제공하는 DataProvider타입은 `SceneReconstructionProvider`이다.

ARKit가 주변 환경을 스캔하면, 주변 환경은 세분화 매시로 재구성되어 `MeshAnchor`의 형태로 제공된다.
`MeshAnchor`역시 `PlaneAnchor`와 같이 원활한 콘텐츠 배치에 사용될 수 있다.
`MeshAnchor`를 사용함으로써 물리 시뮬레이션을 보다 현실적으로 구현할 수 있다.

각 `MeshAnchor`는 메시 지오메트리를 포함한다.
![[Pasted image 20250913210813.png]]
[MechAnchor의 구성]

![[Pasted image 20250913210856.png]]
[Mesh의 분류 종류]

**Image Tracking**
>현실의 2D 이미지를 감지

이미지 추적에 쓰이는 DataProvider 타입은 `ImageTrackingProvider`
`ImageTrackingProvider`는 감지하려는 **ReferenceImage**의 집합으로 설정한다.

**ReferenceImage**를 생성하는 방법에는 몇 가지가 있다.

프로젝트 에셋 카탈로그의 AR 리소스 그룹에서 로드하기.

`CVPixelBuffer`나 `CGImage`를 제공하여 **ReferenceImage**를 직접 초기화.

이미지가 감지되면 `ARKit`는 `ImageAnchor`를 제공한다.
`ImageAnchor`는 알려진 정적으로 배치된 이미지에 배치할 때 유용하다.
	Ex.영화 포스터 이미지 옆에 영화 정보를 보여 줄 때.

![[Pasted image 20250914003111.png]]
[ImageAnchor]

`ImageAnchor`는 스케일 팩터를 포함하는데, 감지된 이미지의 크기가 지정한 물리적 크기 및 앵커가 상응하는 **ReferenceImage**와 비교했을 때 어떤지를 나타낸다.

#### HandTracking
![[Pasted image 20250914003330.png]]
`HandTracking`이 제공하는 `Anchor`에는 








