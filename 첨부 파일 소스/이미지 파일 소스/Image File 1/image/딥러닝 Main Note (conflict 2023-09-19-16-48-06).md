
# 딥러닝 항목과 역사

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916172802.png]]
<딥러닝을 바라보는 4가지 항목>


![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916172650.png]]
<데이터>
이미지에서 어떤 정보를 추출하는지

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916172910.png]]
<모델>
모델에 따라 어떤 결과를 뱉어낼지 다 다름

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916173016.png]]
(최적화)
손실 함수 값을 최소화하는 파라미터 구하기
근사치 더욱 가깝게 구하기

딥러닝의 역사

2012 - AlexNet 딥러닝을 통해 이미지 대회를 최초로 우승
2013 - DQN 알파고 모델 (딥마인드의 시초)
2014 - Encoder/Decoder 번역에 사용되는 모델 // Adam Optimizer 적은 gpu로도 좋은 결과를 뽑아준다?
2015 - GAN (Generatice Adversarial Network)
           네트워크가 제네레이터와 디스크레이미터 두 개를 만들어서 학습시킴
           ResNet (Residual Networks)
		   네트워크가 깊게 쌓게 만들어주는 페러다임 시프트
2017 -  Transformer Attention구조를 다룸
2018 -  Bert (fine-tuned NLP models)
2019 -  Big Language Models (GPT - X)
2020 -  Self-Supervised Learning 주어진 학습 데이터에 라벨을 모르는 이미지 데이터를 학습에 같이 활용. 이미지가 어떻게 하면 컴퓨터가 이해할 수 있는 벡터로 바꿀 수 있는가

# [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/신경망(neural network)]]

- Input에 weight를 곱한 총 합이 activation function(활성함수)에 따라 최종 출력이 결정되는 방식

==**활성함수를 곱하기 전인 기본적인 선형모델의 예**==
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916180440.png]]
- (행렬의 두가지 의미)
	X 처럼 데이터를 모아놓은 행렬
	W 처럼 데이터를 다른 데이터 공간으로 보내주는 가중치 행렬
- b 행렬은 각 행마다 같은 값을 가지고 있어서 데이터 값에 행마다 같은 값을 더해줌
- 출력벡터의 차원은 (n * d) * (d * p) = n * p
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916185721.png]]
화살표에 해당하는게 가중치 행렬이다.(다른 공간으로 보내주는 함수)
화살표의 개수는 (d x p)인 W의 원소 개수

==**대표적인 활성함수인 Softmax Function**==
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916192556.png]]
- 각 뉴런 출력 값과의 상대적인 비교로 최종 출력 값이 결정
- 학습할 때 사용

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916192810.png]]
- 추론할 때는 one_hot 사용

==[[4. Archive/AI 공부/Ai Tech 딥러닝 공부/신경망(neural network)]] 과정==
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916193054.png]]
- 인풋 x * 가중치 w + 편향 b = z, z * 활성함수 σ = σ(z1) 
- **z** 는 이전층의 모든 입력이 각각의 가중치와 곱해진 값들이 모두 더해진 가중합이다.
	아직 활성함수를 거치지 않은 상태.
- **z** 에 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/활성함수]]**σ**를 씌우면 새로운 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/잠재벡터]]인 H(각 뉴런의 출력 값)를 뱉게 된다.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916193645.png]]
- x를z로 연결하는 W(1) 가중치 행렬과 활성함수를 곱한 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/잠재벡터]] H를 O라는 출력벡터로 연결하는 W(2) 가중치 행렬.
- 총 가중치 행렬을 두개 (W1 , W2)사용하므로 2층 신경망.

==**MLP(Multi-Layer Perceptron) 다층 퍼셉트론**==
- [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/신경망(neural network)]]을 여러층으로 합성한 함수
- 여러층의 퍼셉트론으로 적어도 1개 이상의 은닉층(hidden layer) 보유
- 일반적으로 지도학습
- 역전파 알고리즘(Backpropagation)으로 학습 - 다층 퍼셉트론 문제 해결위한 알고리즘 
- [[3. Resource(정보 저장소)/프로그래밍/Ai Tech 딥러닝 공부/관련 단어/경사하강법]]으로 에러를 최소화
- Overfitting : 트레이닝셋에 너무 과최적화되어 실제 데이터에서 정확도 하락
- Vanishing Gradient : 역전파로 에러를 뒤로 전파하면서 w를 업데이트하는데 여러 레이어를 거치면서 경사하강법으로 미분이 계속되어 에러값이 현저히 작아서 학습 안되는 현상

