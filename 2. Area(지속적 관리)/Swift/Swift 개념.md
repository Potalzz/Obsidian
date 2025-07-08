
### 타입
Double과 CGFloat는 모두 소수점이 있는 숫자를 의미하지만, 기본적으로는 똑같이 인식된다. Double형의 변수에 CGFloat형 변수를 대입해도 문제가 없다.
하지만 사용 목적에 따라서 나뉜다. Double은 수학적 계산에서 사용되고,
CGFloat는 UI에서 사용된다.(예: 픽셀 계산)

연산자
산술 연산자는 Pendas기법을 사용하며, 이는 수학 공식과 동일하다.
이는 연산자에만 적용되는 것이 아니라 if문에도 적용된다.
and와 or이 여러개 추가 된 if문에 괄호를 사용하여 조건 판별 순서를 변경할 수 있다.

함수
함수에서 화살표로 반환할 타입을 지정하는 경우 반드시 return문을 포함해야 한다.
함수에서 void를 반환하는 경우 아무것도 반환하지 않는 것을 의미한다.

클로저
클로저는 함수의 중괄호 내부에 있는 코드를 의미한다.
클로저는 함수 내부에서 private하게 처리되어 있기 때문에,
함수 외부에서 접근할 수 없다.
  
배열
배열에 값 추가
arr.append(5) // 끝에 5 추가
arr += [4,5] // 끝에 4,5 추가
arr.insert(10, at:1) // 1번 인덱스에 10추가
arr.append(contentsOf: arr2) // 배열에 다른 배열 추가
swift에서 let으로 선언된 배열에는 값을 추가할 수 없다.

### Udemy 강의

Main 스토리보드의 요소들은 모두 소스 코드에 코드 형태로 저장된다.

때문에 main의 요소들을 viewController에 옮기고 해당 프로퍼티의 이름을 지정해 저장하게 되면 main파일의 소스코드의 형태로 변경되므로, 프로퍼티 이름을 변경하고 싶다면, viewController에서만 변경하는 것이 아니라 main의 소스코드에서도 찾아서 변경해줘야 한다. 해당 방법을 자동으로 적용시키는 방법이 viewController에서 이름에 우클릭 버튼 누르고 rename하면 된다.

  

**랜덤 만들기**

랜덤 숫자 만드는 방법은 Int.random(in: lower…upper)이다.
배열의 요소를 랜덤으로 골라야 하는 경우에는 랜덤으로 숫자를 생성해서 하는 것 보다 간편한 방법이 있다. Index안에서 랜덤으로 숫자를 만들어도 되고, 이것 보다 더욱 간편한 방법은 array.randomElement() 메서드를 사용하여 배열 안에 있는 요소 중에 랜덤으로 하나를 고를 수 있다.

배열을 무작위로 섞는 방법 : array.shuffle()

**오토 레이아웃**

우측 하단의 align, constraints를 통해서 요소를 상대적으로 정렬할 수 있다.

상대적으로 참조하는 상위 요소를 stack view를 통해서 상위 레이어로 만들어 줄 수 있으며, 해당 stack view는 참조에만 사용되도록 배경을 default로 바꿔 보이지 않게 설정해준다.

여러개의 요소를 박스화 시키거나 동일한 구조로 정렬시켜야 할 경우 stack view로 박스를 만들어서 한다.

**모르는 부분 찾기**
동작할 기능, 언어, 찾을 사이트 형태로 검색.

**모르는 방법 구현하는 접근 방법**
검색해서 찾는다. -> 코드 구현 -> 코드 기능 검색 -> 코드 커스터마이징

**옵셔널**

옵셔널이란 값이 있을 수도 있을 수도 있고, 없을 수도 있는 변수를 정의할 때에는 ?를 붙여야 하며, 이렇게 정의한 변수를 옵셔널이라고 한다.

값이 확실하게 존재하지 않는 경우에 사용

옵셔널에 초깃값을 지정하지 않으면 기본값은 nil이다.

nil은 값이 없음을 의미하며, 옵셔널외에 다른 변수에는 부여할 수 없다.

  

**옵셔널 바인딩**

옵셔널의 값을 가져오는 것을 옵셔널 바인딩이라고 한다.
옵셔널의 값이 존재하는지를 검사한 뒤, 존재한다면 그 값을 다른 변수에 대입시켜준다.
If let 또는 if var을 사용하여 옵셔널의 값을 벗겨서 값이 있다면 if문 안으로 들어가고, 값이 nil이라면 그냥 통과한다.

**Xcode 단축키**

창 열고 닫기
Settings : command + ,
Navigator : command + 0
Document outline : command + control + 0
Inspectors : command + option + 0

보조 뷰 불러오기 -> 우측 상단 햄버거에서 Assistant
메서드나 변수 등등이 무슨 기능을 하는지 확인하려면 option + 클릭
코드 Auto formatting : Ctrl + I

아이폰 화면에서 navigator추가: 스토리보드 파일에서 상단 Editor -> Embedded In -> Navigator Contoroller

### Swift Class

스위프트에서 클래스와 구조체의 차이점은, 상속 기능이다.
Class는 super(부모) class를 `class son: parent`형태로 상속받을 수 있으며,
부모 클래스의 모든 기능과 속성들을 상속받아서 사용할 수 있다.
override를 통해서 부모의 속성을 재정의 할 수 있다.
또한 이미 요소를 재정의 했더라도 super. 키워드를 통해서 부모 클래스 원본의 속성이나 기능을 사용할 수 있다.
swift에서는 UILabel, UIButton등 많은 클래스가 상속을 통해서 가장 큰 NSObject라는 기본 Class로부터 아래로 상속받아 오면서 사용이 가능하다.

**struct와 class의 차이점**

struct는 초기값을 변수 : 타입 형태로 지정해 둘 수 있지만
class는 초기값에 값이 없는 경우로 둘 수는 없고 init() 메서드를 사용해 초기값을 타입 형태로 지정해야 한다.

또한, class는 이미 생성된 class를 변수로 복사하여 생성하는 경우, 속성 값들을 모두 참조하여 이어받게 되지만, struct는 변수로 기존에 생성된 struct를 복사해서 생성하면 새로운 struct를 생성하기 때문에, 변경되는 값들을 이어받지 않는다.
**struct는 불변성**을 가지고, **class는 레퍼런스**를 참고한다. 

UILabel, UIViewController 등은 Apple이 만든 UIKit이라는 프레임워크에 내장되어 있는 Class이기 때문에, 먼저 UIKit이라는 프레임워크를 import해야 사용할 수 있다.

**화면 전환**
**self**.performSegue(withIdentifier: "goToResult", sender: **self**)
스토리보드에서 설정한 Segue(화면 전환)를 실행하는 메서드
“goToResult”라는 Segue Identifier를 가진 화면 전환을 실행함.

화면을 전환하기 전에 데이터를 전달해야 하면, prepare(for segue:)가 자동으로 호출됨.

  

prepare(for segue:, sender:)

