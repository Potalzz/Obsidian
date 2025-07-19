
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

