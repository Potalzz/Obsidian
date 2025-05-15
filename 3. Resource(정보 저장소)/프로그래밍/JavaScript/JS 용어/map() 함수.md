**기존 배열을 통해 새로운 배열을 생성하는 함수**

![[첨부 파일 소스/Image File 1/Pasted image 20240318180544.png]]
- callback: 각 요소에 대해 실행할 함수로, currentValue, index, array 세 가지 매개변수를 받습니다.
    - currentValue: 현재 처리 중인 요소의 값입니다.
    - index (선택적): 현재 처리 중인 요소의 인덱스입니다.
    - array (선택적): map()을 호출한 배열 자체입니다.
- thisArg (선택적): callback 함수 내부에서 this로 사용할 값입니다.

map() 함수는 주어진 배열의 각 요소에 대해 callback 함수를 순차적으로 호출하고, 각 요소에 대한 callback 함수의 반환 값을 새로운 배열에 추가합니다. 이렇게 하여 새로운 배열이 만들어지고, map() 메서드는 이 새로운 배열을 반환합니다.

**예제)**
![[첨부 파일 소스/Image File 1/Pasted image 20240318180752.png]]

위의 예제에서, numbers 배열의 각 요소에 대해 새로운 배열 doubledNumbers를 생성합니다. 각 요소는 2배가 되어 새로운 배열에 추가됩니다.