화면이 전환되기 전에 데이터를 전달할 수 있도록 호출되는 메서드.

segue.destination을 사용하여 **다음 화면(ViewController)에 데이터를 전달**할 수 있음.

performSegue(withIdentifier:)가 실행될 때 **자동으로 실행됨.**

  

  

### 프로토콜(Protocol)

프로토콜은 일종의 약속과도 같다.
해당 프로토콜을 참조하는 경우에 프로토콜 내부에서 지정한 속성이나 기능들이 모두 구현되어야 한다.
프로토콜에서 속성은 저장 형태와 연산 형태로 구현할 수 있는데, 저장 형태의 경우 let, var 모두 사용 가능하고 연산 형태의 경우 var만 사용 가능하다.

저장,연산 형태 모두 {get}, {get set} 모두 사용 가능하다.

다만 저장 형태에서 프로퍼티를 선언할 때 {get set}을 사용하는 경우 반드시 var로 선언하여야 하며, 구현하는 쪽에서도 var로 선언하여야 한다.

### Delegate 패턴

객체의 동작을 다른 객체에 위임하여 사용하기 위한 패턴
Ex) A가 B의 기능을 사용하고 싶을 때 직접 구현하지 않고 C에게 위임(delegate)하여 구현하는 방법. 이를 통해서 A와 B간의 결합도를 낮출 수 있다.

예를 들어 응급 구조 증명서, 호출 요원, 구급 요원 이렇게 있다고 해보자.

응급 상황이 발생하면 호출 요원이 응급 구조 증명서를 가진 구급 요원을 호출한다.

호출 요원은 구급 요원이 누군지 알 필요 없고 단순하게 호출하기만 한다.

각 기능을 코드로 구현해보자.

```
Protocol 응급구조증명서 {

func 심폐소생술()

}

  

Class 호출요원 {

var delegate: 응급구조증명서?

  

func 상황파악 {

	print(“무슨 상황인가요 ?”)
}

  

func 응급처치 {

	delegate?.심폐소생술()
}

  

struct 구급대원: 응급구조증명서 {

	init(handler: 호출 요원) {
	handler.delegate = self
}

  

func 심폐소생술() {

	print(“초당 1회 속도로 30초간 가슴압박 시행”)
}

  

let 김미진 = 호출요원()

let 문우림 = 구급대원(handler: 김미진)
```

—

위와 같이 역할이나 기능을 위임하여 작동하는 방식이 delegate패턴이다.

응급구조증명서는 심폐소생술을 할 줄 알아야 안다고 명시해놓고, 해당 protocol을 상속받은 struct나 class는 심폐소생술을 알고있어야 함으로, 내부에 해당 기능을 반드시 구현해야 한다.

또한 호출 요원이 심폐소생술을 직접 시행하는게 아니므로, 응급처치를 실행하면 구급대원에게 연결되어 시행하도록 구성한다.

delegate패턴을 왜 사용하나 ?
-> 뷰 컨트롤러간 결합도를 낮추기 위해.

보통 mvc같은 큰 아키텍쳐를 구성하기 위한 행동 패턴으로 활용된다.

### 클로저(Closure) [[클로저(Closure)]]

#### 클로저란 ?

함수처럼 사용하지만 이름이 없는 **익명 함수**

하지만 사실 `func 키워드`를 이용해 이름을 붙여주는 함수들도 클로저이다 !
	클로저는 **Named Closure**와 **Unnamed Closure** 총 두 가지 종류가 있다. 이름을 붙여 선언하는 함수는 **Named Closure**이지만 편하게 **함수**라고 부르는 것 뿐이다.`(그래도 클로저란 사실은 변함 없다)`

이름을 붙이지 않고 사용하는 함수를 **익명 함수** 즉, **클로저**라고 부른다!

변수나 상수에 할당할 수 있으며, 함수의 매개변수로 전달 가능

클로저는 **1급 객체**이므로 함수의 파라미터로 클로저를 전달할 수 있다.

#### 클로저 표현식

```
{ (Parameters) -> Ruturn Type in
	실행 구문
}
```

또한, 클로저는 **클로저 헤드**와 **클로저 바디**로 이루어져 있다.
![[Pasted image 20250325110415.png]]

이 둘을 구분지어주는 것이 `in` 이라는 **키워드** 이다 !

#### 그래서 클로저를 왜 사용할까 ?

##### 먼저 인자와 반환값에 대해 알아보자.

스위프트에서 `( ) -> Void`는 함수의 형식을 나타내는 표시로써, 인자값으로 사용될 함수의 형식을 나타내는 데에 주로 사용된다.

보통 화살표 `->`를 기준으로 양쪽에 작성된 기호나 문자들은 함수의 매개변수와 반환값의 형식을 의미한다.


![[Pasted image 20250326232015.png]]
**왼쪽이 함수의 매개변수**를, **오른쪽이 반환값**을 뜻한다.

**매개변수**에 해당하는 **왼쪽**이 `()`인 것은 매개변수가 없는 함수라는 것을 의미하고,
**반환값**에 해당하는 **오른쪽**이 `Void`인 것은 아무 값도 반환하지 않는 함수를 의미한다.
즉, 매개변수와 반환값이 **모두 없는** 함수 타입을 의미한다.
```
// 매개변수와 반환값이 없는 함수
func exec() {
	tabBar?.alpha = ( tabBar?.alpha == 0 ? 1 : 0)
}
```


만약 `Int` 타입 하나를 입력받아 `String`을 반환한다면 이 함수의 타입 표시는 다음과 같다.
`(Int) -> String`

이렇게 함수가 완성되면, 이를 인자값으로 전달해 줄 차례이다.
함수를 인자값으로 전달할 때에는 단순히 함수의 이름만 사용한다.
함수를 실행하기 위한 `( )` 같은 것을 제외하고.
```
UIView.animate(withDuration: TimeInterval(0.15), animations: exec)
```

그런데 이런 방식으로 **함수를 인자값으로** 사용하다 보면 **두 가지 불편한 점**이 드러난다.
> 1. 함수를 인자값으로 넘기기 전에 **먼저 정의**해야 한다.
> 2. 재사용성이 거의 없는 인자값을 위해 **굳이 함수를 정의**해야 한다.

이 같은 문제를 해결하기 위해 ***클로저(Closure)*** 를 사용한다.
(자바스크립트의 익명 함수 같은 개념)

##### 클로저 사용법
클로저를 사용하면 앞의 **두 가지 문제**를 한꺼번에 해결할 수 있다.
먼저 미리 정의해 둘 필요 없이 인자값으로 전달하는 시점에 함수를 정의할 수 있으며,
모든 함수를 클로저 형식으로 변환할 수 있다.
```
// 앞의 exec()함수를 클로저로 정의
{
	tabBar?.alpha = ( tabBar?.alpha == 0 ? 1 : 0)
}
```

