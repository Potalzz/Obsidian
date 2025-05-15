## (기초) 타이핑 랜딩 페이지
`fonts.google.com`에서 다양한 아이콘 무료로 사용 가능.

![[첨부 파일 소스/Image File 1/Pasted image 20240628182046.png]]
![[첨부 파일 소스/Image File 1/Pasted image 20240628182059.png]]
emit을 활용해 p태그 빠르게 생성하는 방법

```
.wrap {

  /*요소를 절대 위치에 배치*/
  position: absolute;

  /*상단 부모 요소의 50%아래에 배치*/
  top: 50%;

  /*왼쪽 부모요소의 50% 오른쪽에 배치*/
  left: 50%;

  /*요소를 자신의 너비와 높이의 50%만큼 왼쪽과 위로 이동*/
  transform: translate(-50%, -50%);

  color: white;

  text-align: center;
}
```

![[첨부 파일 소스/Image File 1/Pasted image 20240628193818.png]]


**CSS로 문자 마지막에 오는 인디케이터 만들기.**
```
//p태그에 있는 dynamic에 가상 요소 만들기.
#dynamic::after {

  // 가상 요소 생성에 필요. 빈 문자열을 사용하여 텍스트 추가 X
  content: "";

  display: block;
  position: absolute;
  top: 0;
  right: 0;
  
  // 너비 4px로 설정
  width: 4px;
  
  // 가상 요소 높이를 부모 요소의 높이와 동일하게 설정.
  height: 100%;
  
  background-color: white;
}
```
`가상요소`란 ? 
- HTML 요소 뒤에 추가되는 콘텐츠를 나타냄.

**인디케이터 깜빡이게 만들기**

우선 CSS에서 먼저 설정을 해준다.
```
//CSS

// dynamic에 active클래스가 달리면, display를 none으로 바꿔준다
#dynamic.active::after {
	display : none;
}
```

```
// JavaScript

// p태그를 자바스크립트로 가져온 뒤,
let target = document.querySelector("#dynamic");

// toggle을 통해 active클래스를 만들어줬다,지웠다 하는 함수 blink를 만든다.
const blink = () => {
  target.classList.toggle("active");
};

// 0.5초 단위로 blink가 실행되도록 한다.
setInterval(blink, 500);
```

**텍스트 한 자씩 타이핑하듯이 생성 반복하기**
```
// Javascript
let target = document.querySelector("#dynamic");

// 랜덤 텍스트 생성 함수

const randomString = () => {

  const stringArr = [
    "Learn to HTML",
    "Learn to Python",
    "Learn to Javascript",
    "Learn to Java",
  ];
  let selectString = stringArr[Math.floor(Math.random() * stringArr.length)];
  let selectStringArr = selectString.split("");
  return selectStringArr;
};

// 랜덤 배열을 받아서 target텍스트에 한 자씩 추가해주는 함수.
const dynamic = (stringArr) => {
  if (stringArr.length > 0) {
    target.textContent += stringArr.shift();

	setTimeout(() => {
      dynamic(stringArr);
    }, 80);
  } else {
    setTimeout(resetTyping, 3000);
  }
};

// 함수 입력이 끝나고 텍스트를 초기화함과 동시에, 텍스트 생성함수 소환
const resetTyping = () => {
  target.textContent = "";
  dynamic(randomString());
};

dynamic(randomString());

//커서 깜빡임 효과
const blink = () => {
  target.classList.toggle("active");
};

//0.6초에 한번씩 blink함수 실행
setInterval(blink, 600);
```

프로젝트를 시작하기 전에는 엄청 간단한 거라고 얕아봤지만, CSS지식이 많이 부족하다는 사실과, 코딩테스트에서 사용하던 Javascript와는 많이 다르다는 걸 깨달았다. **프로젝트를 많이 따라해보며 페이지를 만드는 감각을 키우자!!**
반복해서 하다보면 어느샌가 익숙해져 자연스럽게 제작할 수 있을 것이다.

## (기초) 3D Flip Button 만들기
**CSS에서 텍스트 수직 중앙 정렬하기**
`height: 100px;`
`line-height: 100px;`
(수평 중앙 정렬은 text-align효과)

