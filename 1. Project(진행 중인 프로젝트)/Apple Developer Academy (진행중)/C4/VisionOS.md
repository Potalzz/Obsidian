
## VisionOS 개념

VisionOS는  **Apple Vision Pro**와 같은 **혼합현실(MR, Mixed Reality) 기기**를 구동하기 위해 설계된 운영체제이며, 공간 컴퓨팅(spatial computing)을 
중심으로 동작하는 것이 가장 큰 특징이다.

**RealityKit**으로 **AR + 3D렌더링** 용도로 사용하고, **ARKit**을 **AR 기술(추적, 감지, 매핑 등)**의 용도로 사용한다.

RealityKit으로 물체를 만들고, ARKit으로 배치를 하는 개념.

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

### VisionOS 앱의 종류
#### Windowed 앱
기존 iPad 앱처럼, 하나의 평면 창에서 작동하는 형태.

#### Volumetric 앱
3D 오브젝트 중심의 인터랙션 제공. 공간 내 입체적으로 배치됨.

#### Full Space 앱
전체 시야를 차지하는 몰입형 앱. AR/VR 게임, 교육 콘텐츠 등에 사용.


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
> **증강 현실** (AR)은 기기 센서의 실시간 뷰에 2D 또는 3D 요소를 추가하여 마치 현실 세계에 존재하는 것처럼 보이게 하는 사용자 경험을 말합니다. ARKit은 기기 동작 추적, 세계 추적, 장면 이해 및 디스플레이 편의성을 결합하여 AR 경험 구축을 간소화합니다. - https://developer.apple.com/documentation/arkit

쉽게 얘기하자면, RealityKit이 사용자의 환경에 3D 객체를 자연스럽게 구현해주는 역할을 해준다면, ARKit은 주변환경과 가상의 3D 객체들이 상호작용을 할 수 있도록 해주는 프레임워크.

### ARKit의 기능들
대표적인 기능만 몇 가지 살펴보자면

- **Plane Detection:** 평면을 찾는 기능 (예: 바닥, 벽, 천장 등)
- **World Tracking:** 주변 환경을 Tracking
- **Hand Tracking:** 손을 추적하고 Custom Gesture 기능
- **Scene reconstruction:** 주변 환경을 재구성, 물리적 환경을 mesh로 만들어 디지털 객체와 상호작용 가능
- **Image traking:** 이미지를 앵커 포인터로 사용
- **Object Tracking:** 실제 물체 추적
- **Barcode detection:** 바코드, QR 추적
- **Room Tracking:** 방, 구역 등을 기록 및 추적
- **Light estimation:** 주변 환경 조명의 특성을 분석
- **Camera frames:** 카메라 프레임을 변환



## 비전프로 앱 레퍼런스는 풍부한가 ?
https://www.pcmag.com/picks/the-best-apple-vision-pro-apps
카테고리별 다양한 앱 존재



## 개발에 제약되는 사항은 뭐가 있을까 ?
### 개인 개발자에게 적용되는 기술적 제약사항

