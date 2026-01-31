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


### 외적(Cross Product)
내적이 **두 벡터가 얼마나 비슷한가**를 묻는 것이었다면,
3D에서 외적은 **두 벡터가 만드는 새로운 공간의 축은 어디인가**를 찾아내는 연산이며 "$u \times v$"로 쓴다.
내적의 결과는 숫자(스칼라)이지만, 외적의 결과는 또 다른 벡터이다.

![[Pasted image 20260129180022.png]]

기하학적으로
- 크기는 평행사변형의 넓이와 같다.
- 방향은 두 벡터 모두에 직교(수직)한다.

**이 정의는 왜 3차원에서만 성립될까 ?**
2차원에서는 두 벡터가 평행을 이루어야만 두 벡터 모두에 직교할 수 있다.

**외적의 방향을 확인하는 방법**
![[Pasted image 20260131165002.png]]
[오른 손 법칙]

다만, 오른손 법칙은 코드 상에서 사용하기 어려우므로 손이 필요 없는 방법이 필요하다.

### 외적(Cross Product), 행렬식(Determinant), and Angle

$$\sqrt{det(u,v,u\times v)}=|u||v|sin(\theta)$$
[더욱 정확한 정의(손이 필요 없는)]
- $\theta$는 u와 v 사이의 각도
- "det"는 세 열 벡터의 행렬식
- 좌표 공식을 고유하게 결정한다
	- ![[Pasted image 20260131165713.png]]

![[Pasted image 20260131171308.png]]
원래 외적은 3차원에서 벡터를 반환하지만, 2차원에서도 $z$축이 있다 치고, 계산해서 나오는 숫자를 그냥 **2D 외적**이라고 퉁쳐서 부른다. 계산하거나 코딩할 때 간편하기에.
각도를 구하지 않고도(비싼 연산) 회전 방향과 좌우 위치를 확인하는 용도로 자주 사용된다.


### 90도 회전으로서의 외적
단위벡터 N과의 외적은 법선이 N인 평면에서의 90도 회전과 동일하다.
$$n \times u$$
평면 위 벡터를 90도 회전시키기 위한 목적이라면 복잡하게 회전 행렬을 사용하지  않고, 축과의 외적을 통해 간단하게 구할 수 있다.

![[Pasted image 20260131175729.png]]
위 질문에 대해서, $\theta$만큼 회전한 벡터 $\mathbf{u}'$를 구하는 공식은 다음과 같다.
$$\mathbf{u}' = \mathbf{u}(\cos \theta) + (\mathbf{N} \times \mathbf{u})(\sin \theta)$$

![[Pasted image 20260131180039.png]]
[공식이 성립되는 이유]