**3D효과 주기**
`transform-style: preserve-3d;`
하위 요소들을 모두 3D 개체로 바꿔준다.

**원근감 생성**
`perspective: 1000px;`
3D처럼 볼 수 있는 카메라 생성함으로써 원근감 조절
*자식 태그(자신 제외)에 적용되므로 3D개체 부모 태그에 적용.*
![[첨부 파일 소스/Image File 1/Pasted image 20240701172158.png]]
px 크기는 카메라의 위치라고 생각하면 된다. (작으면 가깝고 크면 멀어짐)
가까이 가면 원근감이 크게 느껴지고, 멀리가면 원근감이 작게 느껴진다. 

대신 카메라가 멀리 있다고 요소들이 보이는 크기에는 영향을 미치지 않고 오직 원근감에만 영향을 미친다.

**3D 개체 이동**
```
.back {
  background-color: darkgoldenrod;
  height: 100px;
  transform: rotateX(90deg) translateZ(150px); //X축 30도회전, Z축으로 150px 이동 
}
```
`transform: rotateX(90deg) translateZ(150px)`
x축으로 90도 이동 후, Z축(위)로 150px 이동한다.

*위로 이동하는게 왜 Y축이 아니라 Z축인가 ?*
HTML에서는 X,Y,Z축이 공통 축으로 기준을 삼는 것이 아니라, 개체마다 개별 축을 부여받아서, 해당 개체가 X축으로 90도 회전하면 앞,뒤를 기준으로 삼던 Z축도 같이 회전해서 위 아래 기준을 담당하게 된다.
`예시 이미지 `
![[첨부 파일 소스/Image File 1/Pasted image 20240701174213.png]]

back태그를 90도 회전하고 위로 이동하여 front태그의 이미지 맨 위 모서리에 붙여준다. 사각형의 크기 100px중에 앞으로 50px 나와있으므로 front태그를 뒤로 50px 이동해준다. `transform: translateZ(50px);` 

**3D 개체 회전하기**
`front` 와 `back` 을 포함하고 있는 `flip-btn`태그에 가상클래스 `:hover`를 붙여서 마우스를 가져다대면 회전하게 만든다.
```
.flip-btn:hover {
  transform: rotateX(-90deg);
}
```
그리고 flip-btn에 마우스를 올리면 커서가 변경되는 효과를 주기 위해
flip-btn태그에 `cursor: pointer;`를 적용시켜준다.

이렇게만 하면, 상자가 0초만에 회전하여 순간이동한 것 처럼 보인다.
동작하는 시간을 만들어 주기 위해 flip-btn태그에 `transition: 0.5s;`를 붙여준다.

## Design House 웹 페이지 만들기
![[첨부 파일 소스/Image File 1/Pasted image 20240709162300.png]]
이미지 마스크 레이어로 깔기.
`height가 100%가 아니라 100vh인 이유는 ?`  height는 width와 달리 100%가 전체를 포함하려면 바디 태그에도 100%를 달아줘야 함.

```
margin : 0 auto
```
**요소 수평 기준 중앙으로 오게 만들기**
`margin-left : auto`와 `margin-right : auto` 를 각각 적용시켜줘야 하지만, `margin-top`과 `margin-bottom`이 0이여도 상관없이 때문에 전체 margin에 적용.

![[첨부 파일 소스/Image File 1/Pasted image 20240709164959.png]]
**버튼 디자인**

---

## 계산기 만들기
### HTML 구현하기
클릭해서 상호작용하기에 어울리는 태그는 `input`과 `button`이 있다.

input이 상호작용하기에 더 강한 느낌이 있으므로 `input으로 구성`해준다.

