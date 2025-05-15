## 행렬 고유값 구하기

**행렬의 고유값이란 ?**
- 정방 행렬 A를 선형 변환으로 봤을 때, 선형 변환 A에 의한 변환 결과가 자기 자신의 상수 배가 되는 0이 아닌 벡터를 고유벡터(eigenvector)라고 하고, 이 상수배 값을 고유값(eigenvalue)이라고 합니다. 고유값, 고유 벡터는 정방 행렬에 대해서만 정의됩니다. 다시 말해, 정방 행렬 A에 대해서 A**v** = λ**v**를 만족하는 0이 아닌 열벡터 **v**를 고유 벡터, 상수 λ를 고유값이라고 합니다.
- 고유값, 고유 벡터를 처음 접하시는 분들은 위 설명이 무슨 말인지 하나도 이해가 안 갈 겁니다. 저도 그랬습니다. 이제 차근차근 설명해보겠습니다.

"행렬 A를 선형 변환으로 봤을 때"부터 보겠습니다. 선형 변환은 쉽게 말해서 벡터에 사칙연산을 해주는 개념으로 보시면 됩니다. 위 식을 예로 들면, 열 벡터 **v**에 행렬 A를 곱하는 것을 '열 벡터 v에 선형 변환 A를 해주었다.'라고 말할 수 있습니다. 

그럼 A**v**라는 것은 **v**라는 열 벡터에 선형 변환 A를 해주었다는 뜻입니다. **v**라는 열 벡터에 선형 변환 A를 해준 결과가 열 벡터 **v**의 상수 배(λ)와 동일하다면, '선형 변환 A에 대하여 **v**는 고유 벡터, λ는 고유값이다'라고 한다는 뜻입니다.

그래도 이해가 잘 가지 않을 겁니다. 

A**v** = λ**v**이 만족한다는 것은 벡터 **v**에 대해 선형 변환 A를 해주었을 때, 벡터 **v**의 방향은 변하지 않고 크기만 변했다는 뜻입니다. 보통 어떤 벡터에 선형 변환을 하면 방향이 바뀝니다. 하지만 선형 변환을 했음에도 어떤 벡터 **v**의 방향이 바뀌지 않고 크기만 변했다면, 그리고 변한 크기가 원래 벡터 크기의 λ배라면 그 λ를 고유값이라고 하고 **v**는 고유 벡터라고 합니다.

'다시 말해, 어떠한 선형 변환 A를 했을 때, 그 크기만 변하고 방향이 변하지 않는 벡터가 있나요?'라고 묻는 질문에 '네! 있습니다!'라고 대답한다면 고유값과 고유벡터가 존재하는 겁니다.

아래 그림을 보겠습니다.

![](https://blog.kakaocdn.net/dn/H6gjc/btqBWqJnQld/A8QndROwnNGHk83bNZU601/img.png)

그림1 (출처: 공돌이의 수학정리노트 유튜브)

![](https://blog.kakaocdn.net/dn/bQEIJO/btqBYtEHulb/zUZO7qw9e4q3T0aNeG98vk/img.png)

그림2 (출처: 공돌이의 수학정리노트 유튜브)

그림2는 그림 1을 선형 변환한 겁니다. 벡터의 색상은 파란색, 분홍색, 빨간색 이렇게 총 3가지입니다. 먼저 빨간색 벡터를 봅시다. 그림 1의 빨간색 벡터에 선형 변환을 해주니 방향과 크기가 모두 변했습니다. 고유값, 고유벡터는 방향은 변하지 않고 크기만 변했을 때 정의할 수 있다고 했습니다. 따라서 빨간색 벡터는 고유 벡터가 아닙니다. 이제 파란색 벡터를 보겠습니다. 파란색 벡터는 선형 변환 후에도 방향은 변함없습니다. 다만 크기만 변했습니다. 이때 해당 선형 변환에 대하여 파란색 벡터는 고유 벡터이며, 고유값은 (그림 2의 파란색 벡터 크기 / 그림 1의 파란색 벡터 크기)만큼 입니다. 즉, 증가한 벡터 크기 비율만큼이 고유값입니다. 마지막으로 분홍색 벡터를 봅시다. 분홍색 벡터는 선형 변환 후 크기도 방향도 유지되었습니다. 따라서 분홍색 벡터도 고유 벡터이며, 고유값은 1입니다.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918121930.png]]
**고유값 구하는 식**

## 행렬의 종류

#### 전치 행렬(Transposed Matrix)

원래의 행렬에서 행과 열을 서로 맞바꾼 행렬을 전치 행렬이라고 합니다. 

![](https://blog.kakaocdn.net/dn/bG2YwM/btqBVeWWnRC/KDhbxYMxR7SlwGrsCM4AF1/img.jpg)

Truth in Engineering

전치 행렬은 다음과 같은 특징을 가집니다.

![](https://blog.kakaocdn.net/dn/bMlRFI/btqBUUqRZI2/CsRg3y4xI9iL8mB6QxfDlk/img.jpg)

Truth in Engineering

#### 단위 행렬(Identity Matrix)

주대각선의 성분이 모두 1이며 나머지 성분은 모두 0인 정사각행렬을 단위행렬이라고 합니다.

![](https://blog.kakaocdn.net/dn/cBJ0Vf/btqBVNdGmrl/m57K868G2MYwChD0CsVhNK/img.jpg)

Truth in Engineering

단위행렬은 아래와 같은 특징이 있습니다.

![](https://blog.kakaocdn.net/dn/OHtvu/btqBUzNYxSz/hkfFHNnAv6yiMedJSqDQEk/img.jpg)

Truth in Engineering

#### 역행렬(Inverse Matrix)

A와 어떤 행렬을 곱했을 때 결과가 단위행렬이라면, 이때 어떤 행렬을 A의 역행렬이라고 합니다.

![](https://blog.kakaocdn.net/dn/deHa6c/btqBWruHorK/a22CTm5PxLAl6xRMvyt9Kk/img.jpg)

Truth in Engineering

#### 직교 행렬(Orthogonal Matrix)

행렬 A와 A의 전치 행렬을 곱했을 때 단위 행렬이 된다면, A를 직교 행렬이라고 합니다.

![](https://blog.kakaocdn.net/dn/TSdqL/btqBXF6PlGG/GkPYEK2KQotESao5VK4okk/img.png)

출처: towardsdatascience

#### 대각 행렬(Diagonal Matrix)

대각 성분 이외의 모든 성분이 0인 행렬을 대각 행렬이라고 합니다. 아래는 대각 행렬의 예시입니다. 

![](https://blog.kakaocdn.net/dn/KsE28/btqBWCpdJto/PeWwzCATz6mzkri2YFVJT0/img.png)

출처: 위키백과

#### 정방 행렬(Square Matrix)

열과 행의 개수가 동일한 행렬을 정방 행렬이라고 합니다. n차 정방 행렬은 열과 행의 개수가 각각 n개인 행렬을 뜻합니다.

![](https://blog.kakaocdn.net/dn/AD3cy/btqBUUK89Cg/ZUHji8FDAcewYlKFLde7zK/img.jpg)

출처: rfriend.tistory

#### 대칭 행렬(Symmetric Matrix)

정사각행렬 A와 A의 전치 행렬이 서로 같다면, A를 대칭 행렬이라고 합니다.

![](https://blog.kakaocdn.net/dn/1xHcH/btqBUTZLeUt/o9WBSkv8nPwPbwOVjrSE61/img.png)

출처: rfriend.tistory
