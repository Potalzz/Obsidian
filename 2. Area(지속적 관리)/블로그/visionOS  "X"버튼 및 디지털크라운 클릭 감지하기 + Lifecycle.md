**12/20 gpt와 gemini에 있는 설명 기반으로, x버튼이 왜 종료가 아닌지에 대한 고찰과 visionOS의 lifecycle 및 view 계층 설명 적기**

Glayer 프로젝트를 진행하면서 Immersive Space상태에서 2D Window를 "X"버튼을 클릭하여 닫으면 Immersive Space만 존재하고 아무 동작도 할 수 없는 문제가 발생했다.


![[Pasted image 20251225063410.png]]
(요게 바로 x 버튼)

`onDisappear`를 통해서 window가 닫히는 순간을 감지하려 했지만 아무 동작도 하지 않았고, 닫기 버튼을 직접 트리거할 수 있는 API는 존재하지 않았다.

![[Pasted image 20251224181834.png]]

때문에, window가 닫힐 때 실제로 어떤 변화가 일어나는지 visionOS의 Lifecycle 관점에서 알아보고 방법을 공유하고자 한다.

---

# visionOS Lifecycle

visionOS에서 view가 나타나고 사라지는 과정을 더 깊게 이해하기 위해서는 visionOS의 Lifecycle에 대해 더욱 알아야할 필요가 있다.

visionOS는 iOS와 동일하게 **SwiftUI의 `App` 프로토콜과 `ScenePhase`** 를 기반으로 작동하지만, **"단일 윈도우(iOS)" vs "다중 윈도우(visionOS)"** 라는 환경 차이로 인해 생명주기를 다루는 전략이 완전히 다르다.

visionOS에서 앱 메인을 보면 아래와 같이 각 window마다 개별로 선언하는 것을 볼 수 있다.
```swift
var body: some Scene {
	// 2D Window Scene
	WindowGroup {
		MainWindowView()
	}
	.windowStyle(.plain)
	
	// Volume Scene
	WindowGroup {
		VolumeView()
	}
	.windowStyle(.volumetric)
	
	// Immersive Scene
	ImmersiveSpace {
		ImmersiveView()
	}
	.immersiveStyle()
}
```

공식문서에서 `WindowGroup`를 확인해보면
`A scene that presents a group of identically structured windows.`
**"구조가 동일한 window들이 모인 Scene"** 이라는 설명을 확인할 수 있다.

결국 하나의 `WindowGroup`에 속한 `view`들은 모두 하나의 `Scene`에 속해 있다는 사실을 알 수 있다.

visionOS의 Lifecycle이 어떻게 구성되어 있는지, 좀 더 친숙한 iOS와 비교를 통해 알아보자.

### 구조적 차이: 기기 중심 vs 씬(Scene) 중심

**iOS (기기 중심)**
- 대부분의 경우 `App Lifecycle` $\approx$ `Scene Lifecycle`
- 앱이 활성화된다는 것은 기기 화면 전체를 차지한다는 의미

**visionOS (씬 중심)**
- `App Lifecycle`과 `Scene Lifecycle`이 **분리**됨
- 앱 하나가 여러 개의 윈도우를 띄울 수 있음
- 앱 자체는 실행 중이지만, **A 윈도우는 Active, B 윈도우는 Inactive**일 수 있다. 따라서 각 `WindowGroup`의 `ScenePhase`를 개별적으로 관리해야 한다

`ScenePhase`는 해당 씬의 상태를 의미하며 총 3단계(Active, Inactive, Background)로 이루어져 있다.

하지만 visionOS에서는 같은 상태이더라도 그 의미가 다르다.

### ScenePhase 상세 비교

| **상태 (State)** | **iOS**                                                                             | **visionOS**                                                                                         |
| -------------- | ----------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Active**     | **[Foregound + Input]**<br><br>  <br><br>앱이 화면에 있고 사용자의 터치를 받을 수 있음.                | **[Focus]**<br><br>  <br><br>사용자의 시선이 머물고 있거나 인터랙션 중인 **특정 윈도우**.                                    |
| **Inactive**   | **[Transition]**<br><br>  <br><br>알림 센터를 내리거나 앱 전환기로 들어가는 **찰나의 순간**. 사용자 입력을 못 받음. | **[Shared Space / No Focus]**<br><br>  <br><br>앱이 공간에 **보이지만**, 사용자가 다른 앱을 보고 있음. **일상적이고 장기적인 상태.** |
| **Background** | **[Invisible]**<br><br>  <br><br>홈으로 나가서 화면에서 사라짐. 곧 Suspended(동결)됨.                | **[Invisible / Closed]**<br><br>  <br><br>사용자가 윈도우를 닫거나, 다른 앱이 'Full Space'를 점유하여 가려짐.               |
위에서 "하나의 `WindowGroup`에 속한 `view`들은 모두 하나의 `Scene`에 속해 있다"고 하였다.
그렇다면, 내부에 있는 view들의 `ScenePhase`는 모두 같은 값을 가리킨다는 사실을 기억하고 있자.


