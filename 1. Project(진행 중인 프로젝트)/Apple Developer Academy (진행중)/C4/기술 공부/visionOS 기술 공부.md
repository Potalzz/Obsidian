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
#### Entity (엔티티)
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


## 커맨드(Command) 패턴

## Entity
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
>`4D 벡터(SIMD4<Float>)`는 **4개의 float 값**으로 이루어진 벡터인데, 단순히 차원이 하나 더 많아졌다고만 보기보다는 **3D 그래픽스에서 특정 목적(위치 or 방향)**으로 추가된 개념이다.

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

#### 왜 행렬 변환을 사용할까 ?
>변환 행렬은 3D공간의 변환을 표현하는 4x4 행렬이다.

**행렬 변환**을 쓰는 이유는,
>*"이동, 회전, 스케일 같은 공간 변환을 수학적으로 간단하고 빠르게 처리하고,  
>여러 변환을 하나로 묶어서 한 번에 적용할 수 있기 때문"*

만약에 특정 좌표에 대해 **위치 이동, 회전, 크기 조절**을 각각 x, y, z 좌표 각각 따로 수식으로 계산하려면 매우 복잡할 것이다.

행렬 변환을 통해 적용하려면