중괄호의 시작 `{`에서 중괄호의 종료 `}`까지가 모두 클로저 범위에 해당한다.
**클로저**는 따로 이름을 가지지 않기 때문에 코드 블록으로 시작하여 코드 블록으로 마감된다.
**클로저**를 인자값으로 사용할 때에는 다음과 같이 통째로 넣어주면 된다.
```
UIView.animate(withDuration: TimeInterval(0.15), animations: {
	tabBar?.alpha = ( tabBar?.alpha == 0 ? 1 : 0)
})
```

#### 트레일링 클로저

>함수의 **마지막 매개변수**가 클로저를 입력받는 경우,
>인자값의 위치에 클로저 구문을 넣지 않고, 대신 **메소드 뒤쪽에 실행 블록처럼** 붙일 수 있도록 하는 예외 문법이다.

```
// 마지막 매개변수 animations를 생략하고 클로저 블록을 맨 뒤에 붙임.
UIView.animate(withDuration: TimeInterval(0.15) ) {
	tabBar?.alpha = ( tabBar?.alpha == 0 ? 1 : 0)
}
```

>추가적인 정보 https://babbab2.tistory.com/82 참고




함수와 달리 주변 컨텍스트(변수 등)를 **캡쳐**하여 사용 가능(변수를 캡쳐한다는 것은 함수 내부에 선언된 변수는 함수가 다시 실행될 때마다 값이 초기화되지만 캡쳐하게 되면 독립적으로 값을 계속해서 기억하고 있기 때문에 함수가 실행될 때마다 이전에 기억한 값을 토대로 업데이트가 진행된다.)

`Int`형태의 `value`타입은 클로저 시작 범위에서 변수를 캡쳐하여 대입하지만, `Stirng`형태의 `Reference`타입은 `Reference Capture`  참조 한다고 생각하면 된다.

클로져 내부에서 변수나 함수를 사용하려면 self키워드를 추가해야 한다.

일반적인 함수는 함수가 종료되면 메모리에서 삭제되기 때문에, var 사용이나 메모리 부분에서 걱정할 부분이 적지만 클로저는 외부 변수를 캡처하기 때문에 함수 종료 후에도 메모리에 남아 있어 메모리 누수가 발생할 수 있다. 이를 방지하려면 `[weak self]` 또는 `[unowned self]`를 사용하여 메모리에서 해제될 수 있도록 관리해야 한다.


### 매개 변수

매개 변수의 이름을 입력할 때, 호출할 때 각각 두 가지로 이름을 설정할 수 있다.

```
func myFunc(name eman: Type) {

	print(eman)
}

// myFunc(name: “Jack”)
// 인자로 넣을 때는 name으로, 호출할 때는 eman으로.
  
입력 매개변수 이름을 언더바(_)로 두어 입력할 때 이름을 생략할 수 있다

func myFunc(_  eman: Type) {
	print(eman)
}
// myFunc(“Jack”)
```
  

### Swift Life Cycle(생명주기)

swift의 생명 주기 순서는

Init -> loadView -> viewDidLoad -> viewWillAppear -> viewDidAppear -> viewWillDisappear -> viewDidDisappear 순서로 구성되어 있다.

**loadView** : 컨트롤러가 뷰를 만드는 역할. loadView가 뷰를 만들고 메모리에 올린 후에, viewDidLoad가 실행된다.

**viewDidLoad** : 뷰의 로딩이 완료되면 호출.
해당 뷰가 생성된 후 초기에만 실행된다.

**viewWillAppear** : 뷰가 나타나기 직전에 호출.
뷰가 나타날거라는 신호를 컨트롤러에게 알리는 역할을 하며, viewDidLoad와 달리 view간 이동을 할 때 마다 실행된다.

**viewDidAppear** : 뷰가 화면에 나타난 직후 호출. 뷰가 나타났다는 것을 컨트롤러에게 알리는 역할을 하며 화면에 적용될 애니메이션을 그려준다.

**viewWillDisappear** : 뷰가 사라지기 직전에 호출. 뷰가 사라질거라고 컨트롤러에게 알려준다.

**viewDidDisappear** : 뷰가 사라진 직후에 호출.
뷰가 사라졌다고 컨트롤러에게 i알려준다.

여러 개의 view가 있을 때, view간 이동을 할 때 각 lifeCycle이 순차적으로 실행되는 것이 아니다. 
기존 뷰가 사라질때와 새로운 뷰의 나타날 때 생명 주기가 조금 다르다.

**예제를 통해 살펴보자**

두 개의 view가 있다면 view전환 시 lifecycle주기는 다음과 같다.

VC1 viewDidLoad()

VC1 viewWillAppear()

VC1 viewDidAppear()

———————————

VC2 viewDidLoad()

VC1 viewWillDisappear()

VC2 viewWillAppear()

VC2 viewDidAppear()

VC1 viewDidDisappear()

  

첫 번째 view를 실행시키면 viewDidLoad -> viewWillAppear -> viewDidAppear까지 view가 나타나는 과정은 동일하다.

첫 번째 view에서 두 번째 view로 넘어가면, viewWillDisAppear이 먼저 호출되고 두 번째 view의 viewDidLoad -> viewWillAppear까지 호출되고 나서 첫 번째 view가 사라져viewDidDisappear이 호출되고 나서야 두 번째 view의 viewDidAppear이 호출된다.

당연히 여기서 각 view가 처음 Load아니라면 viewDidLoad는 생략된다.

각 단계에서 view의 생명주기와 그에 해당하는 생명주기 메서드가 호출되는 시점은 동일하므로 해당 메서드가 호출되는 시점이 해당 view의 생명주기 상태라고 봐도 무방하다.

### 캐스팅

업 캐스팅: 하위 클래스 -> 상위 클래스
다운 캐스팅: 상위 클래스 -> 하위 클래스

업 캐스팅은 항상 안전하게 작동한다.

다운 캐스팅은 불확실한 경우 as? 를 통해서 안전하게 처리하고, as! 의 경우에는 확실한 경우에만 사용하여 강제 다운캐스팅을 진행한다.

실패 시 앱이 종료되므로 주의해서 사용하자.

```
Ex)

Class Animal {

	func sound() {
		print(“animal’s sound”)
	}
}


Class Dog: Animal {

	func bark() {
		print(“bow wow!”)
	}
}

let myDog = Dog()
let animal: Animal = myDog // 업캐스팅
let myAnimal: Animal = Dog() // 업캐스팅

// 안전한 다운 캐스팅 (as?)
If let myRealDog = myAnimal as? Dog {
	myRealDog.bark()
	} else {
	print(“반환 실패”)
}

// 강제 다운 캐스팅 (as!)
let forceDog: Animal = as! Dog
```
  

### swift UI

스위프트 UI는 기존 storyboard형식에서 요소를 가져오면 코드로 생성되고, 이를 코드를 통해 편집을 간편하게 하고 내용을 한 눈에 볼 수 있도록 개선한 것이다.

하나의 요소를 만들면 command + 클릭 을 통해서 모듈화 시킬 수 있으며, 이를 통해서 비슷한 요소를 여러개 생성할 수 있는 것이 장점이다.

