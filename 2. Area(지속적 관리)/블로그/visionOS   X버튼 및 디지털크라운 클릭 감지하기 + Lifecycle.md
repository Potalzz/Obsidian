**12/20 gpt와 gemini에 있는 설명 기반으로, x버튼이 왜 종료가 아닌지에 대한 고찰과 visionOS의 lifecycle 및 view 계층 설명 적기**

visionOS 앱을 개발하며 당황했던 지점 중 하나는 window 하단의 인디케이터에 있는 "X" 버튼을 트리거 할 수 없다는 사실이였다.

[x 버튼 이미지]
(요게 바로 x 버튼)

Ai에게 물어봐도 공식적으로 감지할 수 없는 답변만 제공받았으나, 진행하던 프로젝트에서 필수적으로 필요한 기능이였기 때문에 반드시 트리거해야할 필요가 있었다.

때문에, X버튼이 클릭되었을 때 view와 Scene이 어떻게 변하는지 일일이 확인해가며 알아낸 방법을 공유하고 visionOS의 Lifecycle과 view계층에 대해서 알아보고자 한다.

---

# X 버튼의 실제 동작 과정

[x버튼 이미지]
visionOS의 윈도우 하단 인디케이터 왼쪽에 있는 ‘X’ 버튼은
우리가 직관적으로 생각하는 “뷰 제거”가 아니라,
해당 scene을 background로 전환시키는 동작을 한다.

이게 무슨 소리인가 싶겠지만 visionOS에서 "X" 버튼은 해당 view를 view계층에서 제거하는 것이 아니라 해당 view가 속한 Scene 자체의 상태를 `.background`로 전환시킨다.

그렇기 때문에, view에서 onDisappear를 아무리 추가해도 "X"버튼 클릭 지점을 트리거할 수 없다.

즉,
**❌ View 계층에서 remove → onDisappear 호출 → 메모리 정리**
**⭕ 해당 Scene을 background로 전환 → 메모리는 유지**

사용자가 닫은 것처럼 보이는 화면이 실제로는 완전히 종료되지 않고 **Background Scene**으로 전환될 뿐이다.

`.onDisappear`를 통해서 'X' 버튼을 감지할 수 없는 이유도 이와 같다.

SwiftUI에서 `.onDisappear`는 **뷰가 고유한 부모 뷰 계층에서 제거될 때만** 호출되는데, visionOS에서 X 버튼을 누르면 아래 흐름으로 동작하기 때문이다.

**X 버튼 → 실제 동작 순서**
1. Window가 사용자 시야에서 사라짐
2. SwiftUI View는 **그대로 유지**
3. ScenePhase가 .active → .inactive → .background 로 이동
4. 앱 메모리는 그대로 잡혀 있음
5. 일정 시간이 지나거나 메모리가 부족하면 시스템이 앱을 종료(kill)

[scenePhase 변화 로그 GIF]

즉,
**뷰가 사라진 것이 아니라 Scene이 background로 이동했기 때문에**
**SwiftUI는 ‘뷰가 사라졌다(onDisappear)’고 판단하지 않기 때문에 onDisappear가 호출되지 않는다.**


---

# View Lifecycle vs Scene Lifecycle

> 그래서 view와 scene이 정확히 무엇을 의미하는데 ?

visionOS에서 view가 나타나고 사라지는 과정을 이해하기 위해서는 뷰와 씬에 대한 생명주기의 이해가 필요하다.

**View Lifecycle(뷰의 생명주기)** 과 **Scene Lifecycle(씬의 생명주기)** 은 앱의 상태를 관리하는 두 가지 핵심 축이다.

### View Lifecycle (뷰의 생명주기)

**"사용자에게 이 뷰가 보이는가?" (UI 계층 관점)**

View Lifecycle은 말 그대로 **개별 뷰가 View 계층 구조에 추가되거나 제거되는 과정**을 의미한다.
우리가 흔히 사용하는 `.onAppear`와 `.onDisappear`가 바로 이 생명주기를 감지하는 modifier다.

아래 예제를 통해 쉽게 이해해보자.
```swift
struct ParentView: View {
    @State private var isShow = true

    var body: some View {
        VStack {
            // [A] 조건부 렌더링
            if isShow {
                ChildView() // 뷰 계층에 존재함
            }
        }
        .onTapGesture {
            // [B] 상태 변경 -> 렌더 트리 갱신 유발
            isShow = false
        }
    }
}

struct ChildView: View {
    var body: some View {
        Text("I am here")
            .onDisappear {
                print("ChildView: onDisappear (메모리 해제)")
            }
    }
}
```

