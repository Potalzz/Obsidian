>This post is a personal study note based on CMU 15-462 (Computer Graphics) lectures.
>All original lecture slides and videos are copyrighted by the instructors.

강의에 대한 정보와 슬라이드 노트는 아래 홈페이지에서 확인할 수 있습니다.
https://15462.courses.cs.cmu.edu/fall2020/home

---

선형대수학은 그래픽 분야에서 다양한 문제를 공식화하기 위한 매우 강력한 추상화이다.

선형 대수학은 벡터 공간간의 선형 변환 대한 연구이다. 

벡터에 대한 정의와 기본적인 연산은 이전에 포스팅에 정리해두었다.
[공간 컴퓨팅에서의 수학(벡터)](https://medium.com/@tprhkd1607/visionos%EC%97%90%EC%84%9C%EB%8A%94-%EC%88%98%ED%95%99%EC%9D%B4-%EC%96%B4%EB%96%BB%EA%B2%8C-%ED%99%9C%EC%9A%A9%EB%90%A0%EA%B9%8C-7723c660d033)

벡터 공간은 모든 벡터 `u, v, w`와 스칼라에 대해 아래의 방식으로 동작한다.

- $\mathbf{u} + \mathbf{v} = \mathbf{v} + \mathbf{u}$
- $\mathbf{u} + (\mathbf{v} + \mathbf{w}) = (\mathbf{u} + \mathbf{v}) + \mathbf{w}$
- There exists a _zero vector_ "$\mathbf{0}$" such that $\mathbf{v} + \mathbf{0} = \mathbf{0} + \mathbf{v} = \mathbf{v}$
- For every $\mathbf{v}$ there is a vector "$-\mathbf{v}$" such that $\mathbf{v} + (-\mathbf{v}) = \mathbf{0}$
- $1\mathbf{v} = \mathbf{v}$
- $a(b\mathbf{v}) = (ab)\mathbf{v}$
- $a(\mathbf{u} + \mathbf{v}) = a\mathbf{u} + a\mathbf{v}$
- $(a + b)\mathbf{v} = a\mathbf{v} + b\mathbf{v}$

하지만 위 공식들은 강의에서 원하는 시작 방식이 아니다.
벡터 공간에 대해 말하고 싶은 모든 것들은 아주 자연스러운 곳에서 유래했다.
이것은 연구하기 매우 자연스러운 대상이며, 단순히 추상적인 수학적 대상이 아니다.

일련의 규칙 말고, 다른 관점에서 살표보자.
- **이 규칙들이 어디에서 유래되었는가 ?**
- **왜 유용하고 의미있는 것인가 ?**

> **단순히 정의가 무엇인지뿐만이 아니라, 왜 그 내용이 사실인지에 대해 생각해보자.**

**벡터에 대해 접해본 적이 없는 사람에게 벡터란 무엇인지 어떻게 설명할 것인가 ?**
아마 작은 화살표를 떠올릴 것이다.

**벡터는 어떤 정보를 담고 있는가 ?**

기본적으로 벡터는 **방향**과 **크기**를 담고있다.
이를 2차원에서 encode해보자면, 아래와 같이 표현할 수 있다.
*\*encode(벡터라는 추상적 대상을 특정 좌표계에 따라 숫자 형태로 표현)

![[Pasted image 20260122172125.png]]
크기는 길이 또는 반지름 r로 나타내고,
방향은 수평면과의 각도 $\theta$로 표현한다.

이걸 **극 좌표(polar coordinates)** 라고 부른다.(우리가 가장 흔히 보는 데카트르 좌표계와는 다르다)
극 좌표계에서는 r과 극축과 이루는 각 $\theta$의 순서쌍 $(r,\theta)$으로 나타난다.

여기서 의문이 들 수 있다.

**그래서 벡터는 어느 지점에서 뻗어 나오는건데 ?**

 선형대수에서 이야기할 때는 벡터는 서로 다른 기준점을 가지는 것이 아니라 모두 같은 공간의 **원점**을 기준으로 한다.
`(전통적으로, 벡터는 기준점을 포함하지 않는다. 기준점을 포함하는 벡터는 때때로 "tangent vector"라고 불린다.)`

위에서 얻은 데이터 r과 $\theta$를 사용할 때 유의해야 할 부분은, 하나의 좌표계에서 얻은 데이터를 **절대로 다른 좌표계에 적용해서는 안된다.**
이는 컴퓨터 그래픽에서 수 많은 버그를 유발하는 원인이며, (r, $\theta$)를 (x, y)로 변환하는 일련의 과정을 거쳐야한다.

극 좌표계에서의 값을 데카르트 좌표계에 적용하면 다른 벡터를 얻게 되므로 주의하자.

**데카르트 좌표계에서 벡터를 포현하면 아래와 같이 표현할 수 있다.**
![[Pasted image 20260122174137.png]]


**벡터가 무엇인지에 대해 알아봤으니, 벡터로 실제로 무엇을 할 수 있을까 ?**

기본적으로 두 가지 중류의 작업이 있다.

**1 - Addition**
![[Pasted image 20260122174423.png]]
위의 그림에서 보듯이, $u + v$의 의미는 u 방향으로 가다가 v방향으로 가라는 의미인데, 덧셈의 순서와 상관 없이 같은 결과가 나오므로 벡터의 덧셈은 **교환 법칙이 성립**된다는 사실을 알 수 있다.

$u + v = v + u$

**2 - Scaling**
![[Pasted image 20260122174839.png]]
벡터 u에 대해 스칼라 a배를 하고, 스칼라 b배를 해주던지, 스칼라 ab를 먼저 곱하고 벡터 u에 곱해주던지 결과가 같다는 사실을 알 수 있다.

$a(bu) = (ab)u$

벡터의 덧셈과 곱셉 두 가지에 대해 알아보았으니,
두 가지를 함께 적용해보자.
![[Pasted image 20260122175126.png]]
좌측과 같이 벡터를 먼저 더하고, 스칼라 곱을 적용하던,
우측과 같이 각각의 벡터에 스칼라 곱을 적용하고 두 벡터를 더하던 같은 결과가 나온다.

$a(u + v) = au + av$


이러한 기하학적 원리를 통해 위에서 나온 **벡터의 규칙**이 어떻게 성립되는지 이해할 수 있다.

- $\mathbf{u} + \mathbf{v} = \mathbf{v} + \mathbf{u}$
- $\mathbf{u} + (\mathbf{v} + \mathbf{w}) = (\mathbf{u} + \mathbf{v}) + \mathbf{w}$
- There exists a _zero vector_ "$\mathbf{0}$" such that $\mathbf{v} + \mathbf{0} = \mathbf{0} + \mathbf{v} = \mathbf{v}$
- For every $\mathbf{v}$ there is a vector "$-\mathbf{v}$" such that $\mathbf{v} + (-\mathbf{v}) = \mathbf{0}$
- $1\mathbf{v} = \mathbf{v}$
- $a(b\mathbf{v}) = (ab)\mathbf{v}$
- $a(\mathbf{u} + \mathbf{v}) = a\mathbf{u} + a\mathbf{v}$
- $(a + b)\mathbf{v} = a\mathbf{v} + b\mathbf{v}$


이러한 모든 속성을 만족하는 객체들의 집합을 **벡터 공간**이라고 부른다.

이러한 사소한 속성들을 그림을 그려 나가면서 이해하는 과정은 중요하다.
복잡한 규칙이나 물체가 나오면 **왜 저 규칙들이 맞는 걸까?** 라고 의문을 갖고 이해해나가는 습관을 가지자.

**벡터로서의 함수**
위에서 살펴 본 화살표와 함수는 똑같이 동작한다.

![[Pasted image 20260122180645.png]]
각각의 x에 대해서 f를 평가하고, g를 평가하여 결과를 취한다.

시각적으로 화살표처럼 보이지 않더라도 분명히 **함수는 벡터이다.**





















 