---

# X 버튼의 실제 동작 과정

visionOS의 윈도우 하단 인디케이터 왼쪽에 있는 ‘X’ 버튼은
우리가 직관적으로 생각하는 “뷰 제거”가 아니라,
해당 view의 `ScenePhase`를 `.background`로 전환시키는 동작을 한다.

사용자가 닫은 것처럼 보이는 화면이 실제로는 완전히 종료되지 않고 **Background Scene**으로 전환된다.
(마치 macOS의 "최소화"버튼처럼 느껴지기도 하지만.. 엄밀히 말하면 둘은 완전히 다르게 동작한다.)

view에 `.onDisappear`를 아무리 추가해도 사용자가 "X"버튼을 클릭하는 지점을 트리거할 수 없다.

SwiftUI에서 `.onDisappear`는 **뷰가 고유한 부모 뷰 계층에서 제거될 때만** 호출되는데, visionOS에서 X 버튼을 누르면 아래 흐름으로 동작하기 때문이다.

**X 버튼 → 실제 동작 순서**
1. Window가 사용자 시야에서 사라짐
2. SwiftUI View는 **그대로 유지**
3. ScenePhase가 .active → .inactive → .background 로 전환
4. 앱 메모리는 그대로 잡혀 있음
5. 일정 시간이 지나거나 메모리가 부족하면 시스템이 앱을 종료


즉,
뷰가 사라진 것이 아니라 Scene이 background로 이동하고, view는 메모리에 그대로 잡혀있기 때문에
SwiftUI는 ‘뷰가 사라졌다(onDisappear)’고 판단하지 않는다.


---

# ScenePhase로 X 버튼 감지하기

공식 문서에서는 scenePhase 감지에 대한 예제를 아래와 같이 사용하고 있다.

![[Pasted image 20251225052133.png]]

scenePhase만 감지하기 위해서는 위와 같이 간단하게 scenePhase의 변화를 감지하고 실행하고자 하는 코드를 추가하면 된다.

하지만 위에 얘기했듯이, window가 `.background`로 전환되는 순간은 "X" 버튼 클릭 외에도 여러 상황이 있으므로, 이를 고려해서 설계해야한다.

---

# + 해당 방식으로 디지털 크라운 클릭도 감지할 수 있다

![[Pasted image 20251225062921.png]]
visionOS에서는 **디지털 크라운 클릭** 시,
**Immersive 상태인지 여부에 따라 전혀 다른 동작이 발생한다.**

## Shared Space 상태에서의 디지털 크라운 동작