Swift ui 에서는 변경되는 변수 앞에 @state를 붙여줘야 한다. @state를 붙여줘야 변경되는 값 추적 확인 리스트에 추가가 되고, 값이 변경되면 해당 값이 어디에 있는지 찾아서 view에 반영하기 때문이다.

### 싱글톤 패턴(Singleton Pattern)

싱글톤 패턴이란, 특정 용도로 객체를 하나만 생성하여 공용으로 사용하고 싶을 때 사용하는 디자인 패턴.

클래스가 여러차례 호출 되어도, 인스턴스는 단 한 번만 생성되기 때문에 전역변수처럼 어느 곳에서 접근하던지 같은 메모리에 접근이 가능하다.

일반적인 클래스는 호출될 때마다 인스턴스를 생성하여 모두 다른 메모리를 가리키게 되지만, 싱글톤 패턴을 사용하면 클래스 내부에서 인스턴스를 생성하고 private처리를 하여 외부에서 인스턴스가 생성될 수 없기때문에 모두 같은 인스턴스를 참조한다.

***

// 싱글톤 패턴 사용 예시

```
// Singleton 클래스 정의
class UserInfo {

    static let shared = UserInfo() // 싱글톤 인스턴스
    var name: String?
    var phone: String?
    var address: String?
    
    private init() { } // 외부에서 초기화 막기
}

// A ViewController
let userInfoA = UserInfo.shared
userInfoA.name = "user name"

// B ViewController
let userInfoB = UserInfo.shared
userInfoB.phone = "010-1234-1234"

// C ViewController
let userInfoC = UserInfo.shared
userInfoC.address = "Seoul"

// ⚙️ 확인 (어느 ViewController에서든 동일하게 접근됨)
print(UserInfo.shared.name ?? "")      // "user name"
print(UserInfo.shared.phone ?? "")     // "010-1234-1234"
print(UserInfo.shared.address ?? "")  // "Seoul"
```
  

#### 인코더와 디코더
인코더는 음악을 LP 디스크로 바꾸는 것이고, 디코더는 LP 디스크를 다시 음악으로 만드는 것이다.
Todoey프로젝트에서 보자면, 사용자 지정 개체 배열을 Plist에서 읽을 수 있는 데이터로 인코딩한다.

#### 데이터 베이스

앱에서 데이터를 저장하는 방법은 크게 테이블과 데이터베이스가 있다.

테이블은 간단한 키,값의 데이터를 저장하기에 용이하고 데이터베이스는 단일 테이블보다 훨씬 정교하여 테이블이나 클래스 사이에 관계를 구축하게 해주고, 데이터베이스 쿼리로 특정 항목을 찾거나 관계를 이용해 두 테이블을 링크하는 등 훨씬 더 복잡한 작업을 수행할 수 있게 해준다.

|            |         |
| ---------- | ------- |
| **Method** | **Use** |

|              |                                                  |
| ------------ | ------------------------------------------------ |
| UserDefaults | 빠르게 작은 데이터 조각을 저장 (예: 최고 점수, 플레이어 닉네임, 음악 켜기/끄기) |

|   |   |
|---|---|
|Codable|사용자 정의 객체를 빠르게 저장|

|          |                 |
| -------- | --------------- |
| Keychain | 작은 데이터를 안전하게 저장 |

|   |   |
|---|---|
|SQLite|대용량 데이터를 저장하고 쿼리하기|

|   |   |
|---|---|
|Core Data|객체 지향 데이터베이스|

|   |   |
|---|---|
|Realm|더 빠르고 쉬운 데이터베이스 솔루션|


위 3개는 테이블, 아래 3개는 데이터베이스에 해당한다.

**Entity와 Data Table**

**Entity**: Swift의 객체와 유사하며, Core Data에서 데이터 모델을 정의하는 단위.
**Data Table**: 관계형 데이터베이스(SQLite 등)에서 데이터를 저장하는 구조.

**차이점**: Entity는 **객체 지향적인 데이터 모델**, Data Table은 **관계형 데이터베이스의 물리적 저장 구조**.

**Swift에서 함께 사용**: Core Data는 Entity를 자동으로 SQLite의 테이블로 변환하여 저장.

Core Data에서 DataModel을 생성하여 Entity를 추가함으로써 기존에 class로 만든 model을 대체하여 사용할 수 있다.

Entity - Attribute - 우측 Inspectors에서 Class - Module을 “Current Product Module”로 바꿔주지 않으면 멀티 스레딩이 필요한 경우 에러가 발생할 수 있다.


작은 데이터(Ex. 볼륨 on/off)를 저장할 때는 UserDefault를 사용할 수 있지만 문자열 등의 데이터를 저장할 때는 NSCoder를 사용하는 것이 좋다.

### URLSession

`class URLSession: NSObject`
		`ㄴ> // Type이 아니라 NSObject를 상속받음.`

**URLSession**이란 ?
- 네트워크 통신을 위한 기본 API
- HTTP/HTTPS 네트워크 요청, 파일 다운로드/업로드, 백그라운드 작업 등을 수행
- 비동기 처리 (비동기 콜백 기반으로 네트워크 작업 완료 시점 알림)

**핵심 역할**

| 기능                      | 설명                                    |
| ----------------------- | ------------------------------------- |
| 데이터 요청 (Data Task)      | 서버에서 JSON, XML, 텍스트 등 데이터를 요청하고 응답 받기 |
| 파일 다운로드 (Download Task) | 대용량 파일 다운로드                           |
| 파일 업로드 (Upload Task)    | 파일을 서버로 업로드                           |
| 백그라운드 작업                | 앱이 백그라운드 상태에서도 네트워크 작업 지속             |

**주요 클래스 & 프로토콜**

| 클래스/프로토콜                     | 설명                           |
| ---------------------------- | ---------------------------- |
| `URLSession`                 | 네트워크 요청을 수행하는 클래스 (핵심)       |
| `URLSessionConfiguration`    | 세션의 동작 방식 정의 (기본, 임시, 백그라운드) |
| `URLSessionDataTask`         | 데이터 요청을 위한 작업                |
| `URLSessionDownloadTask`     | 파일 다운로드 작업                   |
| `URLSessionUploadTask`       | 파일 업로드 작업                    |
| `URLSessionDelegate`         | 세션의 이벤트를 처리 (인증, 리다이렉트 등)    |
| `URLSessionDataDelegate`     | 데이터 작업의 이벤트를 처리              |
| `URLSessionDownloadDelegate` | 다운로드 작업의 이벤트를 처리             |

### Binding(바인딩)
>**Binding이란 ?**
>- 상위뷰의 데이터를 하위 데이터로 연결해서 하위 뷰가 직접 상위 뷰의 데이터를 읽고 쓸 수 있게 해주는 **연결 통로**.
>	
>- 하위 뷰에서 상위 뷰의 데이터를 직접 조작하고 싶을 때 사용

