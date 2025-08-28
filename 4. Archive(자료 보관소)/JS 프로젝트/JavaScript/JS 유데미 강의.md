
### 고차함수

**매개변수로 다른 함수를 받는 함수**
ex)

	function callTwice(func) {
		func( );
		func( );
	}

	function rolldie( ) {****************
		const roll = Math.floor(Math.random( ) * 10) +1
		console.log(roll);
	}

		맨 위 callTwice함수에 인수로 rolldie를 넣으면
		밑에 func가 rolldie로 치환되어서 결국 rolldie( ); 가 되어
		rolldie 함수가 실행된다.

		하지만 func자리에 rolldie( )를 넣게되면 rolldie함수가
		실행된 채로 인수로 들어가기에 func가 rolldie함수의 결과값인
		랜덤한 숫자로 치환되어 숫자(); 라는 의미없는 식이 실행된다.



**반환함수**
함수를 반환하는 함수

ex)

	function makeBetweenFunc(min, max) {
		return function (num) {
			return num >= min && num <= max
		}
	}
	
	const isChild = makeBetweenFunc(0, 18);
	const isAdult = makeBetweenFunc(19, 64);
	const isSenior = makeBetweenFunc(65, 120);

### 렉시컬 범위

함수 안에 함수가 있는 구조. (재귀함수랑은 다른 개념.)

	   function bankrRobbery() {
		  const heroes = ['Spiderman', 'Wolverine', 'Black Panther', 'Batman']
		  function CryForHelp() {
			    for (let hero of heroes) {
				      console.log(`Help Me  ${hero.toUpperCase()}!!!!!`);
			    }
		  }
		  CryForHelp();
	   }

이처럼 굳이 따지자면 2중for문이랑 유사함.
가장 아래에서 두번 째 함수를 호출해주지 않으면 안에있는 함수는 동작 X

### 메서드
.toUppercase( ) 처럼 사용하는 걸 메서드라 부름.
모든 메서드는 함수로 이루어져있다.

메서드 만들기.

math.add( ) 로 작동하는 메서드를 만들고 싶다.
먼저 math라는 변수에 객체를 만들어준다.

const math = {
	add : function(x,y) {
		return x + y;
	},
	squre : function(num) {
		return num * num;
	}
}

원래라면 위에처럼 만들지만, 더 간단하게 만들어보자

const math = {
	**add(x,y)** {
		return x + y;
	},
	**squre(num)** {
		return num * num
	}
}

이처럼 function( )구문을 생략하고, 특성 이름으로 바로 만들 수 있음.

### this 키워드

this 키워드는 객체 내에서 쓰이면 해당 객체의 이름을 가리키지만, 밖에서 쓰이면 this는 window객체를 가리킴.

	const cat = {
	    name : '호두',
	    color : 'black',
		meow( ) {
			console.log(`${this.name}야~ 밥먹자~`)
		}
    }

### Try/Catch문

에러가 날 거 같은 구문을 Try로 감싸주면 에러가 났을 때 Catch로 감싼 구문을 실행시켜준다. ex)

	try {
		hello.toUpperCase( ); 
	} catch {
		console.log("ERROR!!!");
	}

### 화살표 함수

![[첨부 파일 소스/Image File 1/Pasted image 20240112204647.png]]
위 과정을통해 화살표 함수를 모두 한 줄로 만들 수 있다.

### setTimeout과 setInterval

setTimeout은 일정 시간 후에 한번만 실행하고,
setInterval은 일정 시간 간격으로 계속해서 실행함.
### 메서드
#### filter 메서드

요소로 구성된 배열에서 필터링을 하거나, 부분 집합을 모아 새 배열을 만드는 데 쓰임.

#### Every/Some 메서드

인수를 받아서 True/False를 반환
Every는 모든 인수가 True일 경우 True반환
Some은 최소 한 개의 인수만 True여도 True반환

#### Reduce 메서드

![[첨부 파일 소스/Image File 1/Pasted image 20240115165405.png]]
**배열의 모든 요소를 지나치면서 callback함수의 실행값을 누적하여 하나의 결과값을 반환.**

**Reduce함수로 최소값 구하기**
무작위 숫자가 있는 배열 RandomArr가 주어졌을 때,

RandomArr.Reduce((min,num) => {
	if (num < min) {
		return num
	}
	return min
})

**배열 arr1과 arr2의 합 구하기**
arr1.Reduce((acc, cur, index) => acc +=arr2[index], 0`<-초기값0` )

### this와 화살표 함수

this는 상위 환경의 this를 계승한다.
그렇기때문에 function 안에서 바로 화살표 함수를 통해 this를 사용 할 경우 상위 환경인 window의 this를 계승하게 된다.