**MLP의 목적**
- 최종 출력값과 실제값의 오차가 최소화 되도록 가중치와 바이어스를 계산하여 결정하는 것. 

==**순전파(Forward Propagation)**==
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916194223.png]]
L개의 순차적인 신경망 계산을 통해서 최종 출력물인 O를 표현.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916194353.png]]
왜 층을 여러개 쌓나요 ?
- 이론적으로는 2층 신경망으로도 가능.
- 층이 깊을수록 목적함수를 근사하는데 필요한 뉴런(노드)의 숫자가 줄어들어 효율적인 학습 가능.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916194729.png]]
(층이 얇으면 뉴런의 숫자가 늘어남)
층이 깊어질 수록 최적화는 더욱 많은 노력을 필요로 한다.

==**역전파(Backpropagation)**==
Supervised learning(지도학습)
- Input과 Output을 알고 있는 상태에서 신경망을 학습 시키는 방법.
- 초기 가중치, weight 값은 랜덤으로 주어지고 각각 노드들은 하나의 퍼셉트론으로
	노드를 지날 때 마다 활성함수를 적용한다.
- 역전파는 1단계와 2단계로 구성되어 있다. (출력층 바로 이전 은닉층을 N층이라 가정)
1. 1단계 - 출력층과 N층 사이의 가중치를 업데이트 하는 단계.
2. 2단계 - N층과 N층의 이전층 사이의 가중치를 업데이트 하는 단계.

**계산 방식**
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918142719.png]]

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916195531.png]]
- 각 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/Parameter]]를 미분해서 경사하강법으로 가중치를 업데이트.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916200028.png]]
- 위에서 부터 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/연쇄법칙]]을 통해 기울기를 구하고 밑에층으로 전달하면서 가중치를 업데이트.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230916204548.png]]
[[4. Archive/AI 공부/Ai Tech 딥러닝 공부/연쇄법칙]]을 통해 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/합성함수]]를 계산
각 뉴런(노드)를 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/텐서]]라 칭함
z를 x로 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/미분]]했을 때 2(x+y)의 값이 나옴
[[4. Archive/AI 공부/Ai Tech 딥러닝 공부/역전파 알고리즘]]은 각 미분값을 메모리에 저장해줘야 되기 때문에 메모리를 더 많이 사용


# 확률론 맛보기

딥러닝에서 확률론이 왜 필요한가 ?
- 딥러닝은 확률론 기반의 기계학습 이론에 바탕을 두고 있다.

- 기계학습에서 사용되는 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/손실함수]](Loss function)들의 작동 원리는 데이터 공간을 통계적으로 해석해서 유도한다. 예측이 틀릴 위험(risk)을 최소화하도록 데이터를 학습하는 원리는 기계학습의 기본 원리

- 회귀 분석에서 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/손실함수]]로 사용되는 L2-노름은 예측오차의 분산을 가장 최소화하는 방향으로 학습하도록 유도

- 분류 문제에서 사용되는 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/교차 엔트로피]](cross-entropy)는 모델 예측의 불확실성을 최소화하는 방향으로 학습하도록 유도

- 분산 및 불확실성을 최소화하기 위해서는 측정하는 방법을 알아야 한다. 두 대상을 측정하는 방법을 통계학에서 제공.
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230919054035.png]]


