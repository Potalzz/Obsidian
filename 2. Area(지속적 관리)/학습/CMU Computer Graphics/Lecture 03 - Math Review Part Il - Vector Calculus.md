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

#### 왜 $u \times v = (u_1i, u2_j, u3_k) \times (v_1i, v_2j, v_3k)$식이 위의 수식이 될까 ?


**3차원 벡터 $u = (u_1, u_2, u_3)$는 사실 세 개의 화살표를 더한 것이다.**
- $x$축 방향 1칸: **$i$**
- $y$축 방향 1칸: **$j$**
- $z$축 방향 1칸: **$k$**


**따라서 벡터를 이렇게 풀어서 쓸 수 있다.**
$$u = u_1 i + u_2 j + u_3 k$$
$$v = v_1 i + v_2 j + v_3 k$$


**외적의 정의에 따라, 서로 직각인 축끼리 곱하면 다음과 같은 규칙이 생긴다.**
- **같은 축끼리 만나면 0이 된다.** (방향이 같으면 회전력이 안 생김)
    - $i \times i = 0$
    - $j \times j = 0$
    - $k \times k = 0$
      
- **다른 축끼리 만나면 나머지 하나가 된다.** (오른손 법칙 순서: $i \to j \to k \to i$)
    - $i \times j = k$
    - $j \times k = i$
    - $k \times i = j$
	
- **순서를 거꾸로 하면 마이너스(-)가 붙는다.**
    - $j \times i = -k$
    - $k \times j = -i$
    - $i \times k = -j$


**이제 두 벡터를 곱해보자.**
우리가 아는 곱셈 공식 $(a+b+c)(x+y+z)$ 처럼 하나씩 전개하면 총 9개의 항이 나온다.
$$u \times v = (u_1 i + u_2 j + u_3 k) \times (v_1 i + v_2 j + v_3 k)$$


**위 식을 전개해서, 위의 외적의 정의에 따른 규칙을 적용하면 다음과 같다.**
**같은 성분끼리의 곱 (3개 항) $\rightarrow$ 모두 0**
- $u_1 v_1 (i \times i) = 0$
- $u_2 v_2 (j \times j) = 0$
- $u_3 v_3 (k \times k) = 0$
- 결과: 0 $\rightarrow$ **모두 사라짐**

**$x$축($i$) 성분이 남는 경우**
- $u_2 j \times v_3 k = u_2 v_3 (j \times k) = u_2 v_3 (\mathbf{i})$
- $u_3 k \times v_2 j = u_3 v_2 (k \times j) = u_3 v_2 (\mathbf{-i})$
- 결과: $(u_2 v_3 - u_3 v_2) \mathbf{i}$ $\rightarrow$ **이게 공식의 첫 번째 줄**

**$y$축($j$) 성분이 남는 경우**
- $u_3 k \times v_1 i = u_3 v_1 (k \times i) = u_3 v_1 (\mathbf{j})$
- $u_1 i \times v_3 k = u_1 v_3 (i \times k) = u_1 v_3 (\mathbf{-j})$
- 결과: $(u_3 v_1 - u_1 v_3) \mathbf{j}$ $\rightarrow$ **이게 공식의 두 번째 줄.**

**$z$축($k$) 성분이 남는 경우**
- $u_1 i \times v_2 j = u_1 v_2 (i \times j) = u_1 v_2 (\mathbf{k})$
- $u_2 j \times v_1 i = u_2 v_1 (j \times i) = u_2 v_1 (\mathbf{-k})$
- 결과: $(u_1 v_2 - u_2 v_1) \mathbf{k}$ $\rightarrow$ **이게 공식의 세 번째 줄**

**결론**
이들을 모두 합쳐서 벡터 형태로 다시 쓰면 위의 공식이 나온다.
$$u \times v = \begin{bmatrix} u_2 v_3 - u_3 v_2 \\ u_3 v_1 - u_1 v_3 \\ u_1 v_2 - u_2 v_1 \end{bmatrix}$$


![[Pasted image 20260131171308.png]]
원래 외적은 3차원에서 벡터를 반환하지만, 2차원에서도 $z$축이 있다 치고, 계산해서 나오는 숫자를 그냥 **2D 외적**이라고 퉁쳐서 부른다. 계산하거나 코딩할 때 간편하기에.
각도를 구하지 않고도(비싼 연산) 회전 방향과 좌우 위치를 확인하는 용도로 유용하게 사용된다.


### 90도 회전으로서의 외적
단위벡터 N과의 외적은 법선이 N인 평면에서의 90도 회전과 동일하다.
$$n \times u$$
평면 위 벡터를 90도 회전시키기 위한 목적이라면 복잡하게 회전 행렬을 사용하지  않고, 축과의 외적을 통해 간단하게 구할 수 있다.

![[Pasted image 20260131175729.png]]
위 질문에 대해서, $\theta$만큼 회전한 벡터 $\mathbf{u}'$를 구하는 공식은 다음과 같다.
$$\mathbf{u}' = \mathbf{u}(\cos \theta) + (\mathbf{N} \times \mathbf{u})(\sin \theta)$$

![[Pasted image 20260131180039.png]]
[공식이 성립되는 이유]

### 내적의 행렬 표현

**점곱을 행렬 곱을 통한 표현**
$$u\cdot v=u^{T}v=[\begin{matrix}u_{1}&\cdot\cdot\cdot&u_{n}\end{matrix}][\begin{bmatrix}v_{1}\\ \vdots\\ v_{n}\end{bmatrix}]=\sum_{i=1}^{n}u_{i}v_{i}$$

**다른 내적에 대해선 어떻게 표현할까 ?**
E.g., $<u,v>:=2u_1v_1+u_1v_2+u_2v_1+3u_2v_2$

![[Pasted image 20260131190117.png]]

![[Pasted image 20260131190149.png]]


### 외적의 행렬 표현

**행렬 곱셈을 통해 외적을 표현할 수도 있다.**
$$u:=(u_{1},u_{2},u_{3}) \Rightarrow \hat{u}:=\begin{bmatrix}0&-u_{3}&u_{2}\\ u_{3}&0&-u_{1}\\ -u_{2}&u_{1}&0\end{bmatrix}$$
성분 $(u_1, u_2, u_3)$를 가지는 3차원상의 벡터 $u$를 3 X 3 행렬로 변환한다.

**왜 행렬로 바꿀까 ?**




$$u\times v=\hat{u}v=\begin{bmatrix}0&-u_{3}&u_{2}\\ u_{3}&0&-u_{1}\\ -u_{2}&u_{1}&0\end{bmatrix}\begin{bmatrix}v_{1}\\ v_{2}\\ v_{3}\end{bmatrix}$$

**Q. 새로운 행렬을 만들지 않고, $u \times v$ 를 어떻게 표현할 수 있을까 ?**
$v \times u = -u \times v$임을 알면 유용하다.
외적은 일종의 반대칭이다.
연산에서 피연산자의 순서를 바꾸면 결과가 마이너스가 된다.

그러한 이유는 오른손 법칙을 생각해보면 쉽게 알 수 있다.
외적은 근본적으로 방향과 관련이 있으므로, 연산 순서가 바뀌면 방향이 정반대로 뒤집히기 때문이다.
![[Pasted image 20260131195756.png]]

외적을 나타내는 데 사용하는 행렬은 비대칭 행렬이다.