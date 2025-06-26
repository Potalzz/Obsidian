
## VisionOS 개념

VisionOS는  **Apple Vision Pro**와 같은 **혼합현실(MR, Mixed Reality) 기기**를 구동하기 위해 설계된 운영체제이며, 공간 컴퓨팅(spatial computing)을 
중심으로 동작하는 것이 가장 큰 특징이다.

### 공간 컴퓨팅 (Spatial Computing)
- 사용자는 물리적인 공간 안에서 앱, 창, UI 요소들을 자유롭게 배치하고 상호작용할 수 있음.
	
- 디스플레이가 "눈 앞의 가상 세계"로 확장되며, 앱이 공간 안에 떠다니는 형태로 표현됨.
	
- **손 제스처, 눈의 시선 추적, 음성 명령**으로 제어 가능.

### 3D 인터페이스와 창
- 기존 iOS/macOS의 2D 창과 달리, VisionOS는 **공간 속에 떠 있는 3D 창** 형태로 앱을 띄움.
    
- 앱 창은 벽에 고정하거나, 공중에 떠 있도록 할 수 있음.

### 새로운 UI 프레임워크: RealityKit + SwiftUI
- SwiftUI를 기반으로 하지만, 공간 인터페이스를 위해 **RealityKit**과 결합됨
	
- 3D 오브젝트, 애니메이션, 깊이 인식 등도 RealityKit에서 제공.


## 애플에서 제공하는 기술들은 어떤 것들이 있을까 ?

VisionOS개발을 위해 애플에서 제공하는 대표적인 프레임워크는 다음과 같다.

### RealityKit
> RealityKit은 iOS, iPadOS, macOS, tvOS 및 visionOS에서 3D 또는 증강 현실(AR) 앱을 개발하는 데 사용할 수 있는 고성능 3D 시뮬레이션 및 렌더링 기능을 제공합니다. **RealityKit**은 **ARKit**을 활용하여 가상 객체를 현실 세계에 완벽하게 통합하는 AR 중심 3D 프레임워크입니다.

애플 공식문서에는 위와 같이 설명되어있다.

쉽게 이해하면, 3D개체를 코드를 통해 생성하고 화면에 객체를 띄운다고 생각하면 될 것 같다.

또한 가상 객체가 실제 세계의 객체와 상호 작용하도록 도와주고,
물리 시뮬레이션을 적용하거나, 수동으로 객체에 애니메이션을 적용할 수 있다.

그럼, 가장 먼저 객체를 만들기 위해서는 **Anchor(위치), Material(재질), Model(객체)** 을 알아야 한다.

#### Anchor(위치)
객체를 생성하면 화면에 배치를 해야 하는데, 어떤 포인트를 통해서 트래킹하여 배치할 지를 지정한다.
``` swift
let anchor = AnchorEntity(plane: .horizontal)
```

#### Material(재질)
객체의 재질을 지정해준다.
``` swift
let boxMaterial = SimpleMaterial(color: .systemPink, isMetalic: true)
```
color은 색상, isMetalic은 반사여부?

#### Model(객체)

``` swift
let box = ModelEntity(
            mesh: MeshResource.generateBox(size: 0.3, cornerRadius: 0.05),
            materials: [boxMaterial]
        )
```
어떤 mesh를 만들지 지정해준다.
materials에는 이전에 만든 재질을 지정해준다.

이렇게 만든 객체를 `arView.scene`에 새로운 Anchor를 추가하여 배치해주면 화면에 객체를 표기할 수 있다.

### ARKit