# **[[4. Archive/AI 공부/Ai Tech 딥러닝 공부/확률분포]]**

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917005555.png]]
- 확률변수는 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/확률분포]] D에 따라 이산형과 연속형 확률변수로 구분
  (데이터 공간이 아닌, 확률 분포의 종류에 따라서 구분한다.)
  
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917010056.png]]
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917010045.png]]
**이산확률변수 vs 연속확률변수**
반드시 두 가지로만 구분되는 것은 아니다.
- 데이터(x,y)에 따라서 분포(D)의 성질이 달라지고, 그 분포(D)의 종류에 따라서 확률분포를 모델링하는 방법이 달라진다.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917011444.png]]
- D는 이론적으로 존재하는 확률분포이기 때문에 사전에 알 수 없다.
- [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/결합분포]]와 D가 각각 이산형인지 연속형인지는 서로 다를 수 있다.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917011525.png]]
- 조건부확률분포 P(x l y) = y가 조건부로 주어졌을 때 x의 확률분포.
- y가 1인 경우의 값에만 대해서 확률분포를 카운팅

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917012524.png]]
- 연속확률분포의 경우에는 확률이 아니라 밀도로 해석
- 조건부기대값은 L2노름인 E ll y - f(x) ll2 을 최소화하는 함수 f(x) 와 일치한다
- 회귀문제에 대해선 보통 연속형을 다루기 때문에 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/적분]]을 통해서 계산

[[4. Archive/AI 공부/Ai Tech 딥러닝 공부/기대값]]
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917013001.png]]
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917013247.png]]
- 연속형인 경우에는 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/적분]]을 통해 밀도함수를 곱해주고
- 이산형인 경우에는 급수를 통해 질량함수를 곱해준다.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917013511.png]]
- 특징패턴을 학습하기 위해 어떤 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/손실함수]]를 사용할지는 기계학습 문제와 모델에 의해 결정된다.!

# [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/몬테카를로 샘플링]]

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917013609.png]]
- **확률 분포를 모를 때 사용**
-  함수 f(x)에 대해서 x에 샘플링한 데이터를 대입. 데이터들에 따라서 f(x(i))의 산술평균 값을 구해주면 구하고자 하는 기대값에 근사하게 된다.
- 샘플링하는 분포에서 독립적으로 샘플링을 해줘야 한다.
- 독립추출만 보장된다면 대수의 법칙(law of large number)에 의해 수렴성을 보장한다.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917020704.png]]
- 일반적인 방법으로 f(x)의 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/적분]]을 구하는 건 불가능하다.
- 몬테카를로 방법을 통해 원하고자 하는 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/적분]]값의 1/2값을 구할 수 있다.
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917020841.png]]
- 균등분포(uniform)에서 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/데이터 샘플링]]해준 다음에, 함수에 값을 대입해주고 대입된 함수값의 데이터를 산술평균 해준 후에 구간의 길이인 2만큼 곱해줌으로써 함수의 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/적분]]값을 구할 수 있다.
- 균등분포에서 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/데이터 샘플링]] -> 함수에 값 대입 -> 합수값 산술평균 -> 구간길이 2만큼 곱해주기 = 1.49387+-0.0039
- 샘플사이즈가 적다면 오차 값이 커질 수 있으므로 적절한 샘플값 설정

# 통계적 모델링(확률분포 가정)

- 통계적 모델링은 적절한 가정 위에서 확률분포를 추정하는 것
- 유한한 데이터로는 한계가 있으므로 근사적으로 추정해서 오차를 줄이는 것이 목표
- 모수(평균과 분산을 묶은 것)=[[4. Archive/AI 공부/Ai Tech 딥러닝 공부/Parameter]] 를 추정하는 방법을 모수적 방법론
- 데이터에 따라 모델 구조, 모수의 개수가 유연하게 바뀌면 비모수 방법론
	(모수가 무한히 많거나 모수의 개수가 바뀜)

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917125641.png]]
**[[4. Archive/AI 공부/Ai Tech 딥러닝 공부/확률분포]] 가정하는 방법**
- 데이터를 먼저 분석하고 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/확률분포]]를 가정해야 한다.
- 모수를 추정한 후에는 검정이 필수 !
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917142522.png]]
- 표집분포와 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/정규분포]]는 다르다