가장 먼저 `컨테이너 div`를 만들어 준다.
`input태그`는 `forms태그`와 같이 사용해야 하므로, forms태그를 만들어 준다.
가장 숫자들이 나오는 칸에는 `type = "text"`로 해주고, 
나머지는 클릭만 되면 되므로 `type = "button"`으로 만들어준다.
나중에 CSS에서 연산자 별로 색상을 추가해주기 위해 `class`도 넣어준다.
```
<!-- HTML 구성 -->
<div class="calculator">
      <form action="">
        <input type="text" name="output" readonly />
        <input type="button" class="clear" value="C" />
        <input type="button" class="operator" value="/" />
        <input type="button" value="1" />
        <input type="button" value="2" />
        <input type="button" value="3" />
        <input type="button" class="operator" value="*" />
        <input type="button" value="4" />
        <input type="button" value="5" />
        <input type="button" value="6" />
        <input type="button" class="operator" value="+" />
        <input type="button" value="7" />
        <input type="button" value="8" />
        <input type="button" value="9" />
        <input type="button" class="operator" value="-" />
        <input type="button" class="dot" value="." />
        <input type="button" value="0" />
        <input type="button" class="operator result" value="=" />
      </form>
    </div>
```

### CSS 구현하기
![[첨부 파일 소스/Image File 1/Pasted image 20240709192429.png]]
HTML만 적용한 모습은 이런 상태이다.

```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```
**가장 먼저 기본 CSS를 초기화 시켜준다.**
일렬로 된 요소들을 계산기 형식에 맞게 정렬해주어야 한다.

![[첨부 파일 소스/Image File 1/Pasted image 20240709193318.png]]
```
.calculator form {
  // grid 적용
  display: grid;
  // 열 4개에 한 열에 65px씩 공간을 만들어 준다.
  grid-template-columns: repeat(4, 65px);
  // 한 행당 65px씩 공간을 만들어준다.
  grid-auto-rows: 65px;
  // 행 끼리의 간격 5px
  row-gap: 5px;
  // 열 끼리의 간격 5px
  column-gap: 5px;
}
```
**`display: grid`를 사용해 원하는 행과 열로 구성해준다.**
적용하고 나면 위와 같이 `한 칸당 65px * 65px의  grid형태`로 배치된다.

![[첨부 파일 소스/Image File 1/Pasted image 20240709193515.png]]
```

body {
  background-color: darkslateblue;
  // flex를 통한 중앙정렬
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.calculator {
  width: 287px;
  background-color: aliceblue;
  border: 1px solid black;
  padding: 5px;
}
```
전체 body에 `display : flex`를 적용해 컨텐츠를 중앙에 배치하고,
container박스에 너비를 배정해주고 배경색상, 여백, 테두리를 깔아준다.

```
.calculator form input {
  border: 2px solid #333;
  color: rgb(24, 24, 24);
  font-size: 1rem;
}
```
모든 input요소들 스타일 조정

```
// Clear 클래스에 열 3칸 부여
.calculator form .clear {
  grid-column: span 3;
}
```
`grid - column`을 통해 여러개의 칸을 사용하는 요소들에게 칸을 만들어준다.

```
// 연산자 클래스를 가진 요소에 색상 부여
.calculator form .operator {
  background-color: orange;
}
```
HTML에서 요소마다 분리해뒀던 클래스를 통해 색상을 부여해준다.

```
.calculator form input[type="text"] {
  grid-column: span 4;
  text-align: right;
  padding: 0 10px;
}
```
결과 칸에는 text가 우측에서부터 시작되게 조정해준다. 

이후 `:hover` 효과를 넣어 마무리해준다.

#### 전체 CSS 코드
```
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: darkslateblue;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.calculator {
  width: 287px;
  background-color: aliceblue;
  border: 1px solid black;
  padding: 5px;
}

.calculator form {
  display: grid;
  grid-template-columns: repeat(4, 65px);
  grid-auto-rows: 65px;
  row-gap: 5px;
  column-gap: 5px;
}

.calculator form input {
  border: 2px solid #333;
  color: rgb(24, 24, 24);
  font-size: 1rem;
}

.calculator form input:hover {
  box-shadow: 1px 2px #acaaaa;
  color: rgb(0, 0, 0);
  cursor: pointer;
  font-size: 17px;
}

.calculator form .clear {
  background-color: #ed4848;
}

.calculator form .operator {
  background-color: orange;
}

.calculator form .dot {
  background-color: green;
}

.calculator form input[type="text"] {
  grid-column: span 4;
  text-align: right;
  padding: 0 10px;
}

.calculator form .clear {
  grid-column: span 3;
}

.calculator form .result {
  grid-column: span 2;
}
```

