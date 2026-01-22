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

작은 화살표로 무엇을 측정할 수 있을까 ? 벡터는 어떤 정보를 담고 있는가 ?

**기본적으로 벡터는 방향과 크기를 담고있다**.

예를 들어, 2D에서 벡터는 고정된 방향에 대해서 길이와 상대적인 각도름 담고 있다.

이걸 **극 좌표(polar coordinates)** 라고 부르는데, 우리가 일반적으로 흔히 볼 수 있는 데카르트 좌표와는 다른 좌표이다.

극 좌표에 대한 설명이 강의에는 포함되어 있지 않아 간단하게 설명해보겠다.

기존 데카르트 좌표계에서 (x, y)로 표현한다면 극 좌표계에서는 (r, $\theta$)로 표현한다.
여기서 r은 원점에서 기준축 방향으로 떨어진 거리이고, $\theta$는 기준축에서 반시계 방향으로 잰 각이라고 생각하면 된다.

![[Pasted image 20260122164358.png]]










 