## 최대 가능도
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917143723.png]]
**주어진 표본에 대해 가능도를 가장 크게 하는 모수θ 를 찾는 방법**
- 세타에 대한 확률이 아니라 세타에 대한 크고 작음을 비교하는 함수
- [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/로그함수]]의 성질을 이용해서 확률분포 함수들의 곱셈을 덧셈으로 최적화 해줌.
- L 은 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/가능도]](likelihood)를 의미.
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917144429.png]]

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917151644.png]]
- 연속확률변수에 해당하는 정규분포에서 최대가능도 사용

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917152413.png]]
- 이산확률변수에 해당하는 카테고리분포에서 최대가능도 사용

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917153207.png]]
- 각각의 차원에 해당하는 경우의 숫자를 세어 비율을 구하여 최대가능도를 달성하는 모수를 측정

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917153401.png]]
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917153517.png]]
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917153601.png]]
**KL Divergence**
- P 분포와 Q 분포가 얼마나 다른지를 측정하는 방법 (P는 사전분포, Q는 사후분포)

기계학습의 원리는 데이터로부터 확률분포 사이의 거리를 최소화하는 것과 동일

==[[4. Archive/AI 공부/Ai Tech 딥러닝 공부/확률]]과 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/가능도]]의 차이==
- 이산형 확률변수에 관해서는 특정 관측치에 관한 확률을 구할 수 있기 때문에 개념적 차이는 없다. 하지만 연속형 확률변수에서 차이가 나타난다
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917155054.png]]

# 신경망 기초이론

신경망(neural network)가 시작은 인간의 뇌를 모방했지만, 잘 된 이유는 인간의 뇌와 별개로 발전되어왔기 때문이다.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917185615.png]]
선형하강법을 통해 계속 업데이트해서 로스값을 최소화 시킴

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917190151.png]]
X를 W1으로 변환시켜서 h라는 히든 벡터를 얻어내고 다시 W2를 곱한다.
하지만 이렇게 되면 또다른 행렬에 지나지 않음.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917190213.png]]
그래서 네트워크가 표현할 수 있는 표현력을 극대화 하기 위해 활성화 함수를 곱해
선형 결합을 반복하는게 아니라 비선형 변환을 활용

# Generalization(일반화)

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917201029.png]]
generalization이 높으면 성능이 좋지 않음.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917201148.png]]
과적합(overfitting) - 테스트 데이터에서만 잘 동작하고 실제 데이터를 가지고 예측을 수행하면 엉망인 결과가 나와버리게 되는 현상

이처럼 고정된 train set과 test set으로 평가를 하고, 반복적으로 모델을 튜닝하다보면 test set에만 과적합(overfitting)되어버리는 결과가 생긴다.

이를 해결하고자 하는 것이 바로 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/교차 검증]](Cross-validation)
# Cross-validation([[4. Archive/AI 공부/Ai Tech 딥러닝 공부/교차 검증]])

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917201622.png]]**[[4. Archive/AI 공부/Ai Tech 딥러닝 공부/교차 검증]](cross validation)**
- 과적합 되는 문제는 test set이 데이터의 일부분으로 고정되어 있기 때문에 발생한다.
- 교차 검증은 데이터 셋의 모든 부분을 사용하여 모델을 검증한다.
- 뉴럴 네트워크를 사용하는데 많은 [[4. Archive/AI 공부/Ai Tech 딥러닝 공부/Hyper Parameter]](내가 정하는 값들. 러닝 레이트,네트워크 크기 등)를 사용한다. 교차 검증을 통해 최적의 하이퍼 파라미터 셋을 찾고, 하이퍼 파라미터를 고정한 상태에서 학습시킬 때는 모든 데이터를 전부 사용.
- 테스트 데이터는 어떤 식으로든 활용해선 안된다.

**[[4. Archive/AI 공부/Ai Tech 딥러닝 공부/교차 검증]]의 과정**
다음은 일반적으로 사용되는 k-fold 교차 검증의 예시이다.
train data를 k개로 나누고 validation data을 중복 없이 바꿔가며 k번의 (validation)을 진행한다 .
그 후 k번의 결과를 평균내어 최종적으로 모델의 성능을 평가.