**Binding 전달 방법**
	`@State`로 선언한 변수를 `$`를 붙이면, `@Binding`형태로 변환돼서 전달된다.
	하위 뷰에서는 `@Binding`을 통해서 불러온다.

```
struct MainView: View {
	@State var buttonIndex: Int // 메인 뷰가 가진 데이터

	var body: some View {
		ButtonView(index: $buttonIndex) // $ 붙이면 원본을 참조해서 넘긴다
	}
}

struct ButtonView? View {
	@Binding buttonIndex: Int

	var body: some View {
		Button(action: {
			self.buttonIndex += 1
		}, label: {
			// 버튼 UI정보...
		}
	}
}
```

**Binding은 원본의 데이터가 가리키는 동일한 메모리 주소를 가리켜 값을 참조한다고 보면 된다.**


### 열거형(Enumeration)
**열거형이란 ?**
- 같은 주제로 **연관된 데이터들**을 멤버로 구성하여 나타내는 **자료형**

하나의 주제에 일일이 값을 입력하여 넣어야 할 경우, 오타가 생길 가능성과 성능 향상을 기대하기 위해 **"정해놓은 입력 값"** 만 선택해서 받고 싶을 때 사용하는 자료형이다.

**어떻게 성능 향상을 기대할 수 있을까 ?**
String은 Heap에 저장되는 데에 반해, 열거형은 Stack에 저장되어 성능면에서 장점이 있다.

#### 열거형 정의하기
**원시값이 없는 열거형**
열거형 이름만 쓰고 선언해주면, 원시값이 없는 열거형이다.

```
enum CalculatorOperator {
	case add
	case substract
	case multiply
	case divide
}
```

---

**계산기 앱을 만든다고 가정해 보자.**

1. `Character Type`을 가지는 원시값이 있는 열거형

```
enum CalculatorOperator: Character {
	case add = "a"
	case substract = "b"
	case multiply = "c"
	case divide = "d"
}
```

`Number Type`을 가지는 경우 직접 **Raw Value**를 지정해주지 않아도 되지만,
`Character Type`을 가지는 경우 위 코드와 같이 **반드시!! 직접** **Raw Value**를 지정해주어야 한다.

2. `String Type`을 가지는 열거형.

```
enum CalculatorOperator: String {
	case add = "+"
	case substract = "-"
	case multiply                   // multiply
	case divide = "÷"
}
```

`String Type`을 가지는 열거형의 경우, **Raw Value**를 지정하지 않으면,
case 이름과 동일한 **Raw Value**가 자동으로 만들어진다.


---

**원시값이 있는 열거형에서 Raw Value에 접근하는 방법**

```
var operator1: CalculatorOperator = .add
var operator2: CalculatorOperator = .multiply

operator1                 // add
operator2                 // multiply

operator1.rawValue        // "+"
operator2.rawValue        // "x"
```

만약, **Raw Value**가 있는 열거형의 경우,
**Raw Value를 통해서도 열거형을 생성**할 수 있는데, 다음과 같은 생성자를 이용하면 된다.

```
var operator1 = CalculatorOperator(rawValue: "+")
var operator2 = CalculatorOperator(rawValue: "x")
```

만약, 없는 **Raw Value**값을 대입할 경우 반환되는 열거형은 **옵셔널 타입**이다.


### if let과 guard let의 차이

`if let`은 조건이 실패하면 다른 대체 로직을 실행할 수 있는 반면에,
`guard let`은 조건을 만족하지 않으면 `return`, `throw`, `fatalError()`등의 탈출 문이 필요하다.

`if let`은 값이 존재할 때만 특정 로직을 실행하는 경우에 적합.
`guard let`은 값이 없으면 더 이상 진행할 수 없는 경우에 적합.

### MVVM 아키텍처 패턴

#### MVVM이란 ?
앱을 3가지 주요 구성 요소로 나누어 관리하는 패턴이다.

**기존 MVC의 단점은 뭘까 ?**
- 일반적인 MVC 애플리케이션에서  많은  로직이 뷰 컨트롤러에 배치된다. 일부는 뷰 컨트롤러에 속하지만, 많은 로직은 MVVM 용어로 ' **프레젠테이션 로직** '이라고 한다. 모델의 값을 뷰가 표현할 수 있는 것으로 변환하는 것과 같은 것, 예를 들어 NSDate를 가져와서 포맷된 NSString으로 변환하는 것과 같은 것이다.

그래서 여기 **presentation logic**을 분리하기 위해 만들어진게 **view model**이다.

결과적으로
	**MVVM이란: MVC의 증강 버전으로, 뷰와 컨트롤러를 공식적으로 연결하고, 프레젠테이션 로직을 컨트롤러에서 꺼내 새로운 객체인 뷰 모델로 옮긴다."**

여기서 기존 **MVC**의 **Controller**와 **MVVM**의 **ViewModel**이 같은 기능을 하는거 아닐까? 라는 의문이 생길 수 있다.

But, IOS에서는 View와 Controller가 강하게 결합되어 있어 **M/V/C** 가 아닌 **M/VC** 라고 볼 수 있다.
**->** View와 Controller가 ViewController라는 거대한 몸을 가지고 있음..

그렇기 때문에, **MVVC** 패턴을 통해 기존 **ViewController**를 **View와** **ViewModel** 완전히 분리시키고 **VC**자체는 **View**의 역할만 하게 **ViewModel.swift** 식의 **ViewModel** 파일을 만들어 주는 것이다.

Contoller == ViewModel이 아닌, VC를 View, ViewModel 두 개로 나누어 준다고 생각하면 편하다.

다만 MVVM의 진가는 RXSwift를 사용할 때 발휘된다.


==**Model**==
- 데이터를 표현하는 구조체 또는 클래스
- 데이터를 저장 및 관리 (예: UserDefaults, Core Data, Firebase, API 요청 등)
- 비즈니스 로직을 일부 포함 (예: 단순 데이터 가공, 변환, 유효성 검사 등)
- 데이터 저장 및 관리하는데에 함수가 사용되지, 앱의 핵심 기능을 담은 로직을 동작시키는 코드는 포함시키지 않는다.

==**View**==
- UI 레이아웃과 사용자 인터페이스를 담당.
- 화면(UI)을 구성
- ViewModel에서 제공하는 데이터를 화면에 표시
- 버튼, 입력 필드 등의 사용자 인터랙션 처리

==**ViewModel**==
- Model과 View를 연결하며, 데이터 변환 및 **비즈니스 로직**을 수행.
- Model에서 데이터를 가져와서 View에 맞게 가공
- UI 업데이트를 위해 데이터 바인딩
- 버튼 클릭, 입력 이벤트 등의 로직 처리
- View가 Model을 직접 접근하지 못하게 중간 역할

**비즈니스 로직이란 ?**
애플리케이션이 수행해야 하는 핵심 기능 및 규칙을 정의하는 로직.
쉽게 말해, **이 앱이 어떤 원칙과 규칙에 따라 동작해야 하는가 ?** 를 결정하는 코드.

