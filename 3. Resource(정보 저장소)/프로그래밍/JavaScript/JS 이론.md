### 배열
#### Array 생성
배열을 생성할 때 `fill([ ])`을 통해 2차원 배열을 생성하면 얕은 복사가 되어, 배열 안의 요소들이 모두 공유된다.
```
EX)
let tree = new Array(5).fill([])
tree[1].push(3)
console.log(tree) // [[3],[3],[3],[3],[3]]
```

이러한 문제를 방지하기 위해 `Array.from( )`을 통해 Array를 채워줘야 한다.
```
EX)
let tree = Array.from({length : n + 1}, () => Array())
tree[1].push(3)
console.log(tree) // [[ ],[3],[ ],[ ],[ ]]
```

#### ForEach
**배열 메서드**
**목적 :** 배열 요소마다 함수와 코드를 한 번씩 실행
**작동 방식 :** 각 요소마다 함수 실행
**아웃풋 :** 무언가를 반환하지 않고 함수를 한 번씩 적용해줌.

```
arr.forEach((e) => {
	if (e/2 === 0) {
	console.log(e)
	}
})
```
for of 나온 뒤로 요즘은 자주 사용 X 

#### Map
**배열 메서드**
**목적 :** 기존 배열을 통해 새로운 배열 생성
**작동 방식:** 각 요소마다 콜백함수를 적용해서 새로운 배열에 추가
**아웃풋** : 요소마다 콜백함수가 실행된 새로운 배열

`arr.map((e) => e * 2)`
각 요소마다 2씩 곱한 값들로 이루어진 새로운 배열 생성 (원본 배열 영향X)

#### Filter
**배열 메서드**
**목적 :** 기존 배열에서 조건에 부합하는 요소만 남겨둠
**작동 방식 :** 각 요소마다 연산을 해서 조건에 맞으면 새로운 배열에 추가
**아웃풋 :** 기존 배열에서 조건에 부합한 요소들로 이루어진 새로운 배열

`arr.filter((e) => e > 5)`
5보다 큰 요소들로 이루어진 새로운 배열 생성 (원본 배열 영향X)
`filter`를 사용할 때 => 이후에 `중괄호{ }`가 포함되면 return을 통해 반환해야 하고, return이 없으면 인수가 자동으로 반환된다.
EX.
```
test = [1,2,3,4,5]

// {} 가 없는 경우
const testResult = test.filter((num) => num > 2)

console.log(testResult) // [3, 4, 5]

// {}를 사용했는데 return이 없는 경우
const testResult = test.filter((num) => {
	num > 2
})

console.log(testResult) // []

//{}를 사용하고 return을 통해 반환하는 경우
const testResult = test.filter((num) => {
	if (num > 2) {
		return num
	}
})

console.log(testResult) // [3, 4, 5]

```

#### Reduce
**배열 메서드**
**목적 :** reduce(줄이다)의 뜻처럼 배열을 순회하면서 하나씩 줄여나가 하나의 값만 반환하는 함수. 가장 큰 값 찾기, 배열 총 합 구하기 등 가능
**작동 방식 :** 배열을 순회하면서 각 요소의 값이 currentValue로 들어가고 return한 값을 accumualtor에 저장
**아웃풋 :** 최종 accumulator값 하나.

```
arr.reduce((accumulator, currentValue) => {
	return accumulator + currentValue
})
```
**(총합을 구하는 reduce메서드 사용법)**

각 요소를 순회할 때마다 return의 값이 accumulator에 순차적으로 저장되고, 각 요소는 currentValue에 들어가서 연산을 진행함.
```
arr.reduce((maxNum, num) => {
	if (num >= maxNum) {
		return num
	}
	return maxNum
})
```
(최대값 구하기)

#### Sort
**Array.sort()**
**목적** : 배열을 오름차순으로 정렬한다.
**작동 방식** : 요소를 문자열로 변환해 유니코드 코드 포인트가 낮은 순으로 정렬한다. 때문에 숫자 정렬에는 정렬 순서를 정의하는 비교 함수를 인수로 전달해야 한다.
**아웃풋** : 정렬된 배열 (기존 배열 변환)

숫자 배열을 정렬하기 위해선 **정렬 순서를 정의하는 비교 함수를 인수로 전달**해야 한다. 비교 함수는 양수나 음수 또는 0을 반환해야 한다.
**비교 함수**
비교 함수의 반환값이 0보다 작으면 첫 번째 인수를 우선하여 정렬하고, 0이면 정렬하지 않으며, 0보다 크면 두 번째 인수를 우선하여 정렬한다.
다음 예시를 통해 살펴보자