**[[4. Archive/AI 공부/Ai Tech 딥러닝 공부/교차 검증]]의 장점과 단점**
장점 :
- 모든 데이터 셋을 평가에 활용할 수 있다.
- 평가에 사용되는 데이터 편중을 막을 수 있다.
- (특정 평가 데이터 셋에 과적합(overfitting) 되는 것을 방지할 수 있다.)
- 평가 결과에 따라 좀 더 일반화된 모델을 만들 수 있다.
- 모든 데이터 셋을 훈련에 활용할 수 있다.
- 정확도를 향상시킬 수 있다.
- 데이터 부족으로 인한 underfitting을 방지할 수 있다.
단점 : 
- Iteration 횟수가 많기 때문에 모델 훈련/평가 시간이 오래 걸린다.

# **Bias and Variance**

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917203336.png]]
- **Variance**란 좌표에 상관 없이 결과가 얼마나 일관적으로 나오는지
	(탄착군 형성과 비슷한 원리)
- **Bias**란 값의 일관성과 상관 없이 원하는 값과 비슷하게 나오는지

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917203647.png]]
에러(cost)에 noise가 껴있다고 가정하면
cost를 minimize하기 위해서 한 쪽을 줄이면 다른 값이 높아질 가능성이 크기 때문에,
근본적으로 학습 데이터에 노이즈가 껴있을 경우에는 bias, variance 둘 다 줄이기는 힘들다.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917204507.png]]
학습 데이터가 고정되어 있을 때 그 데이터를 모두 사용하는 것이 아니라,
일부분만 사용하여 여러개의 모델을 만들어서 하겠다.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230917204853.png]]
부스팅은 여러개의 모델과 데이터가 서로 유기적으로 연결되어 있음.
# Optimization(최적화)

**학습 모델의 손실함수(loss function)의 최소값을 찾아가는 과정**

딥러닝 학습시 최대한 틀리지 않는 방향으로 학습해야 한다,

얼마나 **틀리는지(loss)** 를 알게 하는 함수가 **loss function([[4. Archive/AI 공부/Ai Tech 딥러닝 공부/손실함수]])** 이다.  
loss function 의 최솟값을 찾는 것을 학습 목표로 한다.

이를 수행하는 **최적화 알고리즘 = Optimizer**