계산기 앱을 예로 들자면, 결과를 계산하는 로직이다.
다른 로직으로는 **UI로직(화면에 데이터 표시, 사용자 입력 처리)**, **데이터 로직(데이터를 저장하고 불러오는 로직)** 이 있다.

🔹 **비즈니스 로직을 어디에 넣어야 할까?**

| 비즈니스 로직                   | Model에 넣을까? | ViewModel에 넣을까? |
| ------------------------- | ----------- | --------------- |
| API 응답을 그대로 저장            | ✅ Model     | 🚫 No           |
| 서버 응답 가공 (ex. 날짜 변환)      | ✅ Model     | 🚫 No           |
| 사용자 입력 검증 (ex. 이메일 형식 체크) | 🚫 No       | ✅ ViewModel     |
| 특정 조건에 따른 데이터 필터링         | 🚫 No       | ✅ ViewModel     |
| 비즈니스 규칙 적용 (ex. 할인율 계산)   | 🚫 No       | ✅ ViewModel     |

**💡 결론:**  
👉 **단순한 데이터 변환/검증은 Model**  
👉 **UI에 관련된 데이터 가공/비즈니스 로직은 ViewModel**


다만, iOS/SwiftUI 커뮤니티에서는 다양한 MVVM 변형이 사용되며, 프로젝트의 복잡성과 팀의 선호도에 따라 적절한 구조를 선택할 수 있다.

**MVVM + ModelLogic**은 **"Model Logic"** 을 별도로 두어 비즈니스 로직을 재사용하고 테스트하기 쉬워진다.



### Override(재정의)


==**🔥 override 란?**==

`override`는 **부모 클래스의 메서드, 프로퍼티, 또는 서브스크립트를 재정의(override)할 때 사용하는 키워드**야. 즉, **상속된 기능을 변경하거나 확장**할 때 사용해.


#### ✅ 기본 개념

`class Parent {     func sayHello() {         print("Hello from Parent")     } }  class Child: Parent {     override func sayHello() {         print("Hello from Child")     } }`

##### 📌 설명

1. `Parent` 클래스의 `sayHello()`는 `"Hello from Parent"`를 출력.
    
2. `Child` 클래스에서 `override func sayHello()`를 사용해 재정의.
    
3. 이제 `Child` 인스턴스에서 `sayHello()`를 호출하면 `"Hello from Child"`가 출력됨.
    

---

#### 🔍 `override`의 사용 예시

#### 1️⃣ 메서드 오버라이딩

부모 클래스의 메서드를 재정의할 수 있어.

`class Animal {     func makeSound() {         print("Some generic animal sound")     } }  class Dog: Animal {     override func makeSound() {         print("Woof! Woof!")     } }  let myDog = Dog() myDog.makeSound()  // Woof! Woof!`

---

#### 2️⃣ 프로퍼티 오버라이딩

프로퍼티(변수)도 재정의 가능해.

`class Person {     var name: String {         return "Unknown"     } }  class Student: Person {     override var name: String {         return "Alice"     } }  let student = Student() print(student.name)  // "Alice"`

📌 `override var name`을 사용해서 부모의 `name` 값을 변경할 수 있어.

---

#### 3️⃣ Getter/Setter 오버라이딩

부모 클래스의 **computed property(계산된 프로퍼티)**도 재정의할 수 있어.

`class Rectangle {     var width: Double = 10     var height: Double = 5          var area: Double {         return width * height     } }  class Square: Rectangle {     override var area: Double {         return width * width     } }  let square = Square() square.width = 4 print(square.area)  // 16`

📌 부모의 `area`는 `width * height`였지만, `Square`에서는 `width * width`로 재정의.

---

#### 4️⃣ `super` 키워드와 함께 사용

부모의 기능을 유지하면서 추가 기능을 넣을 수도 있어.

`class Vehicle {     func move() {         print("Vehicle is moving")     } }  class Car: Vehicle {     override func move() {         super.move()  // 부모 클래스의 메서드 실행         print("Car is moving faster!")     } }  let myCar = Car() myCar.move() // 출력: // Vehicle is moving // Car is moving faster!`

📌 `super.move()`를 호출하면 **부모 클래스의 기능을 유지하면서 새로운 동작을 추가**할 수 있어.

---

#### 5️⃣ `override`가 필수적인 경우 (`required`)

부모 클래스에서 `required` 키워드를 사용하면 **서브클래스에서도 반드시 `override` 해야 해**.

`class Parent {     required init() {         print("Parent initializer")     } }  class Child: Parent {     required override init() {  // 부모의 required initializer 반드시 오버라이드해야 함         print("Child initializer")     } }`

📌 `required`가 있으면 **모든 자식 클래스는 반드시 `override`해야 해**.

---

#### 🚨 주의할 점

1. `override`는 **상속된 메서드/프로퍼티만 재정의 가능**  
    → 부모 클래스에 없던 새로운 메서드나 변수에는 `override`를 붙일 수 없음.
    
2. `final` 키워드가 붙은 메서드나 프로퍼티는 `override` 불가능
    
    `class Parent {     final func cannotOverride() { } }  class Child: Parent {     override func cannotOverride() { }  // ❌ 에러 발생! }`
    
3. `super`를 사용하면 **부모 클래스의 기능을 유지하면서 추가적인 동작을 구현 가능**
    

---

#### 🔥 결론

- `override`는 **부모 클래스의 메서드/프로퍼티를 재정의할 때 사용**
    
- `super`를 사용하면 부모 기능을 유지하면서 확장 가능
    
- `final`이 붙어 있으면 `override` 불가능


### Standard Font

`.headline` 등으로 폰트를 지정해주는 경우, 기기의 폰트 사이즈에 따라서 반응형으로 폰트 사이즈가 자동으로 조정된다.

### Navigation

네비게이션은 주로 두 가지 패러다임을 사용한다.

`NavigationStack`, `NavigationView(IOS 16이전)` 
- 계층적 화면 구조를 관리

`NavigationLink`
- 한 화면에서 다른 화면으로 이동하는 방법

`NavigationStack`은 루트 뷰의 화면 전체를 감싸고, 상단에 네비게이션 바를 표시한다.


#### NavigationLink로 화면 이동하기
```swift
NavigationStack {
    List {
        NavigationLink("상세 화면으로") {
            DetailView()
        }
    }
    .navigationTitle("메인 화면")
}

struct DetailView: View {
    var body: some View {
        Text("상세 화면입니다")
            .navigationTitle("상세 정보")
    }
}
```

**화면 간 데이터 전달하기**
swift

```swift
struct Item: Identifiable {
    let id = UUID()
    let name: String
}

struct ContentView: View {
    let items = [Item(name: "사과"), Item(name: "바나나")]
    
    var body: some View {
        NavigationStack {
            List(items) { item in
                NavigationLink(item.name) {
                    DetailView(item: item)
                }
            }
            .navigationTitle("과일 목록")
        }
    }
}

struct DetailView: View {
    let item: Item
    
    var body: some View {
        Text("\(item.name) 상세 정보")
            .navigationTitle(item.name)
    }
}
```