**동작 원리**
1. 사용자가 탭을 하여 `isShow`가 `false`로 바뀐다.
2. SwiftUI는 `ParentView`의 `body`를 다시 그린다.
3. `if isShow` 조건이 거짓이 되므로, **`ParentView`의 자식 목록(계층)에서 `ChildView`가 제거된다.**
4. SwiftUI 엔진이 이를 감지하고, 메모리에 있던 `ChildView`를 **폐기**한다.
5. 폐기되는 순간 `onDisappear`가 호출된다.

View 계층 구조의 과정과 view가 메모리에 언제 등록되고, 해제되는지 알아보았다.

하지만 문제는 visionOS의 윈도우 관리 방식에 있다. 사용자가 'X' 버튼을 눌러 윈도우(또는 볼륨)를 닫는 행위는 뷰를 계층 구조에서 **제거**하는 것이 아니라, 윈도우 전체를 **숨기는** 것에 가깝다. 뷰 자체는 메모리에 살아있고 계층 구조에도 남아있으므로 `onDisappear`는 호출되지 않는 것이다.

그럼 씬은 어떻게 변경될까 ?

### Scene Lifecycle (씬의 생명주기)

**"이 윈도우가 시스템에서 어떤 상태인가?" (OS 시스템 관점)**

Scene Lifecycle은 **Scene이 시스템 상에서 어떤 상태에 있는지**를 `ScenePhase`를 통해 3가지로 구분한다.

- **Active**: 씬이 전면에 있고 사용자와 상호작용 가능한 상태 (현재 보고 있는 윈도우).
    
- **Inactive**: 씬이 화면에는 보이지만 상호작용은 불가능한 상태 (시스템 제어 센터를 내리거나, 다른 윈도우로 포커스가 넘어가는 순간).
    
- **Background**: 씬이 사용자 눈에 보이지 않는 상태. **'X' 버튼을 누르거나 디지털 크라운을 눌러 홈으로 나갔을 때**

실제 'x' 버튼을 클릭했을 때 `ScenePhase`가 어떻게 변경되는지 아래 예제를 통해 살펴보자.

```swift
@main
struct VisionProApp: App {
    // 시스템이 관리하는 앱의 상태 (Active, Inactive, Background)
    @Environment(\.scenePhase) private var scenePhase

    var body: some Scene {
        WindowGroup {
            ParentView() // 위에서 만든 그 뷰
                .onChange(of: scenePhase) { oldPhase, newPhase in
                    if newPhase == .background {
                        print("Window: X 버튼 눌림 (Background 진입)")
                        // 하지만 ParentView 내부의 isShow는 여전히 'true'임
                    }
                }
        }
    }
}
```

시뮬레이터에서 값을 확인해보면..


[시뮬레이터 로그]
오잉..? scenePhase의 변화는 없고 view가 해제된 것을 볼 수 있다.

하지만 실제 기기에서 테스트해보면 다른 결과가 나온다.

scenePhase만 `.background`로 전환되기 때문에 `ChildView`의 `.onDisappear`는 호출되지 않는 것을 볼 수 있다.
(이러한 문제들로 인해 visionOS 개발을 할 때 실 기기가 필수적으로 필요하다고 생각한다...)

결과적으로 scenePhase의 변화를 통해서 x 버튼 클릭을 감지할 수 있다.

---

# ScenePhase로 X 버튼 감지하기 – 실제 사용 예제

공식 문서에서는 scenePhase의 감지에 대한 예제를 아래와 같이 사용하고 있다.

[공식문서 scenePhase감지]

scenePhase만 감지하기 위해서는 위와 같이 간단하게 scenePhase의 변화를 감지하고 실행하고자 하는 코드를 추가하면 된다.

추가로 현재 진행중인 프로젝트에서 이를 어떻게 활용하는지 소개하고자 한다.

사용자가 volume이나 window를 x버튼을 통해 닫는 상황에서 발생하는 예기치 못한 상황을 방지하기 위해 닫힘 버튼을 감지할 필요가 있었다.

커버해야 할 case는 아래와 같다.
**volume과 window가 동시에 떠있는 상태**
- volume을 닫으면 메인 window가 이전 화면으로 돌아가야 한다.
- window를 닫으면 volume도 자동으로 닫히고 앱이 종료되어야 한다.

**ImmersiveSpace에서 메인 윈도우가 떠있는 상태**
- window를 닫으면 Immersive Space가 해제되고 volume과 window가 떠있는 상태로 돌아가야 한다.