```
let nums = [5,1,2,4,3]
nums.sort((a,b) => a-b)
console.log(nums)  => [1,2,3,4,5]
```

하지만 인덱스값과 값을 각각 담은 이중 배열의 경우에, 숫자가 큰 순으로 정렬하되 숫자가 같은 경우 인덱스에 따라 오름차순으로 싶은 경우도 있을 것이다.
그럴 때 비교 함수의 반환값이 0일 경우 반환을 하지 않는 점을 이용하면 된다.

```
let rank = [[1,79], [2,0], [3,92], [4,82], [5,0]]
rank.sort((a,b) => b[1] - a[1] || a[0] - b[0])
console.log(rank) => [[3,92], [4,82], [1,79], [2,0], [5,0]]
```
이처럼 배열의 1번째 인수끼리 비교하는 값이 같은 경우 0번째 인수로 비교할 수 있다.

#### Every/Some 메서드

인수를 받아서 True/False를 반환
Every는 모든 인수가 True일 경우 True반환
Some은 최소 한 개의 인수만 True여도 True반환

---

#### Array.from()
**Array.from()**
`목적` : 배열을 순회
`작동 방식` : 인수로 들어온 배열의 요소들을 순회하면서 해당 요소에 함수를 실행한다.
`아웃풋` : 순회를 마친 요소들을 반환한다.

```
console.log(Array.from('foo'));
// Expected output: Array ["f", "o", "o"]

console.log(Array.from([1, 2, 3], (x) => x + x));
// Expected output: Array [2, 4, 6]
```

**구문**
```
Array.from(arrayLike)
Array.from(arrayLike, mapFn)
Array.from(arrayLike, mapFn, thisArg)
```