#### 프로그래밍 방식으로 네비게이션 제어하기

iOS 16부터는 `NavigationPath`를 사용해 프로그래밍 방식으로 네비게이션을 제어할 수 있습니다:

swift

```swift
struct ContentView: View {
    @State private var path = NavigationPath()
    
    var body: some View {
        NavigationStack(path: $path) {
            VStack {
                Button("두 번째 화면으로") {
                    path.append("두 번째")
                }
            }
            .navigationDestination(for: String.self) { text in
                Text(text)
                    .navigationTitle(text)
                Button("세 번째 화면으로") {
                    path.append("세 번째")
                }
            }
        }
    }
}
```


### Swift Data

Swift Data의 큰 틀 정리

1. **스키마 (Schema)**: 앱에서 사용할 데이터 구조에 대한 설계도
2. **모델 컨테이너 (Model Container)**: 설계도를 바탕으로 앱의 진입점에서 집을 짓는다.
3. **모델 컨텍스트 (Model Context)**: 만들어진 집 안에서 물건 (Data Model)을 넣고, 꺼내고, 지우고 왔다 갔다 하는 역할을 수행한다.
4. **쿼리 (Qeury)**: 집 안을 계속 들여다보면서 필요한 물건 (Data)을 가져오고, 물건이 바뀌면 새롭게 UI를 그리도록 알려준다.
5. 모델 컨테이너 (Model Container)가 지은 집에 담기는 물건은 앱의 **로컬 저장소 (DataBase)** 가 해당된다.

![[Pasted image 20250420141244.png]]

순서를 정리해 보자면,

`@Model`을 붙여 Class로 **스키마**를 정의 -> App 진입점에 모델 컨테이너 설정 -> 데이터를 추가(Create), 수정 (Update), 삭제 (Delete) 할 때는 모델 컨텍스트를 활용해서 수행 -> 데이터를 읽을 때 (Read)는 쿼리를 사용



### @ 속성래퍼

#### @StateObject
>SwiftUI에서 **뷰가 특정 객체의 생명주기를 직접 관리해야 할 때** 사용하는 속성 래퍼.

**초기화 시점**:

- 이 선언문이 평가될 때, SwiftUI는 뷰의 생명주기 동안 이 객체를 **생성**하고 유지한다.
    
- 즉, 해당 뷰가 처음 생성될 때 `ProfileSharingService`의 `init()` 메서드가 호출되어 객체가 초기화된다.

**동작 방식**:

- `@StateObject`는 뷰의 상태로서 관리되므로, 뷰가 다시 그려지더라도 같은 인스턴스를 유지한다.
    
- 만약 뷰가 화면에서 사라지거나 메모리에서 해제되면, 연관된 `ProfileSharingService` 객체도 함께 해제되고, `deinit`이 호출된다.

**사용 목적**:

- SwiftUI는 상태가 변경되면 뷰를 다시 그리는데,  
	이때 상태를 보존하려면 **객체의 생명주기를 직접 관리해야**한다.

- 이 방식은 뷰가 **ObservableObject**를 직접 생성하고 소유할 때 유용하다.
    
- 즉, 뷰가 해당 객체의 상태 변화에 반응하도록 할 수 있다.


**vs `@ObservedObject` 차이**

| 속성 래퍼             | 생명주기        | 누가 소유? | 언제 사용?                |
| ----------------- | ----------- | ------ | --------------------- |
| `@StateObject`    | SwiftUI가 관리 | 뷰 내부   | 객체를 **처음 생성**할 때      |
| `@ObservedObject` | 외부에서 관리     | 부모 뷰   | 이미 생성된 객체를 **전달**받을 때 |

### [[프로토콜 (Protocol)]]

### 제네릭(Generic)
>제네릭이란 타입에 의존하지 않는 범용 코드를 작성할 때 사용한다.
>제네릭을 사용하면 중복을 피하고, 코드를 유연하게 작성할 수 있다.

쉽게 말해서 타입을 미리 지정하지 않고 인자를 받아서,
실제 함수가 호출될 때 해당 매개변수의 타입으로 대체되는 Placeholder이다.
**어떤 타입이든 담을 수 있는 통!**

#### 제네릭 사용법

##### 1. 제네릭 함수(Generic Function)
``` swift
// 일반 함수
func printString(_ text: String) {
    print(text)
}

// 제네릭 함수
func printAnything<T>(_ value: T) {
    print(value)
}
```
**일반 함수**
- 오직 `String`만 출력 가능

**제네릭 함수**
- `String`, `Int`, `Bool`, `Double`, `내가 만든 타입` 뭐든 다 출력 가능

꺽새`< >`사이에 타입처럼 사용할 **임의의 이름**을 선언해주면,
그 뒤로 해당 이름을 타입처럼 사용할 수 있다.

위 코드에서는 `T`로 지정하였지만, 어떤 문자든 사용 가능하다.

일반적으로는 T를 많이 사용하는데 그 이유는 바로바로...
어떤 타입이 들어올 지 모르니까 **Type**의 이니셜을 따와서 대충 **T**라고 써두는 것.


> **어떤 상황에서 유용하게 쓸 수 있을까 ?**

**문자열을 스왑하는 함수를 만든다고 가정해보자.**

```swift
func swapTwoNumber (_ a: inout Int, _ b: inout Int) {
	let tempA = a
	a = b
	b = tempA
}
```

위와 같이 함수를 작성하면 잘 작동할 것 같아 보이지만...
인자로 `Int`타입이 아닌 `Double`이나 다른 타입을 받는 경우 해당 타입을 받는 함수를 각각 제작해줘야 한다...

이럴 때 **제네릭**을 유용하게 사용할 수 있다 !


``` swift
func swapTwoValues<T>(_ a: inout: T, _ b: inout T) {
	let tempA = a
	a = b
	b = tempA
}
```

무엇이든 담을 수 있는 제네릭 타입을 선언해주고`<T>` 해당 이름(`T`)을 타입이 들어가는 곳에 사용하면 된다.


##### 2. 제네릭 타입(Generic Type)
위에서 제네릭을 이용한 함수를 **제네릭 함수(Generic Function)** 이라고 하는데, 
제네릭은 함수에만 가능한 것이 아니라 `구조체`, `클래스`, `열거형`, 타입에도 선언할 수 있는데,
이것을 **제네릭 타입(Generic Type)** 이라고 한다.

>만약 **Stack**을 제네릭 타입으로 만들고 싶다면 ?

``` swift
struct Stack<T> {
	let items: [T] = []
	
	mutating func push(_ item: T) { ... }
	mutating func pop() -> T { ... }
}
```

이렇게 제네릭 타입으로 Stack을 선언할 수 있다.
(**클래스와** **열거형** 또한 가능하다 !)

