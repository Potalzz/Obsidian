# **visionOS Lifecycle**


Vision Pro 앱을 개발하며 당황했던 지점 중 하나는 **View가 사라지는 시점이 명확하게 감지되지 않는다**는 점이었다.

Glayer프로젝트를 진행하며, 엣지 케이스를 처리하는 과정에서 window의 하단 'x'버튼 클릭과, 디지털 크라운이 클릭되는 순간을 트리거해야 할 필요가 있었다.

하지만 onDisappear가 기대한 대로 동작하지 않았고, 여러 테스트를 진행하며 해답을 찾게 되었다.

이 글에서는 실제 경험을 기반으로 **visionOS의 View와 Scene의 라이프 사이클**을 정리하고,
어떤 방식으로 윈도우가 사라지는 순간을 감지하고 **앱 상태 전환을 처리할 수 있었는지** 설명하려고 한다.


---

# **visionOS에서 X 버튼은 ‘닫기’가 아니라 ‘최소화’이다**  

[x버튼 이미지]
visionOS의 윈도우 하단 인디케이터 왼쪽에 있는 ‘X’ 버튼은
우리가 직관적으로 생각하는 “뷰 제거”가 아니라,
macOS의 ‘노란색 최소화’ 버튼과 동일한 동작을 한다.

즉,
**❌ View 계층에서 remove → onDisappear 호출 → 메모리 정리**
**⭕ Window가 해당 Scene을 background로 전환 → 메모리는 유지**

사용자가 닫은 것처럼 보이는 앱도 실제로는 완전히 종료되지 않고 **Background Scene**으로 전환될 뿐이다.

onDisappear를 통해서 'X' 버튼을 감지할 수 없는 이유도 이와 같다.

SwiftUI에서 onDisappear는 **뷰가 고유한 부모 뷰 계층에서 제거될 때만** 호출되는데, visionOS에서 X 버튼을 누르면 아래 흐름으로 동작하기 때문이다.

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


# **X버튼은 왜 닫기가 아니라 최소화로 설계되었을까 ?**

개인적으로 'X' 버튼을 클릭했는데 최소화가 된다는 사실이 어색하게 느껴졌기에, Apple에서 왜 이렇게 설계했을까 많은 고민을 하였고 그 결과 아래와 같은 생각이 들었다.

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


---


애플 공식 포럼 및 문서 기준으로
**“X 버튼이 눌렸다는 이벤트를 직접 감지하는 API는 존재하지 않는다.”**
(해당 부분을 GPT 포함 AI들에게 여러 번 물었지만 동일한 답변을 받았다.)
[AI 답변 이미지]

하지만 실제 visionOS 앱 동작을 관찰해보면,
**UIScenePhase 변화가 매우 명확하게 발생**한다.

즉,
- X 버튼을 누르면 Window → Background 상태로 전환된다
- 이 시점에서 ScenePhase는 반드시 .background를 거친다

따라서 **ScenePhase 기반으로 X 버튼 클릭을 트리거**할 수 있다.
(아래에 바로 사용할 수 있는 커스텀 modifier코드를 첨부해두었다.)

---

# **visionOS Window View 계층 동작 정리**

[아래 문구를 이전 섹션 마지막에 배치할지 여기 배치할지 고민해보기]
여기서 헷갈릴 수 있는 View의 개념과 Scene의 개념을 짚고 넘어가자.

아래는 visionOS에서 Window가 나타났다 사라지기까지의 내부 상태 흐름이다.

### **Window가 나타날 때**
1. Scene 생성
2. ScenePhase: .inactive → .active
3. Window가 사용자 앞에 실제로 표시됨
4. SwiftUI View 렌더링
5. onAppear 호출

### **X 버튼을 눌러 Window를 닫을 때**
1. Window가 ‘사라짐’ (시각적으로만)
2. ScenePhase: .active → .inactive → .background
3. SwiftUI View는 계층에서 제거되지 않음
4. onDisappear **호출되지 않음**
5. 앱은 background에 남아 있음
6. 메모리 압박이 발생하면 → 시스템이 앱 kill

# **따라서, Window 닫힘을 감지하려면 ScenePhase를 사용해야 한다**

visionOS의 'X'버튼은 view단위를 조작하는 것이 아니라, scene단위를 조작하는 것이다.
그렇기 때문에 view의 생명주기가 아닌 scene의 생명주기를 감지해야 한다.

특히:
- Window를 닫을 때 → .background
- 창이 다시 열릴 때 → .active
- 시스템 알림 등 일시적 비활성 → .inactive

공식 문서에서는 scenePhase의 감지에 대한 예제를 아래와 같이 사용하고 있다.

그래서 나는 아래와 같이 **ScenePhaseChangeModifier**를 만들어 사용했다.

---

# **ScenePhase 감지용 Modifier 전체 코드**