==Optimizer 종류==
![](https://velog.velcdn.com/images/freesky/post/57e14895-6eb0-4c86-a9d1-0acdb0398406/image.png)
출처 : https://velog.io/@freesky/Optimizer

SGD , Momentum , AdaGrad , RMSProp, Adam의 자세한 내용을 보려면..
ㄴ> https://amber-chaeeunk.tistory.com/23

# Ragularization(규제화)

**overfitting**을 방지하는 방법 중 하나로써 모델에 제약을 줌.
쉽게 말하자면, **perfect fit 을 포기함으로써(trainging accuracy를 낮춤으로써)  potential fit을 증가시키고자(testing accuracy를 높이고자) 하는 것** 입니다.
![](https://blog.kakaocdn.net/dn/Td9EY/btqxJx5IVHD/5gVSXVPgzNG85E49PLvYw1/img.png)
위의 오른쪽 그래프를 보면 모든 traing data에대해서는 완벽하게 fitting되어 있습니다. 하지만 이 모델은 일반적으로 적용했을때 옳바른 output을 내지 못하겠죠.

따라서 너무 높은 complexity를 피하기 위해서 쓰는 방법이 **Regularization** 입니다.

- W(weight)가 너무 큰 값들을 가지지 않도록 하는 것이다.
- W가 너무 큰 값을 가지게 되면 과하게 구불구불한 형태의 함수가 만들어지는데, Regularization은 이런 모델의 복잡도를 낮추기 위한 방법이다.
- Regularization은 단순하게 cost function을 작아지는 쪽으로 학습하면 특정 가중치 값들이 커지면서 결과를 나쁘게 만들기 때문에 cost function을 바꾼다.

# Normalization(정규화)

**데이터 정규화(Normalization)는 모델 학습 이전에 여러 Feature 데이터 값의 범위를 조정하는 과정을 말하며, Feature Scaling 또는 Data Scaling이라고 부른다**

**필요성**
- 데이터 값의 범위 차이가 클 경우, 아래의 **그림 1 좌측**처럼 비효율적인 최적화 과정을 거치게 됩니다. 데이터 간 편차가 큰 Feature 위주로 학습이 진행되기 때문에 X축 방향 위주로 파라미터가 갱신되며 최적화가 진행됩니다. 반면, 상대적으로 편차가 적은 Y축 방향의 Feature의 영향력은 상대적으로 무시되는 현상이 발생합니다.

![](https://blog.kakaocdn.net/dn/K9ZO4/btrHJAluQVI/jPCad2L4pT95TPu8Z5rmQ0/img.png)
- 데이터를 정규화하게 되면 위의 문제점을 해결할 수 있습니다. 즉, **그림 1 우측**처럼, 데이터 범위의 차이가 작아지기 때문에, 모델 학습 시 모든 Feature마다 파라미터가 유사한 중요도를 갖고 개선되기 때문에 최적화 과정이 개선되는 효과가 있습니다.

## Batch Normalization

**배치 정규화(Batch Normalization)는 학습 과정에서 Batch마다 평균과 분산을 활용하여 데이터의 분포를 정규화하는 과정을 말합니다(그림 3). 데이터 종류에 따라 값의 범위는 천차만별이기 때문에, Batch마다 입력값의 범위를 스케일링하는 과정이 바로 Batch Normalization입니다.**

![](https://blog.kakaocdn.net/dn/cKfcZy/btrHILHAx6c/4gdt1EkyeSxnfaCjohc9C1/img.png)
- 그림 3. Batch Normalization 예시

**장점**
#### 1) 데이터 Scale 통일

첫째, 어떠한 데이터 분포가 입력으로 들어와도 모두 정규화하기 때문에 모든 Layer의 Feature가 동일한 Scale이 되도록 만드는 점입니다. 즉, 앞서 살펴본 Batch마다 데이터 분포가 달라지는 Internal Covariate Shift 현상을 방지할 수 있고 학습률 결정 시 효과적입니다. 모델 학습 과정에는 [손실함수(Loss Function)](https://heytech.tistory.com/361)와 가까운 Layer일수록 학습이 잘 되고, 멀리 있는 Layer일수록 학습이 잘 안 되는 특징이 있습니다. 즉, 손실함수에 멀리 있는 Layer일수록 학습률을 높게 설정하는 것처럼, 일반적으로 학습 성능을 올리기 위해서는 Layer마다 학습률을 다르게 설정할 필요가 있었습니다. 하지만, Batch Normalization을 사용할 경우 모든 Layer의 Feature마다 동일한 scale이 되기 때문에 학습률을 결정하는 데 도움이 됩니다.
#### 2) 활성화 함수 맞춤형 분포 변화

둘째, Batch Normalization 시 추가적인 스케일링과 편향(bias)을 학습함으로써 [활성화 함수(Activation Function)](https://heytech.tistory.com/360) 종류에 맞게 적합한 분포로 변환이 가능하다는 점입니다.
# CNN(Convolution Neural Network)콘볼루션신경망

https://rubber-tree.tistory.com/entry/%EB%94%A5%EB%9F%AC%EB%8B%9D-%EB%AA%A8%EB%8D%B8-CNN-Convolutional-Neural-Network-%EC%84%A4%EB%AA%85

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918084901.png]]
- 가중치 행렬 W의 i행과 x가 곱해서 히든벡터 h의 i행을 만들어 내는 방식
- 단점 : h의 행마다 가중치 행렬이 필요하므로 학습해야 하는 Parameter가 많아짐

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918085052.png]]
- 활성함수를 제외한 괄호 내의 Convolution연산은 선형변환에 속한다.
- Convolution 연산의 수학적인 의미는 신호(signal)를 커널을 이용해 국소적으로 증폭 또는 감소시켜서 정보를 추출 또는 필터링하는 것
- CNN에서 사용하는 연산은 사실 Cross-correlation인데, 역사적으로 Convolution이라 사용해왔기 때문에 그렇게 부른다.
- continuous 일 때는 적분으로, discrete 일 때는 급수로 계산

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918090050.png]]
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918090437.png]]
- 입력 벡터 상에서 한 칸씩 움직여 가면서 연산

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918090754.png]]
- 채널이 여러개인 2차원 (=3차원 텐서)

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918090951.png]]
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918091120.png]]
- 역전파를 계산해도 convolution이 나옴

