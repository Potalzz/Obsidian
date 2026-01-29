
# Project
```
다른 Entity와의 관계
Project(1): AutoSave(1)
Project(1): Thumbnail(1)
Project(1): Immersive(1)
Project(1): Scene(Volume)(1)
```

```
project_id (PK) : UUID()
title(Uni ID) : String
image: String(확정 X)
createdAt: Date()
updatedAt: Date()
```


## AutoSave
```
다른 Entity와의 관계
Project(1): AutoSave(1)
```

```
미정
```

## Thumbnail
```
다른 Entity와의 관계
Project(1): Thumbnail(1)
```

```
미정
```

## Immersive
```
다른 Entity와의 관계
Project(1): Immersive(1)
```

```
immersiveID(PK): UUID()
projectID(FK): UUID()
immsersiveBg: String
userPositionX: Float
userPositionZ: Float
viewMode: bool
```
## Scene(Volume)
```
다른 Entity와의 관계
Project(1): Scene(1)
Scene(1): Object(씬에 배치된 개체)(N)
```

```
sceneID(PK): UUID()
projectID(FK): UUID()
groundSizeX: Int
groundSizeY: Int
groundSizeZ: Int
roomType(enum: room_o | room_x): String
viewMode: bool
```

### Object(씬에 배치된 객체)
```
다른 Entity와의 관계
Scene(1): Object(씬에 배치된 개체)(N)
Object(씬에 배치된 개체)(1) : Asset(1)
Object(씬에 배치된 개체)(1) : ImageObject(0..1)
Object(씬에 배치된 개체)(1) : SoundObject(0..1)
```

```
objectID(PK): UUID()
sceneID(FK): UUID()
assetID(FK): List(String)
type(enum: image | sound | both): String
positionX: Float
positionY: Float
positionZ: Float
editable(bool): Bool
```
#### ImageObject
```
다른 Entity와의 관계
Object(씬에 배치된 개체)(1) : ImageObject(0..1)
```

```
미정
```

#### SoundObject
```
다른 Entity와의 관계
Object(씬에 배치된 개체)(1) : SoundObject(0..1)
```

```
미정
```
#### Asset
```
다른 Entity와의 관계
Object(씬에 배치된 개체)(1) : Asset(1)
Asset(1) : ImageAsset(0..1)
Asset(1) : SoundAsset(0..1)
```

```
assetId(PK): UUID()
type(enum: image | sound): String
filename(초기값은 원본 파일명): String
mime(MIME타입 파일 형식): String(삭제될 수 있음)
fileSize: Int(삭제될 수 있음)
url(해당 파일이 저장된 위치): String
createdAt: Date()

```
##### ImageAsset
```
다른 Entity와의 관계
Asset(1) : ImageAsset(0..1)
assetId(PK/FK): UUID()
width: Float
height: Float
```

##### SoundAsset
```
다른 Entity와의 관계
Asset(1) : SoundAsset(0..1)
assetId(PK/FK): UUID()
durationSec: Int
channels(enum: mono | stereo | binaural): String
```