```swift
import SwiftUI  

struct ScenePhaseChangeModifier: ViewModifier {

    let targetPhase: ScenePhase

    let action: () -> Void

    @Environment(\.scenePhase) private var scenePhase

    func body(content: Content) -> some View {
        content
            .onChange(of: scenePhase) { oldPhase, newPhase in
                if newPhase == targetPhase {
                    action()
                }
            }
    }
}

extension View {

    func onActive(perform action: @escaping () -> Void) -> some View {
        self.modifier(ScenePhaseChangeModifier(targetPhase: .active, action: action))
    }

    func onInactive(perform action: @escaping () -> Void) -> some View {
        self.modifier(ScenePhaseChangeModifier(targetPhase: .inactive, action: action))
    }

    func onBackground(perform action: @escaping () -> Void) -> some View {
        self.modifier(ScenePhaseChangeModifier(targetPhase: .background, action: action))
    }
}
```

해당 코드를 통해 원하는 view에 modifier를 추가하는 형식으로 `.active`, `.inactive`, `.background`를 트리거할 수 있다.

# **ScenePhase로 Window 닫힘(X 버튼) 감지하기 – 실제 사용 예제**

현재 개발중인 visionOS 앱에서 사용자가 volume이나 window를 x버튼을 통해 닫는 상황에서 발생하는 예기치 못한 상황을 방지하기 위해 닫힘 버튼을 감지할 필요가 있었다.

커버해야 할 case는 아래와 같다.
**volume과 window가 동시에 떠있는 상태**
- volume을 닫으면 메인 window가 이전 화면으로 돌아가야 한다.
- window를 닫으면 volume도 자동으로 닫히고 앱이 종료되어야 한다.

**ImmersiveSpace에서 메인 윈도우가 떠있는 상태**
- window를 닫으면 Immersive Space가 해제되고 volume과 window가 떠있는 상태로 돌아가야 한다.

현재 프로젝트에서는 appState를 중앙화하여 관리하고, 해당 값을 바꾸는 함수를 다른 곳에서 호출함으로써 앱 상태를 관리하고 있다.

또한, Coordinator 패턴을 사용하여 앱 상태가 변경되면 앱 메인에서 onChange를 통해 appState 변화를 추적하고, open/dismiss window를 호출하는 형식을 통해 띄우고 지워야 할 scene들을 컨트롤하고 있다.

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


# **해당 방식으로 디지털 크라운 클릭도 감지할 수 있다**

[디지털 크라운 버튼 이미지]
visionOS에서는 **디지털 크라운 클릭** 시,
**Immersive 상태인지 여부에 따라 전혀 다른 동작이 발생한다.**

### **1. Shared Space 상태에서의 디지털 크라운 동작**

Immersive가 아닐 때 디지털 크라운을 누르면
현재 시야에 떠 있는 모든 Window(Volume 포함)가 **일괄적으로 .inactive 상태**로 전환된다.
iOS로 예시를 들면, 알림 센터가 살짝 내려왔을 때 

즉, 디지털 크라운 클릭 = 화면에 보이는 모든 Window의 일시적 비활성화

---

### **2. Full Space 상태에서의 디지털 크라운 동작**

반면 Full Space 즉, Immersive가 활성화된 상태에서는 동작이 달라진다.

디지털 크라운 클릭 시:
1. 시스템이 **자동으로 `dismissImmersiveSpace()`를 호출**한다.
2. Immersive Space는 .inactive로 전환된 뒤 곧 종료된다.

여기서 중요한 점은,
**이 자동 호출은 개발자가 직접 호출하는 `dismissImmersiveSpace()`와 다르게 동작한다는 것**이다.

---

## **3. 왜 차이가 발생하는가? (onDisappear가 불리지 않는 이유)**

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

## **4. 따라서 디지털 크라운 클릭은 View의 라이프사이클로 감지할 수 없다**

디지털 크라운 클릭은:
- View 계층이 사라지는 이벤트가 아니고
- 앱(Scene) 레벨의 상태 변화이기 때문에

**View의 onDisappear 기반으로 감지하는 것은 불가능하다.**

따라서 반드시 **ScenePhase 기반 감지**가 필요하다.

---

## **5. ImmersiveSpace의 .inactive 전환을 감지하면 디지털 크라운 클릭을 추적할 수 있다**

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

# **visionOS 개발 시 알아두어야 할 중요한 포인트**

### **1) window가 닫혀도 View는 메모리에서 제거되지 않는다**
→ onDisappear 대신 ScenePhase 사용 필수

### **2) background로 옮겨진 순간, 시스템은 언제든 kill할 수 있다**
→ 저장 작업은 빠르게 처리해야 함

### **3) view 계층을 직접 제어하는 것이 아니라 ‘Scene 단위 라이프사이클’을 기반으로 관리해야 한다**

---

# **마무리**
visionOS는 iOS, macOS와 닮은 듯 완전히 다른 **Scene 중심의 UI/UX 구조**를 갖고 있다.
특히 Window하단 인디케이터의 **X**버튼을 클릭했을 때, Window가 ‘완전히 사라지지 않는다는 점’은 visionOS 개발을 진행하며 많이 겪는 혼란 지점이다.

이 글에 정리한 것처럼,
- Window 닫힘 = ScenePhase .background
- 재열림 = .active
- onDisappear는 신뢰하면 안 됨

이 흐름만 정확히 이해하면,
visionOS에서 윈도우와 상태 전환을 다루는 대부분의 문제를 해결할 수 있다.