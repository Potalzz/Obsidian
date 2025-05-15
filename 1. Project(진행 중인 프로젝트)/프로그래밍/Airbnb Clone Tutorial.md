DDD 방식으로 폴더를 구성하고 시작.

### View
전체적으로 `Stack`내부에서 간격과, 정렬은 `Stack`에서 `spacing`과 `alignment`를 통해서 전체적으로 관리하기.

**요소마다 값 넣어서 일일이 조정 X**

#### 스크롤하는 화면
`ExploreView`에 `NavigationStack`, `ScrollView`, `LazyVStack`으로 검은 화면의 틀을 먼저 만들어 둔다.

틀을 먼저 만들어 두고 `ListingItemView`에서 `TabView`로 이미지를 여러장 넣을 수 있게 구성하고, `.tabViewStyle(.page)`를 통해서 페이지 형식의 스와이프를 추가한다.

#### 페이지 이동
전체 페이지 목록 각 아이템에서 해당하는 상세 페이지로 들어가려면 `NavigationLink`와 `NavigationDestination`이 있어야 한다.
즉, 상세 페이지로 이동하는 링크와 도착점이 있어야 한다.

`ForEach` 내부에 각 아이템을 `NavigationLink(value: listing)`로 감싸줘서, 링크를 구성한다.


