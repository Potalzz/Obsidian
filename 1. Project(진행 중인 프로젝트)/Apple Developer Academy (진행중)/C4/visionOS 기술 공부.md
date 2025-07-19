
### TapGesture
![[Pasted image 20250719163815.png]]

해당 코드를 `RealityView {...}`밖에 추가해준다.
`targetedToAnyEntity()`를 통해서 어떤 물체가 선택되었는지 확인할 수 있다.



### Turntable 예제 코드
> https://developer.apple.com/documentation/visionos/creating-immersive-spaces-in-visionos-with-swiftui

**Component**
- 컴포넌트는 데이터를 저장하는 구조체
- Entity에 부착되어 특정한 속성이나 상태를 부여
- 컴포넌트는 일반저긍로 행동은 없고, 값만 갖고 있다.

**System**
- **시스템**은 행동(Behavior)을 정의하는 객체.
- 특정 컴포넌트를 가진 **Eniity**를 찾아서, 그에 따른 로직을 실행
- 시간의 흐름에 따라 컴포넌트가 붙은 Entity를 어떻게 업데이트할지 결정

#### ECS(Entity-Component-System) 아키텍처
> 행위(Behavior)와 데이터(Data)를 분리하는 구조

**ECS 아키텍처**는 게임 엔진과 실시간 그래픽 환경(예: RealityKit, Unity DOTS 등)에서 자주 사용되는 구조로써, 전통적인 OOP(객체지향 프로그래밍)와는 **전혀 다른 방식**으로 시스템을 구성한다.
##### Entity (엔티티)
- 고유 ID를 가진 존재
- 자기 자신은 아무 기능도 하지 않음
- 컴포넌트를 붙여야 의미가 생김

> 예: 자동차 엔티티, 캐릭터 엔티티, 사과 엔티티 등
```swift
let car = Entity()
```

##### Component (컴포넌트)
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


##### System (시스템)
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


##### 동작 방식 요약 (예시)

예를 들어, 회전하는 공을 만들고 싶다면:

1. `Entity`를 만든다 → 공 자체
    
2. `TurnTableComponent`를 붙인다 → 공은 회전해야 한다는 속성
    
3. `TurnTableSystem`이 돌아가며 → 그 공을 계속 회전시킴


##### 객체지향과의 차이점

| 항목      | ECS 아키텍처                    | 객체지향 프로그래밍 (OOP)     |
| ------- | --------------------------- | -------------------- |
| 핵심 단위   | Entity + Component + System | Class (객체 자체가 기능 포함) |
| 데이터와 행위 | 분리                          | 결합                   |
| 재사용성    | 매우 높음 (컴포넌트 조합 가능)          | 클래스 상속으로 제한됨         |
| 확장성     | 유연함                         | 상속 깊어질수록 어려워짐        |
| 성능      | 캐시 친화적, 병렬처리 쉬움             | 상대적으로 느림 (특히 실시간 환경) |

##### 현실 예시
|상황|Entity|Component|System|
|---|---|---|---|
|비행기 시뮬레이터|비행기 Entity|위치, 속도, 방향|물리 시스템, 조작 시스템|
|RPG 게임 캐릭터|캐릭터 Entity|체력, 위치, 장비, 애니메이션 상태|전투 시스템, AI 시스템|
|VisionOS에서 회전 오브젝트|큐브 Entity|TurnTableComponent|TurnTableSystem|

