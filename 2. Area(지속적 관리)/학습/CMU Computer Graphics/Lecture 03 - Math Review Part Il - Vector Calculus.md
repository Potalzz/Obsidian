>This post is a personal study note based on CMU 15-462 (Computer Graphics) lectures.
>All original lecture slides and videos are copyrighted by the instructors.

강의에 대한 정보와 자료는 아래 홈페이지에서 확인할 수 있습니다.
https://15462.courses.cs.cmu.edu/fall2020/home

본 포스팅은 강의 내용을 바탕으로 하되, 이해를 돕기 위해 별도의 자료 조사와 개념 정리를 덧붙여 작성했습니다. 따라서 원 강의 내용과 100% 일치하지 않을 수 있으며, 개인적인 학습 내용이 포함되어 있습니다.

---

### Vector Calculus
> 벡터 미적분학은 spatial relationships, transformations 등을 이야기하기 위한 기본 언어이다.

현대 컴퓨터 그래픽스의 상당 부분이 편미분 방정식(PDEs)으로 공식화된다.


### 유클리드 노름(Euclidean Norm)
> 유클리드 노름은 공간의 회전/이동/반사에 의해 보존되는 길이의 개념.

정규 직교(orthonormal) 좌표계에서의 **유클리드 노름**
$$|u|:=\sqrt{u_{1}^{2}+\cdot\cdot\cdot+u_{n}^{2}}$$
**주의해야 할 부분**
위 표현식은 벡터가 정규 직교 기저로 인코딩되지 않는 한 기하학적 길이를 인코딩하지 않는다.
`(버그의 흔한 원인)`


### 유클리드 내적(Euclidean Inner Product / Dot Product)

![[Pasted image 20260129172436.png]]
n차원 벡터에 대해, 유클리드 내적은 다음과 같이 정의된다.
$$\langle u,v\rangle:=|u||v|cos(\theta)$$

정규 직교 데카르트 좌표계에서는 **점곱(dot product)** 을 통해 표현될 수 있다.
$$u\cdot v:=u_{1}v_{1}+\cdot\cdot\cdot+u_{n}v_{n}$$

**주의해야 할 부분**
유클리드 노름과 마찬가지로, 좌표가 정규 직교 기저에서 오지 않는 한 기하학적 의미가 없다.