(Shared Space와 Full Space의 개념에 대해서 잘 모른다면 아래 글에 정리해놓았으니 보고오자)
[visionOS 공간 개념 정리](https://medium.com/@tprhkd1607/visionos-%EA%B3%B5%EA%B0%84-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC-f0fe476285de)

Immersive가 아닐 때 디지털 크라운을 누르면
현재 시야에 떠 있는 모든 Window(Volume 포함)가 **일괄적으로 .inactive 상태**로 전환된다.


---

## Full Space 상태에서의 디지털 크라운 동작

반면 Full Space 즉, Immersive가 활성화된 상태에서는 동작이 달라진다.

디지털 크라운 클릭 시:
1. 시스템이 **자동으로 `dismissImmersiveSpace()`를 호출**한다.
2. Immersive Space는 .inactive로 전환된 뒤 곧 종료된다.

여기서 중요한 점은,
**이 자동 호출은 개발자가 직접 호출하는 `dismissImmersiveSpace()`와 다르게 동작한다는 것**이다.

---

## 왜 차이가 발생하는가?

일반적으로 우리가 `dismissImmersiveSpace()`를 직접 호출하면:
- 앱은 여전히 `.active` 상태를 유지하고
- Immersive 레이어만 제거되기 때문에
- SwiftUI View의 `.onDisappear`가 정상적으로 실행된다.

그러나 **디지털 크라운을 클릭해 Immersive가 종료될 때는 상황이 다르다.**

디지털 크라운 클릭 시 시스템은:
- ImmersiveSpace를 닫는 것과 동시에
- **앱 전체를 즉시 .inactive로 전환**한다.

즉,
> 앱이 .inactive로 넘어가면서 메인 런루프가 멈추거나 우선순위가 밀려
> onDisappear가 실행되기 전에 시스템에 의해 정지되는 것.

결과적으로,
- dismissImmersiveSpace는 호출되지만
- SwiftUI View의 onDisappear는 실행되지 않는다.

---

## ImmersiveSpace의 .inactive 전환을 감지하면 디지털 크라운 클릭을 추적할 수 있다

디지털 크라운 클릭 → ImmersiveSpace가 .inactive → 종료

이 흐름을 기반으로:
```swift
.onChange(of: scenePhase) { oldPhase, newPhase in
	if newPhase == .inactive {
		// 여기서 디지털 크라운 클릭 감지
	}
}
```

ImmersiveSpace가 .inactive로 바뀌는 지점을 캐치하면
- Immersive 종료 처리
- Volume 보이기
- 상태 초기화
- RealityView 리소스 정리

등 원하는 후처리를 안정적으로 수행할 수 있다.

---

# 3줄 요약
1. window가 닫혀도 View는 메모리에서 제거되지 않는다
2. background로 옮겨진 순간, 시스템은 언제든 kill할 수 있다
3. view 계층을 직접 제어하는 것이 아니라 ‘Scene 단위 라이프사이클’을 기반으로 관리해야 한다

---

# X버튼은 왜 닫기가 아니라 최소화로 설계되었을까 ?

개인적으로 'X' 버튼을 클릭했는데 종료가 아니라 백그라운드 전환이 된다는 사실이 어색하게 느껴졌기에, Apple에서 왜 이렇게 설계했을까 많은 고민을 하였고 아래와 같은 생각이 들었다.

## 사용자가 창을 끄고 켜는 개념조차 잊게하자

사용자가 window를 종료하는 상황은 언제일까 ?

불필요한 창의 메모리 낭비를 줄이기 위해서 ?
이는 지극히 개발자 중심의 사고이고 일반적인 사용자는 메모리 관리가 어떻게되고 불필요한 리소스를 낭비하는지 신경쓰지 않을 것이며, Apple도 그걸 원한 것 같다.

사용자는 단순히 자신의 눈 앞에서 창이 사라지길 원할 때 닫을 것이다.
(이런 의도가 담겨 있기에 윈도우를 닫는 함수명도 dismisswindow로 만든 것이 아닐까 ?)

사용자가 창을 닫았을 때 메모리에서 제거하지 않고 백그라운드로 전환함으로써 실제 사용자가 원하는 시야에서 종료라는 효과는 제공하되, 기술적/UX적 이득을 챙길 수 있다.

방 안이Vision Pro 화면의 공간이고, TV가 하나의 window라고 생각해보자.
TV의 화면이 신경쓰여서 TV를 끈다고 해서 "TV 전원이 종료되고 플러그도 뽑혀!!" 라는 의도가 담기지 않았을 것이다.
TV의 전원이 꺼지지 않고 대기 상태로 돌아가는 것이 사용자에겐 전혀 어색하지 않고,
무엇보다 TV가 다시 켜졌을 때 전원이 켜질 때와 같이 재부팅 화면이 보이지 않고 바로 이전의 화면이 복원되기를 원할 것이다.

만약 사용자가 'X'버튼을 눌렀다고 해서 해당 씬을 메모리에서 제거해버린다면 다시 열었을 때 로딩 스피너가 나오거나, 이전의 화면을 복원하지 못할 가능성이 있다.
그러기 위해선 background로 전환시키고 데이터를 안전하게 저장하고 다시 active시킴으로써 이러한 문제를 해결하고자 했을거라는 생각이 든다.

개발자의 관점에서 봤을 때는 왜 background로 전환이 될까? 라는 고민이 들지만,
사용자 입장에서는 background로 전환되는지 알기도 어려울 뿐더러 궁금하지 않을 가능성이 높다라는 생각이 들게 되었다.


# 마무리
visionOS는 iOS, macOS와 닮은 듯 완전히 다른 **Scene 중심의 UI/UX 구조**를 갖고 있다.

x 버튼이 macOS의 최소화 버튼과 같은 동작을 하는 것 같아 보여도 내부적으로는 전혀 다른 동작을 한다.
(visionOS와 macOS의 차이점에 대해서는 추후 글을 작성 후 블로그에 업로드 하고자 한다.)

특히 Window하단 인디케이터의 **X**버튼을 클릭했을 때, Window가 ‘완전히 사라지지 않는다는 점’은 visionOS 개발을 진행하며 많이 겪는 혼란 지점이다.

이 글에 정리한 것처럼,
- Window 닫힘 = ScenePhase .background
- 재열림 = .active
- onDisappear는 신뢰하면 안 됨

이 흐름만 정확히 이해하면,
visionOS에서 윈도우와 상태 전환을 다루는 대부분의 문제를 해결할 수 있다.