### JavaScript 작업
처음에는 당연하게 JS로 가져와서 DOM을 통해 작업해야 한다고 생각했지만, 생각보다 스크립트를 넣어줄 것들이 많지 않았고, HTML에서 매우 간단하게 구현이 되었다.

```
<input type="text" name="output" readonly />
```
우선, 결과가 나오는칸에 `name`을 할당해주고 텍스트를 입력할 수 없도록 `readonly`를 적용시켜준다. 

```
onclick="document.forms.output.value += '+'"
```
각 태그마다 onclick을 넣어주어  아까 넣어 주었던 `name = "output"`을 통해 value값에 각 버튼의 값을 추가시켜준다.
이렇게 모든 버튼 각각의 값에 맞춰 onclick을 넣어주고나면 연산하는 작업만 남게된다.
**연산하는 로직은 생각보다 매우매우 간단하다**

```
<input type="button" class="operator result" value="=" onclick="document.forms.output.value = eval(document.forms.output.value)" />
```
자바스크립트의 메서드 `eval()`이 입력된 값들이 각각의 역할에 맞춰 연산되도록 동작시켜준다.

### 프로젝트를 마치고
**가장 먼저 HTML로 어떻게 구현해야 할 지에 대해 익숙해질 필요가 있다!!**


## Button Design UI
### CSS
**body태그에서 `align-items : center`를 지정해도 중앙에 오지 않는 이유.**
높이값은 지정해주지않으면 없기 때문에 높이를 지정해줘야 중앙 정렬이 된다.
`height : 100vh` 추가

**before**가상 요소를 활용해 맨 앞부터 빨간 게이지가 차오르는 모션 만들어줌.

**가상 요소란 ?**
`content : ""`를 통해 `""`안의 콘텐츠를 지정된 요소에  추가하게 만들어준다.
위에서 사용한 `::before` 가상 요소는 지정된 요소의 콘텐츠 앞에 추가적인 콘텐츠를 삽입한다. 예를 들어 기호 `!`를 추가하고 싶은 경우 `content : "!"`이렇게 작성하면 된다. 다른 가상 요소로는 `::after(콘텐츠 뒤에 추가)` , `::first-line(첫 번째 줄에 스타일 적용)`, `::first-letter(첫 번째 글자에 스타일 적용)` 등이 있다.


## 3D Cube Banner
HTML에서는 먼저 작성된 태그가 아래 레이어에 위치한다.

`nth-of-child()`를 통해서 이미지 지정하고, 각도와 위치조정해준다. 

**스크립트 통해서 회전 넣어주기**
![[첨부 파일 소스/Image File 1/Pasted image 20240724183419.png]]
cube에 transition all 넣어주기.

## Card UI
![[첨부 파일 소스/Image File 1/Pasted image 20240729192931.png]]
마우스 hover하면 배경,로고 switching 되는 효과.

**배경 바꾸기**
![[첨부 파일 소스/Image File 1/Pasted image 20240729193100.png]]
`box-shadow` 사용하고, `transisition`을 통해 변경.

**로고 바꾸기**
![[첨부 파일 소스/Image File 1/Pasted image 20240729193155.png]]
`nth-of-type()`으로 로고 두 개의 스케일을 0과 1로 각각 바꿔줌.


## Full Screen Page
`width : 100vh, height : 100vh` 를 지정하면, 메인 화면에 꽉차게 크기가 설정된다.

## 그림판 만들기
**전체적인 과정**
이미지를 보고 사용할 HTML태그들을 추려 HTML을 작성한다.
CSS에서 이미지에 맞게 디자인 해준다.
JS로 넘어가서 DOM초기화를 먼저 진행해준다.
사용하는 `canvasAPI`를 공식문서에서 필요한 기능을 살펴보고 가져온다.
`addEventListener`를 통해 클릭별 기능을 함수로 만들어서 `event`데이터를 넘겨준다.

이러한 프로젝트들을 반복하면서 다음 능력을 기르자.
1. 구상한 이미지를 보고 **HTML 작성**하기.
2. 구상한 이미지대로 **CSS를 통해 디자인**하기
3. 구상한 기능을 **JS에서 구현**하기.**(공식문서 참조)**

그림판 만들기를 직접 다시 해보면서 과정을 정리하자.