> 제네릭 타입의 인스턴스를 생성할 땐 어떻게 해야할까 ?
``` swift
let stack1 = Stack<T> = .init()
let stack2 = Stack<T>.init()
```

제네릭 타입을 사용할 땐 선언과 마찬가지로 `<>`를 통해 타입을 명시해주면 된다.

그런데, 해당 방식은 어디서 많이 본 방식인데...
바로바로 배열 생성할 때와 같은 방식이다 !
``` swift
let array1: Array<Int> = .init()
let array2: Array<Int>.init()
```

**그 이유는 바로 Swift에서 Array가 제네릭 타입이기 때문이다 !**
``` swift
@frozen public struct Array<Element>
```


#### 제네릭과 프로토콜 ?

앞에서 설명했듯이, 제네릭은 아무 타입이나 받아와서 사용할 수 있다.

그런데 문제는, 아무 타입이나 받아오기 때문에 해당 타입이 무엇을 할 수 있는지 알 수가 없다는 것이다!

>예제를 통해 살펴보자.
``` swift
func decode<T>(_ data: Data) -> T {
    // ❌ T가 JSON을 디코딩할 수 있다는 보장이 없잖아?
    let decoded = try? JSONDecoder().decode(T.self, from: data)
    return decoded // 오류 발생
}
```

데이터를 받아와서 **디코딩**하는 함수이다.
하지만 **T**가 JSON을 디코딩할 수 있는 타입이라는 **보장이 없다!!**

그렇기 때문에 다음과 같이 프로토콜을 붙여 사용한다.
``` swift
func decode<T: Decodable>(_ data: Data) -> T? {
    return try? JSONDecoder().decode(T.self, from: data)
}
```

이렇게 하면 Swift는 **T**가 무조건 **Decodable**프로토콜을 따르는 타입이란걸 안다.
그렇기에, `decode()`함수는 T가 JSON을 디코딩할 수 있는 타입일 때만 쓸 수 있다 !

디코딩이 뭔지 헷갈린다면 ?
>[[인코딩&디코딩(Encoding&Decoding)]]

> **비유를 통해 더욱 간단하게 알아보자**

제네릭 T는 그냥 “아무 사람”이야.  
근데 어떤 함수는 “운전 가능한 사람”만 받는다고 해보자.

``` swift
func drive<T: 운전면허있는사람>(_ person: T) {
	person.운전하기()
}
```
이런 식으로 조건을 달아주는 것이다.  
즉,
> “**T는 아무나 받아도 되긴 한데, 운전할 수 있어야 해!**”

이런 조건을 건 것 !!


### Combine Framework
>비동기 이벤트를 핸들링할 수 있게 하는 Apple의 순정 Framework


**Combine**은 시간에 따른 비동기 이벤트들을 처리하는 Swift API를 제공한다.

콤바인은 시간에 따른 값을 제공할 수 있는 `Publishers`와 `Publishers`로부터 해당 값들을 받는 `Subscribers`로 정의된다.

>C3 파티 상세화면 ViewModel에 쓰인 combine 알아보기
``` swift
private func setupObservers() {
        // 에러 메시지 자동 숨김
        $showError
            .filter { $0 }
            .delay(for: .seconds(3), scheduler: DispatchQueue.main)
            .sink { [weak self] _ in
                self?.showError = false
                self?.errorMessage = nil
            }
            .store(in: &cancellables)
    }
```


``` swift
$showError
```
에러 발생 여부를 `@Published var showError: Bool`을 통해서 선언해둔다.
`$showError`는 `showError`의 변경을 감지하는 `Publisher`임.
즉, `showError`가 `true`나 `false`로 바뀌면 감지할 수 있다.

```
.filter { $0 }
```
`.filter { $0 }`는 `true`만 통과시킨다는 뜻이다.
즉, `showError == true`일 때만 그 다음 단계로 넘어간다.
`false`일 땐 무시.

```swift
.delay(for: .seconds(3), scheduler: DispatchQueue.main)
```
에러가 `true`되면 3초간 기다린다.
(3초동안 에러메시지를 보여주고 그 다음 코드에서 사라지게 하기 위해)

```swift
.sink { [weak self] _ in
	self?.showError = false
	self?.errorMessage = nil
}
```

3초가 지난 후 `showError`를 다시 `false`로 바꾸고,
`errorMessage`도 nil로 지운다.

```swift
.store(in: &cancellables)
```

이 구독을 `cancellables`에 저장해 둬서, 뷰모델이 사라질 때 자동으로 구독이 해제되게 한다.

`@Published`로 선언한 변수의 `$변수명`은 **Combine**에서 변경 사항을 감지하는 **Publisher**역할을 한다.
`sink`는 그 변화에 대해 반응하는 **Subscriber(구독자)** 역할이다.

`sink`, `assign`같은 **Combine** 구독 연산자를 사용할 때는 `store(in: &cancellables)`로 저장해 주어야 한다.

**& 기호가 무엇일까 ?**
>`&`는 Swift 함수에 변수를 직접 전달할 때,  
	그 변수의 "참조"를 넘긴다(inout)는 뜻이다.  
	→ 함수 내부에서 해당 변수에 값을 직접 저장할 수 있음.



**구독을 저장하지 않으면 ?**
- **Combine**이 내부적으로 강하게 참조해서 구독이 계속 살아있게 된다.
- 뷰모델이 사라져도 구독이 남아있게 되어, 결과적으로 메모리 누수가 발생한다.

`Set<AnyCancellable>`는 `deinit` 시점에 안에 있는 구독들을 **자동으로 cancel**해주기 때문에, 
별도로 신경 안 써도 돼서 편리하다.

>++ 별도로 구독을 저장하지 않아도 되는 경우**
	SwiftUI에서 `@Published`를 `View`에서 `@ObservedObject`, `@StateObject`로 자동 구독 할 때는 SwiftUI가 내부에서 알아서 해주기 때문에 store해주지 않아도 된다.



### ARKit
ARKit은 데이터 보안이 철저하게 구성되어있다.

카메라 프레임처럼 이런 센서로 얻은 데이터는 클라이언트 공간으로 절대 전송되지 않는다. 센서의 데이터는 대신 ARKit demon으로 전송되어 Apple의 알고리즘으로 안전하게 처리된다. 알고리즘으로 생성된 데이터는 큐레이션된 후 앱에서 데이터를 요청하는 클라이언트로 전달된다.


**ARKit에 접근하기 위한 선별조건**
1. 앱이 Full Space로 실행되어야 한다. (Shared Space로 실행되서는 X)
2. 일부 유형의 ARKit 데이터는 접근 권한을 요구한다.권한이 부여되지 않으면 해당 유형의 데이터는 앱에 전송되지 않는다.
	1. ARKit은 해당 작업이 편리하게 처리되도록 권한 설정 API를 제공한다.
	2. 접근하려는 유형의 데이터는 세션으로 권한 설정을 요청할 수 있다.
	3. 해당 작업을 실행하지 않으면 ARKit이 실행될 때 자동으로 권한 요청을 띄운다.