1. **Enterprise API 사용 불가** 
    https://developer.apple.com/documentation/visionOS/building-spatial-experiences-for-business-apps-with-enterprise-apis
    - 
    - 카메라 피드, LiDAR 센서 데이터 등 하드웨어 저수준 접근은 **기업 계정 전용**입니다[1](https://www.reddit.com/r/VisionPro/comments/1fdhlh3/what_can_we_as_devs_not_do_yet/)[2](https://framesixty.com/apple-vision-pro-development-for-enterprise/). 개인 개발자는 다음 기능을 구현할 수 없습니다:
        
    - 실시간 카메라 데이터를 활용한 AR 오버레이
        
    - LiDAR를 이용한 정밀 공간 매핑
        
    - 화면 캡처 시 패스스루 영상 포함[2](https://framesixty.com/apple-vision-pro-development-for-enterprise/)
        
2. **상호작용 데이터 접근 제한**
    
    - 시선 추적, 정교한 손동작 인식 데이터는 **'꼬집기' 제스처 수준**으로 제한됩니다[3](https://www.rebel9.co.kr/kr/works/archive-exhibition/ae-research/apple-vision-pro-case-study/)[4](https://www.fline.dev/why-i-stopped-building-for-visionos-and-what-could-bring-me-back/):
        
    - 손 뼈대 정보 미제공 → 복잡한 제스처 구현 불가
        
    - 시선 위치 추적 불가 → 주의 집중도 분석 등 활용 제한
        
3. **공간 고정 API 부재**
    
    - 가상 오브젝트를 물리적 공간에 **영구 고정**할 수 없습니다[4](https://www.fline.dev/why-i-stopped-building-for-visionos-and-what-could-bring-me-back/):
        
    - "Magnetically Pinning" API 미구현 → 앱 재실행 시 위치 초기화
        
    - 가구/벽면에 UI 고정 불가 → 혼합현실 경험 제한적
        
4. **시각 효과 기술 한계**
    
    - Shader Graph에서 **HLSL(고급 셰이더 언어) 미지원**[5](https://www.gianty.com/apple-vision-pro-app-development/):
        
    - 복잡한 머티리얼 효과 구현 어려움
        
    - 파티클 시스템 제한 → 화려한 VFX 구현 불가능
        

### 개발이 특히 어려운 앱 유형

|앱 유형|주요 제약사항|
|---|---|
|실시간 AR 증강 앱|카메라 피드 수정 불가([1](https://www.reddit.com/r/VisionPro/comments/1fdhlh3/what_can_we_as_devs_not_do_yet/)), 공간 고정 API 부재([4](https://www.fline.dev/why-i-stopped-building-for-visionos-and-what-could-bring-me-back/))|
|정교한 제스처 제어 앱|손 뼈대 데이터 접근 불가([3](https://www.rebel9.co.kr/kr/works/archive-exhibition/ae-research/apple-vision-pro-case-study/)), 시선 추적 제한([3](https://www.rebel9.co.kr/kr/works/archive-exhibition/ae-research/apple-vision-pro-case-study/)[4](https://www.fline.dev/why-i-stopped-building-for-visionos-and-what-could-bring-me-back/))|
|산업용 원격 지원 앱|기업 전용 패스스루 영상 공유 필요([2](https://framesixty.com/apple-vision-pro-development-for-enterprise/))|
|지속적 공간 메모리 앱|오브젝트 위치 저장 기능 미지원([4](https://www.fline.dev/why-i-stopped-building-for-visionos-and-what-could-bring-me-back/)[6](https://ubos.tech/news/challenges-and-opportunities-in-developing-for-apples-vision-pro/))|
|고도화된 VFX 앱|파티클 시스템 제한([3](https://www.rebel9.co.kr/kr/works/archive-exhibition/ae-research/apple-vision-pro-case-study/)[5](https://www.gianty.com/apple-vision-pro-app-development/)), HLSL 미지원([5](https://www.gianty.com/apple-vision-pro-app-development/))|

## Vision Pro 사용자들은 어떤 앱을 필요로 할까 ?

### Vision Pro 구입 결정 이유
- **최고 수준의 트래킹과 몰입형 디스플레이**
    
    - 사용자들은 Apple Vision Pro의 뛰어난 공간 트래킹(손동작, 시선 추적)과 micro-OLED 기반의 고해상도 디스플레이에 매료되어 구매를 결정합니다. 다른 AR/VR 헤드셋과 비교할 수 없는 몰입감과 시각적 충실도가 큰 매력입니다[1](https://bgr.com/tech/6-reasons-to-buy-an-apple-vision-pro/)[2](https://basicappleguy.com/basicappleblog/apple-vision-pro-1-year-later)[3](https://www.techradar.com/computing/virtual-reality-augmented-reality/apple-vision-pro-8-reasons-to-buy-it-and-6-reasons-to-skip).
        
- **컨트롤러 없이 손과 눈으로 조작**
    
    - 기존 VR/AR 기기와 달리 별도의 컨트롤러 없이 손동작과 시선으로 직관적으로 조작할 수 있어 접근성이 높고, 사용이 편리하다는 점이 강조됩니다[1](https://bgr.com/tech/6-reasons-to-buy-an-apple-vision-pro/)[4](https://www.linkedin.com/pulse/5-user-experience-advantages-apple-vision-pro-oliver-weidlich-ix6jc).
        
- **생산성 향상 및 멀티태스킹**
    
    - Mac과 연동해 큰 화면에서 멀티태스킹이 가능하고, 여러 앱을 공간에 배치해 동시에 사용할 수 있어 업무 효율이 크게 높아집니다[1](https://bgr.com/tech/6-reasons-to-buy-an-apple-vision-pro/)[4](https://www.linkedin.com/pulse/5-user-experience-advantages-apple-vision-pro-oliver-weidlich-ix6jc)[5](https://xmind.com/blog/these-apps-will-be-supported-on-apple-vision-pro-at-launch).
        
- **최고의 프라이빗 시네마 경험**
    
    - Apple TV+, Disney+, Max 등 주요 스트리밍 서비스의 HDR 및 3D 영화, 180도 8K 영상(Apple Immersive Video) 시청이 가능해 집에서 영화관을 즐기는 듯한 경험을 제공합니다[1](https://bgr.com/tech/6-reasons-to-buy-an-apple-vision-pro/)[2](https://basicappleguy.com/basicappleblog/apple-vision-pro-1-year-later).
        
- **애플 생태계와의 연동**
    
    - iPhone, iPad, Mac 등 애플 기기와의 원활한 연동, 사진·비디오·캘린더 등 데이터의 자동 동기화, Optic ID 등 보안 기능도 구매 결정에 영향을 미칩니다[4](https://www.linkedin.com/pulse/5-user-experience-advantages-apple-vision-pro-oliver-weidlich-ix6jc)[2](https://basicappleguy.com/basicappleblog/apple-vision-pro-1-year-later).
        
- **미래지향적인 경험**
    
    - 새로운 기술을 먼저 경험하고 싶은 얼리어답터 심리, 그리고 애플이 제시하는 미래 컴퓨팅 비전에 대한 신뢰도 구매 동기 중 하나입니다[1](https://bgr.com/tech/6-reasons-to-buy-an-apple-vision-pro/)[3](https://www.techradar.com/computing/virtual-reality-augmented-reality/apple-vision-pro-8-reasons-to-buy-it-and-6-reasons-to-skip).
        

### 가장 만족스럽게 활용하는 앱

- **미디어 및 엔터테인먼트 앱**
    
    - Apple TV, Disney+, Max 등 영화·TV 시청 앱이 가장 인기가 높으며, 몰입형 비디오(Immersive Video)와 3D 영화 감상 경험은 사용자 만족도가 매우 높습니다[2](https://basicappleguy.com/basicappleblog/apple-vision-pro-1-year-later)[6](https://www.pcmag.com/picks/the-best-apple-vision-pro-apps)[7](https://9to5mac.com/best-apple-vision-apps/).
        
- **사진·비디오 앱**
    
    - 공간 사진(panorama), 3D 비디오 등 몰입형 사진/비디오 감상 앱도 큰 호응을 얻고 있습니다. 과거 여행 사진을 360도로 감상하거나, iPhone에서 촬영한 Spatial Video를 Vision Pro에서 보는 경험이 매우 감동적이라는 평가가 많습니다[2](https://basicappleguy.com/basicappleblog/apple-vision-pro-1-year-later)[4](https://www.linkedin.com/pulse/5-user-experience-advantages-apple-vision-pro-oliver-weidlich-ix6jc)[7](https://9to5mac.com/best-apple-vision-apps/).
        
- **생산성/업무 앱**
    
    - Microsoft Office(Word, Excel, PowerPoint), Evernote, Trello, Zoom, Slack 등 업무용 앱이 널리 활용되고 있습니다. 멀티태스킹과 공간 배치가 가능해 업무 효율이 크게 향상됩니다[5](https://xmind.com/blog/these-apps-will-be-supported-on-apple-vision-pro-at-launch)[7](https://9to5mac.com/best-apple-vision-apps/)[8](https://appsforapplevision.com/).
        
- **게임 및 창작 앱**
    
    - 공간 게임(Apple Arcade), 음악 제작(Moog), 디지털 아트(Da Vinci Eye) 등 창의적이고 몰입감 있는 앱도 인기가 높습니다[7](https://9to5mac.com/best-apple-vision-apps/)[8](https://appsforapplevision.com/).
        


### 사용자들이 기대하는 앱

- **더 다양한 몰입형 미디어 및 게임**
    
    - 3D 영화, 몰입형 콘텐츠, 공간 게임 등 더 많은 엔터테인먼트 앱이 출시되길 기대합니다[2](https://basicappleguy.com/basicappleblog/apple-vision-pro-1-year-later)[7](https://9to5mac.com/best-apple-vision-apps/)[8](https://appsforapplevision.com/).
        
- **생산성 및 협업 도구**
    
    - 업무 효율을 높일 수 있는 새로운 협업 앱, 화상회의, 프로젝트 관리, 데이터 시각화 앱 등이 추가되길 원합니다[5](https://xmind.com/blog/these-apps-will-be-supported-on-apple-vision-pro-at-launch)[7](https://9to5mac.com/best-apple-vision-apps/).
        
- **건강 및 피트니스 앱**
    
    - 몰입형 피트니스, 요가, 명상, 건강 관리 앱 등 건강 관련 앱에 대한 기대도 큽니다[7](https://9to5mac.com/best-apple-vision-apps/).
        
- **교육 및 학습 앱**
    
    - 3D 모델, 가상 현장 학습, 언어 학습 등 교육용 앱도 많은 관심을 받고 있습니다[7](https://9to5mac.com/best-apple-vision-apps/)[8](https://appsforapplevision.com/).
        
- **실생활 연계 앱**
    
    - 쇼핑, 여행, 항공, 내비게이션 등 일상생활에 유용한 공간 컴퓨팅 앱이 더 다양해지길 바라고 있습니다[7](https://9to5mac.com/best-apple-vision-apps/)[8](https://appsforapplevision.com/)



## 개발 기술 타당성 조사
### 조명(전시 or 인테리어)
방 안에 가상 조명을 설치하고, 테스트해볼 수 있는 앱


#### AR로 구현
VisionOS에서는 RoomPlan API가 아예 없으므로, 실내 환경의 구조를 가져오기 위해서는 ARKit을 통해서 가져와야 한다.

ARKit의 PlaneDetectionProvider를 통해서 평면 감지(바닥, 벽 등 평면 식별)를 하고, SceneReconstructionProvider를 통해서 실시간 메쉬 재구성(주변 환경의 폴리곤 메쉬)를 ARKit 세션을 통해서 얻을 수 있으며, 이를 조합해서 RoomPlan처럼 방의 구조를 파악하는 로직을 직접 개발해야 한다.
(**사례** - https://apps.apple.com/us/app/magic-room-lidar-environment/id6477834941)

공간을 스캐닝해서 매쉬를 재구성하는 것까지도 큰 도전이고 이것만 성공한다고 해도 실현해볼 수 있는 것들이 무궁무진할 것 같다. 하지만 여기서 meterial을 새로 적용해서 직접 조명을 적용하는 것은 cost도 너무 많이 들고 그에비해 dynamic한 결과물이 나오지 않아 보인다.

**결론적으로** 직접 조명을 적용하기에는 무리가 있다.

**리서치 자료**
https://chatgpt.com/s/dr_686393909ed08191a417929cd5c426f4


#### VR로 구현



## 앱 사용기
### Sceno
지도를 통해 갤러리에 있는 이미지 위치 표시하고, 거리뷰로 탐험하는 앱

360 Immersive space로 구현돼어서 몰입도는 좋지만, 이동할 때마다 이미지를 불러오는 과정에서 블러처리 되는 과정과, 뚝뚝 끊기며 이동하는 부분에서 몰입도가 깨짐. 거리뷰 보는 느낌.

### AroundUs
지도에서 주변 관광지를 표시해주고 해당 관광지에 대한 설명이 적혀있는 앱
해당 관광지를 클릭하면, apple map의 3d 모델링 된 데이터로 볼 수 있다.
거리뷰를 통한 탐색은 제공 X

**장점**
지도에서 관광지 리스트를 보고 골라서 갈 수 있어 좋다.
해당 관광지에 대한 설명이 적혀있어 좋다.
3D모델링 맵을 제공하는 점이 좋다.
(애플맵의 해당 API를 사용하면 길찾기 앱에서도 유용하게 사용 가능할듯)

### MindNodeNext
브레인 스토밍을 공간 컴퓨팅 형태로 할 수 있고,
마입드 맵이나 도식도같은 것들은 윈도우 형식으로 제공한다.

다만, 브레인 스토밍 기능이 단순히 아이디어를 입력하고 화면에 나온 아이디어의 위치를 옮기거나 하는 등의 기능밖에 하지 않아서, 경험은 새롭지만 유용해보이지는 않는다.


## 공잡기

**VR**
1. 공이 날아온다.(Reality Kit으로 3D 구현
   배경을 구성한다. (reality composer pro로 evnirionment 구성)
   
   
2. 공을 쳐다본다.
3. 쳐다본 공이 hover되면 손짓으로 잡는다.

공을 타이밍 맞게 잡으면 추가점수 (리듬게임처럼 perfect, great 와 같이)
gamekit을 연동해서 리더보드로 점수 등록

**체크리스트**
- [ ] 공이 가까워지면 커지게 가능한지
- [ ] 손을 미트 자세로 잡고있는지 인식 가능한지(손의 위치값도)
- [ ] 손이 잡는 모양을 했는지 확인
- [ ] 사용자가 앉아있는지 확인
- [ ] 손 위에 글러브를 끼울 수 있는지(가상의 손 사용 ?)
- [ ] 오른손, 왼손 선택 가능한지
- [ ] 설정한 속도에 맞춰서 공이 오게끔 가능한지
- [ ] 공이 변화구처럼 휘어오게 가능한지
- [ ] 손에끼워진 글러브가 공의 위치에 맞게 이동했는지 판별 가능한지
- [ ] 공에 위치에 맞게 소리가 나게할 수 있는지