**Convolution 역전파 계산**
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918091505.png]]
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918092022.png]]

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918091945.png]]
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918091956.png]]

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918093429.png]]
- 기본적인 Convolution 구조

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918093801.png]]
- Stride : 다음 연산을 몇 칸을 옮겨서 할거냐

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918094043.png]]
- Padding : 칸을 확장 해줘서 끝 부분 연산을 해줄 것이냐

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918094259.png]]
- 네트워크 모양만 보고 파라미터 개수를 유추할 수 있어야 한다.

![[4. Archive/AI 공부/Ai Tech 딥러닝 공부/Pasted image 20230918175119.png]]


# RNN(Recurrent Neural Network)순환신경망
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918095839.png]]
- 앞 뒤 맥락 없이 예측하는 것은 굉장히 어렵다
- 순차적으로 들어오는 정보를 어떻게 반영할까 ?

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918100331.png]]
- Summation과 달리 파이는 모든 값을 곱해줌
- 반드시 아주 먼 과거의 모든 정보들까지 필요한 것은 아니다

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918102453.png]]
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918103935.png]]
- BPTT : RNN의 역전파 방법

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918104004.png]]

==**Sequential Model**==
- 일상생활에서 접하는 대부분의 데이터

**시퀀셜 데이터를 처리하는데 가장 큰 어려움 ?**
- 내가 원하는 정보의 길이가 언제 끝날 지 모름. 몇 개의 입력이 들어올 지 모르기  때문

**가장 기본적인 시퀀셜 모델**
- 입력이 들어올 때 다음 번 입력에 대한 예측을 하는 것 ex)language model
- 뒤로 갈 수록 고려해야 할 과거의 데이터가 점점 늘어난다. 이런 문제를 해결하기 위해, 과거의 데이터 몇개만 볼 건지 정해 놓는다.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918105415.png]]
**Latent autoregressive model**
- 과거의 모든 데이터를 다룰 수 없으므로, 과거의 데이터를 Ht를 통해서 요약하고, Ht-1을 통해서 과거를 요약한 데이터 1개만 본다.

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918105713.png]]
- MLP와 비슷하게 생겼지만, 하나의 차이점은 자기 자신으로 돌아오는 구조가 하나 존재한다. 
- RNN모델을 시간 순으로 푼 것. x0을 가지고 x1이 나오고 또 x1을 가지고 x2가 나오고 ...  반복

![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918110049.png]]
- RNN의 가장 큰 단점 : 과거의 모든 정보들이 미래에 살아남아야 하는데, 먼 미래까지 살아남기가 힘들다. 

RNN의 단점을 해결한 LSTM
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918115135.png]]
- 이전 값들을 지우고 어떤 값들을 얼마나 업데이트 할 지 계산해서 값을 뽑아냄
LSTM의 더욱 자세한 정보:https://dgkim5360.tistory.com/entry/understanding-long-short-term-memory-lstm-kr

LSTM의 변형 모델
![[첨부 파일 소스/이미지 파일 소스/Image File 1/image/Pasted image 20230918115543.png]]
- LSTM모델에서 Forget gate와 input gate를 하나의 Update gate로 합치고, Cell state와 hidden state를 합쳐 더욱 단순한 구조를 가진다.
- 하지만 요즘에는 Transformer구조의 등장으로 RNN구조에서 Transformer로 점차 바뀌고 있다

요약 : RNN이 짧은 거리에서는 데이터가 살아 남지만, 먼 거리에 까지 데이터가 살아서 전달되기 힘든 문제가 있다. 그걸 개선한 것이 LSTM모델이고, 더욱 개선한 것이 GRU. 하지만 더욱 강력한 Transformer의 등장으로 페러다임 시프트가 일어남.