알맞게 사용하기 위해선, 정석적으로 화살표 함수를 사용하지 않고 function으로 감싼 뒤 this를 사용해야 this가 있는 함수의 요소를 가리키게 된다.

ex)
const person = {
	name: 'Sekwang',
	**sayHi( ) => console.log(`Hi ${this.name})**
};
**이렇게 되면 window의 this를 가리킴**

const person = {
	name: 'Sekwang',
	**sayHi: function( ) {
		console.log(`Hi ${this.name}`)**
	}
};

## JavaScript 최신 기능들

### Spread 구문

배열을 인수로 넣어서 각각의 요소들을 사용하려고 할 때 앞에 . . . 을 넣어서 각 요소를 사용할 수 있다. EX) arr = [1,2,3,4,5,6,7,8]
FindMax.max(...arr) -> 8

**출력값이 분리돼서 나옴**
EX) console.log(...arr) -> 1 2 3 4 5 6 7 8
(문자에도 똑같이 적용)

**배열 합치기**
cats와 dogs의 배열이 주어졌을 때
allPets = [...cats, ...dogs, 'tiger']

**배열로 객체 만들기**
EX) const numDict = {...arr}
	ㄴ> {0:1, 1:2, 2:3 . . .}
index값이 Key값으로 들어감.

**areguments**
함수 내부 인수 자리에 arguements값을 넣으면 입력 값을 객체로 만들어줌
![[첨부 파일 소스/Image File 1/Pasted image 20240115130203.png]]

**객체 분해**
const {key값1, key값2, key값3} = 객체이름
 ㄴ> key = value 구조로 변수 생성해줌![[첨부 파일 소스/Image File 1/Pasted image 20240115130508.png]]

**구조 분해**
매개 변수 자리에 구조 분해를 이용하면 더욱 간결하게 작성할 수 있다.
EX) user 객체에서 이름 가져오는 코드 변환 과정

const fullName(user) {
	return `${user.firstName} ${user.lastName}`
} ----------------------------------------------

const fullName(user) {
	**const ({firstName, lastName}) = user;**
	return `${firstName} ${lastName}`
}----------------------------------------------

const fullName({**firstName, lastName}**) {
	return `{firstName} ${lastName}`
}

**filter같은 메서드에도 활용 가능.**
movies.filter( (movie) => movie.score > 90)
매개변수 자리에 구조분해를 이용하면
movies.filter(**{score} => score** > 90)

#### DOM
**DOM(문서 객체 모델)** : 웹 페이지(HTML이나 XML)의 콘텐츠 및 구조, 그리고 스타일 요를 구조화 시켜 표현하여 프로그래밍 언어가 해당 문서에 접근하여 읽고 조작할 수 있도록 API를 제공하는 일종의 인터페이스이다.

#### SELECTING (선택자)
- **getElementById** : ID 선택
- **getElementsByTagName** : 모든 태그 선택
- **getElementsByClassName** : 모든 클래스 선택

#### **querySelector**
(querySelectorAll : 요소 전부 선택)
하나의 선택자로 다 해결 가능
EX) document.querySelector('a[title="java"]')
    `a태그에 있는 java라는 이름의 title 선택`
1) 태그 : "태그"
2) .클래스: ".h2"
3) **#ID** : "#h3"
4) 복합 : "div span"

#### 계층이동 (메서드)
**1. parentElement(부모) / children(자식)**
- 계층간 부모,자식 관계로 이동 가능. 
- ex)버튼 클릭시 상위나 하위 코드 변형 가능

**2. nextSibling (다음)/ previousSibling(이전)**
- 같은 부모의 형제 객체 반환
- 공백이나 줄바꿈도 하나의 노드로 인식하므로 그런 노드가 필요한 게 아니라면 일반적으로는 nextElementSibling / previousElementSibling으로 사용하면 됨.

#### append / appendChild
- 문자나 이미지 삽입 가능.
- append는 문자로 삽입
- appendChild는 변수에 담아서 삽임
- **ex) appendChild를 통해 body에(위치는 변경 가능) 이미지 삽입하기**
	document.createElement('img')
	const newImg = document.createElement('img') 
	newImg.src = 'https://이미지링크~~~'
	document.body.appendChild(newImg)
- prepend로 맨 앞에 삽입도 가능.

#### remove()
- 원하는 부분을 지울 수 있음.
- **ex) remove를 통해 p태그에 있는 내용 지우기**
	const p = document.querySelector('p')
	p.remove(p)
- IE 지원 X (removeChild써야 함)

#### addEventListener
**변수.addEventListener('동작', ( ) => }
	~구현하고 싶은 기능~
	})

- click : 클릭 감지
- keydown : 키 눌렀을 때 인식
- keyup : 키에서 뗐을 때 인식
- submit : 버튼 클릭 인식
- change : 인풋에 값이 변경되고 다른 곳을 클릭하면 인식 
- input : 인풋에 값이 추가될 "때"마다 인식
e.key와 e.code의 차이
- key는 입력되는 값 ex.Shift
- code는 키보드에서의 실제 위치 ex.LeftShift

**preventDefaul**
- 기본 동작을 어떤 것으로 할 지 재설정
- form에서 기본 동작을 입력 값을 리스트로 만들게 바꿈.![[첨부 파일 소스/Image File 1/Pasted image 20240124153510.png]]

**일일이 querySelector로 가져오는 것 말고 간편하게 가져오는 법**![[첨부 파일 소스/Image File 1/Pasted image 20240125181256.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240125181316.png]]
- 이 방법은 querySelctor로 가져와서 변수로 저장하고 value값을 다시 가오는 거라면
![[첨부 파일 소스/Image File 1/Pasted image 20240125181650.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240125181419.png]]
- querySelector로 가져온 form에서 elements로 접근함으로써 더 간편하게 가져옴.

**이벤트 버블링**
이벤트 리스너가 계속해서 올라가면서 명령 실행.
![[첨부 파일 소스/Image File 1/Pasted image 20240126120243.png]]
이러한 구조에서 p태그와 button 둘 다 이벤트리스너가 걸려있을 때
버튼을 클릭하면 버튼에 걸린 이벤트와 p에 걸린 이벤트 둘 다 실행된다.

이렇게 이벤트가 버블링 되는 걸 막으려면 button의 이벤트 리스너에e.stopPropagation( )을 넣어주면 해결.

**이벤트 위임**
나중에 생성되는 값에 연산을 해야 할 때 사용. 
![[첨부 파일 소스/Image File 1/Pasted image 20240126123757.png]]
- e.target을 통해 e로 들어오는 값을 받아서 처리 가능
- &&연산자를 통해 왼쪽의 식이 거짓이면 오른쪽 식 연산 X 


## 점수 관리자 프로젝트

![[첨부 파일 소스/Image File 1/Pasted image 20240127172413.png]]

#### javaScript

**점수 올리기**
점수를 올릴 때 HTML내에 있는 수에 1씩 더하는게 아니라
자바스크립트 내에서 점수 변수를 지정하고, 점수를 올린 뒤에 HTML에 업로드한다. HTML은 표기만, 계산은 자바스크립트 내에서.
**==this 키워드 사용 할 때는 화살표 함수 사용 X !!!==**

**코드 리팩터링**
문제점 : 처음에 player1과 player2 모두 지정을 해서 업데이트 해줘서 코드가 길어지고 업데이트 함수가 player1 , player2 두 개가 존재함.
해결방안 : 
![[첨부 파일 소스/Image File 1/Pasted image 20240127173030.png]]player1과 player2 각각을 객체로 만들어줌

![[첨부 파일 소스/Image File 1/Pasted image 20240127173138.png]]
점수 업데이트 함수를 만들고 플레이어를 인자로 받아서 하나로 통합.

![[첨부 파일 소스/Image File 1/Pasted image 20240127173201.png]]
이벤트 리스너만 따로 하나씩 만들어줌.
#### bulma----
**select앞에 텍스트 붙이기**
![[첨부 파일 소스/Image File 1/Pasted image 20240127172339.png]]
- `<label for="playto" class="label is-large is-inline">Play to</label>`


## 비동기식 자바스크립트

비동기 : 자기가 준비 하는 동안 다른 함수 먼저 실행시킴 또는 자신이 실행되려면 미래에 있을 코드의 값이 필요한데, 필요한 값이 나올 때 까지 기다리고 있기.

자바스크립트는 기본적으로 싱글 스레드이기 때문에 하나의 한 가지 작업밖에 진행하지 못한다. 하지만 몇몇 함수는 비동기식 처리로 여러가지 작업을 동시에 할 수 있다.
자바스크립트의 대표적인 3가지 비동기 방식
- 콜백 함수 : 중첩되면 상당히 복잡함
- Promise : 콜백 헬을 보완한 함수
- async await : Promise를 편하게 사용할 수 있는 가장 최신 문법법

![[첨부 파일 소스/Image File 1/Pasted image 20240127194412.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240127194431.png]]

==**promises**==
- 값이나 오류에 대한 최종 약속.
- 비동기식으로 진행하다 보면 무수히 많은 콜백함수를 사용하여 코드가 복잡해지고 알아보기 어려워진다. 
- Promise를 사용하여 콜백함수를 사용하지 않고 비동기식 방식 사용 가능

**promise함수 만들기**
![[첨부 파일 소스/Image File 1/Pasted image 20240127205642.png]]
- promise 함수를 사용하면 성공 여부에 따라 resolved,rejected 둘 중 하나를 반환한다.

**promise함수 사용 방법**
![[첨부 파일 소스/Image File 1/Pasted image 20240127205840.png]]
- 위 식은 request라는 변수에 담아서 사용했지만 그대로 사용해도 됨됨

**promise함수 깔끔하게 줄이기**
![[첨부 파일 소스/Image File 1/Pasted image 20240127213027.png]]
- catch구문은 마지막에 하나만 넣어줘도 됨됨
![[첨부 파일 소스/Image File 1/Pasted image 20240128015134.png]]
- 이런 식으로 return 생략도 가능

**async await**
![[첨부 파일 소스/Image File 1/Pasted image 20240128022900.png]]
- **async** : function 앞에 붙여서 사용. async를 붙이면 해당 함수는 항상 promise반환.
- **await** : Promise가 처리될 때 까지 함수 실행을 기다리게 만듬 (promise값이 있어야 실행할 수 있으니까.) 그리고 promise가 처리되면 그 결과와 함께 실행이 재개된다. promise가 처리되길 기다리는 동안에는 엔진이 다른 작업을 할 수 있기 때문에 리소스 낭비 x
- 
- 비동기식 함수를 사용했을 떄 오류 처리 방법은 try...catch 구문을 사용하면 된다.

## AJAX
AJAX : **A**synchronous **J**avascript **A**nd **X**ml
- 비동기 통신
- 최근에는 xml이 아닌 Json을 의미하며 그대로 AJAX라 부른다.
- xhr객체나 fetch함수 axios라이브러리를 이용한 비동기 통신 방식 의미

API : **A**pplication **P**rograming **I**nterface
- 소프트웨어간 상호작용
- API자체는 웹과는 관련이 없지만, 웹 개발에서 말하는 API는 대부분 [WebAPI]를 의미한다.
- 
WebAPI : 웹, HTTP를 기반으로 하는 인터페이스.

JSON : **J**ava **S**cript **O**bject **N**otation
- 이름에 뜻이 JavaScript언어를 의미하는 것은 아님.
- JSON.parse를 통해서 사용하는 언어에 맞게 파싱(변환)해줌. 반대는 strigify

1. **XHR** : **X**ML **H**ttps **R**equest 
- AJAX 요청을 생성하는 JavaScript API
- 브라우저와 서버간의 네트워크 요청 전송 가능 
2. **fetch**
- Promise를 반환하는 API.
- Promise만으로는 웹 통신을 할 수 없으므로 그 통신을 도와주는 API 
3. **axios**
- fetch를 이용한 라이브러리. fetch보다 더욱 간편하고 기능이 많다.
- fetch와 똑같이 Promise를 반환.

## 프로토타입,클래스,OOP(객체지향 프로그래밍)

**프로토타입**
- 템플릿 객체와도 같다. 많은 메서드를 담고 있음.
- 같은 프로토타입을 갖고 있는 여러 객체를 만들 수 있고 복사 할 필요 없이 같은 메서드에 접근 가능. 즉, arr같이 많은 메서드를 담고있는 패키지(템플릿?)
- 이러한 프로토타입을 원하는대로 수정할 수 있음. (ex.Array .protorype으로 접근.)

**팩토리함수**
- 객체를 생성하여 반환하는 함수
- 생성자 함수와 유사한 역할을 하지만, 생성자 함수는 new 연산자를 사용하여 객체를 생성하고 초기화하고, 팩토리 함수는 함수 호출을 통해 객체 생성.

**생성자 함수**
- 유사한 객체를 여러 개 만들 때 사용.
- 생성자 함수도 일반 함수이다.
- 함수의 첫 글자는 대문자로 시작
- 반드시 'new' 연산자를 붙여 실행
- 팩토리 함수 처럼 고유의 복사본을 함수마다 생성하는 게 아니라, 프로토타입을만들고, 그 프로토타입에 개별의 값을 저장하는 시스템. 프로토타입으로 객체를 추가하고, 개별 객체에 접근할 수 있는 것이 장점.  

**클래스**
- 객체를 만드는 데에 가장 적합함
- 생성자 함수는 메서드를 함수 외부에서 따로 만들어줘야 하는데, 클래스는 내부에서 모두 가능하다. 

- 사용예시
	![[첨부 파일 소스/Image File 1/Pasted image 20240131140808.png]]

- extends(확장)과 super 키워드
	![[첨부 파일 소스/Image File 1/Pasted image 20240131145934.png]]


## 문법

**map 함수와 전개 연산자의 차이**
- [[map() 함수]]는 배열의 각 요소에 작업을 하여 새로운 배열을 만드는 데에 사용
- 전개 연산자는 기존의 배열을 펼쳐서 새로운 사용처에 적용할 때 사용