현재 프로젝트에서는 appState를 중앙화하여 관리하고, 해당 값을 바꾸는 함수를 다른 곳에서 호출함으로써 앱 상태를 관리하고 있다.

또한, Coordinator 패턴을 통해 앱 상태가 변경되면 앱 메인에서 onChange를 통해 appState 변화를 추적하고, open/dismiss window를 호출하는 형식을 통해 띄우고 지워야 할 scene들을 컨트롤하고 있다.

**실제 프로젝트에서 사용 예시**
```swift
struct MainWindowView: View {
	@Environment(\.dismissWindow) private var dismissWindow
    @Environment(\.openImmersiveSpace) private var openImmersiveSpace
    @Environment(\.dismissImmersiveSpace) private var dismissImmersiveSpace
    @Environment(\.openWindow) private var openWindow

    var body: some View {
	    LibraryView()
        .onBackground {
	        if appStateManager.appState.isImmersiveOpen {
		        appStateManager.closeProject() // 이전 window화면으로 이동
		    } else {
			    appStateManager.closeApp() // 앱 종료하기
			}
		}
		.onChange(of: appStateManager.appState) { oldState, newState in
            Task { @MainActor in
                await windowCoordinator?.handleStateChange(
                    from: oldState,
                    to: newState,
                    openWindow: { id in openWindow(id: id) },
                    dismissWindow: { id in dismissWindow(id: id) },
                    openImmersiveSpace: { id in await openImmersiveSpace(id: id) },
                    dismissImmersiveSpace: { await dismissImmersiveSpace() }
                )
            }
        }
	}
}
```

이 방식의 장점:
- X 버튼을 누르는 순간 인터셉트 가능
- immersive → volume 이동 같은 로직 처리 가능
- SwiftData 저장/정리, RealityView 리소스 해제 모두 처리 가능
- 뷰 계층과 정합성 문제 X

---


# + 해당 방식으로 디지털 크라운 클릭도 감지할 수 있다

[디지털 크라운 버튼 이미지]
visionOS에서는 **디지털 크라운 클릭** 시,
**Immersive 상태인지 여부에 따라 전혀 다른 동작이 발생한다.**

## Shared Space 상태에서의 디지털 크라운 동작

(Shared Space와 Full Space의 개념에 대해서 잘 모른다면 아래 글에 정리해놓았으니 보고오자)
[Spatial Computing을 위한 SwiftUI를 정리한 내용 블로그 글]

Immersive가 아닐 때 디지털 크라운을 누르면
현재 시야에 떠 있는 모든 Window(Volume 포함)가 **일괄적으로 .inactive 상태**로 전환된다.
iOS로 예시를 들면, 알림 센터가 살짝 내려왔을 때 

즉, 디지털 크라운 클릭 = 화면에 보이는 모든 Window의 일시적 비활성화

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
- 앱은 여전히 .active 상태를 유지하고
- Immersive 레이어만 제거되기 때문에
- SwiftUI View의 onDisappear가 정상적으로 실행된다.

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
.onInactive {
    // 디지털 크라운 클릭 시점 감지
}
```

이전에 소개한 ScenePhaseChangeModifier를 활용해
ImmersiveSpace가 .inactive로 바뀌는 지점을 캐치하면
- Immersive 종료 처리
- Volume 보이기
- 상태 초기화
- RealityView 리소스 정리

등 원하는 후처리를 안정적으로 수행할 수 있다.

**지금까지 설명한 내용을 간단하게 3줄 요약하면 다음과 같다.**

1. window가 닫혀도 View는 메모리에서 제거되지 않는다
2. background로 옮겨진 순간, 시스템은 언제든 kill할 수 있다
3. view 계층을 직접 제어하는 것이 아니라 ‘Scene 단위 라이프사이클’을 기반으로 관리해야 한다

---

# X버튼은 왜 닫기가 아니라 최소화로 설계되었을까 ?

개인적으로 'X' 버튼을 클릭했는데 최소화가 된다는 사실이 어색하게 느껴졌기에, Apple에서 왜 이렇게 설계했을까 많은 고민을 하였고 아래와 같은 생각이 들었다.

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
특히 Window하단 인디케이터의 **X**버튼을 클릭했을 때, Window가 ‘완전히 사라지지 않는다는 점’은 visionOS 개발을 진행하며 많이 겪는 혼란 지점이다.

이 글에 정리한 것처럼,
- Window 닫힘 = ScenePhase .background
- 재열림 = .active
- onDisappear는 신뢰하면 안 됨

이 흐름만 정확히 이해하면,
visionOS에서 윈도우와 상태 전환을 다루는 대부분의 문제를 해결할 수 있다.