**매개변수**
[`arrayLike`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/from#arraylike)
배열로 변환할 순회 가능 또는 유사 배열 객체.

[`mapFn`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/from#mapfn)(Optional)
배열의 모든 요소에 대해 호출할 함수이다. 이 함수를 제공하면 배열에 추가할 모든 값이 이 함수를 통해 먼저 전달되고, `mapFn`의 반환 값이 대신 배열에 추가된다. 이 함수는 다음 인수를 사용하여 호출됩니다.

[`element`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/from#element)
배열에서 처리 중인 현재 요소.

[`index`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/from#index)
배열에서 처리 중인 현재 요소의 인덱스.

[`thisArg`](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/from#thisarg)Optional

`mapFn` 실행 시에 `this`로 사용할 값이다.

#### Rest 매개변수
함수의 인자위치에 들어가서 값의 개수와 상관없이 인자로 받게 해줌.
```
function sumAll(...nums) {
	return nums.reduce((total, element) => total + element)
}
```
이렇게 하면 sumAll함수에 sumAll(1,2,3,4,5) 처럼 인자의 개수를 원하는 만큼 넣을 수 있고, 인자에 배열 메서드를 사용할 수 있게 만들어준다.

#### 배열 분해
배열 값 편하게 꺼내오기
```
const scores = [20,14,10,7]
const [gold, silver] = scores
```
이러면 `const gold = score[0]`처럼 번거롭게 하지 않고,
gold는 scores배열의 첫 번째 값을 가지고, silver는 두 번째 값을 가진다.

#### 객체 분해
객체 값 편하게 꺼내오기
```
const james = {
	age : 30,
	city: "NewYork"
}
const {city} = james
```
city 변수에 james.city를 할당.
`const {city : jamesHome} = james` 
변수명 할당도 가능.

#### 구조 분해
함수의 매개변수에 객체분해 적용
```
movies.map({title, score, year}) => {
	return ${title} (${year}) is rated ${score}
}
```
movie를 element로 놓고 movie.title movie.year 이렇게 일일이 작성하는 것 보다 코드 간결화 가능.

#### 배열의 복사
배열을 변수에 할당할 때, 변수를 변경시에 원본 배열에 영향을 가지않게 하려면 얕은 복사와 깊은 복사를 활용해야 한다.
`얕은 복사` : 배열이 1차원 배열일 때 사용.
```
let copiedArray = arr.slice() // 또는 [...arr]
```

`깊은 복사` : 배열이 중첩된 배열일 때 사용.
```
let copiedArray = JSON.parse(JSON.stringify(arr))
```




### 객체
#### Map객체

##### 인스턴스 메서드

- `set(key, value)`: 지정한 키와 값의 쌍을 맵에 추가합니다. 만약 키가 이미 존재하면, 해당 키의 값을 업데이트합니다.
- `get(key)`: 지정한 키에 해당하는 값을 반환합니다. 만약 키가 존재하지 않으면 `undefined`를 반환합니다.
- `has(key)`: 지정한 키가 맵에 존재하면 `true`, 그렇지 않으면 `false`를 반환합니다.
- `delete(key)`: 지정한 키와 해당 값을 맵에서 제거합니다. 성공하면 `true`, 키가 존재하지 않으면 `false`를 반환합니다.
- `clear()`: 맵의 모든 키-값 쌍을 제거합니다.
- `size`: 맵에 있는 키-값 쌍의 개수를 반환합니다.

##### 반복 메서드

- `keys()`: 맵 객체의 각 키를 포함하는 새로운 Iterator 객체를 반환합니다.
- `values()`: 맵 객체의 각 값을 포함하는 새로운 Iterator 객체를 반환합니다.
- `entries()`: 맵 객체의 각 [키, 값] 쌍을 포함하는 새로운 Iterator 객체를 반환합니다. 기본적으로 `for...of` 루프와 함께 사용됩니다.
- `forEach(callbackFn, thisArg)`: 맵 객체의 각 키-값 쌍에 대해 지정한 함수를 한 번씩 실행합니다. `thisArg`는 `callbackFn`을 실행할 때 `this`로 사용할 값을 지정합니다.

##### 사용 예시
```
const myMap = new Map();

// set
myMap.set('key1', 'value1');
myMap.set('key2', 'value2');

// get
console.log(myMap.get('key1')); // 'value1'

// has
console.log(myMap.has('key2')); // true
console.log(myMap.has('key3')); // false

// delete
myMap.delete('key1');
console.log(myMap.has('key1')); // false

// size
console.log(myMap.size); // 1

// clear
myMap.clear();
console.log(myMap.size); // 0

// keys, values, entries
myMap.set('a', 1);
myMap.set('b', 2);
myMap.set('c', 3);

for (let key of myMap.keys()) {
    console.log(key); // 'a', 'b', 'c'
}

for (let value of myMap.values()) {
    console.log(value); // 1, 2, 3
}

for (let [key, value] of myMap.entries()) {
    console.log(key, value); // 'a' 1, 'b' 2, 'c' 3
}

// forEach
myMap.forEach((value, key) => {
    console.log(key, value); // 'a' 1, 'b' 2, 'c' 3
});

```

### 비동기
#### AJAX
**AJAX** (**A**synchronous **J**avaScript **A**nd **X**ML)
- 웹 페이지를 새로 고침하지 않고도 비동기적으로 서버와 데이터를 주고받을 수 있게 해주는 기술. => **비동기 통신**
- 이전에는 XML을 의미했지만, 최근에는 xml이 아닌 Json을 의미하며 명칭은 그대로 AJAX라고 부른다.
- xhr객체나 fetch, axios 등을 이용한 비동기 통신 방식을 의미한다.


다음은 AJAX를 구성하는 주요 기술들에 대한 설명.
- **JavaScript**
	- AJAX 요청을 생성하고, 서버 응답을 처리하는데 사용.
- **XML (Extensible Markup Language)**
	- 초기 AJAX 기술에서 데이터 교환 형식으로 주로 사용. 현재는 JSON이 주로 사용된다.
- **JSON (JavaScript Object Notation)**
	- 현재 AJAX에서 가장 널리 사용되는 데이터 교환 형식이다. 경량 데이터 형식으로, JavaScript와 호환성이 좋고, 읽기와 쓰기가 용이하다.
- **XMLHttpRequest 객체**
	-  AJAX의 핵심 객체로, 서버와 HTTP 요청을 주고 받을 수 있게 해준다.
- **이 외에도 Html과 Css가 사용된다.**
#### Call Stack
JavaScript Interpreter가 사용하는 매커니즘으로, 함수를 호출하는 스크립트(js파일)에서 해당 함수의 위치를 추적. 
![[첨부 파일 소스/Image File 1/Pasted image 20240523214733.png]]
예를 들어 위와 같은 함수가 있을 때 isRightTriangle 함수를 실행하면 연산에 필요한 square(a)의 값을 받아오기 위해 square 함수가 콜스택에 올라가고 multiply값을 구하기 위해 multiply가 콜스택에 올라간다.

#### Web API
JavaScript는 싱글스레드이기 때문에 한 번에 하나의 작업만 처리할 수 있다.
이런 직렬적인 구조의 단점을 보완하기 위해 비동기적 처리 방식을 진행하는데 대표적으로 사용되는 게 콜백함수이고 비동기적으로 처리하면 병렬적 처리가 가능해진다.

**비동기적 처리가 가능한 이유?**
자바스크립트는 싱글 스레드이지만 자바스크립트를 구성하는 소프트웨어인 브라우저가 멀티 스레드이기 때문이다. 때문에 비동기적 처리를 하는 과정에서도 비동기 처리가 필요한 부분만 웹에 넘겨서 처리를 맡기고 나머지 코드들은 싱글 스레드(직렬적)으로 처리가 된다.

`EX)` setTimeOut같은 webApi함수를 사용하면 시간이 걸리게 되는데 이러한 작업은 javascript가 하는 것이 아니라 브라우저에게 해달라고 작업을 넘겨놓고 javascript는 다른 작업을 수행하고 있는다. 그러다가 브라우저에서 작업이 끝나면 javascript로 넘겨주는 형식. (요리하면서 고기를 전자레인지에 돌려놓는다고 생각하면 됨.)

위와 같이 작동하는 Web Api코드 실행 방식처럼, CallBack을 통해서 같은 방식으로 원하는 함수가 돌아가게 할 수 있다.

#### Promise
어떤 연산, 비동기 연산이 최종적으로 완료 혹은 실패했는지 알려주는 객체
```
const fakeRequset = ((url) => {
	return new Promise((resolve, reject) => {
	const rand = Math.Random()
	setTimeOut(() => {
		if (rand > 0.7) {
			resolve("YOUR DATA !!")
	}
	reject("ERROR")
	}, 1000)
	})
})

fakeRequest("/dog/page1")
	.then((data) => {
		console.log("CONNECT PAGE 1 !", data)
	})
	.catch((err) => {
		console.log("FAIL CONNECT", err)
	})
```
기본적인 promise 코드 진행 방식
Promise를 직접 생성하지 않고 간결화 시킨 비동기 방식이 async/await이다.

#### Async/Await
>Async/Await은 기존 promise.then 문법에서 promise가 과도하게 체이닝 되어 복잡해 보이는 문제를 해결하기 위해 생긴 **문법적 설탕**(기능은 똑같지만 사용하기 편리한 것)이다. Class도 이에 해당함.

**async :** 함수를 선언할 때 함수 앞에 붙여 비동기로 선언하여 Promise를 반환시켜준다.
**await :** promise가 값을 반환할 때 까지 기다리기 위해 비동기 함수의 실행을 일시 정지시킨다.
`예를 들어 웹에서 로그인 하는 경우를 생각해보자. 홈페이지에 아이디와 비밀번호를 입력하고, 로그인 정보가 맞는지 확인한 후 로그인 해야 하는데 정보를 확인하는 과정을 기다리지 않고 그냥 로그인 해버리면 큰 문제가 발생한다 !!

**비동기 함수의 예외 처리 ?**
예외가 발생하는 경우에 무한하게 기다릴 수 없으므로, 예외 처리도 해주어야 한다.
이럴 때는 try/catch문을 꺼내와서 사용해준다.
```
async function makeTwoRequest() {
	try {
		let data1 = await fakeRequest('/page1')
		console.log(data1)
	} catch (e) {
		console.log("CAUGHT AN ERROR!")
		console.log("error is :", e)
	}
```
try 구문 안에 실행시킬 코드를 넣어주고 catch를 통해 에러를 잡아내기만 하면 된다 !


#### Axios
- **네이티브 함수가 아닌, JS 라이브러리로써 가장 선호하는 HTTP 요청 방법**
- [[JSON]] 데이터를 자동으로 변환해 주어 별도의 파싱 작업이 필요 없다.
- 클라이언트(브라우저)와 서버(Node.js)모두에서 사용 가능하다.
- 사용 예시:
```
// Axios 라이브러리 불러오기
const axios = require('axios'); // Node.js 환경에서
// 브라우저 환경에서는 <script> 태그를 통해 Axios를 불러올 수 있습니다.

// GET 요청
axios.get('https://api.example.com/data')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error('Error:', error);
  });

// POST 요청
axios.post('https://api.example.com/data', {
    key1: 'value1',
    key2: 'value2'
  })
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error('Error:', error);
  });

// 인터셉터 설정
axios.interceptors.request.use(config => {
  // 요청을 보내기 전에 작업 수행
  console.log('Request was sent');
  return config;
}, error => {
  // 요청 에러 처리
  return Promise.reject(error);
});

axios.interceptors.response.use(response => {
  // 응답 데이터를 가공
  console.log('Response received');
  return response;
}, error => {
  // 응답 에러 처리
  return Promise.reject(error);
});
```

**DadJoke API를 통한 사용방법**

![[첨부 파일 소스/Image File 1/Pasted image 20240624205501.png]]
API주소를 복사하여 Postman에 get요청을 보내 데이터를 확인한다.

![[첨부 파일 소스/Image File 1/Pasted image 20240624205537.png]]
html코드가 데이터로 나와 원하는 데이터가 어디에 있는지 알아보기가 힘들다.
원하는 정보를 찾기 위해서 헤더 탭에서 형식을 지정해주어야 한다.

 **API 에서 Header란 ?**
 API 요청에서 헤더(Headers)는 HTTP 요청이나 응답에서 부가적인 정보를 전달하는 역할을 한다. 헤더는 일반적으로 특정 데이터의 형식, 인증 정보, 세션 관리, 캐싱 제어 등 다양한 목적으로 사용된다.
 
 대표적인 헤더 몇 가지를 알아보자.
**Content-Type**
- 요청 또는 응답의 본문 데이터 형식을 정의한다.
**Authorization** 
- 보안을 위해 인증 토큰 전달.
**Accept**
- 서버가 반환해야 하는 응답의 데이터 형식을 지정.
**User-Agent**
- 클라이언트 애플리케이션의 정보를 전달.
**Cache-control**
- 캐시 정책을 지정.

여기서 우리가 사용해야 할 헤더는 Accept이고 JSON형식으로 이루어진 데이터만 확인하기 위해서 **Accept: application/json** 형식으로 사용한다.


![[첨부 파일 소스/Image File 1/Pasted image 20240624205627.png]]
Headers 탭에서 key: Accept(), Value : application/json 으로 다시 get요청을 한다.

![[첨부 파일 소스/Image File 1/Pasted image 20240624210826.png]]
JSON으로 이루어진 데이터만 나온다.

![[첨부 파일 소스/Image File 1/Pasted image 20240624210959.png]]
이제 JavaScript로 돌아가서 API를 불러오는 함수 axios에 해당 내용을 추가해준다.

![[첨부 파일 소스/Image File 1/Pasted image 20240624211104.png]]
확인해보면 정상적으로 출력이 되는 모습을 볼 수 있다.

#### Fetch API
- 네트워크 요청을 비동기 적으로 처리
- Promise를 반환하여 콜백 지옥(callback hell)을 피함.
- [[JSON]]을 따로 구문 분석해야 해서 약간 복잡하다.
- 사용 예시:
```
fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

#### XHR(XMLHttpRequest)
- Fetch API가 나오기 전에 사용하던, 구식 HTTP요청 방법
- 콜백을 사용하여 비동기적으로 동작하지만, 콜백 지옥에 빠질 수 있음.
- XHR을 사용한 Http 요청 방식이 AJAX이다.
- 사용 예시:
```
var xhr = new XMLHttpRequest();
xhr.open('GET', 'https://api.example.com/data', true);
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status === 200) {
    var data = JSON.parse(xhr.responseText);
    console.log(data);
  }
};
xhr.send();
```

**Axios - Fetch - XHR 순으로 출시 되었고, 가장 최근에 나온 Axios가 가장 많이 사용되며 편리하다.**


### Prototype
**프로토타입이란 ?**
- 모든 Javascript 객체가 가지고 있는 속성으로, **객체의 원형(prototype object)**(= 넌 어디에서 왔니 ?) 을 가리키는 링크이다. 이 링크를 통해 객체는 다른 객체로부터 상속받은 매서드와 속성을 참조할 수 있다.

**`prototype`의 주요 개념**

1. **프로토타입 체인 (Prototype Chain)**:
    
    - JavaScript에서 모든 객체는 자신의 부모 역할을 하는 프로토타입 객체를 가진다.
    - 객체는 자신의 프로토타입 객체의 속성과 메서드를 상속받아 사용할 수 있다.
    - 이런 상속 구조를 통해 여러 객체 간에 코드를 재사용할 수 있고, 객체 지향 프로그래밍의 상속 개념을 구현할 수 있다.
2. **`__proto__` 속성**:
    
    - 모든 JavaScript 객체는 `__proto__` 속성을 가진다.
    - `__proto__` 속성은 객체를 생성할 때 사용된 생성자 함수의 `prototype` 속성을 가리킨다.
    - 예를 들어, 배열 객체 `myArray`가 있다면, `myArray.__proto__`는 `Array.prototype`을 가리킨다.
    - `__proto__`속성을 직접 건들일 일은 많지 않다.
1. **프로토타입 객체의 활용**:
    
    - 프로토타입 객체에 메서드나 속성을 추가하면, 해당 생성자 함수로부터 생성된 모든 객체가 이를 상속받는다.
    - 이를 통해 메모리 사용을 최적화하고, 코드 재사용성을 높일 수 있다.

우선 객체에 대해 헷갈리는 사람들이 있을 것이다.
키,값 쌍으로 이루어진 { } 이것만 객체가 아니라, (중괄호 `{}`로 이루어진 키-값 쌍 형식의 객체는 일반객체(plain object)라고 불린다.)
**자바스크립트에서 배열(Array)과 문자열(String)또한 모두 객체이다.**

배열은 **Array** 객체의 인스턴스이며, `Array.prototype`을 상속 받는다.
`Array.prototype`객체는 배열 메서드들을 정의하고 있어 우리가 array.map( )등의 메서드들을 마음 껏 사용할 수 있는 것이다.
MDN같은 사이트에서 보다시피 원래의 형식은 array.prototype.map( )이지만 array.prototype을 상속받았기 때문에 바로 사용할 수 있는 것이다 !!

예를 들어 **Array.prototype.map()** 와 같이 동작하는 메서드를 직접 만들 수 있는데,
```
// sum기능을 하는 메서드 만들기
Array.prototype.sum = function() {
	return array.reduce((total,el) => total += el, 0)
}
const array = [1,2,3,4,5,6,7,8,9,10]
console.log(array.sum()) => `55`
```

하지만 직접 만들어서 사용할 수는 있지만, 그렇게 좋은 방법은 아니다.
함수로 만들어서 사용하는게 더 직관적이고 용이하다...
```
// 함수로 sum 기능 구현하기
const sum = (array) => {
	return array.reduce((total,el) => total += el, 0)
}
```

**프로토 타입 객체의 종류**

- **일반 객체(plain object)** 는 `{}`로 정의된 키-값 쌍을 가지는 객체이다.
- **배열(array)** 은 숫자 인덱스를 통해 접근 가능한 값들을 가지는 객체이다.
- **함수(function)** 는 호출 가능한 메서드와 프로퍼를 가질 수 있는 객체이다.
- **날짜(date)** 는 날짜와 시간을 표현하는 객체이다
- **문자열(string)** 은 원시 값이지만, 문자열 메서드를 호출할 때 `String`객체로 변환된다.

**요약**
- **모든 건 다 객체로 이루어져 있음.**
- **프로토타입 객체**는 해당 객체가 연결되어 있는 부모 객체를 의미한다.
	객체는 프로토타입 객체와 연결되어있어 여러 메서드들 과 속성을 상속받아 사용할 수 있다. 그 개념이 바로 **프로토타입 체인.**
- `__proto__`는 해당 객체가 가진 프로토타입 객체를 의미.
	예를 들어 배열 객체의 `__proto__`는 **Array.prototype**을 가리킨다.

*이처럼 자바스크립트에서는 모든 것이 객체로 다루어지며,
다양한 객체 타입들이 서로 다른 특성과 메서드들을 제공한다 !!*

### 객체 지향 프로그래밍


### etc...
#### 함수 선언
function함수 선언과 const 함수(함수 표현식)의 차이점
**function 함수 (함수 선언식)**
- **호이스팅** : 함수가 호이스팅 된다.
- **범위** : 전역 범위 또는 함수 범위 내에서 정의됨.

**const 함수 (함수 표현식)**
- **호이스팅** : 호이스팅되지 않는다
- **범위** : 함수가 선언된 블록 내부 내에서 정외된다. (블록스코프)

함수 선언식과 함수 표현식은 **var과 const의 차이**와 비슷하다.