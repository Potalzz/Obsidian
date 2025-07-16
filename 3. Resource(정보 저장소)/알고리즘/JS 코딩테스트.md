# 프로그래머스 Lv. 1
## Lv. 1 폰켓몬
### 문제
###### 문제 설명

당신은 폰켓몬을 잡기 위한 오랜 여행 끝에, 홍 박사님의 연구실에 도착했습니다. 홍 박사님은 당신에게 자신의 연구실에 있는 총 N 마리의 폰켓몬 중에서 N/2마리를 가져가도 좋다고 했습니다.
홍 박사님 연구실의 폰켓몬은 종류에 따라 번호를 붙여 구분합니다. 따라서 같은 종류의 폰켓몬은 같은 번호를 가지고 있습니다. 예를 들어 연구실에 총 4마리의 폰켓몬이 있고, 각 폰켓몬의 종류 번호가 [3번, 1번, 2번, 3번]이라면 이는 3번 폰켓몬 두 마리, 1번 폰켓몬 한 마리, 2번 폰켓몬 한 마리가 있음을 나타냅니다. 이때, 4마리의 폰켓몬 중 2마리를 고르는 방법은 다음과 같이 6가지가 있습니다.

1. 첫 번째(3번), 두 번째(1번) 폰켓몬을 선택
2. 첫 번째(3번), 세 번째(2번) 폰켓몬을 선택
3. 첫 번째(3번), 네 번째(3번) 폰켓몬을 선택
4. 두 번째(1번), 세 번째(2번) 폰켓몬을 선택
5. 두 번째(1번), 네 번째(3번) 폰켓몬을 선택
6. 세 번째(2번), 네 번째(3번) 폰켓몬을 선택

이때, 첫 번째(3번) 폰켓몬과 네 번째(3번) 폰켓몬을 선택하는 방법은 한 종류(3번 폰켓몬 두 마리)의 폰켓몬만 가질 수 있지만, 다른 방법들은 모두 두 종류의 폰켓몬을 가질 수 있습니다. 따라서 위 예시에서 가질 수 있는 폰켓몬 종류 수의 최댓값은 2가 됩니다.  
당신은 최대한 다양한 종류의 폰켓몬을 가지길 원하기 때문에, 최대한 많은 종류의 폰켓몬을 포함해서 N/2마리를 선택하려 합니다. N마리 폰켓몬의 종류 번호가 담긴 배열 nums가 매개변수로 주어질 때, N/2마리의 폰켓몬을 선택하는 방법 중, 가장 많은 종류의 폰켓몬을 선택하는 방법을 찾아, 그때의 폰켓몬 종류 번호의 개수를 return 하도록 solution 함수를 완성해주세요.

##### 제한사항

- nums는 폰켓몬의 종류 번호가 담긴 1차원 배열입니다.
- nums의 길이(N)는 1 이상 10,000 이하의 자연수이며, 항상 짝수로 주어집니다.
- 폰켓몬의 종류 번호는 1 이상 200,000 이하의 자연수로 나타냅니다.
- 가장 많은 종류의 폰켓몬을 선택하는 방법이 여러 가지인 경우에도, 선택할 수 있는 폰켓몬 종류 개수의 최댓값 하나만 return 하면 됩니다.

---

##### 입출력 예

| nums          | result |
| ------------- | ------ |
| [3,1,2,3]     | 2      |
| [3,3,3,2,2,4] | 3      |
| [3,3,3,2,2,2] | 2      |

### 나의 풀이
```
function solution(nums) {
    const noDuplicateNums = new Set(nums)
    const pokemonMax = nums.length / 2
    const count = noDuplicateNums.size

    return count >= pokemonMax ? pokemonMax : count
}
```
nums배열에서 중복만 제거하면 되는 간단한 문제.
처음에는 for문으로 includes를 사용해 각 요소마다 비교했는데, set 객체로 만들어주면 간단하게 해결 가능하다.


## LV. 1 모의고사
### 문제
###### 문제 설명

수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...  
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...  
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

##### 제한 조건

- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.

##### 입출력 예

| answers     | return  |
| ----------- | ------- |
| [1,2,3,4,5] | [1]     |
| [1,3,2,4,2] | [1,2,3] |



### 나의 풀이
```
/*
각 수포자별로 문제 찍는 방법을 담은 배열을 배정하고,
문제를 대입해서 일치하는 사람이 가장 많은 사람을 리턴한다.

채점 방법
for문으로 문제 하나씩 비교

순위 가리기
가장 큰 숫자를 알아내고, 그 숫자에 해당하는 인덱스+1을 나란히 반환.

*/

function solution(answers) {
    let answer = [];
    
    const playerAnswers = [
        [1,2,3,4,5,1,2,3,4,5],
        [2,1,2,3,2,4,2,5,2,1,2,3,2,4,2,5],
        [3,3,1,1,2,2,4,4,5,5,3,3,1,1,2,2,4,4,5,5],
    ]
    let playerScores = [0,0,0]
  
    for (let i=0; i<playerAnswers.length; i++) {
        let player = playerAnswers[i]
        for (let j=0; j < answers.length; j++) {
            player[j % player.length] === answers[j] ? playerScores[i] ++ : ''
        }
    }
  
    const maxScore = Math.max(...playerScores)
    
    for (let i = 0; i < playerScores.length; i++ ) {
        playerScores[i] === maxScore ? answer.push(i+1) : ''
    }

    return answer;
}
```
#### 풀이방법
각 수포자별로 문제 찍는 방법을 담은 배열을 배정하고,
문제를 대입해서 일치할 경우 점수를 더해 점수가 가장 높은 사람을 답에 추가한다.

#### 풀이 구조
for문으로 문제와 사람 정답 비교하면서 점수 더하기.
가장 큰 점수가 나오면 중복 우승을 고려해 player배열에서 최대값에 해당하는 player 인덱스+1 값 반환

정답 비교하는 for문에서 문제 번호가 player정답 배열을 넘어가면 index를 재할당 했는데, 중괄호 안에서 계산해서 넣으면 더 깔끔하다.

## Lv .1 소수 찾기
### 문제
###### 문제 설명

1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환하는 함수, solution을 만들어 보세요.

소수는 1과 자기 자신으로만 나누어지는 수를 의미합니다.  
(1은 소수가 아닙니다.)

##### 제한 조건

- n은 2이상 1000000이하의 자연수입니다.

##### 입출력 예

|n|result|
|---|---|
|10|4|
|5|3|
일반적인 반복문으로는 효율성에서 탈락하고 에라토네스의 체를 활용해 풀 수 있다.

***풀이***
```
function solution(n) {
    let answer = 0;
    let nums = []
    for (let i=2; i<=n; i++) {
        nums[i] = i
    }
    for (let j=2; j<n; j++) {
        if(nums[j] === 0) {
            continue
        }
        for (let k = j + j; k<=n; k += j ) {
            nums[k] = 0
        }
    }
    return nums.filter((el) => el).length
}
```
for문으로 단순히 반복문을 돌리는게 아니라 원리를 이해해야 한다.
소수는 어떤 수의 배수도 아니므로. 배열에서 모든 수의 배수에 해당하는 수들을 0으로 지워주면 소수만 남게 된다.

filter를 통해 0과 underfind 값을 지워 소수의 개수를 구한다.

## Lv. 1 덧칠하기
### 문제
###### 문제 설명

어느 학교에 페인트가 칠해진 길이가 `n`미터인 벽이 있습니다. 벽에 동아리 · 학회 홍보나 회사 채용 공고 포스터 등을 게시하기 위해 테이프로 붙였다가 철거할 때 떼는 일이 많고 그 과정에서 페인트가 벗겨지곤 합니다. 페인트가 벗겨진 벽이 보기 흉해져 학교는 벽에 페인트를 덧칠하기로 했습니다.

넓은 벽 전체에 페인트를 새로 칠하는 대신, 구역을 나누어 일부만 페인트를 새로 칠 함으로써 예산을 아끼려 합니다. 이를 위해 벽을 1미터 길이의 구역 `n`개로 나누고, 각 구역에 왼쪽부터 순서대로 1번부터 `n`번까지 번호를 붙였습니다. 그리고 페인트를 다시 칠해야 할 구역들을 정했습니다.

벽에 페인트를 칠하는 롤러의 길이는 `m`미터이고, 롤러로 벽에 페인트를 **한 번** 칠하는 규칙은 다음과 같습니다.

- 롤러가 벽에서 벗어나면 안 됩니다.
- 구역의 일부분만 포함되도록 칠하면 안 됩니다.

즉, 롤러의 좌우측 끝을 구역의 경계선 혹은 벽의 좌우측 끝부분에 맞춘 후 롤러를 위아래로 움직이면서 벽을 칠합니다. 현재 페인트를 칠하는 구역들을 완전히 칠한 후 벽에서 롤러를 떼며, 이를 벽을 **한 번** 칠했다고 정의합니다.

한 구역에 페인트를 여러 번 칠해도 되고 다시 칠해야 할 구역이 아닌 곳에 페인트를 칠해도 되지만 다시 칠하기로 정한 구역은 적어도 한 번 페인트칠을 해야 합니다. 예산을 아끼기 위해 다시 칠할 구역을 정했듯 마찬가지로 롤러로 페인트칠을 하는 횟수를 최소화하려고 합니다.

정수 `n`, `m`과 다시 페인트를 칠하기로 정한 구역들의 번호가 담긴 정수 배열 `section`이 매개변수로 주어질 때 롤러로 페인트칠해야 하는 최소 횟수를 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- 1 ≤ `m` ≤ `n` ≤ 100,000
- 1 ≤ `section`의 길이 ≤ `n`
    - 1 ≤ `section`의 원소 ≤ `n`
    - `section`의 원소는 페인트를 다시 칠해야 하는 구역의 번호입니다.
    - `section`에서 같은 원소가 두 번 이상 나타나지 않습니다.
    - `section`의 원소는 오름차순으로 정렬되어 있습니다.

---

##### 입출력 예

| n   | m   | section      | result |
| --- | --- | ------------ | ------ |
| 8   | 4   | [2, 3, 6]    | 2      |
| 5   | 4   | [1, 3]       | 1      |
| 4   | 1   | [1, 2, 3, 4] | 4      |

### 나의 풀이
```
function solution(n, m, section) {
    let count = 0;
    let indicate = 0
    for (let i = indicate + 1; i<=section.length; i++) {
        if (i === section.length) {
            break
        }
        if (section[i] - section[indicate] < m) {
            continue
        } else {
            count += 1
            indicate = i
        }
    }
    count += 1
    return count;
}
```

변수 indicate와 i를 통해 두 개의 화살표를 통해 배열 안의 숫자 차를 비교하며 풀었다.

### 다른 풀이
```
function solution(n, m, sections) {
    var answer = 0;
    var painted = 0;
    for(var section of sections) {
        if(painted < section) {
            answer++;
            painted = section+m-1;
        }
    }
    return answer;

```

배열의 숫자를 하나씩 가져와서 페인트된 부분이 칠해야 될 부분보다 뒤에있는 경우, 칠해야 될 부분부터 페인트하면서 품.
문제를 풀기 위한 코드가 아니라 **칠해야 될 부분부터 페인트칠한다**. 는 로직 하나를 코드로 표현해 낸 좋은 풀이라고 생각한다.

문제를 풀기위한 코드를 짜지 말고, 문제를 해결하기 위한 가장 효율적인 로직이 무엇인지 생각하고, 해당 로직을 코드로 옮겨서 쓰자.

## Lv. 1 실패율
### 문제
###### 문제 설명


![failture_rate1.png](https://grepp-programmers.s3.amazonaws.com/files/production/bde471d8ac/48ddf1cc-c4ea-499d-b431-9727ee799191.png)

슈퍼 게임 개발자 오렐리는 큰 고민에 빠졌다. 그녀가 만든 프랜즈 오천성이 대성공을 거뒀지만, 요즘 신규 사용자의 수가 급감한 것이다. 원인은 신규 사용자와 기존 사용자 사이에 스테이지 차이가 너무 큰 것이 문제였다.

이 문제를 어떻게 할까 고민 한 그녀는 동적으로 게임 시간을 늘려서 난이도를 조절하기로 했다. 역시 슈퍼 개발자라 대부분의 로직은 쉽게 구현했지만, 실패율을 구하는 부분에서 위기에 빠지고 말았다. 오렐리를 위해 실패율을 구하는 코드를 완성하라.

- 실패율은 다음과 같이 정의한다.
    - 스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수 / 스테이지에 도달한 플레이어 수

전체 스테이지의 개수 N, 게임을 이용하는 사용자가 현재 멈춰있는 스테이지의 번호가 담긴 배열 stages가 매개변수로 주어질 때, 실패율이 높은 스테이지부터 내림차순으로 스테이지의 번호가 담겨있는 배열을 return 하도록 solution 함수를 완성하라.

##### 제한사항

- 스테이지의 개수 N은 `1` 이상 `500` 이하의 자연수이다.
- stages의 길이는 `1` 이상 `200,000` 이하이다.
- stages에는 `1` 이상 `N + 1` 이하의 자연수가 담겨있다.
    - 각 자연수는 사용자가 현재 도전 중인 스테이지의 번호를 나타낸다.
    - 단, `N + 1` 은 마지막 스테이지(N 번째 스테이지) 까지 클리어 한 사용자를 나타낸다.
- 만약 실패율이 같은 스테이지가 있다면 작은 번호의 스테이지가 먼저 오도록 하면 된다.
- 스테이지에 도달한 유저가 없는 경우 해당 스테이지의 실패율은 `0` 으로 정의한다.

##### 입출력 예

| N   | stages                   | result      |
| --- | ------------------------ | ----------- |
| 5   | [2, 1, 2, 6, 2, 4, 3, 3] | [3,4,2,1,5] |
| 4   | [4,4,4,4,4]              | [4,1,2,3]   |

스테이지 별로 스테이지를 실패한 사람들의 수 구하기.

### 나의 풀이

```
function solution(N, stages) {
    let answer = [];
    let fail = [false]
    
    // 스테이지별 실패율을 배열에 추가
    for (let i = 1; i <=N; i++ ) {
        let failStage = stages.reduce((cnt,el) => cnt + (i === el),0)
        let onStage = stages.reduce((cnt,el) => cnt + (i <= el), 0)
        if (onStage === 0) {
            fail.push(0)
        } else {
            fail.push(failStage / onStage)
        }
    }
    
    // 가장 큰 실패율에 해당하는 숫자의 인덱스를 배열에 추가
    for (let i = 1; i <= N; i++) {
        let max = fail.reduce((a,b) => Math.max(a,b), -Infinity)
        let index = fail.indexOf(max)
        fail[index] = false
        answer.push(index)
    }
    
    return answer;
}
```

문제를 풀긴 했지만, 최대값을 구하는 과정에서, reduce와 index함수를 사용해 최대 시간 복잡도가 O(N^2)까지 올라가는 것이 문제다.

### 다른 풀이

```
function solution(N, stages) {
    let answer = [];
    let stageCounts = new Array(N + 2).fill(0);  // 각 스테이지에 머물고 있는 플레이어 수
    let playerCounts = new Array(N + 2).fill(0); // 각 스테이지에 도달한 플레이어 수
    
    // 각 스테이지에 머물고 있는 플레이어 수를 계산
    for (let stage of stages) {
        stageCounts[stage]++;
    }

    // 각 스테이지에 도달한 플레이어 수를 계산
    playerCounts[N + 1] = stageCounts[N + 1]; // 마지막 스테이지 이후에 머물고 있는 플레이어 수
    for (let i = N; i >= 1; i--) {
        playerCounts[i] = stageCounts[i] + playerCounts[i + 1];
    }

    // 각 스테이지의 실패율을 계산
    let failRates = [];
    for (let i = 1; i <= N; i++) {
        let failRate = playerCounts[i] === 0 ? 0 : stageCounts[i] / playerCounts[i];
        failRates.push([i, failRate]);
    }

    // 실패율을 기준으로 정렬, 실패율이 같은 경우 스테이지 번호가 작은 것이 우선
    failRates.sort((a, b) => b[1] - a[1] || a[0] - b[0]);

    // 정렬된 스테이지 번호를 추출
    answer = failRates.map(item => item[0]);

    return answer;
}
```

**스테이지에 머물러 있는 플레이어 수**
**해당 스테이지를 도달한 플레이어 수**
`(머물러 있는 플레이어+ 스테이지를 클리어한 플레이어 = 머물러 있는 플레이어 + 다음 스테이지에 도달한 플레이어)`
총 두 개의 배열을 만들고 두 개의 배열을 통해 실패율을 계산해여 failRates배열에 스테이지 번호,실패율을 담은 배열을 넣어 이중 배열로 만든다.
이후 실패율의 크기별로 배열을 정렬하고 map을 통해 스테이지 넘버를 추출함.

내가 했던 방법은 for문에서 매번 플레이어 수를 계산하는 거였는데, 배열을 만들어 추가하는 형식으로 하면 훨씬 효율적으로 해결할 수 있다.
배열을 잘 활용하고, **내가 필요한 변수가 무엇이고 어떻게 효율적으로 만들지 고민하자**

## LV. 1 로또의 최고 순위와 최저 순위
### 문제
`로또 6/45`(이하 '로또'로 표기)는 1부터 45까지의 숫자 중 6개를 찍어서 맞히는 대표적인 복권입니다. 아래는 로또의 순위를 정하는 방식입니다. [1](https://school.programmers.co.kr/learn/courses/30/lessons/77484#fn1)

|순위|당첨 내용|
|---|---|
|1|6개 번호가 모두 일치|
|2|5개 번호가 일치|
|3|4개 번호가 일치|
|4|3개 번호가 일치|
|5|2개 번호가 일치|
|6(낙첨)|그 외|

로또를 구매한 민우는 당첨 번호 발표일을 학수고대하고 있었습니다. 하지만, 민우의 동생이 로또에 낙서를 하여, 일부 번호를 알아볼 수 없게 되었습니다. 당첨 번호 발표 후, 민우는 자신이 구매했던 로또로 당첨이 가능했던 최고 순위와 최저 순위를 알아보고 싶어 졌습니다.  
알아볼 수 없는 번호를 `0`으로 표기하기로 하고, 민우가 구매한 로또 번호 6개가 `44, 1, 0, 0, 31 25`라고 가정해보겠습니다. 당첨 번호 6개가 `31, 10, 45, 1, 6, 19`라면, 당첨 가능한 최고 순위와 최저 순위의 한 예는 아래와 같습니다.

|당첨 번호|31|10|45|1|6|19|결과|
|---|---|---|---|---|---|---|---|
|최고 순위 번호|**31**|0→**10**|44|**1**|0→**6**|25|4개 번호 일치, 3등|
|최저 순위 번호|**31**|0→11|44|**1**|0→7|25|2개 번호 일치, 5등|

- 순서와 상관없이, 구매한 로또에 당첨 번호와 일치하는 번호가 있으면 맞힌 걸로 인정됩니다.
- 알아볼 수 없는 두 개의 번호를 각각 10, 6이라고 가정하면 3등에 당첨될 수 있습니다.
    - 3등을 만드는 다른 방법들도 존재합니다. 하지만, 2등 이상으로 만드는 것은 불가능합니다.
- 알아볼 수 없는 두 개의 번호를 각각 11, 7이라고 가정하면 5등에 당첨될 수 있습니다.
    - 5등을 만드는 다른 방법들도 존재합니다. 하지만, 6등(낙첨)으로 만드는 것은 불가능합니다.

민우가 구매한 로또 번호를 담은 배열 lottos, 당첨 번호를 담은 배열 win_nums가 매개변수로 주어집니다. 이때, 당첨 가능한 최고 순위와 최저 순위를 차례대로 배열에 담아서 return 하도록 solution 함수를 완성해주세요.

##### 제한사항

- lottos는 길이 6인 정수 배열입니다.
- lottos의 모든 원소는 0 이상 45 이하인 정수입니다.
    - 0은 알아볼 수 없는 숫자를 의미합니다.
    - 0을 제외한 다른 숫자들은 lottos에 2개 이상 담겨있지 않습니다.
    - lottos의 원소들은 정렬되어 있지 않을 수도 있습니다.
- win_nums은 길이 6인 정수 배열입니다.
- win_nums의 모든 원소는 1 이상 45 이하인 정수입니다.
    - win_nums에는 같은 숫자가 2개 이상 담겨있지 않습니다.
    - win_nums의 원소들은 정렬되어 있지 않을 수도 있습니다.

---

##### 입출력 예

| lottos                | win_nums                 | result |
| --------------------- | ------------------------ | ------ |
| [44, 1, 0, 0, 31, 25] | [31, 10, 45, 1, 6, 19]   | [3, 5] |
| [0, 0, 0, 0, 0, 0]    | [38, 19, 20, 40, 15, 25] | [1, 6] |
| [45, 4, 35, 20, 3, 9] | [20, 9, 3, 45, 4, 35]    | [1, 1] |

번호 비교해서 최저 순위 정하고, 0 개수에 맞춰서 최고 순위 정하는 간단한 문제.

**나의 풀이**
```
/*
0의 개수만큼 당첨번호가 추가된 등수가 고점.
0을 제외한 숫자로 비교해본 최고 등수가 저점.
count변수 만들고 includes를 통해 맞는 번호가 있을 때마다 count 추가
*/

function solution(lottos, win_nums) {
    let answer = [0,0];
    let count = 0
    let zeroCount = 0
    
    for (let i = 0; i < lottos.length; i++) {
        let currNum = lottos[i]
        if (win_nums.includes(currNum)) {
            count ++
        } else if (currNum === 0) {
            zeroCount ++
        }
    }
    console.log(count,zeroCount)
    count === 0 ? count = 1 : ''
    zeroCount === 6 ? zeroCount = 5 : ''
    answer[1] = 7 - count 
    answer[0] = answer[1] - zeroCount
    
    return answer;
}
```

**다른 풀이**
```
function solution(lottos, win_nums) {
    let answer = [];
    const rank = [6,6,5,4,3,2,1]
    
    let win = lottos.filter((e) => win_nums.includes(e)).length
    let zero = lottos.filter((e) => e === 0).length
    
    answer.push(rank[win+zero])
    answer.push(rank[win])
    
    return answer;
}
```
for문으로 무작정 돌리는 것이 아니라, filter를 통해 더 간결하게 작성.
그 후 rank에 있는 순위에 맞추면 된다.

**코드를 간결화 시킬 수 있는 메서드를 잘 활용하자** 

## LV. 1 대충 만든 자판
### 문제
`로또 6/45`(이하 '로또'로 표기)는 1부터 45까지의 숫자 중 6개를 찍어서 맞히는 대표적인 복권입니다. 아래는 로또의 순위를 정하는 방식입니다. [1](https://school.programmers.co.kr/learn/courses/30/lessons/77484#fn1)

|순위|당첨 내용|
|---|---|
|1|6개 번호가 모두 일치|
|2|5개 번호가 일치|
|3|4개 번호가 일치|
|4|3개 번호가 일치|
|5|2개 번호가 일치|
|6(낙첨)|그 외|

로또를 구매한 민우는 당첨 번호 발표일을 학수고대하고 있었습니다. 하지만, 민우의 동생이 로또에 낙서를 하여, 일부 번호를 알아볼 수 없게 되었습니다. 당첨 번호 발표 후, 민우는 자신이 구매했던 로또로 당첨이 가능했던 최고 순위와 최저 순위를 알아보고 싶어 졌습니다.  
알아볼 수 없는 번호를 `0`으로 표기하기로 하고, 민우가 구매한 로또 번호 6개가 `44, 1, 0, 0, 31 25`라고 가정해보겠습니다. 당첨 번호 6개가 `31, 10, 45, 1, 6, 19`라면, 당첨 가능한 최고 순위와 최저 순위의 한 예는 아래와 같습니다.

|당첨 번호|31|10|45|1|6|19|결과|
|---|---|---|---|---|---|---|---|
|최고 순위 번호|**31**|0→**10**|44|**1**|0→**6**|25|4개 번호 일치, 3등|
|최저 순위 번호|**31**|0→11|44|**1**|0→7|25|2개 번호 일치, 5등|

- 순서와 상관없이, 구매한 로또에 당첨 번호와 일치하는 번호가 있으면 맞힌 걸로 인정됩니다.
- 알아볼 수 없는 두 개의 번호를 각각 10, 6이라고 가정하면 3등에 당첨될 수 있습니다.
    - 3등을 만드는 다른 방법들도 존재합니다. 하지만, 2등 이상으로 만드는 것은 불가능합니다.
- 알아볼 수 없는 두 개의 번호를 각각 11, 7이라고 가정하면 5등에 당첨될 수 있습니다.
    - 5등을 만드는 다른 방법들도 존재합니다. 하지만, 6등(낙첨)으로 만드는 것은 불가능합니다.

민우가 구매한 로또 번호를 담은 배열 lottos, 당첨 번호를 담은 배열 win_nums가 매개변수로 주어집니다. 이때, 당첨 가능한 최고 순위와 최저 순위를 차례대로 배열에 담아서 return 하도록 solution 함수를 완성해주세요.

##### 제한사항

- lottos는 길이 6인 정수 배열입니다.
- lottos의 모든 원소는 0 이상 45 이하인 정수입니다.
    - 0은 알아볼 수 없는 숫자를 의미합니다.
    - 0을 제외한 다른 숫자들은 lottos에 2개 이상 담겨있지 않습니다.
    - lottos의 원소들은 정렬되어 있지 않을 수도 있습니다.
- win_nums은 길이 6인 정수 배열입니다.
- win_nums의 모든 원소는 1 이상 45 이하인 정수입니다.
    - win_nums에는 같은 숫자가 2개 이상 담겨있지 않습니다.
    - win_nums의 원소들은 정렬되어 있지 않을 수도 있습니다.

---

##### 입출력 예

| lottos                | win_nums                 | result |
| --------------------- | ------------------------ | ------ |
| [44, 1, 0, 0, 31, 25] | [31, 10, 45, 1, 6, 19]   | [3, 5] |
| [0, 0, 0, 0, 0, 0]    | [38, 19, 20, 40, 15, 25] | [1, 6] |
| [45, 4, 35, 20, 3, 9] | [20, 9, 3, 45, 4, 35]    | [1, 1] |

### 나의 풀이
```
function solution(keymap, targets) {
    let answer = [];
    let keymaps = keymap.join("")
    
    // 타겟키 문장 나누기
    for (let i = 0; i < targets.length; i++) {
        let count = 0
        
        // 타겟키에 해당하는 키 검사
        for (let j = 0; j < targets[i].length; j++) {
            let targetKey = (targets[i])[j]
            if (!keymaps.includes(targetKey)) {
                count = -1
                break
            }
            let onKeys = keymap.filter((el) => el.includes(targetKey))
            let minCount = 101
            for (let j =0; j < onKeys.length; j++) {
                if (onKeys[j].indexOf(targetKey) < minCount) {
                    minCount = onKeys[j].indexOf(targetKey)     
                }
            }
            count += minCount +1
        }
        answer.push(count)
    
    }
    
    return answer;
```


### 다른 풀이
```
function solution(keymap, targets) {
    const answer = [];
    const map = {}
    for (const items of keymap) {
        items.split('').map((item, index) => map[item] = (map[item] < index+1 ? map[item] : index+1))
    }
    for (const items of targets) {
        answer.push(items.split('').reduce((cur, item) => cur += map[item], 0) || -1)
    }
    return answer;
```
내가 푼 코드에는 targets키에 해당하는 키를 각각 keymap배열에 넣어서 확인했다. 하지만 다른 풀이방법으로는 각 키의 최소 클릭 값을 담은 map 객체를 만들고, targets키 값을 넣어 바로 확인하는 방법으로 풀었다.

코드 또한 for문과 if문을 반복하기 보다, 적절한 배열 함수와 for of문과 삼항연산자를 활용하여 더욱 깔끔하다. (더욱 직관적인가 ?)

**맵 객체 예시**
```
map = {
  A: 1,
  B: 1,
  C: 2,
  D: 5,
  E: 3,
  F: 4
}
```

## Lv. 1 둘만의 암호
### 문제
두 문자열 `s`와 `skip`, 그리고 자연수 `index`가 주어질 때, 다음 규칙에 따라 문자열을 만들려 합니다. 암호의 규칙은 다음과 같습니다.

- 문자열 `s`의 각 알파벳을 `index`만큼 뒤의 알파벳으로 바꿔줍니다.
- `index`만큼의 뒤의 알파벳이 `z`를 넘어갈 경우 다시 `a`로 돌아갑니다.
- `skip`에 있는 알파벳은 제외하고 건너뜁니다.

예를 들어 `s` = "aukks", `skip` = "wbqd", `index` = 5일 때, a에서 5만큼 뒤에 있는 알파벳은 f지만 [b, c, d, e, f]에서 'b'와 'd'는 `skip`에 포함되므로 세지 않습니다. 따라서 'b', 'd'를 제외하고 'a'에서 5만큼 뒤에 있는 알파벳은 [c, e, f, g, h] 순서에 의해 'h'가 됩니다. 나머지 "ukks" 또한 위 규칙대로 바꾸면 "appy"가 되며 결과는 "happy"가 됩니다.

두 문자열 `s`와 `skip`, 그리고 자연수 `index`가 매개변수로 주어질 때 위 규칙대로 `s`를 변환한 결과를 return하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 5 ≤ `s`의 길이 ≤ 50
- 1 ≤ `skip`의 길이 ≤ 10
- `s`와 `skip`은 알파벳 소문자로만 이루어져 있습니다.
    - `skip`에 포함되는 알파벳은 `s`에 포함되지 않습니다.
- 1 ≤ `index` ≤ 20

---

##### 입출력 예

| s       | skip   | index | result  |
| ------- | ------ | ----- | ------- |
| "aukks" | "wbqd" | 5     | "happy" |
### 나의 풀이
**로직**
문자열 값에 index만큼 더해주고, 다시 문자열로 변환해준다.
변환하는 과정 사이에 skip에 해당하는 문자가 있으면, 개수만큼 추가로 더 더해줌.

**코드 전개**
s와 skip을 unicode로 변환
skip의 값이 s부터 s + index값 사이에 해당하는 지 살펴본다.
해당하는 skip의 개수만큼 index를 더해준다.
값이 z를 넘어가면 -26 한다.
값을 문자로 변환해서 정답에 푸쉬한다.
정답을 반환한다.

이렇게 계산하니 코드도 너무 복잡하고, z를 넘어간 뒤 다시 a로 와서 skip문자를 계산하는걸 해결 못했다.

### 다른 풀이
```
function solution(s, skip, index) {
    let answer = []
    const alphabets = []
    
    // skip에 있는 알파벳을 제외한 알파벳 배열 생성
    for (let i = 97; i < 123; i++) {
        let alphabet = String.fromCharCode(i)
        if (!skip.includes(alphabet)) {
            alphabets.push(String.fromCharCode(i))            
        }
    }
    
    // 인덱스 값 더해서 알파벳 추가하기
    for (let i = 0; i < s.length; i++) {
        answer.push(alphabets[(alphabets.indexOf(s[i]) + index) % alphabets.length])
    }
    
    return answer.join("")
}
```

skip에 포함되는 알파벳은 s에 포함되지 않는 점이 키포인트였다.
skip 알파벳을 단순히 건너뛰면 되므로 skip알파벳을 제외한 알파벳 배열을 만들어준다. 그 뒤로 index만큼 더해주고, 배열 넘어가는 값을 컨트롤 하기 위해 alphabets.length로 나눈 나머지값을 인덱스로 넣어준다.

## Lv. 1 완주하지 못한 선수
### 문제
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.

##### 입출력 예

| participant                                       | completion                               | return   |
| ------------------------------------------------- | ---------------------------------------- | -------- |
| ["leo", "kiki", "eden"]                           | ["eden", "kiki"]                         | "leo"    |
| ["marina", "josipa", "nikola", "vinko", "filipa"] | ["josipa", "filipa", "marina", "nikola"] | "vinko"  |
| ["mislav", "stanko", "mislav", "ana"]             | ["stanko", "ana", "mislav"]              | "mislav" |



### 나의 풀이
```
function solution(participant, completion) {
    let answer = '';
    participant = participant.sort()
    completion = completion.sort()
    console.log(participant)
    console.log(completion)
    
    for (let i = 0; i < participant.length; i++) {
        if (participant[i] !== completion[i]) {
            return participant[i]
        }
    }
    
    
    
    return answer;
}
```

### 다른 풀이
```
function solution(participant, completion) {
    let map = new Map()
    
    for (let i = 0; i < participant.length; i++) {
        let a = participant[i]
        let b = completion[i]
        
        map.set(a, (map.get(a) || 0) + 1)
        map.set(b, (map.get(b) || 0) - 1)
        
    }
    
    for([k,v] of map) {
        if (v > 0) {
            return k
        }
    }
    
    return "error";
}

```

내가 풀었던 방법인 배열을 sort하고 요소를 하나씩 비교하는 것 대신  map 객체를 활용하여 푸는 것이 시간 복잡도에서 훨씬 효율적이다.

## Lv. 1 체육복
### 문제
점심시간에 도둑이 들어, 일부 학생이 체육복을 도난당했습니다. 다행히 여벌 체육복이 있는 학생이 이들에게 체육복을 빌려주려 합니다. 학생들의 번호는 체격 순으로 매겨져 있어, 바로 앞번호의 학생이나 바로 뒷번호의 학생에게만 체육복을 빌려줄 수 있습니다. 예를 들어, 4번 학생은 3번 학생이나 5번 학생에게만 체육복을 빌려줄 수 있습니다. 체육복이 없으면 수업을 들을 수 없기 때문에 체육복을 적절히 빌려 최대한 많은 학생이 체육수업을 들어야 합니다.

전체 학생의 수 n, 체육복을 도난당한 학생들의 번호가 담긴 배열 lost, 여벌의 체육복을 가져온 학생들의 번호가 담긴 배열 reserve가 매개변수로 주어질 때, 체육수업을 들을 수 있는 학생의 최댓값을 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 전체 학생의 수는 2명 이상 30명 이하입니다.
- 체육복을 도난당한 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
- 여벌의 체육복을 가져온 학생의 수는 1명 이상 n명 이하이고 중복되는 번호는 없습니다.
- 여벌 체육복이 있는 학생만 다른 학생에게 체육복을 빌려줄 수 있습니다.
- 여벌 체육복을 가져온 학생이 체육복을 도난당했을 수 있습니다. 이때 이 학생은 체육복을 하나만 도난당했다고 가정하며, 남은 체육복이 하나이기에 다른 학생에게는 체육복을 빌려줄 수 없습니다.

##### 입출력 예

| n   | lost   | reserve   | return |
| --- | ------ | --------- | ------ |
| 5   | [2, 4] | [1, 3, 5] | 5      |
| 5   | [2, 4] | [3]       | 4      |
| 3   | [3]    | [1]       | 2      |
### 나의 풀이
```
function solution(n, lost, reserve) {
    let reserve2 = reserve.filter((e) => !lost.includes(e))
    lost.filter((e) => !reserve.includes(e)).sort((a,b) => a-b)
    let answer = n - lost.length;
    
    for (let i = 0; i < lost.length; i++) {
        if (reserve2.includes(lost[i] -1)) {
            reserve2 = reserve2.filter((e) => e !== lost[i] - 1)
            answer ++
        } else if (reserve2.includes(lost[i] + 1)) {
                reserve2 = reserve2.filter((e) => e !== lost[i] + 1)
                answer ++
            }
        }
    return answer
}
```

처음에 lost와 reserve 겹치는 부분을 제거하고 시작해야 하는데, for문 안에서 해결하려고 하다 보니 통과하지 못했다.

### 다른 풀이
```
function solution(n, lost, reserve) {
    let answer = 0;
    let students = new Array(n).fill(1)
    
    for (number of lost) {
        students[number-1] --
    }
    for (number of reserve) {
        students[number-1] ++
    }
    
    for(let i = 0; i < students.length; i++) {
        if (students[i] === 2) {
            if (students[i-1] === 0) {
                students[i-1] ++
            } else if (students[i+1] === 0) {
                students[i+1] ++
            }
        }
    }
    
    return students.filter((e) => e >= 1).length
}
```

같은 로직으로 학생들의 체육복 개수를 담은 배열을 만들어 해결.

## Lv. 1 숫자 짝꿍
### 문제
두 정수 `X`, `Y`의 임의의 자리에서 공통으로 나타나는 정수 k(0 ≤ k ≤ 9)들을 이용하여 만들 수 있는 가장 큰 정수를 두 수의 짝꿍이라 합니다(단, 공통으로 나타나는 정수 중 서로 짝지을 수 있는 숫자만 사용합니다). `X`, `Y`의 짝꿍이 존재하지 않으면, 짝꿍은 -1입니다. `X`, `Y`의 짝꿍이 0으로만 구성되어 있다면, 짝꿍은 0입니다.

예를 들어, `X` = 3403이고 `Y` = 13203이라면, `X`와 `Y`의 짝꿍은 `X`와 `Y`에서 공통으로 나타나는 3, 0, 3으로 만들 수 있는 가장 큰 정수인 330입니다. 다른 예시로 `X` = 5525이고 `Y` = 1255이면 `X`와 `Y`의 짝꿍은 `X`와 `Y`에서 공통으로 나타나는 2, 5, 5로 만들 수 있는 가장 큰 정수인 552입니다(`X`에는 5가 3개, `Y`에는 5가 2개 나타나므로 남는 5 한 개는 짝 지을 수 없습니다.)  
두 정수 `X`, `Y`가 주어졌을 때, `X`, `Y`의 짝꿍을 return하는 solution 함수를 완성해주세요.

##### 제한사항

- 3 ≤ `X`, `Y`의 길이(자릿수) ≤ 3,000,000입니다.
- `X`, `Y`는 0으로 시작하지 않습니다.
- `X`, `Y`의 짝꿍은 상당히 큰 정수일 수 있으므로, 문자열로 반환합니다.

---

##### 입출력 예

| X       | Y        | result |
| ------- | -------- | ------ |
| "100"   | "2345"   | "-1"   |
| "100"   | "203045" | "0"    |
| "100"   | "123450" | "10"   |
| "12321" | "42531"  | "321"  |
| "5525"  | "1255"   | "552"  |

### 나의 풀이
```
/*
X와 Y별로 포함된 숫자와 해당 숫자의 개수가 담긴 객체 생성
두 객체에 공통된 요소가 있을 경우, X와 Y중 적은 값만큼 [숫자,개수] 형태로 저장
숫자의 개수만큼 answer 배열에 추가
answer 길이가 0일경우 "-1" 반환
0만 있을 경우 0 반환
answer배열을 오름차순 정렬하고 join.
*/

function solution(X, Y) {
    let answer = []
    const mapX = new Map()
    const mapY = new Map()
    
    // 각 X,Y에 포함된 숫자와 개수를 담은 객체 생성
    for (let i = 0; i < X.length; i++ ) {
        mapX.set(X[i], (mapX.get(X[i]) || 0) + 1)
    }
    for (let i = 0; i < Y.length; i++ ) {
        mapY.set(Y[i], (mapY.get(Y[i]) || 0) + 1)
    }
    
    let numCounts = []

    // 두 개의 객체에서 공통된 숫자 찾아서 개수 반환
        for (item of mapX.keys()) {
            if (mapY.has(item)) {
              numCounts.push(mapX.get(item) < mapY.get(item)? [item,mapX.get(item)] : [item, mapY.get(item)] )
            }
        }
    
    // 공통된 숫자 없을 경우 "-1" 리턴
    if (numCounts.length < 1) {
        return "-1"
    }
    
    // 배열형태를 숫자의 개수만큼 반환
    for ([k,v] of numCounts) {
        for (let i = 0; i < v; i++) {
            answer.push(k)
        }
    }
    
    // 0만 있으면 "0" 반환
    if (answer.join("") * 1 === 0) {
        return "0"
    }
    
    return answer.sort((a,b) => b - a).join("")
```

### 코드 리팩토링
```
function solution(X, Y) {
    let answer = []
    const mapX = new Map()
    const mapY = new Map()
    
    for (let i = 0; i < X.length; i++ ) {
        mapX.set(X[i], (mapX.get(X[i]) || 0) + 1)
    }
    for (let i = 0; i < Y.length; i++ ) {
        mapY.set(Y[i], (mapY.get(Y[i]) || 0) + 1)
    }
    
    let result = []

	// 숫자 9부터 내려가면서 비교함으로써 오름차순 정렬 안해도 됨
        for (let digit = 9; digit >= 0; digit--) {
            const digitStr = String(digit)
            if (mapX.has(digitStr) && mapY.has(digitStr)) {
              const commonCount = Math.min(mapX.get(digitStr),mapY.get(digitStr))
				
			// 숫자의 개수만큼 for문으로 바로 추가해줌
              for (let i = 0; i < commonCount; i++) {
                  result.push(digitStr)
              }
            }
        }
    
    if (result.length < 1) {
        return "-1"
    }
    
    if (result[0] === "0") {
        return "0"
    }
    
    return result.join("")
}
```

### 다른 풀이
```
function solution(x, y){
  let answer = "";
  const xHash = new Map();
  const yHash = new Map();

  x.split("")
      .forEach(i=> xHash.set(i, xHash.has(i) ?  xHash.get(i)  +1 : 1));
  y.split("")
      .forEach(i=> yHash.set(i, yHash.has(i) ? yHash.get(i) +1 : 1));


    for(let i = 9; i >= 0; i --){
        const index = i.toString();
        if(!xHash.has(index)) continue;
        if(!yHash.has(index)) continue;

        const num = Math.min(xHash.get(index), yHash.get(index))
        answer += index.repeat(num)
    }
    if(answer.length === 0) return "-1"
    if(answer[0] === "0" ) return "0";
    return answer;
}
```
**x.split("")**
      **.forEach(i=> xHash.set(i, xHash.has(i) ?  xHash.get(i)  +1 : 1));**
      
- 해쉬를 채우는 방식을 X를 split하여 배열로 만들어 주고, forEach를 통해 더욱 깔끔하게 처리.

**if(!xHash.has(index)) continue;**
- 숫자 포함 여부를 비교하는 로직은 같지만, 숫자가 없는 경우 continue하는 예외처리를 통해 더욱 효율적이게 처리
- if문에서 대괄호를 사용하지 않고 한줄로 작성함으로써 가독성 높임

**answer += index.repeat(num)**
- answer에 숫자를 추가하는 형식을 for문이 아니라 repeat()를 사용하여 해당 횟수만큼 숫자를 더해줌.

## Lv. 1 햄버거 만들기
### 문제
햄버거 가게에서 일을 하는 상수는 햄버거를 포장하는 일을 합니다. 함께 일을 하는 다른 직원들이 햄버거에 들어갈 재료를 조리해 주면 조리된 순서대로 상수의 앞에 아래서부터 위로 쌓이게 되고, 상수는 순서에 맞게 쌓여서 완성된 햄버거를 따로 옮겨 포장을 하게 됩니다. 상수가 일하는 가게는 정해진 순서(아래서부터, 빵 – 야채 – 고기 - 빵)로 쌓인 햄버거만 포장을 합니다. 상수는 손이 굉장히 빠르기 때문에 상수가 포장하는 동안 속 재료가 추가적으로 들어오는 일은 없으며, 재료의 높이는 무시하여 재료가 높이 쌓여서 일이 힘들어지는 경우는 없습니다.

예를 들어, 상수의 앞에 쌓이는 재료의 순서가 [야채, 빵, 빵, 야채, 고기, 빵, 야채, 고기, 빵]일 때, 상수는 여섯 번째 재료가 쌓였을 때, 세 번째 재료부터 여섯 번째 재료를 이용하여 햄버거를 포장하고, 아홉 번째 재료가 쌓였을 때, 두 번째 재료와 일곱 번째 재료부터 아홉 번째 재료를 이용하여 햄버거를 포장합니다. 즉, 2개의 햄버거를 포장하게 됩니다.

상수에게 전해지는 재료의 정보를 나타내는 정수 배열 `ingredient`가 주어졌을 때, 상수가 포장하는 햄버거의 개수를 return 하도록 solution 함수를 완성하시오.

---

##### 제한사항

- 1 ≤ `ingredient`의 길이 ≤ 1,000,000
- `ingredient`의 원소는 1, 2, 3 중 하나의 값이며, 순서대로 빵, 야채, 고기를 의미합니다.

---

##### 입출력 예

| ingredient                  | result |
| --------------------------- | ------ |
| [2, 1, 1, 2, 3, 1, 2, 3, 1] | 2      |
| [1, 3, 2, 1, 2, 1, 3, 1, 2] | 0      |

### 나의 풀이
replace를 사용하여 푸니 시간복잡도가 너무 높게 나왔고, replaceAll을 사용하니, 햄버거를 완성하고 나면 다시 앞으로 가서 비교하는게 불가능했다.
햄버거가 완성되면 앞에있는 재료와 뒤에있는 재료 모두에 영향이 간다고 착각했는데, 햄버거 바로 앞 재료 1개만 영향을 받는다는 사실을 놓침.
한 번에 재료 전체를 비교하지 말고 재료를 한개씩 추가해서 해야 된다는 사실을 놓쳐서 풀지 못했다.

### 다른 풀이
```
function solution(ingredient) {
    let stk = [];
    let count = 0;
    for (let i = 0; i < ingredient.length; i++) {
        stk.push(ingredient[i]);
        if (
            stk[stk.length-1] === 1 &&
            stk[stk.length-2] === 3 &&
            stk[stk.length-3] === 2 &&
            stk[stk.length-4] === 1
        ) {
            count++;
            stk.splice(-4);
        }
    }
    return count;
}
```
스택을 통해 재료를 한 개씩 추가하고 비교.
크기가 큰 배열의 요소를 비교하는 경우 stack을 사용해야 한다는 사실을 잊지 말자.
## Lv. 1 크레인 인형뽑기 게임
### 문제
게임개발자인 "죠르디"는 크레인 인형뽑기 기계를 모바일 게임으로 만들려고 합니다.  
"죠르디"는 게임의 재미를 높이기 위해 화면 구성과 규칙을 다음과 같이 게임 로직에 반영하려고 합니다.

![crane_game_101.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/69f1cd36-09f4-4435-8363-b71a650f7448/crane_game_101.png)

게임 화면은 **"1 x 1"** 크기의 칸들로 이루어진 **"N x N"** 크기의 정사각 격자이며 위쪽에는 크레인이 있고 오른쪽에는 바구니가 있습니다. (위 그림은 "5 x 5" 크기의 예시입니다). 각 격자 칸에는 다양한 인형이 들어 있으며 인형이 없는 칸은 빈칸입니다. 모든 인형은 "1 x 1" 크기의 격자 한 칸을 차지하며 **격자의 가장 아래 칸부터 차곡차곡 쌓여 있습니다.** 게임 사용자는 크레인을 좌우로 움직여서 멈춘 위치에서 가장 위에 있는 인형을 집어 올릴 수 있습니다. 집어 올린 인형은 바구니에 쌓이게 되는 데, 이때 바구니의 가장 아래 칸부터 인형이 순서대로 쌓이게 됩니다. 다음 그림은 [1번, 5번, 3번] 위치에서 순서대로 인형을 집어 올려 바구니에 담은 모습입니다.

![crane_game_102.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/638e2162-b1e4-4bbb-b0d7-62d31e97d75c/crane_game_102.png)

만약 같은 모양의 인형 두 개가 바구니에 연속해서 쌓이게 되면 두 인형은 터뜨려지면서 바구니에서 사라지게 됩니다. 위 상태에서 이어서 [5번] 위치에서 인형을 집어 바구니에 쌓으면 같은 모양 인형 **두 개**가 없어집니다.

![crane_game_103.gif](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/8569d736-091e-4771-b2d3-7a6e95a20c22/crane_game_103.gif)

크레인 작동 시 인형이 집어지지 않는 경우는 없으나 만약 인형이 없는 곳에서 크레인을 작동시키는 경우에는 아무런 일도 일어나지 않습니다. 또한 바구니는 모든 인형이 들어갈 수 있을 만큼 충분히 크다고 가정합니다. (그림에서는 화면표시 제약으로 5칸만으로 표현하였음)

게임 화면의 격자의 상태가 담긴 2차원 배열 board와 인형을 집기 위해 크레인을 작동시킨 위치가 담긴 배열 moves가 매개변수로 주어질 때, 크레인을 모두 작동시킨 후 터트려져 사라진 인형의 개수를 return 하도록 solution 함수를 완성해주세요.

##### **[제한사항]**

- board 배열은 2차원 배열로 크기는 "5 x 5" 이상 "30 x 30" 이하입니다.
- board의 각 칸에는 0 이상 100 이하인 정수가 담겨있습니다.
    - 0은 빈 칸을 나타냅니다.
    - 1 ~ 100의 각 숫자는 각기 다른 인형의 모양을 의미하며 같은 숫자는 같은 모양의 인형을 나타냅니다.
- moves 배열의 크기는 1 이상 1,000 이하입니다.
- moves 배열 각 원소들의 값은 1 이상이며 board 배열의 가로 크기 이하인 자연수입니다.

##### **입출력 예**

|board|moves|result|
|---|---|---|
|[[0,0,0,0,0],[0,0,1,0,3],[0,2,5,0,1],[4,2,4,4,2],[3,5,1,3,1]]|[1,5,3,5,1,2,1,4]|4|
### 나의 풀이
```
/*
스택으로 해결하는 간단한 문제
각 칸마다 인형이 담긴 배열을 2차원 배열로 새로 만들어 준다.
크레인이 작동한 칸에서 shift해주고 바구니에 넣어준다.
바구니 마지막,마지막-1 비교해서 똑같으면 splice해준다.
moves.length만큼 반복
*/

function solution(board, moves) {
    let count = 0;
    let box = []
    let hashTable = []
    const length = board.length
    for (let i = 0; i <= length; i++) {
        hashTable.push([])
    }
    for (let i = 0; i < length; i++) {
        for (let j =0; j < length; j++) {
            let num = board[i][j]
            if (num !== 0) hashTable[j].push(num)
        }
    }
    
    for (let i = 0; i < moves.length; i++) {
        let target = (moves[i] - 1)
        let doll = hashTable[target][0]
        
        if (doll > 0 ) {
            box.push(doll)
            hashTable[target].shift()
         
        
            if (box[box.length - 1] === box[box.length - 2]) {
                box.splice(box.length -2)
                count += 2
            }
        }
    }
    
    return count;
}

```
처음에 board의 배열을 각 칸에 인형이 담긴 의미인줄 알고 잘못 풀었다.
board의 배열에서 0일 경우 다음 배열로 건너 뛰는 것보다, 각 칸마다 담긴 인형들을 넣은 배열을 만들고 푸는 것이 더욱 간단해 보여, 새로 hashTable 배열을 만들어 준 뒤 첫번째 요소(가장 위에있는 인형)을 뽑아서 box에 넣어준 뒤 비교.

## Lv. 1 키패드 누르기

### 문제
**문제 설명**
스마트폰 전화 키패드의 각 칸에 다음과 같이 숫자들이 적혀 있습니다.

![kakao_phone1.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/4b69a271-5f4a-4bf4-9ebf-6ebed5a02d8d/kakao_phone1.png)

이 전화 키패드에서 왼손과 오른손의 엄지손가락만을 이용해서 숫자만을 입력하려고 합니다.  
맨 처음 왼손 엄지손가락은 `*` 키패드에 오른손 엄지손가락은 `#` 키패드 위치에서 시작하며, 엄지손가락을 사용하는 규칙은 다음과 같습니다.

1. 엄지손가락은 상하좌우 4가지 방향으로만 이동할 수 있으며 키패드 이동 한 칸은 거리로 1에 해당합니다.
2. 왼쪽 열의 3개의 숫자 `1`, `4`, `7`을 입력할 때는 왼손 엄지손가락을 사용합니다.
3. 오른쪽 열의 3개의 숫자 `3`, `6`, `9`를 입력할 때는 오른손 엄지손가락을 사용합니다.
4. 가운데 열의 4개의 숫자 `2`, `5`, `8`, `0`을 입력할 때는 두 엄지손가락의 현재 키패드의 위치에서 더 가까운 엄지손가락을 사용합니다.  
    4-1. 만약 두 엄지손가락의 거리가 같다면, 오른손잡이는 오른손 엄지손가락, 왼손잡이는 왼손 엄지손가락을 사용합니다.

순서대로 누를 번호가 담긴 배열 numbers, 왼손잡이인지 오른손잡이인 지를 나타내는 문자열 hand가 매개변수로 주어질 때, 각 번호를 누른 엄지손가락이 왼손인 지 오른손인 지를 나타내는 연속된 문자열 형태로 return 하도록 solution 함수를 완성해주세요.

##### **[제한사항]**

- numbers 배열의 크기는 1 이상 1,000 이하입니다.
- numbers 배열 원소의 값은 0 이상 9 이하인 정수입니다.
- hand는 `"left"` 또는 `"right"` 입니다.
    - `"left"`는 왼손잡이, `"right"`는 오른손잡이를 의미합니다.
- 왼손 엄지손가락을 사용한 경우는 `L`, 오른손 엄지손가락을 사용한 경우는 `R`을 순서대로 이어붙여 문자열 형태로 return 해주세요.

---

##### **입출력 예**

|numbers|hand|result|
|---|---|---|
|[1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5]|`"right"`|`"LRLLLRLLRRL"`|
|[7, 0, 8, 2, 8, 3, 1, 5, 7, 6, 2]|`"left"`|`"LRLLRRLLLRR"`|
|[1, 2, 3, 4, 5, 6, 7, 8, 9, 0]|`"right"`|`"LLRLLRLLRL"`|

### 나의 풀이
```
function solution(numbers, hand) {
    let answer = '';
    const numTable = [
        [1,2,3],
        [4,5,6],
        [7,8,9],
        ["*",0,"#"]
    ]
    
    let indexL = [3,0]
    let indexR = [3,2]
    
    for (num of numbers) {
        let find = false
        
        for (let i=0;i<numTable.length;i++) {
            if (find === true) {
                break
            }
            
            for (let j=0;j<numTable[i].length;j++) {
                if (find === true) {
                    break
                }
                if (numTable[i][j] === num) {
                    if (num === 1 || num === 4 || num === 7) {
                        indexL[0] = i
                        indexL[1] = j
                        answer += "L"
                        find = true
                    } else if (num === 3 || num === 6 || num === 9) {
                        indexR[0] = i
                        indexR[1] = j
                        answer += "R"
                        find = true
                    } else {
                        let distanceL = Math.abs(indexL[0] - i) + Math.abs(indexL[1] - j)
                        let distanceR = Math.abs(indexR[0] - i) + Math.abs(indexR[1] - j)
                        
                        if (distanceL < distanceR) {
                            indexL[0] = i
                            indexL[1] = j
                            answer += "L"
                            find = true
                        } else if (distanceL > distanceR) {
                            indexR[0] = i
                            indexR[1] = j
                            answer += "R"
                            find = true
                        } else if (hand === "left"){
                            indexL[0] = i
                            indexL[1] = j
                            answer += "L"
                            find = true
                        } else {
                            indexR[0] = i
                            indexR[1] = j
                            answer += "R"
                            find = true
                        }
                    }
                }
            }
        }
    }
        
    return answer;
}
```
번호를 2차원 배열로 만들고 1,4,7 왼손 고정 3,6,9 오른손 고정. 2,5,8,0 일 경우 거리가 짧은 손으로 누르고 해당 좌표에 index 부여. 3중 for문으로 계산하기 떄문에, 배열을 순회하며 해당 번호를 찾을 경우 break를 통해 나머지 연산을 건너뛰어 다음 번호로 계산하게 끔 작성했다. 테스트코드 경우 해당 로직 유무에 따라 연산 시간이 최대 2초정도 차이남.

## Lv. 1 성격 유형 검사하기
### 문제

나만의 카카오 성격 유형 검사지를 만들려고 합니다.  
성격 유형 검사는 다음과 같은 4개 지표로 성격 유형을 구분합니다. 성격은 각 지표에서 두 유형 중 하나로 결정됩니다.

|지표 번호|성격 유형|
|---|---|
|1번 지표|라이언형(R), 튜브형(T)|
|2번 지표|콘형(C), 프로도형(F)|
|3번 지표|제이지형(J), 무지형(M)|
|4번 지표|어피치형(A), 네오형(N)|

4개의 지표가 있으므로 성격 유형은 총 16(=2 x 2 x 2 x 2)가지가 나올 수 있습니다. 예를 들어, "RFMN"이나 "TCMA"와 같은 성격 유형이 있습니다.

검사지에는 총 `n`개의 질문이 있고, 각 질문에는 아래와 같은 7개의 선택지가 있습니다.

- `매우 비동의`
- `비동의`
- `약간 비동의`
- `모르겠음`
- `약간 동의`
- `동의`
- `매우 동의`

각 질문은 1가지 지표로 성격 유형 점수를 판단합니다.

예를 들어, 어떤 한 질문에서 4번 지표로 아래 표처럼 점수를 매길 수 있습니다.

|선택지|성격 유형 점수|
|---|---|
|`매우 비동의`|네오형 3점|
|`비동의`|네오형 2점|
|`약간 비동의`|네오형 1점|
|`모르겠음`|어떤 성격 유형도 점수를 얻지 않습니다|
|`약간 동의`|어피치형 1점|
|`동의`|어피치형 2점|
|`매우 동의`|어피치형 3점|

이때 검사자가 질문에서 `약간 동의` 선택지를 선택할 경우 어피치형(A) 성격 유형 1점을 받게 됩니다. 만약 검사자가 `매우 비동의` 선택지를 선택할 경우 네오형(N) 성격 유형 3점을 받게 됩니다.

**위 예시처럼 네오형이 비동의, 어피치형이 동의인 경우만 주어지지 않고, 질문에 따라 네오형이 동의, 어피치형이 비동의인 경우도 주어질 수 있습니다.**  
하지만 각 선택지는 고정적인 크기의 점수를 가지고 있습니다.

- `매우 동의`나 `매우 비동의` 선택지를 선택하면 3점을 얻습니다.
- `동의`나 `비동의` 선택지를 선택하면 2점을 얻습니다.
- `약간 동의`나 `약간 비동의` 선택지를 선택하면 1점을 얻습니다.
- `모르겠음` 선택지를 선택하면 점수를 얻지 않습니다.

검사 결과는 모든 질문의 성격 유형 점수를 더하여 각 지표에서 더 높은 점수를 받은 성격 유형이 검사자의 성격 유형이라고 판단합니다. 단, 하나의 지표에서 각 성격 유형 점수가 같으면, 두 성격 유형 중 사전 순으로 빠른 성격 유형을 검사자의 성격 유형이라고 판단합니다.

질문마다 판단하는 지표를 담은 1차원 문자열 배열 `survey`와 검사자가 각 질문마다 선택한 선택지를 담은 1차원 정수 배열 `choices`가 매개변수로 주어집니다. 이때, 검사자의 성격 유형 검사 결과를 지표 번호 순서대로 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 1 ≤ `survey`의 길이 ( = `n`) ≤ 1,000
    - `survey`의 원소는 `"RT", "TR", "FC", "CF", "MJ", "JM", "AN", "NA"` 중 하나입니다.
    - `survey[i]`의 첫 번째 캐릭터는 i+1번 질문의 비동의 관련 선택지를 선택하면 받는 성격 유형을 의미합니다.
    - `survey[i]`의 두 번째 캐릭터는 i+1번 질문의 동의 관련 선택지를 선택하면 받는 성격 유형을 의미합니다.
- `choices`의 길이 = `survey`의 길이
    
    - `choices[i]`는 검사자가 선택한 i+1번째 질문의 선택지를 의미합니다.
    - 1 ≤ `choices`의 원소 ≤ 7
    
    |`choices`|뜻|
    |---|---|
    |1|매우 비동의|
    |2|비동의|
    |3|약간 비동의|
    |4|모르겠음|
    |5|약간 동의|
    |6|동의|
    |7|매우 동의|
    

---

##### 입출력 예

| survey                           | choices         | result   |
| -------------------------------- | --------------- | -------- |
| `["AN", "CF", "MJ", "RT", "NA"]` | [5, 3, 2, 7, 5] | `"TCMA"` |
| `["TR", "RT", "TR"]`             | [7, 1, 3]       | `"RCJA"` |


### 나의 풀이
```
/*
지표는 총 4가지
[
[R,T],
[C,F],
[J,M],
[A,N]
]
이 중 점수가 같은 경우 알파벳 사전순으로 우선 (R,C,J,A)
유형 2개를 묶어서 1,2,3일경우 앞 유형 "+". 5,6,7 일 경우 뒷 유형 "+". 4는 pass
*/
function solution(survey, choices) {
    let answer = '';
    const chars =  {
            "R" : 0,
            "T" : 0,
            "C" : 0,
            "F" : 0,
            "J" : 0,
            "M" : 0,
            "A" : 0,
            "N" : 0,
    }
    const charsMap = new Map(Object.entries(chars))
    const points = [false,3,2,1,0,1,2,3]
    let char = ""
    for (let i = 0; i < survey.length; i++) {
        let point = points[choices[i]]
        if (choices[i] < 4) {
            char = survey[i][0]
            charsMap.set(char, charsMap.get(char) + point)
        } else if (choices[i] > 4) {
            char = survey[i][1]
            charsMap.set(char, charsMap.get(char) + point)
        }
    }
    const entriesArray = Array.from(charsMap.entries());
    
    for (let i = 0; i <= 6; i+=2) {
        let [key,value] = entriesArray[i]
        let [key2,value2] = entriesArray[i+1]
        if (value > value2) {
            answer += key
        } else if (value < value2) {
            answer += key2
        } else {
            answer += key
        }
    }
    
    return answer;
}
```

### 다른 풀이
```
function solution(survey, choices) {
    const MBTI = {};
    const types = ["RT","CF","JM","AN"];

    types.forEach((type) =>
        type.split('').forEach((char) => MBTI[char] = 0)
    )

    choices.forEach((choice, index) => {
        const [disagree, agree] = survey[index];

        MBTI[choice > 4 ? agree : disagree] += Math.abs(choice - 4);
    });

    return types.map(([a, b]) => MBTI[b] > MBTI[a] ? b : a).join("");
}
```

내가 한 풀이는 객체를 통해 for문과 if문을 돌려 코드가 길어지고 가독성이 떨어짐. 다른 풀이는 forEach를 통해 반복하고 삼항연산자를 통해 더욱 깔끔하다.
점수를 더하는 로직도 따로 점수 배열을 만들지 않고 4를 뺴준 절대값이 해당 포인트인걸 활용해서 해결.

## Lv. 1 신규 아이디 추천
### 문제

카카오에 입사한 신입 개발자 `네오`는 "카카오계정개발팀"에 배치되어, 카카오 서비스에 가입하는 유저들의 아이디를 생성하는 업무를 담당하게 되었습니다. "네오"에게 주어진 첫 업무는 새로 가입하는 유저들이 카카오 아이디 규칙에 맞지 않는 아이디를 입력했을 때, 입력된 아이디와 유사하면서 규칙에 맞는 아이디를 추천해주는 프로그램을 개발하는 것입니다.  
다음은 카카오 아이디의 규칙입니다.

- 아이디의 길이는 3자 이상 15자 이하여야 합니다.
- 아이디는 알파벳 소문자, 숫자, 빼기(`-`), 밑줄(`_`), 마침표(`.`) 문자만 사용할 수 있습니다.
- 단, 마침표(`.`)는 처음과 끝에 사용할 수 없으며 또한 연속으로 사용할 수 없습니다.

"네오"는 다음과 같이 7단계의 순차적인 처리 과정을 통해 신규 유저가 입력한 아이디가 카카오 아이디 규칙에 맞는 지 검사하고 규칙에 맞지 않은 경우 규칙에 맞는 새로운 아이디를 추천해 주려고 합니다.  
신규 유저가 입력한 아이디가 `new_id` 라고 한다면,

```
1단계 new_id의 모든 대문자를 대응되는 소문자로 치환합니다.
2단계 new_id에서 알파벳 소문자, 숫자, 빼기(-), 밑줄(_), 마침표(.)를 제외한 모든 문자를 제거합니다.
3단계 new_id에서 마침표(.)가 2번 이상 연속된 부분을 하나의 마침표(.)로 치환합니다.
4단계 new_id에서 마침표(.)가 처음이나 끝에 위치한다면 제거합니다.
5단계 new_id가 빈 문자열이라면, new_id에 "a"를 대입합니다.
6단계 new_id의 길이가 16자 이상이면, new_id의 첫 15개의 문자를 제외한 나머지 문자들을 모두 제거합니다.
     만약 제거 후 마침표(.)가 new_id의 끝에 위치한다면 끝에 위치한 마침표(.) 문자를 제거합니다.
7단계 new_id의 길이가 2자 이하라면, new_id의 마지막 문자를 new_id의 길이가 3이 될 때까지 반복해서 끝에 붙입니다.
```

---

예를 들어, new_id 값이 "...!@BaT#*..y.abcdefghijklm" 라면, 위 7단계를 거치고 나면 new_id는 아래와 같이 변경됩니다.

1단계 대문자 'B'와 'T'가 소문자 'b'와 't'로 바뀌었습니다.  
`"...!@BaT#*..y.abcdefghijklm"` → `"...!@bat#*..y.abcdefghijklm"`

2단계 '!', '@', '#', '*' 문자가 제거되었습니다.  
`"...!@bat#*..y.abcdefghijklm"` → `"...bat..y.abcdefghijklm"`

3단계 '...'와 '..' 가 '.'로 바뀌었습니다.  
`"...bat..y.abcdefghijklm"` → `".bat.y.abcdefghijklm"`

4단계 아이디의 처음에 위치한 '.'가 제거되었습니다.  
`".bat.y.abcdefghijklm"` → `"bat.y.abcdefghijklm"`

5단계 아이디가 빈 문자열이 아니므로 변화가 없습니다.  
`"bat.y.abcdefghijklm"` → `"bat.y.abcdefghijklm"`

6단계 아이디의 길이가 16자 이상이므로, 처음 15자를 제외한 나머지 문자들이 제거되었습니다.  
`"bat.y.abcdefghijklm"` → `"bat.y.abcdefghi"`

7단계 아이디의 길이가 2자 이하가 아니므로 변화가 없습니다.  
`"bat.y.abcdefghi"` → `"bat.y.abcdefghi"`

따라서 신규 유저가 입력한 new_id가 "...!@BaT#*..y.abcdefghijklm"일 때, 네오의 프로그램이 추천하는 새로운 아이디는 "bat.y.abcdefghi" 입니다.

---

#### **[문제]**

신규 유저가 입력한 아이디를 나타내는 new_id가 매개변수로 주어질 때, "네오"가 설계한 7단계의 처리 과정을 거친 후의 추천 아이디를 return 하도록 solution 함수를 완성해 주세요.

#### **[제한사항]**

new_id는 길이 1 이상 1,000 이하인 문자열입니다.  
new_id는 알파벳 대문자, 알파벳 소문자, 숫자, 특수문자로 구성되어 있습니다.  
new_id에 나타날 수 있는 특수문자는 `-_.~!@#$%^&*()=+[{]}:?,<>/` 로 한정됩니다.

---

##### **[입출력 예]**

| no  | new_id                          | result              |
| --- | ------------------------------- | ------------------- |
| 예1  | `"...!@BaT#*..y.abcdefghijklm"` | `"bat.y.abcdefghi"` |
| 예2  | `"z-+.^."`                      | `"z--"`             |
| 예3  | `"=.="`                         | `"aaa"`             |
| 예4  | `"123_.def"`                    | `"123_.def"`        |
| 예5  | `"abcdefghijklmn.p"`            | `"abcdefghijklmn"`  |

--- 

**풀이 방법**
아이디 new_id를 받아 7가지 프로세스에 맞춰 아이디 변환
1. 대문자 -> 소문자 변환
2. [소문자, 숫자, -, _, .] 를 제외한 모든 문자 제거
3. "."가 2번이상 연속되면 하나로 치환
4. "."가 처음이나 끝에 위치하면 제거
5. 빈 문자열이면 "a" 대입
6. 16자 이상이면 15개 이후 문제 제거. 마지막에 "."오면 제거
7. 길이가 2 이하이면 마지막 문자를 3이 될 때 까지 반복


### 나의 풀이
```
function solution(new_id) {
    let answer = '';
    new_id = new_id.toLowerCase().split("").filter((el) => 
        el !== el.toUpperCase() ||
        isNaN(el) === false     ||
        el === "-"              ||
        el === "_"              ||
        el === "."              
    )
    
    for (let i = 0; i < new_id.length; i++) {
        if (new_id[i] + new_id[i+1] === "..") {
            new_id[i] = ""
        }
    }
    new_id = new_id.filter((el) => el !== "")
    
    new_id[new_id.length - 1] === "."  ? new_id.pop() : ""
    new_id[0] === "."  ? new_id.shift() : ""
    new_id.join("").length === 0 ? new_id.push("a") : ""
    while (new_id.length > 15) {
        new_id.pop()
    }
    new_id[new_id.length-1] === "."  ? new_id.pop() : ""
    while (new_id.length < 3) {
        new_id.push(new_id[new_id.length - 1])
    }
    
    return new_id.join("");
}
```
조건에 맞춰서 분류하고 pop과 shift를 활용해 연산을 최소화 시켰다.

### 다른 풀이
```
const solution = (new_id) => {
    const id = new_id
        .toLowerCase()
        .replace(/[^\w\d-_.]/g, '')
        .replace(/\.{2,}/g, '.')
        .replace(/^\.|\.$/g, '')
        .padEnd(1, 'a')
        .slice(0, 15)
        .replace(/^\.|\.$/g, '')        
    return id.padEnd(3, id[id.length-1])
}
```
정규식을 활용하여 문자를 치환한 풀이

## Lv. 1 바탕화면 정리
### 문제

코딩테스트를 준비하는 머쓱이는 프로그래머스에서 문제를 풀고 나중에 다시 코드를 보면서 공부하려고 작성한 코드를 컴퓨터 바탕화면에 아무 위치에나 저장해 둡니다. 저장한 코드가 많아지면서 머쓱이는 본인의 컴퓨터 바탕화면이 너무 지저분하다고 생각했습니다. 프로그래머스에서 작성했던 코드는 그 문제에 가서 다시 볼 수 있기 때문에 저장해 둔 파일들을 전부 삭제하기로 했습니다.

컴퓨터 바탕화면은 각 칸이 정사각형인 격자판입니다. 이때 컴퓨터 바탕화면의 상태를 나타낸 문자열 배열 `wallpaper`가 주어집니다. 파일들은 바탕화면의 격자칸에 위치하고 바탕화면의 격자점들은 바탕화면의 가장 왼쪽 위를 (0, 0)으로 시작해 (세로 좌표, 가로 좌표)로 표현합니다. 빈칸은 ".", 파일이 있는 칸은 "#"의 값을 가집니다. 드래그를 하면 파일들을 선택할 수 있고, 선택된 파일들을 삭제할 수 있습니다. 머쓱이는 최소한의 이동거리를 갖는 한 번의 드래그로 모든 파일을 선택해서 한 번에 지우려고 하며 드래그로 파일들을 선택하는 방법은 다음과 같습니다.

- 드래그는 바탕화면의 격자점 S(`lux`, `luy`)를 마우스 왼쪽 버튼으로 클릭한 상태로 격자점 E(`rdx`, `rdy`)로 이동한 뒤 마우스 왼쪽 버튼을 떼는 행동입니다. 이때, "**점 S에서 점 E로 드래그한다**"고 표현하고 점 S와 점 E를 각각 드래그의 시작점, 끝점이라고 표현합니다.
    
- 점 S(`lux`, `luy`)에서 점 E(`rdx`, `rdy`)로 드래그를 할 때, "**드래그 한 거리**"는 |`rdx` - `lux`| + |`rdy` - `luy`|로 정의합니다.
    
- 점 S에서 점 E로 드래그를 하면 바탕화면에서 두 격자점을 각각 왼쪽 위, 오른쪽 아래로 하는 직사각형 내부에 있는 모든 파일이 선택됩니다.
    

예를 들어 `wallpaper` = [".#...", "..#..", "...#."]인 바탕화면을 그림으로 나타내면 다음과 같습니다.  
![eg1.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/ec8b3f44-17e9-4044-8117-fad0f1f4402f/eg1.png)  
이러한 바탕화면에서 다음 그림과 같이 S(0, 1)에서 E(3, 4)로 드래그하면 세 개의 파일이 모두 선택되므로 드래그 한 거리 (3 - 0) + (4 - 1) = 6을 최솟값으로 모든 파일을 선택 가능합니다.  
![eg1-2.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/e69e8776-4e56-4abb-b2a7-3dc695620ef4/eg1-2.png)  
(0, 0)에서 (3, 5)로 드래그해도 모든 파일을 선택할 수 있지만 이때 드래그 한 거리는 (3 - 0) + (5 - 0) = 8이고 이전의 방법보다 거리가 늘어납니다.

머쓱이의 컴퓨터 바탕화면의 상태를 나타내는 문자열 배열 `wallpaper`가 매개변수로 주어질 때 바탕화면의 파일들을 한 번에 삭제하기 위해 최소한의 이동거리를 갖는 드래그의 시작점과 끝점을 담은 정수 배열을 return하는 `solution` 함수를 작성해 주세요. 드래그의 시작점이 (`lux`, `luy`), 끝점이 (`rdx`, `rdy`)라면 정수 배열 [`lux`, `luy`, `rdx`, `rdy`]를 return하면 됩니다.

---

#### 제한사항

- 1 ≤ `wallpaper`의 길이 ≤ 50
- 1 ≤ `wallpaper[i]`의 길이 ≤ 50
    - `wallpaper`의 모든 원소의 길이는 동일합니다.
- `wallpaper[i][j]`는 바탕화면에서 `i + 1`행 `j + 1`열에 해당하는 칸의 상태를 나타냅니다.
- `wallpaper[i][j]`는 "#" 또는 "."의 값만 가집니다.
- 바탕화면에는 적어도 하나의 파일이 있습니다.
- 드래그 시작점 (`lux`, `luy`)와 끝점 (`rdx`, `rdy`)는 `lux` < `rdx`, `luy` < `rdy`를 만족해야 합니다.

---

#### 입출력 예

| wallpaper                                                                                   | result       |
| ------------------------------------------------------------------------------------------- | ------------ |
| [".#...", "..#..", "...#."]                                                                 | [0, 1, 3, 4] |
| ["..........", ".....#....", "......##..", "...##.....", "....#....."]                      | [1, 3, 5, 8] |
| [".##...##.", "#..#.#..#", "#...#...#", ".#.....#.", "..#...#..", "...#.#...", "....#...."] | [0, 0, 7, 9] |
| ["..", "#."]                                                                                | [1, 0, 2, 1] |

--- 

**문제 정리**
바탕화면의 모든 파일들을 드래그할 수 있는 가장 작은 사각형의 왼쪽 위 좌표, 오른쪽 위 좌표 리턴.
즉, [[맨 좌측 파일의 y좌표, 최상단 파일의 x좌표], [맨 우측 파일의 y좌표 + 1, 최하단 파일의 y좌표 + 1]] 이다.

파일의 좌표는 1차원 배열안에 스트링으로 담겨있으며, 스트링이 행(row)을, 각 배열의 index가 열(col)을 담당한다.

### 나의 풀이
```
function solution(wallpaper) {
    let lengthX = wallpaper[0].length
    let lengthY = wallpaper.length
    let answer = [lengthY,lengthX,0,0];
    
    for (let i = 0; i < lengthY; i++) {
        for (let j = 0; j < lengthX; j++) {
            if (wallpaper[i][j] === "#") {
                i < answer[0] ? answer[0] = i : ""
                j < answer[1] ? answer[1] = j : ""
                i+1 > answer[2] ? answer[2] = i + 1 : ""
                j+1 > answer[3] ? answer[3] = j + 1 : ""
            }
        }
    }
    
    return answer;
}
```

시작점에서의 마우스 위치는 파일 위치의 최소값을 구해서 추가해주고, 끝점 마우스 위치는 파일을 넘어가므로 파일 위치의 최대값 + 1을 해준다.

## Lv. 1 개인정보 수집 유효기간
### 문제

고객의 약관 동의를 얻어서 수집된 1~`n`번으로 분류되는 개인정보 `n`개가 있습니다. 약관 종류는 여러 가지 있으며 각 약관마다 개인정보 보관 유효기간이 정해져 있습니다. 당신은 각 개인정보가 어떤 약관으로 수집됐는지 알고 있습니다. 수집된 개인정보는 유효기간 전까지만 보관 가능하며, 유효기간이 지났다면 반드시 파기해야 합니다.

예를 들어, A라는 약관의 유효기간이 12 달이고, 2021년 1월 5일에 수집된 개인정보가 A약관으로 수집되었다면 해당 개인정보는 2022년 1월 4일까지 보관 가능하며 2022년 1월 5일부터 파기해야 할 개인정보입니다.  
당신은 오늘 날짜로 파기해야 할 개인정보 번호들을 구하려 합니다.

**모든 달은 28일까지 있다고 가정합니다.**

다음은 오늘 날짜가 `2022.05.19`일 때의 예시입니다.

|약관 종류|유효기간|
|---|---|
|A|6 달|
|B|12 달|
|C|3 달|

|번호|개인정보 수집 일자|약관 종류|
|---|---|---|
|1|`2021.05.02`|A|
|2|`2021.07.01`|B|
|3|`2022.02.19`|C|
|4|`2022.02.20`|C|

- 첫 번째 개인정보는 A약관에 의해 2021년 11월 1일까지 보관 가능하며, 유효기간이 지났으므로 파기해야 할 개인정보입니다.
- 두 번째 개인정보는 B약관에 의해 2022년 6월 28일까지 보관 가능하며, 유효기간이 지나지 않았으므로 아직 보관 가능합니다.
- 세 번째 개인정보는 C약관에 의해 2022년 5월 18일까지 보관 가능하며, 유효기간이 지났으므로 파기해야 할 개인정보입니다.
- 네 번째 개인정보는 C약관에 의해 2022년 5월 19일까지 보관 가능하며, 유효기간이 지나지 않았으므로 아직 보관 가능합니다.

따라서 파기해야 할 개인정보 번호는 [1, 3]입니다.

오늘 날짜를 의미하는 문자열 `today`, 약관의 유효기간을 담은 1차원 문자열 배열 `terms`와 수집된 개인정보의 정보를 담은 1차원 문자열 배열 `privacies`가 매개변수로 주어집니다. 이때 파기해야 할 개인정보의 번호를 오름차순으로 1차원 정수 배열에 담아 return 하도록 solution 함수를 완성해 주세요.

---

##### 제한사항

- `today`는 "`YYYY`.`MM`.`DD`" 형태로 오늘 날짜를 나타냅니다.
- 1 ≤ `terms`의 길이 ≤ 20
    - `terms`의 원소는 "`약관 종류` `유효기간`" 형태의 `약관 종류`와 `유효기간`을 공백 하나로 구분한 문자열입니다.
    - `약관 종류`는 `A`~`Z`중 알파벳 대문자 하나이며, `terms` 배열에서 `약관 종류`는 중복되지 않습니다.
    - `유효기간`은 개인정보를 보관할 수 있는 달 수를 나타내는 정수이며, 1 이상 100 이하입니다.
- 1 ≤ `privacies`의 길이 ≤ 100
    - `privacies[i]`는 `i+1`번 개인정보의 수집 일자와 약관 종류를 나타냅니다.
    - `privacies`의 원소는 "`날짜` `약관 종류`" 형태의 `날짜`와 `약관 종류`를 공백 하나로 구분한 문자열입니다.
    - `날짜`는 "`YYYY`.`MM`.`DD`" 형태의 개인정보가 수집된 날짜를 나타내며, `today` 이전의 날짜만 주어집니다.
    - `privacies`의 `약관 종류`는 항상 `terms`에 나타난 `약관 종류`만 주어집니다.
- `today`와 `privacies`에 등장하는 `날짜`의 `YYYY`는 연도, `MM`은 월, `DD`는 일을 나타내며 점(`.`) 하나로 구분되어 있습니다.
    - 2000 ≤ `YYYY` ≤ 2022
    - 1 ≤ `MM` ≤ 12
    - `MM`이 한 자릿수인 경우 앞에 0이 붙습니다.
    - 1 ≤ `DD` ≤ 28
    - `DD`가 한 자릿수인 경우 앞에 0이 붙습니다.
- 파기해야 할 개인정보가 하나 이상 존재하는 입력만 주어집니다.

---

##### 입출력 예

| today          | terms                    | privacies                                                                          | result    |
| -------------- | ------------------------ | ---------------------------------------------------------------------------------- | --------- |
| `"2022.05.19"` | `["A 6", "B 12", "C 3"]` | `["2021.05.02 A", "2021.07.01 B", "2022.02.19 C", "2022.02.20 C"]`                 | [1, 3]    |
| `"2020.01.01"` | `["Z 3", "D 5"]`         | `["2019.01.01 D", "2019.11.15 Z", "2019.08.02 D", "2019.07.01 D", "2018.12.28 Z"]` | [1, 4, 5] |

--- 

**풀이 방법**
약관 시작날짜와 약관이 담긴 배열을 받아, 시작날짜에 약관의 개월을 더해 today를 지나면 해당 요소의 index를 answer에 추가.
만료 날짜는 시작날짜 -1 이며 0이 될 시 전 달의 마지막 날짜인 28일이 된다.
개월수가 12를 초과하면 년도를 +1하고 1월부터 시작.
각 년,월,일의 끝자리 index정보
연도 = 3
월 = 6
날짜 = 9
약관 = 11
2중 for문으로 privacies와 terms의 요소를 반복시킨다.

### 나의 풀이
```
function solution(today, terms, privacies) {
    let answer = [];
    let todayDate = 
        parseInt(today.slice(2,4) + today.slice(5,7) + today.slice(8,10))
    
    for (let i = 0; i < privacies.length; i++) {
        let year = parseInt(privacies[i].slice(2,4))
        let month = parseInt(privacies[i].slice(5,7))
        let date = parseInt(privacies[i].slice(8,10)) - 1
        let type = privacies[i][11]
        if (date === 0) {
            month -= 1
            date = 28
            if (month === 0) {
                year -= 1
                month = 12
            }
        }
        for (let j = 0; j < terms.length; j++) {
            if (type === terms[j][0]) {
                month += parseInt(terms[j].slice(2,5))
                if (month > 12) {
                    year += Math.floor(month / 12)
                    month = month % 12
                    if (month === 0) {
                        year --
                        month = 12
                    }
                }
                month < 10 ? month = "0" + month.toString() : month = month.toString()
                date < 10 ? date = "0" + date.toString() : date = date.toString()
                let dueDate = parseInt(year.toString() + month + date)
                if (dueDate < todayDate) {
                answer.push(i+1)
                }
                break
            }
            
        }
    }
    return answer;
}
```
날짜를 따로 변경하지 않고 비교만 하면 되므로, slice를 통해 날짜 변수를 만들어줌. 반드시 1개월 이상은 가므로, 만료 날짜는 하루 이전까지인 것을 이용해 먼저 하루씩 빼준다. 그리고 숫자로 변환시켜 준 뒤 개월수를 더해서 today날짜와 크기 비교.

다 작성하고 보니, 마지막에 대소 비교할 때 "<" 대신 "<="로 비교하면, 처음에 하루씩 빼주지 않아도 된다.

### 다른 풀이
```
unction solution(today, terms, privacies) {
  var answer = [];
  var [year, month, date] = today.split(".").map(Number);
  var todates = year * 12 * 28 + month * 28 + date;
  var t = {};
  terms.forEach((e) => {
    let [a, b] = e.split(" ");
    t[a] = Number(b);
  });
  privacies.forEach((e, i) => {
    var [day, term] = e.split(" ");
    day = day.split(".").map(Number);
    var dates = day[0] * 12 * 28 + day[1] * 28 + day[2] + t[term] * 28;
    if (dates <= todates) answer.push(i + 1);
  });
  return answer;
}
```
변수를 하나씩 정의하지 않고, 배열로 묶은 뒤 split과 map을 통해 채워줌으로써 코드가 짧아지고 가독성이 더 좋아짐.
또한, for문보다 forEach를 통해 배열을 반복시킴으로써 가독성 증가.

## Lv. 1 달리기 경주
### 문제
###### 문제 설명

얀에서는 매년 달리기 경주가 열립니다. 해설진들은 선수들이 자기 바로 앞의 선수를 추월할 때 추월한 선수의 이름을 부릅니다. 예를 들어 1등부터 3등까지 "mumu", "soe", "poe" 선수들이 순서대로 달리고 있을 때, 해설진이 "soe"선수를 불렀다면 2등인 "soe" 선수가 1등인 "mumu" 선수를 추월했다는 것입니다. 즉 "soe" 선수가 1등, "mumu" 선수가 2등으로 바뀝니다.

선수들의 이름이 1등부터 현재 등수 순서대로 담긴 문자열 배열 `players`와 해설진이 부른 이름을 담은 문자열 배열 `callings`가 매개변수로 주어질 때, 경주가 끝났을 때 선수들의 이름을 1등부터 등수 순서대로 배열에 담아 return 하는 solution 함수를 완성해주세요.

---

##### 제한사항

- 5 ≤ `players`의 길이 ≤ 50,000
    - `players[i]`는 i번째 선수의 이름을 의미합니다.
    - `players`의 원소들은 알파벳 소문자로만 이루어져 있습니다.
    - `players`에는 중복된 값이 들어가 있지 않습니다.
    - 3 ≤ `players[i]`의 길이 ≤ 10
- 2 ≤ `callings`의 길이 ≤ 1,000,000
    - `callings`는 `players`의 원소들로만 이루어져 있습니다.
    - 경주 진행중 1등인 선수의 이름은 불리지 않습니다.

---

##### 입출력 예

| players                               | callings                       | result                                |
| ------------------------------------- | ------------------------------ | ------------------------------------- |
| ["mumu", "soe", "poe", "kai", "mine"] | ["kai", "kai", "mine", "mine"] | ["mumu", "kai", "mine", "soe", "poe"] |


### 나의 풀이
```
/*
players의 이름과 인덱스를 담은 객체를 만들고, callings로 호출될 때마다 인덱스 값을 -1 해주고 원래 자리에 있던 플레이어의 인덱스를 +1 해준다.
*/

function solution(players, callings) {
    let playersObj = {}
    for (let i = 0; i < players.length; i++) {
        playersObj[players[i]] = i
    }
    
    for (call of callings) {
        let idx = playersObj[call]
        players[idx] = players[idx-1]
        players[idx-1] = call
        
        playersObj[call] --
        playersObj[players[idx]] ++
    }
    return players
}
```
처음에 playersObj를 등수에 맞춰서 다시 배열하려고 했지만, 시간 초과로 해결이 되지 않았다. playersObj는 이름과 등수를 저장하는 용도로만 쓰고, players배열의 순서를 바꿔주어 해결. 등수를 바꾼 후에 playersObj를 업데이트하여 정보 저장했다.

추가로 players객체를 만드는 과정을 forEach를 통해 작업하여 좀 더 효율적으로 동작할 수 있다.


### 코드 수정
```
function solution(players, callings) {
    let playersObj = {}
    
    players.forEach((player,idx) => playersObj[player] = idx)
    
    for (call of callings) {
        let idx = playersObj[call]
        players[idx] = players[idx-1]
        players[idx-1] = playersObj[idx]
        
        playersObj[call] --
        playersObj[players[idx]] ++
    }
    return players
}
```

## Lv. 1 공원 산책
### 문제
지나다니는 길을 'O', 장애물을 'X'로 나타낸 직사각형 격자 모양의 공원에서 로봇 강아지가 산책을 하려합니다. 산책은 로봇 강아지에 미리 입력된 명령에 따라 진행하며, 명령은 다음과 같은 형식으로 주어집니다.

- ["방향 거리", "방향 거리" … ]

예를 들어 "E 5"는 로봇 강아지가 현재 위치에서 동쪽으로 5칸 이동했다는 의미입니다. 로봇 강아지는 명령을 수행하기 전에 다음 두 가지를 먼저 확인합니다.

- 주어진 방향으로 이동할 때 공원을 벗어나는지 확인합니다.
- 주어진 방향으로 이동 중 장애물을 만나는지 확인합니다.

위 두 가지중 어느 하나라도 해당된다면, 로봇 강아지는 해당 명령을 무시하고 다음 명령을 수행합니다.  
공원의 가로 길이가 W, 세로 길이가 H라고 할 때, 공원의 좌측 상단의 좌표는 (0, 0), 우측 하단의 좌표는 (H - 1, W - 1) 입니다.

![image](https://user-images.githubusercontent.com/62426665/217702316-1bd5d3ba-c1d7-4133-bfb5-36bdc85a08ba.png)

공원을 나타내는 문자열 배열 `park`, 로봇 강아지가 수행할 명령이 담긴 문자열 배열 `routes`가 매개변수로 주어질 때, 로봇 강아지가 모든 명령을 수행 후 놓인 위치를 [세로 방향 좌표, 가로 방향 좌표] 순으로 배열에 담아 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 3 ≤ `park`의 길이 ≤ 50
    - 3 ≤ `park[i]`의 길이 ≤ 50
        - `park[i]`는 다음 문자들로 이루어져 있으며 시작지점은 하나만 주어집니다.
            - S : 시작 지점
            - O : 이동 가능한 통로
            - X : 장애물
    - `park`는 직사각형 모양입니다.
- 1 ≤ `routes`의 길이 ≤ 50
    - `routes`의 각 원소는 로봇 강아지가 수행할 명령어를 나타냅니다.
    - 로봇 강아지는 `routes`의 첫 번째 원소부터 순서대로 명령을 수행합니다.
    - `routes`의 원소는 "op n"과 같은 구조로 이루어져 있으며, op는 이동할 방향, n은 이동할 칸의 수를 의미합니다.
        - op는 다음 네 가지중 하나로 이루어져 있습니다.
            - N : 북쪽으로 주어진 칸만큼 이동합니다.
            - S : 남쪽으로 주어진 칸만큼 이동합니다.
            - W : 서쪽으로 주어진 칸만큼 이동합니다.
            - E : 동쪽으로 주어진 칸만큼 이동합니다.
        - 1 ≤ n ≤ 9

---

##### 입출력 예

| park                      | routes              | result |
| ------------------------- | ------------------- | ------ |
| ["SOO","OOO","OOO"]       | ["E 2","S 2","W 1"] | [2,1]  |
| ["SOO","OXX","OOO"]       | ["E 2","S 2","W 1"] | [0,1]  |
| ["OSO","OOO","OXO","OOO"] | ["E 2","S 3","W 1"] | [0,0]  |

### 나의 풀이
```
function solution(park, routes) {
    let lengthW = park[0].length;
    let lengthH = park.length;
    let startPoint = park.join("").indexOf("S");
    let h = Math.floor(startPoint / park[0].length);
    let w = startPoint % park[0].length;

    for (let route of routes) {
        let move = true;
        let direction = route[0];
        let distance = parseInt(route.split(' ')[1]);  // 수정: 거리 부분을 제대로 파싱

        if(direction === 'E') {
            if (w + distance >= lengthW) continue;
            for(let i = 1; i <= distance; i++) {
                if (park[h][w + i] === "X") {  // 수정: 장애물 체크
                    move = false;
                    break;
                }
            }
            if (move) w += distance;
        }
        else if(direction === 'W') {
            if (w - distance < 0) continue;
            for(let i = 1; i <= distance; i++) {
                if (park[h][w - i] === "X") {  // 수정: 장애물 체크
                    move = false;
                    break;
                }
            }
            if (move) w -= distance;
        }
        else if(direction === 'S') {
            if (h + distance >= lengthH) continue;
            for(let i = 1; i <= distance; i++) {
                if (park[h + i][w] === "X") {  // 수정: 장애물 체크
                    move = false;
                    break;
                }
            }
            if (move) h += distance;
        } 
        else if(direction === 'N') {
            if(h - distance < 0) continue;
            for(let i = 1; i <= distance; i++) {
                if (park[h - i][w] === "X") {  // 수정: 장애물 체크
                    move = false;
                    break;
                }
            }
            if (move) h -= distance;
        }
    }

    return [h, w];
}

```
처음에 이동 거리가 2자리 수인 경우를 체크 못하고, 이동할 칸이 장애물일 경우 건너뛰는 게 아니라 O일경우 이동하는 걸로 했더니 장애물 파악에 어려움이 있었음.
**주어진 예제의 범위를 잘 확인할 것 !!**

### 다른 풀이
```
function solution(park, routes) {
    const height = park.length;
    const width = park[0].length;

    // 현재 위치 찾기
    let h, w;
    for (let i = 0; i < height; i++) {
        const start = park[i].indexOf('S');
        if (start !== -1) {
            h = i;
            w = start;
            break;
        }
    }

    // 이동 가능성 확인 함수
    function canMove(newH, newW) {
        if (newH < 0 || newH >= height || newW < 0 || newW >= width) return false;
        return park[newH][newW] !== 'X';
    }

    // 명령어 처리
    for (const route of routes) {
        const [direction, distStr] = route.split(' ');
        const distance = parseInt(distStr);
        let newH = h;
        let newW = w;

        for (let i = 1; i <= distance; i++) {
            if (direction === 'E') newW++;
            if (direction === 'W') newW--;
            if (direction === 'S') newH++;
            if (direction === 'N') newH--;

            if (!canMove(newH, newW)) {
                move = false;
                break;
            }
        }

        if (canMove(newH, newW)) {
            h = newH;
            w = newW;
        }
    }

    return [h, w];
}
```
routes를 인덱스로 나누는 것이 아니라 빈칸을 split으로 나누어 더욱 깔끔하게 분리 가능. 문제를 해결 하려면 어떤 단계가 필요한지 나누고, 단계에 따라 코드를 구성하자. 필요한 작업들을 한 곳에 몰아놓음으로써, 읽기도 더 좋고 더욱 효율적이다. 예시로 나의 코드에선 방향별로 나누어서 범위를 벗어나는지 확인하고, 장애물을 확인하고, 거리를 더해줬다. 위의 코드는 이동가능 여부 파악 함수를 만들고, 좌표를 더한 뒤 함수에 넣어줌으로써 판별이 되도록 로직이 분리되어 작성되었다.

## Lv. 1 신고 결과 받기
### 문제
##### 문제 설명

신입사원 무지는 게시판 불량 이용자를 신고하고 처리 결과를 메일로 발송하는 시스템을 개발하려 합니다. 무지가 개발하려는 시스템은 다음과 같습니다.

- 각 유저는 한 번에 한 명의 유저를 신고할 수 있습니다.
    - 신고 횟수에 제한은 없습니다. 서로 다른 유저를 계속해서 신고할 수 있습니다.
    - 한 유저를 여러 번 신고할 수도 있지만, 동일한 유저에 대한 신고 횟수는 1회로 처리됩니다.
- k번 이상 신고된 유저는 게시판 이용이 정지되며, 해당 유저를 신고한 모든 유저에게 정지 사실을 메일로 발송합니다.
    - 유저가 신고한 모든 내용을 취합하여 마지막에 한꺼번에 게시판 이용 정지를 시키면서 정지 메일을 발송합니다.

다음은 전체 유저 목록이 ["muzi", "frodo", "apeach", "neo"]이고, k = 2(즉, 2번 이상 신고당하면 이용 정지)인 경우의 예시입니다.

|유저 ID|유저가 신고한 ID|설명|
|---|---|---|
|"muzi"|"frodo"|"muzi"가 "frodo"를 신고했습니다.|
|"apeach"|"frodo"|"apeach"가 "frodo"를 신고했습니다.|
|"frodo"|"neo"|"frodo"가 "neo"를 신고했습니다.|
|"muzi"|"neo"|"muzi"가 "neo"를 신고했습니다.|
|"apeach"|"muzi"|"apeach"가 "muzi"를 신고했습니다.|

각 유저별로 신고당한 횟수는 다음과 같습니다.

|유저 ID|신고당한 횟수|
|---|---|
|"muzi"|1|
|"frodo"|2|
|"apeach"|0|
|"neo"|2|

위 예시에서는 2번 이상 신고당한 "frodo"와 "neo"의 게시판 이용이 정지됩니다. 이때, 각 유저별로 신고한 아이디와 정지된 아이디를 정리하면 다음과 같습니다.

|유저 ID|유저가 신고한 ID|정지된 ID|
|---|---|---|
|"muzi"|["frodo", "neo"]|["frodo", "neo"]|
|"frodo"|["neo"]|["neo"]|
|"apeach"|["muzi", "frodo"]|["frodo"]|
|"neo"|없음|없음|

따라서 "muzi"는 처리 결과 메일을 2회, "frodo"와 "apeach"는 각각 처리 결과 메일을 1회 받게 됩니다.

이용자의 ID가 담긴 문자열 배열 `id_list`, 각 이용자가 신고한 이용자의 ID 정보가 담긴 문자열 배열 `report`, 정지 기준이 되는 신고 횟수 `k`가 매개변수로 주어질 때, 각 유저별로 처리 결과 메일을 받은 횟수를 배열에 담아 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 2 ≤ `id_list`의 길이 ≤ 1,000
    - 1 ≤ `id_list`의 원소 길이 ≤ 10
    - `id_list`의 원소는 이용자의 id를 나타내는 문자열이며 알파벳 소문자로만 이루어져 있습니다.
    - `id_list`에는 같은 아이디가 중복해서 들어있지 않습니다.
- 1 ≤ `report`의 길이 ≤ 200,000
    - 3 ≤ `report`의 원소 길이 ≤ 21
    - `report`의 원소는 "이용자id 신고한id"형태의 문자열입니다.
    - 예를 들어 "muzi frodo"의 경우 "muzi"가 "frodo"를 신고했다는 의미입니다.
    - id는 알파벳 소문자로만 이루어져 있습니다.
    - 이용자id와 신고한id는 공백(스페이스)하나로 구분되어 있습니다.
    - 자기 자신을 신고하는 경우는 없습니다.
- 1 ≤ `k` ≤ 200, `k`는 자연수입니다.
- return 하는 배열은 `id_list`에 담긴 id 순서대로 각 유저가 받은 결과 메일 수를 담으면 됩니다.

---

##### 입출력 예

|id_list|report|k|result|
|---|---|---|---|
|`["muzi", "frodo", "apeach", "neo"]`|`["muzi frodo","apeach frodo","frodo neo","muzi neo","apeach muzi"]`|2|[2,1,1,0]|
|`["con", "ryan"]`|`["ryan con", "ryan con", "ryan con", "ryan con"]`|3|[0,0]|

---

문제 정리
유저의 ID목록 id_list와 신고 목록 report, 정지 기준 k가 주어진다.
유저별로 정지 완료 메일받은 횟수를 배열로 리턴하라.
id_list = id가 문자열로 순서대로 담겨있음.
report = 신고한 사람, 신고당한사람이 하나의 문자열로 묶여서 담겨있음.
한 유저당 같은 유저 신고는 1회만 가능.

풀이
{유저 : 신고한 유저들} 로 이루어진 객체 reportUsers를 만들고,
{유저 : 신고당한횟수} 로 이루어진 객체 reportCount를 만든다.
report를 순회하면서, 신고한 유저를 추가하고, 신고당한 횟수를 업데이트 해준다.
배열 순회가 모두 끝나면, 정지된 유저들로 이루어진 배열 suspendUsers를 만들고,
reportUsers객체에 유저별로 suspendUsers가 포함된만큼 개수를 카운트해서 result배열에 각각 추가해준다.

### 나의 풀이
```
function solution(id_list, report, k) {
    let result =[]
    const reportUsers = {}
    const reportCount = {}
    
    // 객체에 id추가
    id_list.forEach((el) => {
        reportUsers[el] = []
        reportCount[el] = 0
    })
    
    // 중복 신고 방지를 위한 report 배열 중복제거
    const newReport = [...new Set(report)]
    
    // 유저별 신고 유저 추가
    for (item of newReport) {
        let reported = item.split(" ")[1]
        reportUsers[item.split(" ")[0]].push(reported)
        reportCount[reported] ++
    }
    
    let suspendUsers = []
    // 정지된 유저 배열에 추가
    for (user of id_list) {
        if (reportCount[user] >= k) suspendUsers.push(user)
    }

	// 정지된 유저가 포함되어있으면 카운트 +1
    for (userName of id_list) {
        let count = 0
        for (suspendUser of suspendUsers) {
            let lastIndex = result.length - 1
            if (reportUsers[userName].includes(suspendUser))  {
                count ++
            }
        }
        result.push(count)
    }
    return result;
}
```
정지된 유저의 수를 세는 부분에서 다소소 비효율적임.

### 다른 풀이
```
function solution(id_list, report, k) {
    let reports = [...new Set(report)].map(a=>{return a.split(' ')});
    let counts = new Map();
    for (const bad of reports){
        counts.set(bad[1],counts.get(bad[1])+1||1)
    }
    let good = new Map();
    for(const report of reports){
        if(counts.get(report[1])>=k){
            good.set(report[0],good.get(report[0])+1||1)
        }
    }
    let answer = id_list.map(a=>good.get(a)||0)
    return answer;
}
```
전부 map 객체를 활용하였기 때문에, 시간 복잡도에서 유리하고 간결하다.
map객체에서 값을 추가하는 방법을 숙지하자 !!

**map객체를 통해 값 추가하기**
```
counts.set(bad[1], counts.get(bad[1]) + 1 ||| 1))
```
counts의 값이 존재하지 않으면 초기값으로 1을 넣어주고 값이 들어가 있으면 +1을 해줌.

## Lv. 1 붕대 감기

### 문제
어떤 게임에는 `붕대 감기`라는 기술이 있습니다.

`붕대 감기`는 `t`초 동안 붕대를 감으면서 1초마다 `x`만큼의 체력을 회복합니다. `t`초 연속으로 붕대를 감는 데 성공한다면 `y`만큼의 체력을 추가로 회복합니다. 게임 캐릭터에는 최대 체력이 존재해 현재 체력이 최대 체력보다 커지는 것은 불가능합니다.

기술을 쓰는 도중 몬스터에게 공격을 당하면 기술이 취소되고, 공격을 당하는 순간에는 체력을 회복할 수 없습니다. 몬스터에게 공격당해 기술이 취소당하거나 기술이 끝나면 그 즉시 `붕대 감기`를 다시 사용하며, 연속 성공 시간이 0으로 초기화됩니다.

몬스터의 공격을 받으면 정해진 피해량만큼 현재 체력이 줄어듭니다. 이때, 현재 체력이 0 이하가 되면 캐릭터가 죽으며 더 이상 체력을 회복할 수 없습니다.

당신은 `붕대감기` 기술의 정보, 캐릭터가 가진 최대 체력과 몬스터의 공격 패턴이 주어질 때 캐릭터가 끝까지 생존할 수 있는지 궁금합니다.

`붕대 감기` 기술의 시전 시간, 1초당 회복량, 추가 회복량을 담은 1차원 정수 배열 `bandage`와 최대 체력을 의미하는 정수 `health`, 몬스터의 공격 시간과 피해량을 담은 2차원 정수 배열 `attacks`가 매개변수로 주어집니다. 모든 공격이 끝난 직후 남은 체력을 return 하도록 solution 함수를 완성해 주세요. **만약 몬스터의 공격을 받고 캐릭터의 체력이 0 이하가 되어 죽는다면 -1을 return 해주세요.**

---

##### 제한사항

- `bandage`는 [`시전 시간`, `초당 회복량`, `추가 회복량`] 형태의 길이가 3인 정수 배열입니다.
    - 1 ≤ `시전 시간` = `t` ≤ 50
    - 1 ≤ `초당 회복량` = `x` ≤ 100
    - 1 ≤ `추가 회복량` = `y` ≤ 100
- 1 ≤ `health` ≤ 1,000
- 1 ≤ `attacks`의 길이 ≤ 100
    - `attacks[i]`는 [`공격 시간`, `피해량`] 형태의 길이가 2인 정수 배열입니다.
    - `attacks`는 `공격 시간`을 기준으로 오름차순 정렬된 상태입니다.
    - `attacks`의 `공격 시간`은 모두 다릅니다.
    - 1 ≤ `공격 시간` ≤ 1,000
    - 1 ≤ `피해량` ≤ 100

---

##### 입출력 예

|bandage|health|attacks|result|
|---|---|---|---|
|[5, 1, 5]|30|[[2, 10], [9, 15], [10, 5], [11, 5]]|5|
|[3, 2, 7]|20|[[1, 15], [5, 16], [8, 6]]|-1|
|[4, 2, 7]|20|[[1, 15], [5, 16], [8, 6]]|-1|
|[1, 1, 1]|5|[[1, 2], [3, 2]]|3|

---
배틀그라운드의 붕대를 떠올리게하는 문제다.
2차원 배열의 데이터정보를 순회하면서 숫자를 업데이트하기만 하면 되는 간단한 문제.


### 나의 풀이
```
/*
t = 붕대 감기 시전 시간
x = 초당 회복량
y = 붕대 감기 성공시 추가 회복량
bandage = [t, x, y]

attacks배열에 있는 몬스터의 공격을 모두 맞고 남은 체력 반환. 죽으면 -1 반환
attacks배열의 배열을 반복문으로 돌려서 해당 시간에 플레이어의 체력을 업데이트한다.
이전 공격의 시간과 현재 공격의 시간을 비교해, 추가 회복 여부를 판단해 플레이어의 체력을 올려주고
데미지를 통해 플레이어의 체력을 깎는다.

체력 회복 공식
공격 사이 시간 * x + (Math.floor(공격 사이 시간 / t) * y)
*/

function solution(bandage, health, attacks) {
    let maxHP = health;
    let prevAttack = 0
    for (let i = 0; i < attacks.length; i ++) { 
        let currAttack = attacks[i]
        let healTime = currAttack[0] - prevAttack - 1
        health += healTime * bandage[1] + (Math.floor(healTime / bandage[0]) * bandage[2])
        health > maxHP ? health = maxHP - currAttack[1] : health -= currAttack[1]
        prevAttack = currAttack[0]
        if (health <= 0) return -1
    }
    
    return health;
}
```


### 다른 풀이
```
function solution(bandage, health, attacks) {
  let currHealth = health;
  let currTime = 0;

  for (let [attackTime, damage] of attacks) {
    let diffTime = attackTime - currTime - 1;
    currHealth += diffTime * bandage[1] + Math.floor(diffTime / bandage[0]) * bandage[2];

    if (currHealth > health) currHealth = health;
    currHealth -= damage;
    if (currHealth <= 0) return -1;
    currTime = attackTime;
  }

  return currHealth;
}
```
for of로 한번에 attackTime과 damage를 담아 더욱 보기 편하다.

## Lv. 1 가장 많이 받은 선물
### 문제
선물을 직접 전하기 힘들 때 카카오톡 선물하기 기능을 이용해 축하 선물을 보낼 수 있습니다. 당신의 친구들이 이번 달까지 선물을 주고받은 기록을 바탕으로 다음 달에 누가 선물을 많이 받을지 예측하려고 합니다.

- 두 사람이 선물을 주고받은 기록이 있다면, 이번 달까지 두 사람 사이에 더 많은 선물을 준 사람이 다음 달에 선물을 하나 받습니다.
    - 예를 들어 `A`가 `B`에게 선물을 5번 줬고, `B`가 `A`에게 선물을 3번 줬다면 다음 달엔 `A`가 `B`에게 선물을 하나 받습니다.
- 두 사람이 선물을 주고받은 기록이 하나도 없거나 주고받은 수가 같다면, 선물 지수가 더 큰 사람이 선물 지수가 더 작은 사람에게 선물을 하나 받습니다.
    - 선물 지수는 이번 달까지 자신이 친구들에게 준 선물의 수에서 받은 선물의 수를 뺀 값입니다.
    - 예를 들어 `A`가 친구들에게 준 선물이 3개고 받은 선물이 10개라면 `A`의 선물 지수는 -7입니다. `B`가 친구들에게 준 선물이 3개고 받은 선물이 2개라면 `B`의 선물 지수는 1입니다. 만약 `A`와 `B`가 선물을 주고받은 적이 없거나 정확히 같은 수로 선물을 주고받았다면, 다음 달엔 `B`가 `A`에게 선물을 하나 받습니다.
    - **만약 두 사람의 선물 지수도 같다면 다음 달에 선물을 주고받지 않습니다.**

위에서 설명한 규칙대로 다음 달에 선물을 주고받을 때, 당신은 선물을 가장 많이 받을 친구가 받을 선물의 수를 알고 싶습니다.

친구들의 이름을 담은 1차원 문자열 배열 `friends` 이번 달까지 친구들이 주고받은 선물 기록을 담은 1차원 문자열 배열 `gifts`가 매개변수로 주어집니다. 이때, 다음달에 가장 많은 선물을 받는 친구가 받을 선물의 수를 return 하도록 solution 함수를 완성해 주세요.

---

##### 제한사항

- 2 ≤ `friends`의 길이 = 친구들의 수 ≤ 50
    - `friends`의 원소는 친구의 이름을 의미하는 알파벳 소문자로 이루어진 길이가 10 이하인 문자열입니다.
    - 이름이 같은 친구는 없습니다.
- 1 ≤ `gifts`의 길이 ≤ 10,000
    - `gifts`의 원소는 `"A B"`형태의 문자열입니다. `A`는 선물을 준 친구의 이름을 `B`는 선물을 받은 친구의 이름을 의미하며 공백 하나로 구분됩니다.
    - `A`와 `B`는 `friends`의 원소이며 `A`와 `B`가 같은 이름인 경우는 존재하지 않습니다.

---

##### 입출력 예

| friends                                         | gifts                                                                                                       | result |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ------ |
| ["muzi", "ryan", "frodo", "neo"]                | ["muzi frodo", "muzi frodo", "ryan muzi", "ryan muzi", "ryan muzi", "frodo muzi", "frodo ryan", "neo muzi"] | 2      |
| ["joy", "brad", "alessandro", "conan", "david"] | ["alessandro brad", "alessandro joy", "alessandro conan", "david alessandro", "alessandro david"]           | 4      |
| ["a", "b", "c"]                                 | ["a b", "b a", "c a", "a c", "a c", "c a"]                                                                  | 0      |

---

**문제**
friends배열 안에 있는 유저를 모두 두 사람씩 비교하여 선물을 많이 준 사람이 선물을 받는 시스템.
가장 선물을 많이 받은 사람이 몇개를 받았는지 숫자를 반환.
(승리 기준 : 두 사람 사이에 선물 더 많이 준사람, (모두에게 선물준 횟수 - 받은 선물)이 큰 사람 )

**풀이**
유저별로 자신이 선물을 준 사람 목록을 담은 객체 sendGifts에
유저의 index에 맞춰서 누구에게 선물을 몇개 주었는지 배열로 담아준다.
유저별 선물지수가 담긴 객체 giftPoint를 만들어준다(선물 주면 +1 받으면 -1).
friends를 2중 for문으로 순회하면서 result배열에 유저별로 받는 선물의 개수를 추가해준다.

### 나의 풀이
```
function solution(friends, gifts) {
    let result = new Array(friends.length).fill(0)
    const sendGifts = {}
    const giftPoint = {}
    const userIndex = {}
    
    friends.forEach((name,index) => {
        sendGifts[name] = new Array(friends.length).fill(0)
        giftPoint[name] = 0
        userIndex[name] = index
    })
    
    for (gift of gifts) {
        let sendUser = gift.split(" ")[0]
        let receiveUser = gift.split(" ")[1]
        sendGifts[sendUser][userIndex[receiveUser]] += 1
        giftPoint[sendUser] += 1
        giftPoint[receiveUser] -= 1
    }
    
    for (let i = 0; i < friends.length - 1; i++) {
        let currUser = friends[i]
        for (let j = i+1; j < friends.length; j++) {
            let nextUser = friends[j]
            if (sendGifts[currUser][j] === sendGifts[nextUser][i]) {
                if (giftPoint[currUser] > giftPoint[nextUser]) result[i] ++
                if (giftPoint[currUser] < giftPoint[nextUser]) result[j] ++
                continue
            }
            sendGifts[currUser][j] > sendGifts[nextUser][i] ? result[i] ++ : result[j] ++
            }
        }
    
    return Math.max(...result)
}
```
준 선물들을 저장하는 객체를 배열에 유저의 인덱스에 맞춰 저장하다 보니 다소 헷갈린다. 전체적으로 로직은 복잡하지 않음.

# 프로그래머스 Lv. 2
## Lv. 2 이진 변환 반복하기
### 문제
0과 1로 이루어진 어떤 문자열 x에 대한 이진 변환을 다음과 같이 정의합니다.

1. x의 모든 0을 제거합니다.
2. x의 길이를 c라고 하면, x를 "c를 2진법으로 표현한 문자열"로 바꿉니다.

예를 들어, `x = "0111010"`이라면, x에 이진 변환을 가하면 `x = "0111010" -> "1111" -> "100"` 이 됩니다.

0과 1로 이루어진 문자열 s가 매개변수로 주어집니다. s가 "1"이 될 때까지 계속해서 s에 이진 변환을 가했을 때, 이진 변환의 횟수와 변환 과정에서 제거된 모든 0의 개수를 각각 배열에 담아 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- s의 길이는 1 이상 150,000 이하입니다.
- s에는 '1'이 최소 하나 이상 포함되어 있습니다.

---

##### 입출력 예

| s                | result  |
| ---------------- | ------- |
| `"110010101001"` | `[3,8]` |
| `"01110"`        | `[3,3]` |
| `"1111111"`      | `[4,1]` |

---

### 나의 풀이
```
function solution(s) {
    let totalZero = 0
    let countOne = 0
    let countTry = 0
    
    while (countTry < 5) {
        for (num of s) {
            num === "0" ? totalZero ++ : countOne ++
        }
        s = countOne.toString(2)
        countOne = 0
        countTry ++
        if (s === "1") break
    }
    
    
    return [countTry,totalZero]
}
```

처음에 toString메서드의 존재를 몰라서 직접 이진변환 하기 위해 다음과 같이 풀었다.

**처음 풀이방법**
1. S를 배열로 변환 s.split("")
2. 배열에서 0을 제거하면서 0의 개수 카운팅
3. 남아있는 배열의 길이를 이진변환.
4. 3의 결과값 ex)[1,0,1,1]을 다시 2로 가져가서 반복.
--- 

이렇게 하다보니 이진변환 과정과, while문 처음으로 돌아가는 과정에서 오류가 나고 코드가 복잡해지는 문제가 생겼다.
이후 toString메서드를 사용해 풀었지만, countOne을 0으로 초기화 해주지 않아 문제가 발생했다.

**깨달은 점**
숫자를 누적시켜 저장하는 변수와, 반복문이 끝날 때 초기화 해주는 변수를 처음부터 확실하게 구분지어놓고 시작할 필요가 있다.
`EX)변수 이름에 total이 들어가면 누적, count가 들어가면 초기화 용도로 구분짓기`

## Lv. 2 피보나치 수

### 문제
피보나치 수는 F(0) = 0, F(1) = 1일 때, 1 이상의 n에 대하여 F(n) = F(n-1) + F(n-2) 가 적용되는 수 입니다.

예를들어

- F(2) = F(0) + F(1) = 0 + 1 = 1
- F(3) = F(1) + F(2) = 1 + 1 = 2
- F(4) = F(2) + F(3) = 1 + 2 = 3
- F(5) = F(3) + F(4) = 2 + 3 = 5

와 같이 이어집니다.

2 이상의 n이 입력되었을 때, n번째 피보나치 수를 1234567으로 나눈 나머지를 리턴하는 함수, solution을 완성해 주세요.

##### 제한 사항

- n은 2 이상 100,000 이하인 자연수입니다.

##### 입출력 예

| n   | return |
| --- | ------ |
| 3   | 2      |
| 5   | 5      |

---

### 나의 풀이
```
function solution(n) {
    let memory = []
    memory[0] = 0
    memory[1] = 1
    memory[2] = 1
    
    function fib(n) {
        if (memory[n]) {
            return (memory[n])
        } else {
            return memory[n] = fib(n-1) % 1234567 + fib(n-2) % 1234567
        }
    }
    return fib(n) % (1234567)
}
```

처음에 재귀함수를 통해 구현했더니 마지막 테스트 2개에서 런타임 에러가 발생했다. 

```
function solution(n) {
    let fib = [0, 1];
    
    for (let i = 2; i <= n; i++) {
        fib[i] = (fib[i - 1] + fib[i - 2]) % 1234567;
    }
    
    return fib[n];
}
```

반복문을 사용하니 정답처리가 되었다. 처음에 구현했던 재귀함수를 활용한 코드와 반복문을 활용한 코드 모두 시간 복잡도는 O(N)으로 동일하지만, 재귀함수를 활용한 코드에서 함수 호출이 많아지다 보니 스택 메모리를 초과해 스택 오버플로우가 발생한 것이 런타임 에러의 원인인 것 같다.

**배운 점**
자바스크립트에서는 파이썬과 달리 숫자 크기의 한계가 있기때문에 bigInt를 사용할 경우 또는, 위에서 1234567로 나눈 방법인 모듈러 연산을 적용할 필요가 있다는 것을 알게 되었다.

## Lv. 2 짝지어 제거하기
### 문제
짝지어 제거하기는, 알파벳 소문자로 이루어진 문자열을 가지고 시작합니다. 먼저 문자열에서 같은 알파벳이 2개 붙어 있는 짝을 찾습니다. 그다음, 그 둘을 제거한 뒤, 앞뒤로 문자열을 이어 붙입니다. 이 과정을 반복해서 문자열을 모두 제거한다면 짝지어 제거하기가 종료됩니다. 문자열 S가 주어졌을 때, 짝지어 제거하기를 성공적으로 수행할 수 있는지 반환하는 함수를 완성해 주세요. 성공적으로 수행할 수 있으면 1을, 아닐 경우 0을 리턴해주면 됩니다.

예를 들어, 문자열 S = `baabaa` 라면

b _aa_ baa → _bb_ aa → _aa_ →

의 순서로 문자열을 모두 제거할 수 있으므로 1을 반환합니다.

##### 제한사항

- 문자열의 길이 : 1,000,000이하의 자연수
- 문자열은 모두 소문자로 이루어져 있습니다.

---

##### 입출력 예

|s|result|
|---|---|
|baabaa|1|
|cdcd|0|

---


### 나의 풀이
```
function solution(s) {
    let stack = [s[0]]
    let currWord = ""
    
    for(let i = 1; i < s.length; i ++) {
        currWord = s[i]
        if (stack[stack.length-1] === currWord) {
            stack.pop()
        } else {
            stack.push(currWord)
        }
    }

    return stack.length < 1 ? 1 : 0
}
```

### 코드 리팩토링
```
function solution(s) {
    let stack = []
    let length = 0
    
    for(char of s) {
        length = stack.length
        if (length === 0 || stack[length - 1] !== char) {
            stack.push(char)
        } else {
            stack.pop()
        }
    }

    return stack.length < 1 ? 1 : 0
}
```

for of를 통해 가독성을 높이고 조건문을 개선하여 처음 stack배열에 문자를 채우지 않아도 된다.

## Lv. 2 카펫

### 문제
Leo는 카펫을 사러 갔다가 아래 그림과 같이 중앙에는 노란색으로 칠해져 있고 테두리 1줄은 갈색으로 칠해져 있는 격자 모양 카펫을 봤습니다.

![carpet.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/b1ebb809-f333-4df2-bc81-02682900dc2d/carpet.png)

Leo는 집으로 돌아와서 아까 본 카펫의 노란색과 갈색으로 색칠된 격자의 개수는 기억했지만, 전체 카펫의 크기는 기억하지 못했습니다.

Leo가 본 카펫에서 갈색 격자의 수 brown, 노란색 격자의 수 yellow가 매개변수로 주어질 때 카펫의 가로, 세로 크기를 순서대로 배열에 담아 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 갈색 격자의 수 brown은 8 이상 5,000 이하인 자연수입니다.
- 노란색 격자의 수 yellow는 1 이상 2,000,000 이하인 자연수입니다.
- 카펫의 가로 길이는 세로 길이와 같거나, 세로 길이보다 깁니다.

##### 입출력 예

| brown | yellow | return |
| ----- | ------ | ------ |
| 10    | 2      | [4, 3] |
| 8     | 1      | [3, 3] |
| 24    | 24     | [8, 6] |

---

### 나의 풀이
```
/*
격자 1칸의 넓이를 1이라고 가정하면, brown + yellow = 전체 넓이 가 되므로
가로길이 * 세로길이 = brown + yellow
(제한 사항. 가로 길이 >= 세로 길이)
중앙에 노란색 격자가 들어가야 하므로, 세로 길이는 > 3
brown과 yellow는 짝수이다 (yellow가 1이면 정답은 1가지. [3,3])


전체 가로,세로 길이는 노란격자의 가로길이 + 2, 세로길이 + 2 이므로
전체 사각형 네 변의 길이 총 합 - 4 (모서리에서 갈색 사각형 하나가 가로,세로를 1씩 담당하므로)
를 해주면 brown사각형의 개수가 나온다.

노란색 격자의 넓이로 만들 수 있는 [가로,세로]조합을 구하고,
(가로 + 2 * 2) + (세로 + 2 * 2) - 4 === brown 이면 정답.

조건을 총합하면
1. brown + yellow = w * h
2. brown = (w * 2) + (h * 2) - 4
3. yellow = (w - 2) * (h - 2)

*/
function solution(brown, yellow) {
    if (yellow === 1) return [3,3]
    
    let divisiors = []
    
    for(let i = 0; i <= Math.sqrt(yellow); i++) {
        if (yellow % i === 0) {
            divisiors.push([i, yellow / i])
        }
    }
    
    for (let i = divisiors.length - 1; i >= 0; i --) {
        let length = divisiors[i][0] + 2
        let width = divisiors[i][1] + 2
        if (length * width === brown + yellow &&
            (length * 2) + (width * 2) - 4 === brown) {
            return [width,length]
        }
    }
}
```

처음에 yellow의 약수를 구하는 부분에서 i의 범위를 i < Math.sqrt(yellow)로 설정하여, yellow가 제곱근인 케이스에서 오류가 발생했다.

### 다른 풀이
```
function solution(brown, yellow) {
    const totalArea = brown + yellow;
    let w, h;
    
    for (let i = 1; i <= Math.sqrt(totalArea); i++) {
        if (totalArea % i === 0) {
            w = totalArea / i;
            h = i;
            
            if ((w - 2) * (h - 2) === yellow) {
                break;
            }
        }
    }
    return [w, h];
}
```

노란색 사각형의 약수를 통해 계산하는 것이 아닌, 전체 면적의 제곱근까지 수를 반복시켜 0으로 나뉘어 떨어지는 값이 나오면, yellow = (w - 2) * (h - 2)에 대입해서 확인한다.
이렇게 풀게 되면, 약수를 일일이 저장할 필요도 없고 조건 판별도 훨씬 깔끔하다.
**정답의 조건들을 만족시키는 가장 효율적인 방법을 찾자.**

## Lv. 2 점프와 순간 이동
### 문제
OO 연구소는 한 번에 K 칸을 앞으로 점프하거나, (현재까지 온 거리) x 2 에 해당하는 위치로 순간이동을 할 수 있는 특수한 기능을 가진 아이언 슈트를 개발하여 판매하고 있습니다. 이 아이언 슈트는 건전지로 작동되는데, 순간이동을 하면 건전지 사용량이 줄지 않지만, 앞으로 K 칸을 점프하면 K 만큼의 건전지 사용량이 듭니다. 그러므로 아이언 슈트를 착용하고 이동할 때는 순간 이동을 하는 것이 더 효율적입니다. 아이언 슈트 구매자는 아이언 슈트를 착용하고 거리가 N 만큼 떨어져 있는 장소로 가려고 합니다. 단, 건전지 사용량을 줄이기 위해 점프로 이동하는 것은 최소로 하려고 합니다. 아이언 슈트 구매자가 이동하려는 거리 N이 주어졌을 때, 사용해야 하는 건전지 사용량의 최솟값을 return하는 solution 함수를 만들어 주세요.

예를 들어 거리가 5만큼 떨어져 있는 장소로 가려고 합니다.  
아이언 슈트를 입고 거리가 5만큼 떨어져 있는 장소로 갈 수 있는 경우의 수는 여러 가지입니다.

- 처음 위치 0 에서 5 칸을 앞으로 점프하면 바로 도착하지만, 건전지 사용량이 5 만큼 듭니다.
- 처음 위치 0 에서 2 칸을 앞으로 점프한 다음 순간이동 하면 (현재까지 온 거리 : 2) x 2에 해당하는 위치로 이동할 수 있으므로 위치 4로 이동합니다. 이때 1 칸을 앞으로 점프하면 도착하므로 건전지 사용량이 3 만큼 듭니다.
- 처음 위치 0 에서 1 칸을 앞으로 점프한 다음 순간이동 하면 (현재까지 온 거리 : 1) x 2에 해당하는 위치로 이동할 수 있으므로 위치 2로 이동됩니다. 이때 다시 순간이동 하면 (현재까지 온 거리 : 2) x 2 만큼 이동할 수 있으므로 위치 4로 이동합니다. 이때 1 칸을 앞으로 점프하면 도착하므로 건전지 사용량이 2 만큼 듭니다.

위의 3가지 경우 거리가 5만큼 떨어져 있는 장소로 가기 위해서 3번째 경우가 건전지 사용량이 가장 적으므로 답은 2가 됩니다.

##### 제한 사항

- 숫자 N: 1 이상 10억 이하의 자연수
- 숫자 K: 1 이상의 자연수

##### 입출력 예

|N|result|
|---|---|
|5|2|
|6|2|
|5000|5|

---

### 나의 풀이
```
/*
한번에 k칸 이동, 현재위치 x 2로 순간이동.
k칸은 k만큼 에너지 사용, 순간이동은 무제한.
N까지 이동할 때 사용하는 에너지의 최소값.

움직일지 순간이동할지 판단하는 조건.
무작정 순간이동하면 큰일남.
예를들어 목적지 5000일때 순간이동 남발하면, 4096에서 904에너지 써야됨.
순간마다 선택을 판단하는게 아니라, 순간이동할 포인트를 찾는 것이 중요.

풀이 방법
순간이동이 X 2만큼 이동하므로, 목적지부터 거꾸로 돌아오면서
순간이동이 가능하면(짝수) 나누기 2 순간이동이 불가하면(홀수) -1을 해준뒤 나누기 2를 한 뒤 에너지 1 더해줌.
*/

function solution(n) {
    let k = 0
    while (n >=1) {
        if (n % 2 === 0) {
            n = n / 2
        } else {
            n = (n-1) / 2
            k ++
        }
    }
    
    return k;
}
```


## Lv. 2 구명보트
### 문제
무인도에 갇힌 사람들을 구명보트를 이용하여 구출하려고 합니다. 구명보트는 작아서 한 번에 최대 **2명**씩 밖에 탈 수 없고, 무게 제한도 있습니다.

예를 들어, 사람들의 몸무게가 [70kg, 50kg, 80kg, 50kg]이고 구명보트의 무게 제한이 100kg이라면 2번째 사람과 4번째 사람은 같이 탈 수 있지만 1번째 사람과 3번째 사람의 무게의 합은 150kg이므로 구명보트의 무게 제한을 초과하여 같이 탈 수 없습니다.

구명보트를 최대한 적게 사용하여 모든 사람을 구출하려고 합니다.

사람들의 몸무게를 담은 배열 people과 구명보트의 무게 제한 limit가 매개변수로 주어질 때, 모든 사람을 구출하기 위해 필요한 구명보트 개수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 무인도에 갇힌 사람은 1명 이상 50,000명 이하입니다.
- 각 사람의 몸무게는 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 항상 사람들의 몸무게 중 최댓값보다 크게 주어지므로 사람들을 구출할 수 없는 경우는 없습니다.

##### 입출력 예

| people           | limit | return |
| ---------------- | ----- | ------ |
| [70, 50, 80, 50] | 100   | 3      |
| [70, 80, 50]     | 100   | 3      |

---

### 나의 풀이
```
/*
한번에 최대 2명밖에 탈 수 없으며 최대한 적은 수의 구명보트를 사용해 모든 사람을 태워라.

가장 가벼운 사람을 먼저 태우고, 남는 무게중에 가장 무거운 사람을 태워야 한다.
두 수의 합이 limit에 가장 가까우면 됨.
앞에서 태우고, 뒤에서 태우는데 같이 못타면 어차피 혼자타야되니까 pop후 +1
같이 탈 수 있으면 같이 태우기.
*/

function solution(people, limit) {
    let count = 0;
    let totalWeight = 0
    let length = people.length
    let index = 0
    
    people = people.sort((a,b) => a-b)
    
    for(let i = 0; i < length; i ++) {
        if (totalWeight === 0) {
            totalWeight += people[index]
            index ++
        } else if (totalWeight + people[people.length-1] <= limit) {
            people.pop()
            count += 1
            totalWeight = 0
        } else {
            people.pop()
            count += 1
        }
        
}
    return totalWeight === 0 ? count : count + 1
}
```

연산시간 비교 목적으로 pop대신 shift를 사용해봤더니 런타임 에러가 나왔다.
연산속도가 shift( )메서드가 pop( )과 연산속도가 똑같다고 알고 있었는데 알고보니, pop()은 뒤에서 요소를 제거하면 되기때문에 굉장히 빠른데에 반해, shift는 앞에서 요소를 제거하고 나머지 요소들을 한 칸씩 땡겨주어야 하기 때문에 오히려 array[index]로 지정하는 것보다도 연산이 더욱 느리다.

## Lv. 2 N개의 최소공배수

### 문제
두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

##### 제한 사항

- arr은 길이 1이상, 15이하인 배열입니다.
- arr의 원소는 100 이하인 자연수입니다.

##### 입출력 예

|arr|result|
|---|---|
|[2,6,8,14]|168|
|[1,2,3]|6|

---

### 나의 풀이
```
/*
숫자 N개의 최소 공배수를 구해라.
배열은 순회하면서 첫 번째 요소와 두 번째 요소의 최소 공배수를 구한 뒤 그 수를 변수 LCM에 저장한다.
LCM의 값과 세 번째 요소의 최소 공배수를 구하여 다시 LCM의 저장한다.
이걸 배열의 마지막 요소까지 반복.

두 수의 최소 공배수 구하는 방법
a * b / (a,b의 최대공약수)
*/

function solution(arr) {
    
    // 최대공약수 구하는 함수 (유클리드 호제법을 통해 구현)
    function gcd(a,b) {
         while (b !== 0) {
             let temp = b
             b = a % b
             a = temp
         }
        return a
    }
    
    let result = 0
    
    // 최소공배수 저장할 변수
    let lcm = arr[0]
    
    // 배열을 순회하면서 최소 공배수를 구함
    for (let i = 1; i < arr.length; i ++) {
        lcm = (lcm * arr[i]) / gcd(lcm,arr[i])
    }
    
    return lcm;
}
```

**a,b의 최소 공배수 = a * b / gcd(a, b)** 를 이용하여 배열의 각 수와 최소 공배수를 구하고, lcm에 저장해준 뒤 그 수를 배열의 다음 요소와 다시 비교.

최대 공약수를 구하는 계산은 **유클리드 호제법**을 통해 구현하였다.


#### 유클리드 호제법
**두 수의 최대 공약수(GCD)를 구하는 효율적인 알고리즘**

**원리**
- 두 정수 a와 b의 최대 공약수는 b와 **a mod b**(a를 b로 나눈 나머지) 의 최대 공약수와 같다.
- 즉, **GCD(a, b) = GCD(b, a mod b)**

**유도 과정**
- 두 수 a와 b가 있고 **a > b**라고 가정.
- a를 b로 나눈 나머지를 **r**, 몫을 **k**라고 한다면, **a = kb + r**
- a와 b의 공약수는 b와 r의 공약수와 같다.
- 따라서, **GCD(a, b) = GCD(b, r)**
- 이 과정을 **r(나머지)이 0이 될 때 까지 수행**. r이 0이 되는 순간, 그 때의 b가 두 수 a,b의 최대 공약수이다.


## Lv. 2 예상 대진표

### 문제
△△ 게임대회가 개최되었습니다. 이 대회는 N명이 참가하고, 토너먼트 형식으로 진행됩니다. N명의 참가자는 각각 1부터 N번을 차례대로 배정받습니다. 그리고, 1번↔2번, 3번↔4번, ... , N-1번↔N번의 참가자끼리 게임을 진행합니다. 각 게임에서 이긴 사람은 다음 라운드에 진출할 수 있습니다. 이때, 다음 라운드에 진출할 참가자의 번호는 다시 1번부터 N/2번을 차례대로 배정받습니다. 만약 1번↔2번 끼리 겨루는 게임에서 2번이 승리했다면 다음 라운드에서 1번을 부여받고, 3번↔4번에서 겨루는 게임에서 3번이 승리했다면 다음 라운드에서 2번을 부여받게 됩니다. 게임은 최종 한 명이 남을 때까지 진행됩니다.

이때, 처음 라운드에서 A번을 가진 참가자는 경쟁자로 생각하는 B번 참가자와 몇 번째 라운드에서 만나는지 궁금해졌습니다. 게임 참가자 수 N, 참가자 번호 A, 경쟁자 번호 B가 함수 solution의 매개변수로 주어질 때, 처음 라운드에서 A번을 가진 참가자는 경쟁자로 생각하는 B번 참가자와 몇 번째 라운드에서 만나는지 return 하는 solution 함수를 완성해 주세요. **단, A번 참가자와 B번 참가자는 서로 붙게 되기 전까지 항상 이긴다고 가정합니다.**

##### 제한사항

- N : 21 이상 220 이하인 자연수 (2의 지수 승으로 주어지므로 부전승은 발생하지 않습니다.)
- A, B : N 이하인 자연수 (단, A ≠ B 입니다.)

---

##### 입출력 예

|N|A|B|answer|
|---|---|---|---|
|8|4|7|3|

---

### 나의 풀이
```
/*
n명이서 토너먼트를 진행해서 a번의 참가자와 b번 참가자가 몇번째 라운드에서 만나는지 구해라.
(토너먼트 형식은 맨 앞부터 순서대로 2명씩 대결하여 승리하는 사람이 위 라운드로 진출하는 형식)

참가자가 속해있는 팀의 번호 teamNumber는 Math.floor(a+1 / 2)
승리 시 N은 N/2, teamNumber = (teamNumber + 1 / 2) + 1, count++
팀의 번호가 같아지면 count 반환
*/

function solution(n,a,b) {
    let count = 0
    for (let i = 0; i <= Math.sqrt(n); i++) {
        a = Math.floor((a+1) / 2)
        b = Math.floor((b+1) / 2)
        count ++
        if (a === b) {
            return count
        }
    }
}
```
참가자의 번호를 토대로 참가자가 속해있는 팀의 번호를 구성하여 풀었다.

## Lv. 2 멀리 뛰기
### 문제
효진이는 멀리 뛰기를 연습하고 있습니다. 효진이는 한번에 1칸, 또는 2칸을 뛸 수 있습니다. 칸이 총 4개 있을 때, 효진이는  
(1칸, 1칸, 1칸, 1칸)  
(1칸, 2칸, 1칸)  
(1칸, 1칸, 2칸)  
(2칸, 1칸, 1칸)  
(2칸, 2칸)  
의 5가지 방법으로 맨 끝 칸에 도달할 수 있습니다. 멀리뛰기에 사용될 칸의 수 n이 주어질 때, 효진이가 끝에 도달하는 방법이 몇 가지인지 알아내, 여기에 1234567를 나눈 나머지를 리턴하는 함수, solution을 완성하세요. 예를 들어 4가 입력된다면, 5를 return하면 됩니다.

##### 제한 사항

- n은 1 이상, 2000 이하인 정수입니다.

##### 입출력 예

|n|result|
|---|---|
|4|5|
|3|3|

##### 입출력 예 설명

---

### 나의 풀이
```
/*
n을 1과2의 합으로 만들 수 있는 조합의 개수

n(1) = 1
n(2) = 2
n(3) = 3
n(4) = 5
n(5) = 8

피보나치 수열과 동일하다
*/

function solution(n) {
    let dp = new Array(n+1)
    dp[0] = 0
    dp[1] = 1
    dp[2] = 2
    
    for (let i = 3; i <= n; i++) {
        dp[i] = (dp[i-1] + dp[i-2]) % 1234567
    }
    
    return dp[n];
}
```
피보나치 수열을 **동적 계획법**(Dynamic Programing)을 통해 **Botton-up**방식으로 구현했다.

## Lv. 2 영어 끝말잇기
### 문제
1부터 n까지 번호가 붙어있는 n명의 사람이 영어 끝말잇기를 하고 있습니다. 영어 끝말잇기는 다음과 같은 규칙으로 진행됩니다.

1. 1번부터 번호 순서대로 한 사람씩 차례대로 단어를 말합니다.
2. 마지막 사람이 단어를 말한 다음에는 다시 1번부터 시작합니다.
3. 앞사람이 말한 단어의 마지막 문자로 시작하는 단어를 말해야 합니다.
4. 이전에 등장했던 단어는 사용할 수 없습니다.
5. 한 글자인 단어는 인정되지 않습니다.

다음은 3명이 끝말잇기를 하는 상황을 나타냅니다.

tank → kick → know → wheel → land → dream → mother → robot → tank

위 끝말잇기는 다음과 같이 진행됩니다.

- 1번 사람이 자신의 첫 번째 차례에 tank를 말합니다.
- 2번 사람이 자신의 첫 번째 차례에 kick을 말합니다.
- 3번 사람이 자신의 첫 번째 차례에 know를 말합니다.
- 1번 사람이 자신의 두 번째 차례에 wheel을 말합니다.
- (계속 진행)

끝말잇기를 계속 진행해 나가다 보면, 3번 사람이 자신의 세 번째 차례에 말한 tank 라는 단어는 이전에 등장했던 단어이므로 탈락하게 됩니다.

사람의 수 n과 사람들이 순서대로 말한 단어 words 가 매개변수로 주어질 때, 가장 먼저 탈락하는 사람의 번호와 그 사람이 자신의 몇 번째 차례에 탈락하는지를 구해서 return 하도록 solution 함수를 완성해주세요.

##### 제한 사항

- 끝말잇기에 참여하는 사람의 수 n은 2 이상 10 이하의 자연수입니다.
- words는 끝말잇기에 사용한 단어들이 순서대로 들어있는 배열이며, 길이는 n 이상 100 이하입니다.
- 단어의 길이는 2 이상 50 이하입니다.
- 모든 단어는 알파벳 소문자로만 이루어져 있습니다.
- 끝말잇기에 사용되는 단어의 뜻(의미)은 신경 쓰지 않으셔도 됩니다.
- 정답은 [ 번호, 차례 ] 형태로 return 해주세요.
- 만약 주어진 단어들로 탈락자가 생기지 않는다면, [0, 0]을 return 해주세요.

---

##### 입출력 예

|n|words|result|
|---|---|---|
|3|["tank", "kick", "know", "wheel", "land", "dream", "mother", "robot", "tank"]|[3,3]|
|5|["hello", "observe", "effect", "take", "either", "recognize", "encourage", "ensure", "establish", "hang", "gather", "refer", "reference", "estimate", "executive"]|[0,0]|
|2|["hello", "one", "even", "never", "now", "world", "draw"]|[1,3]|

---

### 나의 풀이
```
/*
n명이 끝말잇기를 진행해서 가장 먼저 탈락하는 사람의 번호와 차례를 반환.

단어의 끝과 앞을 비교
단어가 이전 단어에 포함되어있는지 판별하고 push

게임에서 탈락시 index를 통해 차례와 순서를 계산.
*/

function solution(n, words) {
    let pastWords = [words[0]]
    let player = 0
    let turn = 0
    let lastChar = words[0][words[0].length-1]
    for (let i = 1; i < words.length; i ++) {
        let word = words[i]
        
        if (lastChar === word[0] && pastWords.includes(word) !== true) {
            lastChar = word[word.length-1]
            pastWords.push(word)
        } else {
            (i + 1) % n === 0 ? player = n : player = (i + 1) % n
            turn = Math.floor((i + n) / n)
            break
        }
    }
    return [player,turn]
}
```

이전 단어를 새로운 배열에 추가하면서 포함 여부 비교.

## Lv. 2 귤 고르기
### 문제
경화는 과수원에서 귤을 수확했습니다. 경화는 수확한 귤 중 'k'개를 골라 상자 하나에 담아 판매하려고 합니다. 그런데 수확한 귤의 크기가 일정하지 않아 보기에 좋지 않다고 생각한 경화는 귤을 크기별로 분류했을 때 서로 다른 종류의 수를 최소화하고 싶습니다.

예를 들어, 경화가 수확한 귤 8개의 크기가 [1, 3, 2, 5, 4, 5, 2, 3] 이라고 합시다. 경화가 귤 6개를 판매하고 싶다면, 크기가 1, 4인 귤을 제외한 여섯 개의 귤을 상자에 담으면, 귤의 크기의 종류가 2, 3, 5로 총 3가지가 되며 이때가 서로 다른 종류가 최소일 때입니다.

경화가 한 상자에 담으려는 귤의 개수 `k`와 귤의 크기를 담은 배열 `tangerine`이 매개변수로 주어집니다. 경화가 귤 k개를 고를 때 크기가 서로 다른 종류의 수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

---

##### 제한사항

- 1 ≤ `k` ≤ `tangerine`의 길이 ≤ 100,000
- 1 ≤ `tangerine`의 원소 ≤ 10,000,000

---

##### 입출력 예

|k|tangerine|result|
|---|---|---|
|6|[1, 3, 2, 5, 4, 5, 2, 3]|3|
|4|[1, 3, 2, 5, 4, 5, 2, 3]|2|
|2|[1, 1, 1, 1, 2, 2, 2, 3]|1|

---

### 나의 풀이
#### 첫 번째 풀이
```
/*
귤 k개를 고를 때 크기가 서로 다른 종류의 수의 최솟값 반환.

크기를 저장하는 배열을 생성해서, 배열의 index에 크기를 넣어 개수를 정리한다.
배열에서 0을 제거하고 내림차순으로 정렬하여 k에서 빼주면서 종류 수 count.
*/

function solution(k, tangerine) {
    let answer = 0;
    let quantity = new Array(Math.max(...tangerine) + 1).fill(0)
    
    for (let tanger of tangerine) {
        quantity[tanger] += 1
    }
    quantity = quantity.filter((el) => el >= 1).sort((a,b) => a-b)
    
    let count = 0
    while (k > 0) {
        count += 1
        k -= quantity.pop()
    }
    
    return count;
}
```

0으로 채워져있는 빈 배열을 생성해서 크기에 해당하는 index에 수량을 지정해준다.
수량을 저장한 배열에서 0을 제거해주고 정렬하여 비교.

**Issue**
효율성 관련하여 최대 200ms이상의 케이스가 다수 등장한다.

#### 두 번째 풀이
```
/*
귤 k개를 고를 때 크기가 서로 다른 종류의 수의 최솟값 반환.

같은 크기의 개수를 담을 sameCount 배열을 만들어 준다.
tangerine 배열을 정렬해서 이전 값과 현재 값이 같으면 sameCount배열의 마지막 값을 +1 해준다.
새로운 크기가 나타나면 배열에 1을 푸쉬해주고 lastIdx를 업데이트 해준다,
*/

function solution(k, tangerine) {
    let result = 0
    let sameCount = [1]
    tangerine.sort((a,b) => a-b)
    let lastItem = tangerine.pop()
    let length = tangerine.length
    let index = 0
    for (let i = 0 ; i < length ; i ++) {
        let currItem = tangerine.pop()
        if(lastItem === currItem) {
            sameCount[index] += 1
        } else {
            sameCount.push(1)
            index += 1
            lastItem = currItem
        }
    }
    sameCount.sort((a,b) => a-b)
    
    while (k > 0) {
        result += 1
        k -= sameCount.pop()
    }
    return result;
}
```

0으로 가득찬 새 배열을 만드는 것이 아니라, 같은 크기의 개수만 저장하는 배열을 새로 만들어주고, tangerine배열에서 pop으로 하나씩 제거해가며 비교.

**문제점**
효율성은 이전 코드보다 2배가량 좋아졌지만,
가독성이 떨어지고 변수가 너무 많아지는 문제가 발생한다.

#### 세 번째 풀이
```
/*
귤 k개를 고를 때 크기가 서로 다른 종류의 수의 최솟값 반환.

해시맵을 통해 귤의 크기와 빈도수를 담은 뒤에 value 값들을 배열에 담아 정렬한뒤 비교한다.
*/

function solution(k, tangerine) {
    let result = 0
    let frequency = new Map()
    
    for (let tanger of tangerine) {
        frequency.set(tanger, frequency.get(tanger) + 1 || 1)
    }
    let sortedFrequency = Array.from(frequency.values()).sort((a,b) => a-b)
    
    for (let item of sortedFrequency) {
        result ++
        k -= item
        if (k <= 0) break
    }
    return result;
}
```

해시맵을 통해 크기별 개수를 저장해주고, values를 통해 값들을 반환하고 배열로 만들어서 정렬해준다.

**가독성과 효율성 모두 증가**

**효율성**
세 번째 코드 > 두 번째 코드 >> 첫 번째 코드

## Lv. 2 연속 부분 수열 합의 개수
### 문제
철호는 수열을 가지고 놀기 좋아합니다. 어느 날 철호는 어떤 자연수로 이루어진 원형 수열의 연속하는 부분 수열의 합으로 만들 수 있는 수가 모두 몇 가지인지 알아보고 싶어졌습니다. 원형 수열이란 일반적인 수열에서 처음과 끝이 연결된 형태의 수열을 말합니다. 예를 들어 수열 [7, 9, 1, 1, 4] 로 원형 수열을 만들면 다음과 같습니다.  
![그림.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/f207cd37-34dc-4cbd-96bb-83435bd6efd4/%EA%B7%B8%EB%A6%BC.png)  
원형 수열은 처음과 끝이 연결되어 끊기는 부분이 없기 때문에 연속하는 부분 수열도 일반적인 수열보다 많아집니다.  
원형 수열의 모든 원소 `elements`가 순서대로 주어질 때, 원형 수열의 연속 부분 수열 합으로 만들 수 있는 수의 개수를 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 3 ≤ `elements`의 길이 ≤ 1,000
- 1 ≤ `elements`의 원소 ≤ 1,000

---

##### 입출력 예

| elements    | result |
| ----------- | ------ |
| [7,9,1,1,4] | 18     |

---

### 나의 풀이
```
/*
해당 배열을 원형 수열로 확장하기 위해 배열을 한 번 더 반복해준다.
배열을 잘라주면서 배열의 합을 계산해 set객체에 저장해준다.
*/

function solution(elements) {
    let answer = 0
    let circle = elements.concat(elements)
    let totalSum = new Set()
    
    for(let i = 1; i <= elements.length; i++) {
        let length = i
        for (let j = 0; j < elements.length; j++) {
            let subArray = circle.slice(j,j+length)
            totalSum.add(subArray.reduce((sum,el) => sum += el,0))
        }
    }
    return totalSum.size
}
```

i를 길이로 두고 길이 별로 배열을 분리해서 합계를 set객체에 저장해 주었다.
시간 복잡도가 최대 930ms로 간신히 통과되었다.
slice로 배열을 나누는 부분과, 객체에 추가할 때마다 reduce를 해주는 부분에서 시간을 많이 잡아먹는 듯 보인다.

### 다른 풀이
```
function solution(elements) {
    let circle = elements.concat(elements)
    let totalSum = new Set()
    
    for(let i = 0; i < elements.length; i++) {
        let sum = 0
        for (let j = 0; j < elements.length; j++) {
            sum += circle[i + j]
            totalSum.add(sum)
        }
    }
    return totalSum.size
}
```

첫 번째 풀이와 유사한 코드이지만, 시작지점부터 길이 1개, 2개, 3개 ... 최대 길이까지 모두 더해주고, 시작 지점을 한 칸 앞으로 이동해 다시 모두 더해준다. 더해줄 때마다 객체에 값을 추가해주고, 이전 값을 누적시켜 사용할 수 있기 때문에 훨씬 효율적이다.

## Lv. 2 괄호 회전하기
### 문제
다음 규칙을 지키는 문자열을 올바른 괄호 문자열이라고 정의합니다.

- `()`, `[]`, `{}` 는 모두 올바른 괄호 문자열입니다.
- 만약 `A`가 올바른 괄호 문자열이라면, `(A)`, `[A]`, `{A}` 도 올바른 괄호 문자열입니다. 예를 들어, `[]` 가 올바른 괄호 문자열이므로, `([])` 도 올바른 괄호 문자열입니다.
- 만약 `A`, `B`가 올바른 괄호 문자열이라면, `AB` 도 올바른 괄호 문자열입니다. 예를 들어, `{}` 와 `([])` 가 올바른 괄호 문자열이므로, `{}([])` 도 올바른 괄호 문자열입니다.

대괄호, 중괄호, 그리고 소괄호로 이루어진 문자열 `s`가 매개변수로 주어집니다. 이 `s`를 왼쪽으로 x (_0 ≤ x < (`s`의 길이)_) 칸만큼 회전시켰을 때 `s`가 올바른 괄호 문자열이 되게 하는 x의 개수를 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- s의 길이는 1 이상 1,000 이하입니다.

---

##### 입출력 예

| s          | result |
| ---------- | ------ |
| `"[](){}"` | 3      |
| `"}]()[{"` | 2      |
| `"[)(]"`   | 0      |
| `"}}}"`    | 0      |

### 나의 풀이
```
/*
괄호 문자열을 좌측으로 x칸 만큼 이동시켰을 때 올바른 괄호형식이 되는 경우의 수를 구하라

x의 최대 값은 s의 길이 -1

비교 로직
배열의 종류를 담은 객체를 만들고 시작하면 +1 끝나면 -1
*/
function solution(s) {
    let result = 0;
    
    const brackets = {
        small : 0,
        middle : 0,
        big : 0
    }
    s = s.split("")
    let lastOpen = []
    for (let i = 0; i < s.length; i ++ ) {
        for (item of s) {
            if(item === "[") {
                brackets.small += 1
                lastOpen.push("small")
            } else if(item === "(") {
              brackets.middle += 1
                lastOpen.push("middle")
                
            } else if(item === "{") {
              brackets.big += 1  
              lastOpen.push("big")
                
            } 
            
            else if(item === "]") {
                if (lastOpen.pop() !== "small") {
                    lastOpen = false
                    break
                }
                brackets.small -= 1
                
            } else if(item === ")") {
                if (lastOpen.pop() !== "middle") {
                    lastOpen = false
                    break
                }
                brackets.middle -= 1
                
            } else if(item === "}") {
                if (lastOpen.pop() !== "big") {
                    lastOpen = false
                    break
                }
                brackets.big -= 1
            }
            
            if (brackets.small < 0 || brackets.middle < 0 || brackets.big < 0) break
        }
        if (brackets.small === 0 && brackets.middle === 0 && brackets.big === 0 && lastOpen !== false) {
            result += 1
        }
        brackets.small = 0
        brackets.middle = 0
        brackets.big = 0
        lastOpen = []
        s.push(s.shift())
    }
    return result;
}
```

모든 조건을 하나씩 if문으로 설정해 풀긴 했지만, 가독성과 효율성이 너무 떨어지고, 비교 로직이 너무 복잡해 다시 재정립할 필요가 있다.

### 코드 리팩토링
```
function solution(s) {
    const closeMap = new Map ([
        [')', '('],
        ['}', '{'],
        [']', '[']
    ])
    
    let length = s.length
    s = s.split("")
    s = s.concat(s)
    
    let count = 0
    
    for (let i = 0; i < length; i ++) {
        let stack = []
        for(let j = i; j < length + i; j++) {
            if (closeMap.get(s[j])) {
                if (stack.length === 0 ||
                    stack.pop() !== closeMap.get(s[j])) { // pop을 통해 문자의 마지막을 제거함과 동시에 비교
                    stack = false
                    break
                }
            }
            else {
                stack.push(s[j])
            }
        }
        if (stack.length === 0) count += 1
    }
    return count;
}
```

괄호의 짝을 담은 `map객체`를 생성한 뒤에, 문자를 `stack` 배열에 담아서 비교한다.

여는 괄호일 경우 `stack`배열에 추가.
닫히는 괄호일 경우 stack의 마지막 값과 비교해 짝을 이룰 경우 `stack.pop( )`

괄호가 중첩되는 경우도 있는데 왜 마지막 값만 비교해줘도 되는지 의문이 생길 수 있다. 그 이유는, `{()}` 같이 괄호가 중첩된 구조 또한 열리는 괄호에서 `stack`에 차곡차곡 괄호를 쌓다가, 닫히는 괄호가 나오면 바로 이전 괄호와 비교를 통해 짝이 맞으면 `pop`을 통해 사라지므로, **stack의 마지막 문자만 비교하면 된다.**

**다음 예시를 통해 살펴보자.**
```
s = "{()}" // s의 문자열이 "{()}"일 경우 위의 코드에서 어떻게 작동하는지 살펴보자.
s.split("") // s = ["{", "(", ")", "}"]
const closeMap = new Map ([
        [')', '('],
        ['}', '{'],
        [']', '[']
    ])

// 코드는 위 코드 리팩토링 부분에 적혀있으므로 여기서는 생략하고 결과만 나타냄.

stack = ["{"] // "{"는 닫히는 괄호에 없으므로 stack에 추가

stack = ["{", "("] // "(" 또한 닫히는 괄호에 없으므로 stack에 추가

stack = ["{"] ")"는 닫히는 괄호 이므로 마지막 값과 비교 하여 짝이 맞아 제거되어 "{"만 남게됨.

stack = [] 닫히는 괄호 "}" 또한 stack의 마지막 값인 "{"와 짝을 맞춰 사라짐.
```

위를 통해서 다음 올 문자가 닫히는 괄호일 경우 , `stack`의 마지막 문자와 반드시 일치해야 한다. 일치하지 않거나, `stack`에 아무것도 없는 상태에서 닫히는 괄호가 들어올 경우 조건을 충족하지 못하므로 **중복문을 중단**시킨다.

## Lv. 2 할인 행사
### 문제
XYZ 마트는 일정한 금액을 지불하면 10일 동안 회원 자격을 부여합니다. XYZ 마트에서는 회원을 대상으로 매일 한 가지 제품을 할인하는 행사를 합니다. 할인하는 제품은 하루에 하나씩만 구매할 수 있습니다. 알뜰한 정현이는 자신이 원하는 제품과 수량이 할인하는 날짜와 10일 연속으로 일치할 경우에 맞춰서 회원가입을 하려 합니다.

예를 들어, 정현이가 원하는 제품이 바나나 3개, 사과 2개, 쌀 2개, 돼지고기 2개, 냄비 1개이며, XYZ 마트에서 14일간 회원을 대상으로 할인하는 제품이 날짜 순서대로 치킨, 사과, 사과, 바나나, 쌀, 사과, 돼지고기, 바나나, 돼지고기, 쌀, 냄비, 바나나, 사과, 바나나인 경우에 대해 알아봅시다. 첫째 날부터 열흘 간에는 냄비가 할인하지 않기 때문에 첫째 날에는 회원가입을 하지 않습니다. 둘째 날부터 열흘 간에는 바나나를 원하는 만큼 할인구매할 수 없기 때문에 둘째 날에도 회원가입을 하지 않습니다. 셋째 날, 넷째 날, 다섯째 날부터 각각 열흘은 원하는 제품과 수량이 일치하기 때문에 셋 중 하루에 회원가입을 하려 합니다.

정현이가 원하는 제품을 나타내는 문자열 배열 `want`와 정현이가 원하는 제품의 수량을 나타내는 정수 배열 `number`, XYZ 마트에서 할인하는 제품을 나타내는 문자열 배열 `discount`가 주어졌을 때, 회원등록시 정현이가 원하는 제품을 모두 할인 받을 수 있는 회원등록 날짜의 총 일수를 return 하는 solution 함수를 완성하시오. 가능한 날이 없으면 0을 return 합니다.

---

##### 제한사항

- 1 ≤ `want`의 길이 = `number`의 길이 ≤ 10
    - 1 ≤ `number`의 원소 ≤ 10
    - `number[i]`는 `want[i]`의 수량을 의미하며, `number`의 원소의 합은 10입니다.
- 10 ≤ `discount`의 길이 ≤ 100,000
- `want`와 `discount`의 원소들은 알파벳 소문자로 이루어진 문자열입니다.
    - 1 ≤ `want`의 원소의 길이, `discount`의 원소의 길이 ≤ 12

---

##### 입출력 예

| want                                       | number          | discount                                                                                                                       | result |
| ------------------------------------------ | --------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------ |
| ["banana", "apple", "rice", "pork", "pot"] | [3, 2, 2, 2, 1] | ["chicken", "apple", "apple", "banana", "rice", "apple", "pork", "banana", "pork", "rice", "pot", "banana", "apple", "banana"] | 3      |
| ["apple"]                                  | [10]            | ["banana", "banana", "banana", "banana", "banana", "banana", "banana", "banana", "banana", "banana"]                           | 0      |

---

### 나의 풀이
```
/*
문제
회원등록시 10일 할인 받을 수 있다.
원하는 제품의 목록과 수량을 모두 할인받아 구매할 수 있는 날짜의 총 일수 반환.

아이디어
물품과 수량을 객체로 만들고 복사본을 만든다.
10일씩 끊어서 복사본의 수량을 1씩 제거한다.
모든 품목이 0이 되는 날짜가 있으면 count하고, 모든 배열을 순환한다.
*/

function solution(want, number, discount) {
    let result = 0;
    
    const itemQty = new Map ()
    for (let i = 0; i < number.length; i++) {
        itemQty.set(want[i], number[i])
    }
    
    let itemQtyCopy = new Map (itemQty)
    
    for (let i = 0; i < discount.length; i++) {
        for (let j = i; j < i + 10; j ++) {
            let item = discount[j]
            if (itemQtyCopy.get(item) > 0) itemQtyCopy.set(item, itemQtyCopy.get(item) -1)
        }
        if ([...itemQtyCopy.values()].filter((el) => el > 0).length === 0) result += 1
        itemQtyCopy = new Map(itemQty)
    }
    return result;
}
```
모든 값에서부터 10번씩 반복하며 수량을 담은 객체를 수정. 중간에 조건을 만족하여도 반복문이 멈추지 않고 계속해서 돌아가기 때문에, discount 배열의 길이에 연산 시간이 비례한다. 연산이 간단한 조건에서도 효율적으로 작동하지 못하는 이슈 존재.

### 다른 풀이
```
function solution(want, number, discount) {
    let count = 0;
    for (let i = 0; i < discount.length - 9; i++) {
        const slice = discount.slice(i, i+10);

        let flag = true;
        for (let j = 0; j < want.length; j++) {
            if (slice.filter(item => item === want[j]).length !== number[j]) {
                flag = false;
                break;
            }
        }
        if (flag) count += 1;
    }
    return count;
}
```

**`number[i]`는 `want[i]`의 수량을 의미하며, `number`의 원소의 합은 10입니다.**
라는 조건. 즉, 정답이 되는 날짜 10일의 품목은 반드시 원하는 품목과 해당 수량으로만 배열이 구성되어 있다. 라는 조건을 첫 풀이에서 활용하지 못했다.

이 조건을 활용하면 위 코드처럼 10일씩 품목을 slice하여, 안에 구성된 품목의 개수와 want 물건의 수량과 하나라도 일치하지 않으면 조건이 성립되지 않으므로 반복문을 중단한다. 가독성도 좋으며, 더욱 효율적으로 작동하는 코드이다.

**!!제한사항에 있는 조건들을 잘 읽어보고 활용하자**

## Lv. 2 n^2 배열 자르기
### 문제
정수 `n`, `left`, `right`가 주어집니다. 다음 과정을 거쳐서 1차원 배열을 만들고자 합니다.

1. `n`행 `n`열 크기의 비어있는 2차원 배열을 만듭니다.
2. `i = 1, 2, 3, ..., n`에 대해서, 다음 과정을 반복합니다.
    - 1행 1열부터 `i`행 `i`열까지의 영역 내의 모든 빈 칸을 숫자 `i`로 채웁니다.
3. 1행, 2행, ..., `n`행을 잘라내어 모두 이어붙인 새로운 1차원 배열을 만듭니다.
4. 새로운 1차원 배열을 `arr`이라 할 때, `arr[left]`, `arr[left+1]`, ..., `arr[right]`만 남기고 나머지는 지웁니다.

정수 `n`, `left`, `right`가 매개변수로 주어집니다. 주어진 과정대로 만들어진 1차원 배열을 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 1 ≤ `n` ≤ 107
- 0 ≤ `left` ≤ `right` < n2
- `right` - `left` < 105

---

##### 입출력 예

|n|left|right|result|
|---|---|---|---|
|3|2|5|`[3,2,2,3]`|
|4|7|14|`[4,3,3,3,4,4,4,4]`|

### 나의 풀이
```
/*
n x n 크기의 행렬을 만들고, 행끼리 나열하여 arr[left] ~ arr[right]의 값을 반환하라.
한 행이 구성하는 값은, n열일 경우 n번째까지 n의 값을 가지고, 이후로는 +1
[1,2,3,4,5],
[2,2,3,4,5],
[3,3,3,4,5],
[4,4,4,4,5],
[5,5,5,5,5]

아이디어
먼저 2차원 배열을 전부 다 생성하면 n이 최대 10^7까지 가므로 시간 초과.
필요한 구간의 배열만 생성.
*/

function solution(n, left, right) {
    let twoDimArr = [];
    let startRow = Math.floor(left / n) + 1
    let endRow = Math.floor(right / n) + 1
    
    for (let row = startRow; row <= endRow; row ++) {
        for (let idx = 1; idx <= n; idx ++) {
            if (idx > row) {
                twoDimArr.push(idx)
            } else {
                twoDimArr.push(row)
            }
        }
    }
    
    return twoDimArr.slice(left % n, right - n * (startRow-1) + 1)
}
```

left부터 right가 속한 행의 숫자들을 모두 생성한 뒤, slice로 나누어 다소 비효율적으로 작동한다.
**정확히 left부터 right까지의 값만 특정 지을 필요가 있음.**

### 다른 풀이
```
function solution(n, left, right) {
    const result = [];
    for (let i = left; i <= right; i++) {
        const row = Math.floor(i / n);
        const col = i % n;
        result.push(Math.max(row, col) + 1);
    }
    return result;
}
```

결국 필요한 값들은 left부터 right까지의 값이므로, 해당 index의 값이 몇인지 알아낼 수 있으면, left부터 right까지의 값으로만 배열을 생성할 수 있다.

**해당 index가 가지는 값 구하기**
각 칸의 값은 행과 열 중 높은 숫자의 값을 가지므로,
각각 행과 열을 계산해서 더 큰 값을 넣어주면 된다.

## Lv. 2 H-Index
### 문제
H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다. 어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다. 위키백과[1](https://school.programmers.co.kr/learn/courses/30/lessons/42747#fn1)에 따르면, H-Index는 다음과 같이 구합니다.

어떤 과학자가 발표한 논문 `n`편 중, `h`번 이상 인용된 논문이 `h`편 이상이고 나머지 논문이 h번 이하 인용되었다면 `h`의 최댓값이 이 과학자의 H-Index입니다.

어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.

##### 입출력 예

|citations|return|
|---|---|
|[3, 0, 6, 1, 5]|3|

---

### 나의 풀이
```
function solution(citations) {
    citations.sort((a,b) => b-a)
    
    let index = 1
    for (citation of citations) {
        if (index > citation) return index - 1
        else if (index === citation) return citation
        index ++
    }
    return citations.length
}
```

**문제**
어떤 과학자의 논문 n편중 h번 이상 인용된 논문이 h편 이상이고, 나머지 논문이 h번 이하 인용된 h의 최대값 반환.

**풀이 방법**
우선 citations배열을 내림차순으로 정렬한다. `[6,5,4,3,2,1]`
배열을 큰 수부터 순환하면서 해당 값보다 index의 값이 같으면 해당 값 반환,
index가 더 크면, 이전의 index개의 논문들은 최소 index만큼 인용되었으므로 이전 index값 반환.

아무 조건도 일치하지 않으면, 배열안에 있는 논문들은 모두 논문의 개수보다 많이 인용되었으므로, 논문의 개수 반환.

## Lv. 2 행렬의 곱셉
### 문제
2차원 행렬 arr1과 arr2를 입력받아, arr1에 arr2를 곱한 결과를 반환하는 함수, solution을 완성해주세요.

##### 제한 조건

- 행렬 arr1, arr2의 행과 열의 길이는 2 이상 100 이하입니다.
- 행렬 arr1, arr2의 원소는 -10 이상 20 이하인 자연수입니다.
- 곱할 수 있는 배열만 주어집니다.

##### 입출력 예

|arr1|arr2|return|
|---|---|---|
|[[1, 4], [3, 2], [4, 1]]|[[3, 3], [3, 3]]|[[15, 15], [15, 15], [15, 15]]|
|[[2, 3, 2], [4, 2, 4], [3, 1, 4]]|[[5, 4, 3], [2, 4, 1], [3, 1, 1]]|[[22, 22, 11], [36, 28, 18], [29, 20, 14]]|

---

### 나의 풀이
```
/*
입출력 예 1번 시각화
[[1,4],      [[3,3],
 [3,2],       [3,3]]
 [4,1]]
/*

function solution(arr1, arr2) {
    const resultRow = arr1.length
    const resultCol = arr2[0].length
    let result = new Array ()
    for(let i = 0; i < resultRow; i++) {
        result.push([])
    }
    
    const count = arr1[0].length
    for(let row = 0; row < resultRow; row ++) {
        for (let col = 0; col < resultCol; col ++) {
            let value = 0
            for(let cnt = 0; cnt < count; cnt++) {
                value += arr1[row][cnt] * arr2[cnt][col]
            }
            result[row][col] = value
        }
    }
    
    return result;
}
```

**풀이**
 최종 행렬의 행의 크기(arr1의 행 크기), 열의 크기(arr2의 열 크기), 곱해야하는 횟수(arr1의 열의 크기 또는 arr2의 행의 크기) 이 세가지 조건을 통해서 반복문을 설정하고 계산.

## Lv. 2 의상
### 문제
코니는 매일 다른 옷을 조합하여 입는것을 좋아합니다.

예를 들어 코니가 가진 옷이 아래와 같고, 오늘 코니가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면 다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야합니다.

|종류|이름|
|---|---|
|얼굴|동그란 안경, 검정 선글라스|
|상의|파란색 티셔츠|
|하의|청바지|
|겉옷|긴 코트|

- 코니는 각 종류별로 최대 1가지 의상만 착용할 수 있습니다. 예를 들어 위 예시의 경우 동그란 안경과 검정 선글라스를 동시에 착용할 수는 없습니다.
- 착용한 의상의 일부가 겹치더라도, 다른 의상이 겹치지 않거나, 혹은 의상을 추가로 더 착용한 경우에는 서로 다른 방법으로 옷을 착용한 것으로 계산합니다.
- 코니는 하루에 최소 한 개의 의상은 입습니다.

코니가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.

---

##### 제한사항

- clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
- 코니가 가진 의상의 수는 1개 이상 30개 이하입니다.
- 같은 이름을 가진 의상은 존재하지 않습니다.
- clothes의 모든 원소는 문자열로 이루어져 있습니다.
- 모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '_' 로만 이루어져 있습니다.

##### 입출력 예

| clothes                                                                                    | return |
| ------------------------------------------------------------------------------------------ | ------ |
| [["yellow_hat", "headgear"], ["blue_sunglasses", "eyewear"], ["green_turban", "headgear"]] | 5      |
| [["crow_mask", "face"], ["blue_sunglasses", "face"], ["smoky_makeup", "face"]]             | 3      |

---

### 나의 풀이
```
function solution(clothes) {
    let answer = 0;
    
    const hashMap = new Map()
    for (let cloth of clothes) {
        hashMap.set(cloth[1], (hashMap.get(cloth[1]) + 1) || 2)
    }
    let sum = 1
    for (let qty of hashMap.values()) {
        sum *= qty
    }
    
    return sum - 1
}
```

**경우의 수 간단하게 구하는 방법**
옷을 착용하지 않는 경우도 경우의 수에 포함되므로, `착용X`또한 옷 별로 포함시켜주면 된다. 각 종류별 개수에 `착용 X`의 경우를 추가해주기 위해 1씩 더해준 다음,
종류별 옷의 개수를 모두 곱해준 뒤 1을 빼주면 된다. (모든 옷 안입은 경우 제거)

## Lv. 2 캐시
### 문제

지도개발팀에서 근무하는 제이지는 지도에서 도시 이름을 검색하면 해당 도시와 관련된 맛집 게시물들을 데이터베이스에서 읽어 보여주는 서비스를 개발하고 있다.  
이 프로그램의 테스팅 업무를 담당하고 있는 어피치는 서비스를 오픈하기 전 각 로직에 대한 성능 측정을 수행하였는데, 제이지가 작성한 부분 중 데이터베이스에서 게시물을 가져오는 부분의 실행시간이 너무 오래 걸린다는 것을 알게 되었다.  
어피치는 제이지에게 해당 로직을 개선하라고 닦달하기 시작하였고, 제이지는 DB 캐시를 적용하여 성능 개선을 시도하고 있지만 캐시 크기를 얼마로 해야 효율적인지 몰라 난감한 상황이다.

어피치에게 시달리는 제이지를 도와, DB 캐시를 적용할 때 캐시 크기에 따른 실행시간 측정 프로그램을 작성하시오.

### 입력 형식

- 캐시 크기(`cacheSize`)와 도시이름 배열(`cities`)을 입력받는다.
- `cacheSize`는 정수이며, 범위는 0 ≦ `cacheSize` ≦ 30 이다.
- `cities`는 도시 이름으로 이뤄진 문자열 배열로, 최대 도시 수는 100,000개이다.
- 각 도시 이름은 공백, 숫자, 특수문자 등이 없는 영문자로 구성되며, 대소문자 구분을 하지 않는다. 도시 이름은 최대 20자로 이루어져 있다.

### 출력 형식

- 입력된 도시이름 배열을 순서대로 처리할 때, "총 실행시간"을 출력한다.

### 조건

- 캐시 교체 알고리즘은 `LRU`(Least Recently Used)를 사용한다.
- `cache hit`일 경우 실행시간은 `1`이다.
- `cache miss`일 경우 실행시간은 `5`이다.

### 입출력 예제

|캐시크기(cacheSize)|도시이름(cities)|실행시간|
|---|---|---|
|3|["Jeju", "Pangyo", "Seoul", "NewYork", "LA", "Jeju", "Pangyo", "Seoul", "NewYork", "LA"]|50|
|3|["Jeju", "Pangyo", "Seoul", "Jeju", "Pangyo", "Seoul", "Jeju", "Pangyo", "Seoul"]|21|
|2|["Jeju", "Pangyo", "Seoul", "NewYork", "LA", "SanFrancisco", "Seoul", "Rome", "Paris", "Jeju", "NewYork", "Rome"]|60|
|5|["Jeju", "Pangyo", "Seoul", "NewYork", "LA", "SanFrancisco", "Seoul", "Rome", "Paris", "Jeju", "NewYork", "Rome"]|52|
|2|["Jeju", "Pangyo", "NewYork", "newyork"]|16|
|0|["Jeju", "Pangyo", "Seoul", "NewYork", "LA"]|25|

---

### 나의 풀이 
```
/*
LRU알고리즘을 통한 실행시간 반환. (캐시에 있을 경우 5 없으면 1)
*/

function solution(cacheSize, cities) {
    let runTime = 0;
    let cityDB = []
    
    // 도시 이름 전부 소문자로 변환
    cities = cities.map((el)=>el.toLowerCase())
    
    // 캐시 공간이 0일경우 바로 정답 반환.
    if (cacheSize ===0 ) return cities.length * 5
    
    // LRU 알고리즘으로 실행시간 계산
    for (let city of cities) {
        if(cityDB.includes(city) === false) {
            if (cityDB.length === cacheSize) cityDB.shift()
            
            cityDB.push(city)
            runTime += 5
        } else {
            cityDB = cityDB.filter((el) => el !== city)    
            cityDB.push(city)
            runTime += 1
        }
    }
    
    return runTime;
}
```

**문제**
도시들이 담긴 배열의 실행 시간을 구해라.

**풀이**
LRU알고리즘을 통해 cityDB배열을 채우고, 방문 여부에 맞춰 실행시간 반환. (캐시에 있을 경우 5 없으면 1)

**LRU 알고리즘이란?**
cacheSize만큼 정보를 저장해 저장해둔 정보가 나올 경우 꺼내서 사용.
cache용량이 꽉 찰 경우 가장 이전에 저정해둔 정보 제거하고 새로운 정보 저장.(shift 후 pop)

## Lv. 2 기능개발
### 문제
프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다. 각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.

또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.

먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

##### 제한 사항

- 작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
- 작업 진도는 100 미만의 자연수입니다.
- 작업 속도는 100 이하의 자연수입니다.
- 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.

##### 입출력 예

|progresses|speeds|return|
|---|---|---|
|[93, 30, 55]|[1, 30, 5]|[2, 1]|
|[95, 90, 99, 99, 80, 99]|[1, 1, 1, 1, 1, 1]|[1, 3, 2]|

---

### 나의 풀이
```
function solution(progresses, speeds) {
    let distribute = [];
    while (progresses.length > 0) {
        let count = 0
        // 개발 진척도 업데이트
        for(let i = 0; i < progresses.length; i ++) {
            progresses[i] += speeds[i]
        }
        
        // 맨 앞 개발이 완료될 경우 배포 진행
        if (progresses[0] >= 100) {
            for (progress of progresses) {
                if (progress >= 100) count ++
                else break
            }
            distribute.push(count)
        
            progresses.splice(0,count)
            speeds.splice(0,count)
        }
        
    }
    
    return distribute;
}
```

**문제**
기능의 배포 순서에 따라 개발 진척도가 담긴 배열과 개발 속도를 담은 배열이 주어진다.
후순위 기능이 먼저 개발 완료될 경우 바로 앞에있는 기능의 개발이 완료될 때 같이 배포된다.
각 배포마다 몇 개의 기능이 배포되는지 구하여라.

**풀이**
맨 앞의 기능이 완료될 때 까지 개발 진척도를 업데이트해준다.
앞의 기능이 완료될 때, 뒤의 개발이 완료되었으면 count해주고 shift를 통해 배열에서 제거한다.

## Lv. 2 튜플
### 문제
셀수있는 수량의 순서있는 열거 또는 어떤 순서를 따르는 요소들의 모음을 튜플(tuple)이라고 합니다. n개의 요소를 가진 튜플을 n-튜플(n-tuple)이라고 하며, 다음과 같이 표현할 수 있습니다.

- (a1, a2, a3, ..., an)

튜플은 다음과 같은 성질을 가지고 있습니다.

1. 중복된 원소가 있을 수 있습니다. ex : (2, 3, 1, 2)
2. 원소에 정해진 순서가 있으며, 원소의 순서가 다르면 서로 다른 튜플입니다. ex : (1, 2, 3) ≠ (1, 3, 2)
3. 튜플의 원소 개수는 유한합니다.

원소의 개수가 n개이고, **중복되는 원소가 없는** 튜플 `(a1, a2, a3, ..., an)`이 주어질 때(단, a1, a2, ..., an은 자연수), 이는 다음과 같이 집합 기호 '{', '}'를 이용해 표현할 수 있습니다.

- {{a1}, {a1, a2}, {a1, a2, a3}, {a1, a2, a3, a4}, ... {a1, a2, a3, a4, ..., an}}

예를 들어 튜플이 (2, 1, 3, 4)인 경우 이는

- {{2}, {2, 1}, {2, 1, 3}, {2, 1, 3, 4}}

와 같이 표현할 수 있습니다. 이때, 집합은 원소의 순서가 바뀌어도 상관없으므로

- {{2}, {2, 1}, {2, 1, 3}, {2, 1, 3, 4}}
- {{2, 1, 3, 4}, {2}, {2, 1, 3}, {2, 1}}
- {{1, 2, 3}, {2, 1}, {1, 2, 4, 3}, {2}}

는 모두 같은 튜플 (2, 1, 3, 4)를 나타냅니다.

특정 튜플을 표현하는 집합이 담긴 문자열 s가 매개변수로 주어질 때, s가 표현하는 튜플을 배열에 담아 return 하도록 solution 함수를 완성해주세요.

#### **[제한사항]**

- s의 길이는 5 이상 1,000,000 이하입니다.
- s는 숫자와 '{', '}', ',' 로만 이루어져 있습니다.
- 숫자가 0으로 시작하는 경우는 없습니다.
- s는 항상 중복되는 원소가 없는 튜플을 올바르게 표현하고 있습니다.
- s가 표현하는 튜플의 원소는 1 이상 100,000 이하인 자연수입니다.
- return 하는 배열의 길이가 1 이상 500 이하인 경우만 입력으로 주어집니다.

---

##### **[입출력 예]**

| s                                 | result       |
| --------------------------------- | ------------ |
| `"{{2},{2,1},{2,1,3},{2,1,3,4}}"` | [2, 1, 3, 4] |
| `"{{1,2,3},{2,1},{1,2,4,3},{2}}"` | [2, 1, 3, 4] |
| `"{{20,111},{111}}"`              | [111, 20]    |
| `"{{123}}"`                       | [123]        |
| `"{{4,2,3},{3},{2,3,4,1},{2,3}}"` | [3, 2, 4, 1] |

---

### 나의 풀이
```
function solution(s) {
    let numSet = new Map()
    s = s.split(",")
    
    for(let i = 0; i < s.length; i ++) {
        let char = s[i]
        let num = ""
        for (let j = 0; j < char.length; j ++) {
            if (char[j] !== "{" && char[j] !== "}") {
                num += char[j]
            }
        }
        numSet.set(num, (numSet.get(num) + 1) || 1)
    }
    
    numSet = [...numSet].sort((a,b) => b[1] - a[1]).map((el) => parseInt(el[0]))
    
    return numSet
}
```

**문제**
중복되는 숫자를 담은 문자열에서 중복을 제거한 뒤 많이 나온 횟수대로 배열로 반환.

**풀이**
숫자별로 포함된 횟수를 담은 map을 만들어준다.
등장 횟수만큼 오름차순으로 숫자를 정렬하고, 문자열 -> 숫자로 변환한 뒤 반환


## Lv. 2 [스택/큐] 프로세스
### 문제
운영체제의 역할 중 하나는 컴퓨터 시스템의 자원을 효율적으로 관리하는 것입니다. 이 문제에서는 운영체제가 다음 규칙에 따라 프로세스를 관리할 경우 특정 프로세스가 몇 번째로 실행되는지 알아내면 됩니다.

```
1. 실행 대기 큐(Queue)에서 대기중인 프로세스 하나를 꺼냅니다.
2. 큐에 대기중인 프로세스 중 우선순위가 더 높은 프로세스가 있다면 방금 꺼낸 프로세스를 다시 큐에 넣습니다.
3. 만약 그런 프로세스가 없다면 방금 꺼낸 프로세스를 실행합니다.
  3.1 한 번 실행한 프로세스는 다시 큐에 넣지 않고 그대로 종료됩니다.
```

예를 들어 프로세스 4개 [A, B, C, D]가 순서대로 실행 대기 큐에 들어있고, 우선순위가 [2, 1, 3, 2]라면 [C, D, A, B] 순으로 실행하게 됩니다.

현재 실행 대기 큐(Queue)에 있는 프로세스의 중요도가 순서대로 담긴 배열 `priorities`와, 몇 번째로 실행되는지 알고싶은 프로세스의 위치를 알려주는 `location`이 매개변수로 주어질 때, 해당 프로세스가 몇 번째로 실행되는지 return 하도록 solution 함수를 작성해주세요.

---

##### 제한사항

- `priorities`의 길이는 1 이상 100 이하입니다.
    - `priorities`의 원소는 1 이상 9 이하의 정수입니다.
    - `priorities`의 원소는 우선순위를 나타내며 숫자가 클 수록 우선순위가 높습니다.
- `location`은 0 이상 (대기 큐에 있는 프로세스 수 - 1) 이하의 값을 가집니다.
    - `priorities`의 가장 앞에 있으면 0, 두 번째에 있으면 1 … 과 같이 표현합니다.

##### 입출력 예

| priorities         | location | return |
| ------------------ | -------- | ------ |
| [2, 1, 3, 2]       | 2        | 1      |
| [1, 1, 9, 1, 1, 1] | 0        | 5      |

---

### 나의 풀이
```
/*
function solution(priorities, location) {
    let count = 0;
    let max = Math.max(...priorities)
    let running = true
    
    // 우선순위에 맞춰 파일 실행
    while (running) {
        let target = priorities[0]
        
        if (target === max) {
            priorities.shift()
            count ++
            max = Math.max(...priorities)
            
            // 실행된 파일이 location에 해당할 경우 종료 
            location === 0 ? running = false : location --
        }
        else {
            priorities.push(priorities.shift())
            
            // 실행된 파일이 location에 해당할 경우 index 맨 끝으로
            location === 0 ? location = priorities.length-1 : location --
        }
    }
    
    
    return count;
}
```

**문제**
실행 우선순위를 담은 배열에서 location의 순서에 해당하는 파일이 몇번 째로 실행되는지 구하여라.

**풀이**
가장 높은 우선순위 크기를 max에 할당한다.
맨 앞부터 max에 해당하면 count를 올려주고 location --, 아니면 다시 push.
location파일이 실행이 뒤로 밀려났을 경우, location을 length-1로 업데이트.
location파일이 실행 될 경우 count올려주고 반환.

## Lv. 2 [완전탐색] 피로도
### 문제
XX게임에는 피로도 시스템(0 이상의 정수로 표현합니다)이 있으며, 일정 피로도를 사용해서 던전을 탐험할 수 있습니다. 이때, 각 던전마다 탐험을 시작하기 위해 필요한 "최소 필요 피로도"와 던전 탐험을 마쳤을 때 소모되는 "소모 피로도"가 있습니다. "최소 필요 피로도"는 해당 던전을 탐험하기 위해 가지고 있어야 하는 최소한의 피로도를 나타내며, "소모 피로도"는 던전을 탐험한 후 소모되는 피로도를 나타냅니다. 예를 들어 "최소 필요 피로도"가 80, "소모 피로도"가 20인 던전을 탐험하기 위해서는 유저의 현재 남은 피로도는 80 이상 이어야 하며, 던전을 탐험한 후에는 피로도 20이 소모됩니다.

이 게임에는 하루에 한 번씩 탐험할 수 있는 던전이 여러개 있는데, 한 유저가 오늘 이 던전들을 최대한 많이 탐험하려 합니다. 유저의 현재 피로도 k와 각 던전별 "최소 필요 피로도", "소모 피로도"가 담긴 2차원 배열 dungeons 가 매개변수로 주어질 때, 유저가 탐험할수 있는 최대 던전 수를 return 하도록 solution 함수를 완성해주세요.

##### 제한사항

- k는 1 이상 5,000 이하인 자연수입니다.
- dungeons의 세로(행) 길이(즉, 던전의 개수)는 1 이상 8 이하입니다.
    - dungeons의 가로(열) 길이는 2 입니다.
    - dungeons의 각 행은 각 던전의 ["최소 필요 피로도", "소모 피로도"] 입니다.
    - "최소 필요 피로도"는 항상 "소모 피로도"보다 크거나 같습니다.
    - "최소 필요 피로도"와 "소모 피로도"는 1 이상 1,000 이하인 자연수입니다.
    - 서로 다른 던전의 ["최소 필요 피로도", "소모 피로도"]가 서로 같을 수 있습니다.

##### 입출력 예

| k   | dungeons                  | result |
| --- | ------------------------- | ------ |
| 80  | [[80,20],[50,40],[30,10]] | 3      |

---

### 나의 풀이
```
/*
문제
현재 피로도 k와 최소 필요 피로도, 소모 피로도가 담긴 2차원 배열 dungeons를 통해
탐험할 수 있는 최대 던전 수를 return.

아이디어
던전의 개수가 8이하인걸 보면 적어도 O(n^2)이상의 알고리즘을 통해 풀리는 문제.
한 가지 로직으로만은 해결이 불가능하다. 정말 일일이 하나씩 비교해봐야 함.
소모 피로도가 낮은 던전부터 탐색하면, 최소 필요 피로도를 충족하지 못하는 던전이 발생하고,
최소 필요 피로도가 높은 순으로 탐색하면, 소모 피로도가 너무 큰 던전 발생시 나머지 던전 탐색 불가.

모든 경우의 수를 비교해보고, 가장 높은 값 반환(완전 탐색).
/*
function solution(k, dungeons) {
    let answer = 0
    const visited = new Array(dungeons.length).fill(false)
    
    function dfs(currentHp, depth) {
        answer = Math.max(answer,depth)
        
        for (let i = 0; i < dungeons.length; i ++) {
            const [minHp, useHp] = dungeons[i]
            
            if (!visited[i] && currentHp >= minHp) {
                visited[i] = true
                dfs(currentHp - useHp, depth + 1)
                visited[i] = false
            }
        }
    }
    
    dfs(k,0)
    return answer;
}
```

재귀호출을 활용하여 DFS로 풀었다.
아래의 값을 통해 해당 코드의 진행을 파헤쳐보자.
`k = 80`,
`dungeons = [[80,20], [50,40], [30,10]]`,
`result = 3`


*n번째 이동이란 노드간의 링크(간선)를 통한 이동을 의미한다.*
가장 먼저 visted를 던전의 길이만큼 false로 채우기 시작할테니
`visted = [false, false, false]`의 배열이 만들어 지고, 함수 `dfs(80, 0)`이 실행된다.

첫 번째 던전에서 조건이 충족되어 `dfs(60, 1)`이 실행된다.

![[첨부 파일 소스/Image File 1/Pasted image 20240703164047.png]]

**첫 번째 이동 dfs(80, 0) -> dfs(60, 1)**
dfs(60,1)에서 첫 번째 던전인  `[80, 20]`은 visited가 true로 처리되어있어,
i가 ++되어 `dungeons[1]`인 두 번째 던전`[50, 40]`에서 조건이 충족된다.
다시 한 번 재귀함수가 실행되어 `dfs(20, 2)`가 실행된다.

**두 번째 이동 dfs(60, 1) -> dfs(20, 2)**
첫 번째, 두 번째 던전은 방문처리되어 세 번째 던전을 방문하지만
조건이 충족되지 못하고 재귀함수 `dfs(20, 2)` 함수의 실행이 종료된다.

**세 번째 이동 dfs(20, 2) -> dfs(60, 1)**
`dfs(20, 2)`함수의 시작 지점인 `dfs(60, 1)`함수로 돌아가고 , 그 다음 코드인 `visited[1] = false`가 실행된다.
이전에 두 번째 실행내역에서 for문이 i = 1까지 진행되었었으므로, i가 ++ 되어
`dungeons[2]`인 세 번째 던전 `[30, 10]`에서 조건이 충족되고
`dfs(50, 2)`가 실행된다.

**네 번째 이동 dfs(60, 1) -> dfs(50, 2)**
이전과 다른 세 번째 실행인 `dfs(50, 2)`가 실행된다.
이전 세 번째 실행인 `dfs(20, 2)`가 종료되고난 뒤에 두 번째 던전이 `visited[1] = false` 처리 되었으므로,
두 번째 던전의 조건이 충족되어 `dfs(10, 3)`이 실행된다.

**다 번째 이동 dfs(50, 2) -> dfs(10, 3)**
answer가 3으로 가장 높은 값으로 업데이트된다.

이 후 모든 조건을 만족하지 못하고 brench를 따라 노드가 뒤로 이동하면서 모든 함수의 실행이 종료되고 answer = 3을 반환한다.

---

처음에는 재귀함수와 for문 if문이 서로 상호작용하여 이해하기가 어렵다.
하지만 결국 "`무방향 그래프`를 통해 이동하면서 반복문과 조건문을 실행한다." 라는 사실을 깨닫고 나면 이해하기가 한결 수월해진다.


## Lv. 2 뉴스 클러스터링
### 문제
**뉴스 클러스터링**

여러 언론사에서 쏟아지는 뉴스, 특히 속보성 뉴스를 보면 비슷비슷한 제목의 기사가 많아 정작 필요한 기사를 찾기가 어렵다. Daum 뉴스의 개발 업무를 맡게 된 신입사원 튜브는 사용자들이 편리하게 다양한 뉴스를 찾아볼 수 있도록 문제점을 개선하는 업무를 맡게 되었다.

개발의 방향을 잡기 위해 튜브는 우선 최근 화제가 되고 있는 "카카오 신입 개발자 공채" 관련 기사를 검색해보았다.

- 카카오 첫 공채..'블라인드' 방식 채용
- 카카오, 합병 후 첫 공채.. 블라인드 전형으로 개발자 채용
- 카카오, 블라인드 전형으로 신입 개발자 공채
- 카카오 공채, 신입 개발자 코딩 능력만 본다
- 카카오, 신입 공채.. "코딩 실력만 본다"
- 카카오 "코딩 능력만으로 2018 신입 개발자 뽑는다"

기사의 제목을 기준으로 "블라인드 전형"에 주목하는 기사와 "코딩 테스트"에 주목하는 기사로 나뉘는 걸 발견했다. 튜브는 이들을 각각 묶어서 보여주면 카카오 공채 관련 기사를 찾아보는 사용자에게 유용할 듯싶었다.

유사한 기사를 묶는 기준을 정하기 위해서 논문과 자료를 조사하던 튜브는 "자카드 유사도"라는 방법을 찾아냈다.

자카드 유사도는 집합 간의 유사도를 검사하는 여러 방법 중의 하나로 알려져 있다. 두 집합 `A`, `B` 사이의 자카드 유사도 `J(A, B)`는 두 집합의 교집합 크기를 두 집합의 합집합 크기로 나눈 값으로 정의된다.

예를 들어 집합 `A` = {1, 2, 3}, 집합 `B` = {2, 3, 4}라고 할 때, 교집합 `A ∩ B` = {2, 3}, 합집합 `A ∪ B` = {1, 2, 3, 4}이 되므로, 집합 `A`, `B` 사이의 자카드 유사도 `J(A, B)` = 2/4 = 0.5가 된다. 집합 A와 집합 B가 모두 공집합일 경우에는 나눗셈이 정의되지 않으니 따로 `J(A, B)` = 1로 정의한다.

자카드 유사도는 원소의 중복을 허용하는 다중집합에 대해서 확장할 수 있다. 다중집합 `A`는 원소 "1"을 3개 가지고 있고, 다중집합 `B`는 원소 "1"을 5개 가지고 있다고 하자. 이 다중집합의 교집합 `A ∩ B`는 원소 "1"을 min(3, 5)인 3개, 합집합 `A ∪ B`는 원소 "1"을 max(3, 5)인 5개 가지게 된다. 다중집합 `A` = {1, 1, 2, 2, 3}, 다중집합 `B` = {1, 2, 2, 4, 5}라고 하면, 교집합 `A ∩ B` = {1, 2, 2}, 합집합 `A ∪ B` = {1, 1, 2, 2, 3, 4, 5}가 되므로, 자카드 유사도 `J(A, B)` = 3/7, 약 0.42가 된다.

이를 이용하여 문자열 사이의 유사도를 계산하는데 이용할 수 있다. 문자열 "FRANCE"와 "FRENCH"가 주어졌을 때, 이를 두 글자씩 끊어서 다중집합을 만들 수 있다. 각각 {FR, RA, AN, NC, CE}, {FR, RE, EN, NC, CH}가 되며, 교집합은 {FR, NC}, 합집합은 {FR, RA, AN, NC, CE, RE, EN, CH}가 되므로, 두 문자열 사이의 자카드 유사도 `J("FRANCE", "FRENCH")` = 2/8 = 0.25가 된다.

#### 입력 형식

- 입력으로는 `str1`과 `str2`의 두 문자열이 들어온다. 각 문자열의 길이는 2 이상, 1,000 이하이다.
- 입력으로 들어온 문자열은 두 글자씩 끊어서 다중집합의 원소로 만든다. 이때 영문자로 된 글자 쌍만 유효하고, 기타 공백이나 숫자, 특수 문자가 들어있는 경우는 그 글자 쌍을 버린다. 예를 들어 "ab+"가 입력으로 들어오면, "ab"만 다중집합의 원소로 삼고, "b+"는 버린다.
- 다중집합 원소 사이를 비교할 때, 대문자와 소문자의 차이는 무시한다. "AB"와 "Ab", "ab"는 같은 원소로 취급한다.

#### 출력 형식

입력으로 들어온 두 문자열의 자카드 유사도를 출력한다. 유사도 값은 0에서 1 사이의 실수이므로, 이를 다루기 쉽도록 65536을 곱한 후에 소수점 아래를 버리고 정수부만 출력한다.

#### 예제 입출력

|str1|str2|answer|
|---|---|---|
|FRANCE|french|16384|
|handshake|shake hands|65536|
|aa1+aa2|AAAA12|43690|
|E=M*C^2|e=m*c^2|65536|

### 나의 풀이
```
/*
문제
두 단어를 자카드 유사도를 통해 유사도 측정

조건
영문자 이외의 문자(공백, 특수문자, 숫자)가 포함되어있으면 포함 X
대소문자 구분 X
원소를 중복으로 가지고 있으면, 합집합은 해당 원소 개수의 최대값. 교집합은 최소값을 가진다.

*/
function solution(str1, str2) {
    let answer = 0;
    let str1Arr = []
    let str2Arr = []
    
    str1 = str1.toLowerCase().split("")
    str2 = str2.toLowerCase().split("")
	
	// str1 알파벳묶음 배열 생성
    for(let i = 0; i < str1.length-1; i ++) {
	    // 알파벳 판별
        if(str1[i] !== str1[i].toUpperCase() && str1[i+1] !== str1[i+1].toUpperCase()) {
            str1Arr.push(str1[i] + str1[i+1])
        }
    }
	
	// str2 알파벳묶음 배열 생성
    for(let i = 0; i < str2.length-1; i ++) {
        if(str2[i] !== str2[i].toUpperCase() && str2[i+1] !== str2[i+1].toUpperCase()) {
            str2Arr.push(str2[i] + str2[i+1])
        }
    }
	
	// 두 문자 모두 공집합일시 종료
    if (str1Arr.length === 0 && str2Arr.length === 0) return 65536
        
    let interChars = []
    let unionCount = 0
    let interCount = 0
    
	// 합집합, 교집합 구하기
    for(char of str1Arr) {
        if (interChars.includes(char)) continue
        
        if (str2Arr.includes(char)) {
            // str1 배열에서 중복 원소 개수 구하기
            let str1Count = str1Arr.reduce((count, el) => {
                return char === el ? count + 1 : count
            }, 0)
            // str2 배열에서 중복 원소 개수 구하기
            let str2Count = str2Arr.reduce((count,el) => {
                return char === el ? count + 1 : count
            }, 0)
            // 교집합, 합집합, 교집합 원소모음 업데이트
            unionCount += Math.max(str1Count, str2Count)
            interCount += Math.min(str1Count, str2Count)
            interChars.push(char)
        } else {
            unionCount += 1
        }
    }
	
	// str2배열에서 중복되는 요소들은 이미 추가해줬으므로 제거
    str2Arr = str2Arr.filter((el) => interChars.includes(el) === false)
    unionCount += str2Arr.length
    
    answer = Math.floor((interCount / unionCount) * 65536)
    
    return answer;
}
```

**아이디어**
각 단어를 문자 2개씩 끊어서 배열로 만들고, (공통된 문자 개수  / 두 배열 길이의 총 합) 을 통해 구한다
합집합은 많이 가지고 있는 쪽의 개수.
교집합은 중복으로 가지고 있는 것 중 적게 가지고 있는 쪽의 개수

**풀이**
*교집합, 합집합 동시에 구하기*
먼저 str1 배열을 순회하면서 중복인 경우와 아닌 경우로 나눈다.

`중복으로 가지고 있을 경우 :` 적은 개수를 교집합에, 많은 개수를 합집합에 숫자로 추가한다. 그리고 교집합 모음 배열에 문자를 따로 추가해준다.
`중복이 아닌 경우 :` 합집합 배열에 추가.
str2 배열에서 중복되는 문자는 이미 추가해줬으므로, 중복을 제거한  개수만큼 합집합에 더해준다.

## Lv. 2 [해시] 전화번호 목록
### 문제
전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.  
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

##### 제한 사항

- phone_book의 길이는 1 이상 1,000,000 이하입니다.
    - 각 전화번호의 길이는 1 이상 20 이하입니다.
    - 같은 전화번호가 중복해서 들어있지 않습니다.

##### 입출력 예제

|phone_book|return|
|---|---|
|["119", "97674223", "1195524421"]|false|
|["123","456","789"]|true|
|["12","123","1235","567","88"]|false|

---

### 나의 풀이
```
function solution(phone_book) {
    phone_book.sort()
    for(let i = 0; i < phone_book.length -1; i++) {
        if (phone_book[i+1].startsWith(phone_book[i])) {
            return false
        }
    }

    return true; 
}
```

문제 분류는 해시로 되어 있었지만, 더욱 간단하게 해결되는 방법이 있다.
.sort( )를 사용하면 문자를 유니코드 포인트로 변환해 오름차순으로 정렬하기 때문에, 바로 뒤 번호와만 비교하면 되어 간단하게 해결된다.

---

### 해시를 활용한 풀이
```
function solution(phone_book) {
    let phoneMap = new Map()
    
    for (phone of phone_book) {
        phoneMap.set(phone, true)
    }
    
    for (phone of phone_book) {
        for(let i = 1; i < phone.length; i++) {
            let startNum = phone.substring(0,i)
            if (phoneMap.has(startNum)) return false
        }
    }
    
    return true
}
```

모든 번호들을 저장한 해시맵을 만들어 준다.
2중 for문을 통해 전체 번호를 반복하고, 해당 번호의 앞 1자리 ~ 전체 자릿수를 반복하면서
일치하는 번호가 해시맵에 존재하는지 확인한다.

해당 풀이가 출제 의도에 맞는 풀이가 아닐까라는 생각이 들지만 효율성은 sort를 활용한 풀이가 더욱 좋게 나온다.

## Lv. 2 [DFS] 타겟 넘버
### 문제
n개의 음이 아닌 정수들이 있습니다. 이 정수들을 순서를 바꾸지 않고 적절히 더하거나 빼서 타겟 넘버를 만들려고 합니다. 예를 들어 [1, 1, 1, 1, 1]로 숫자 3을 만들려면 다음 다섯 방법을 쓸 수 있습니다.

```
-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3
```

사용할 수 있는 숫자가 담긴 배열 numbers, 타겟 넘버 target이 매개변수로 주어질 때 숫자를 적절히 더하고 빼서 타겟 넘버를 만드는 방법의 수를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 주어지는 숫자의 개수는 2개 이상 20개 이하입니다.
- 각 숫자는 1 이상 50 이하인 자연수입니다.
- 타겟 넘버는 1 이상 1000 이하인 자연수입니다.

##### 입출력 예

|numbers|target|return|
|---|---|---|
|[1, 1, 1, 1, 1]|3|5|
|[4, 1, 2, 1]|4|2|

---

### 문제 풀이
#### 풀이 과정
**문제**
주어진 숫자들을 통해 target넘버를 만들 수 있는 조합 개수의 총 합을 구해라.

**아이디어**
모든 경우의 수를 탐색해야 하므로 DFS를 통해 구현.
DFS로 구현할 때 고려해야 할 부분들은 다음과 같다.
`경우의 수` : 한 가지 요소당 +하는 경우와 -하는 경우 총 2가지로 나뉜다.
`수행 동작` : 재귀 함수가 호출됐을 때 수행할 동작을 지정한다.
`탈출 조건` : stack overflow에 빠지지 않기 위해서 재귀함수가 종료되는 조건을 만들어줘야 한다.

#### 답안 코드
```
function solution(numbers, target) {
    let answer = 0
    let length = numbers.length
    
    function dfs(index, sum) {
        if (index === length) {
            if (sum === target ) {
                answer ++
            }
            return
        }
        
        dfs(index + 1, sum + numbers[index])
        dfs(index + 1, sum - numbers[index])
    }
    
    dfs(0,0)
    
    return answer;
}
```

`경우의 수`는 +와 - 두 가지 경우로 모두 연산에 포함되어야 하므로, 방문 처리를 하지 않고 +해주는 경우와 -해주는 경우 두 개의 방향으로 뻗어나갈 수 있도록 재귀 함수를 호출한다.
`수행 동작`은 index를 1씩 더해주면서 해당 index의 숫자를 sum에 더하거나 빼준다.
`탈출 조건`은 index가 배열의 길이와 일치할 때(=모든 숫자를 연산에 적용시켰을 때) target과 일치하면 answer에 값을 더해주고, return을 통해 연산이 종료되도록 조건을 정해준다.

## Lv. 2 n진수 게임
### 문제
튜브가 활동하는 코딩 동아리에서는 전통적으로 해오는 게임이 있다. 이 게임은 여러 사람이 둥글게 앉아서 숫자를 하나씩 차례대로 말하는 게임인데, 규칙은 다음과 같다.

1. 숫자를 0부터 시작해서 차례대로 말한다. 첫 번째 사람은 0, 두 번째 사람은 1, … 열 번째 사람은 9를 말한다.
2. 10 이상의 숫자부터는 한 자리씩 끊어서 말한다. 즉 열한 번째 사람은 10의 첫 자리인 1, 열두 번째 사람은 둘째 자리인 0을 말한다.

이렇게 게임을 진행할 경우,  
`0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 1, 0, 1, 1, 1, 2, 1, 3, 1, 4, …`  
순으로 숫자를 말하면 된다.

한편 코딩 동아리 일원들은 컴퓨터를 다루는 사람답게 이진수로 이 게임을 진행하기도 하는데, 이 경우에는  
`0, 1, 1, 0, 1, 1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1, …`  
순으로 숫자를 말하면 된다.

이진수로 진행하는 게임에 익숙해져 질려가던 사람들은 좀 더 난이도를 높이기 위해 이진법에서 십육진법까지 모든 진법으로 게임을 진행해보기로 했다. 숫자 게임이 익숙하지 않은 튜브는 게임에 져서 벌칙을 받는 굴욕을 피하기 위해, 자신이 말해야 하는 숫자를 스마트폰에 미리 출력해주는 프로그램을 만들려고 한다. 튜브의 프로그램을 구현하라.

#### 입력 형식

진법 `n`, 미리 구할 숫자의 갯수 `t`, 게임에 참가하는 인원 `m`, 튜브의 순서 `p` 가 주어진다.

- 2 ≦ `n` ≦ 16
- 0 ＜ `t` ≦ 1000
- 2 ≦ `m` ≦ 100
- 1 ≦ `p` ≦ `m`

#### 출력 형식

튜브가 말해야 하는 숫자 `t`개를 공백 없이 차례대로 나타낸 문자열. 단, `10`~`15`는 각각 대문자 `A`~`F`로 출력한다.

#### 입출력 예제

| n   | t   | m   | p   | result             |     |
| --- | --- | --- | --- | ------------------ | --- |
| 2   | 4   | 2   | 1   | "0111"             |     |
| 16  | 16  | 2   | 1   | "02468ACE11111111" |     |
| 16  | 16  | 2   | 2   | "13579BDF01234567" |     |

---

### 문제 풀이
#### 풀이 과정
**문제**
진법 n, 미리 구할 숫자의 갯수 t, 게임에 참가하는 인원 m, 튜브의 순서 p
1부터 시작해 진법에 맞춰 변환된 문자를 한 자리씩 얘기할 때, 문자 모음을 반환해라.

**아이디어**
게임이 진행 되는 총 차례는 m * t
m * t 까지의 숫자를 해당 진법으로 변환해 배열에 담은 뒤,
index를 m만큼 더해주면서 p부터 시작한다.

#### 답안 코드
```
function solution(n, t, m, p) {
    let result = '';
    let words = []
    
    // 게임 진행에 필요한 숫자의 크기
    let length = p-1 + (m * t)
    
    // 숫자별로 진법 변환 후 배열에 담아줌.
    for (let i = 0; i < length; i++) {
        words.push(i.toString(n))
    }
    
    // 대문자로 변환작업, 붙어있는 문자 각각 나눠서 다시 배열에 담기.
    words = words.join("").toUpperCase().split("")
    
    // 총 인원인 m만큼 더해주면서 튜브의 차례에 해당하는 문자 추가
    for (let i = p-1; i < length; i += m) {
        result += words[i]
    }
    
    return result;
}
```

## Lv. 2 k진수에서 소수 개수 구하기
### 문제
양의 정수 `n`이 주어집니다. 이 숫자를 `k`진수로 바꿨을 때, 변환된 수 안에 아래 조건에 맞는 소수(Prime number)가 몇 개인지 알아보려 합니다.

- `0P0`처럼 소수 양쪽에 0이 있는 경우
- `P0`처럼 소수 오른쪽에만 0이 있고 왼쪽에는 아무것도 없는 경우
- `0P`처럼 소수 왼쪽에만 0이 있고 오른쪽에는 아무것도 없는 경우
- `P`처럼 소수 양쪽에 아무것도 없는 경우
- 단, `P`는 각 자릿수에 0을 포함하지 않는 소수입니다.
    - 예를 들어, 101은 `P`가 될 수 없습니다.

예를 들어, 437674을 3진수로 바꾸면 `211`0`2`01010`11`입니다. 여기서 찾을 수 있는 조건에 맞는 소수는 왼쪽부터 순서대로 211, 2, 11이 있으며, 총 3개입니다. (211, 2, 11을 `k`진법으로 보았을 때가 아닌, 10진법으로 보았을 때 소수여야 한다는 점에 주의합니다.) 211은 `P0` 형태에서 찾을 수 있으며, 2는 `0P0`에서, 11은 `0P`에서 찾을 수 있습니다.

정수 `n`과 `k`가 매개변수로 주어집니다. `n`을 `k`진수로 바꿨을 때, 변환된 수 안에서 찾을 수 있는 **위 조건에 맞는 소수**의 개수를 return 하도록 solution 함수를 완성해 주세요.

---

##### 제한사항

- 1 ≤ `n` ≤ 1,000,000
- 3 ≤ `k` ≤ 10

---

##### 입출력 예

| n      | k   | result |
| ------ | --- | ------ |
| 437674 | 3   | 3      |
| 110011 | 10  | 2      |

---

### 문제 풀이
#### 풀이 과정
**문제**
주어진 수 n을 k진수로 변환했을 때, 소수(p)가 0P0, P0, 0P, P에 해당하는 경우의 총합을 반환해라.
단, 각 자리수에 0이 포함되는 소수는 제외.

**아이디어**
주어진 수 n을 먼저 k 진수로 변환한다.
0을 기점으로 숫자를 카운트하면서 소수에 맞는지 판별한다.

---

#### 답안 코드
```
function solution(n, k) {
    let count = 0;
    
    function isPrime(num) {
        num = parseInt(num)
        if (num === 1) return false
        for (let i = 2; i <= Math.sqrt(num); i++) {
            if (num % i === 0) {
                return false
            }
        }
        return true
    }
    
    let nums = n.toString(k).split(0).filter((el) => el)
    
    for (num of nums) {
        if (isPrime(num)) count ++
    }
    
    return count;
}
```

## Lv. 2 [BFS] 게임 맵 최단거리
### 문제
ROR 게임은 두 팀으로 나누어서 진행하며, 상대 팀 진영을 먼저 파괴하면 이기는 게임입니다. 따라서, 각 팀은 상대 팀 진영에 최대한 빨리 도착하는 것이 유리합니다.

지금부터 당신은 한 팀의 팀원이 되어 게임을 진행하려고 합니다. 다음은 5 x 5 크기의 맵에, 당신의 캐릭터가 (행: 1, 열: 1) 위치에 있고, 상대 팀 진영은 (행: 5, 열: 5) 위치에 있는 경우의 예시입니다.

![최단거리1_sxuruo.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/dc3a1b49-13d3-4047-b6f8-6cc40b2702a7/%E1%84%8E%E1%85%AC%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A5%E1%84%85%E1%85%B51_sxuruo.png)

위 그림에서 검은색 부분은 벽으로 막혀있어 갈 수 없는 길이며, 흰색 부분은 갈 수 있는 길입니다. 캐릭터가 움직일 때는 동, 서, 남, 북 방향으로 한 칸씩 이동하며, 게임 맵을 벗어난 길은 갈 수 없습니다.  
아래 예시는 캐릭터가 상대 팀 진영으로 가는 두 가지 방법을 나타내고 있습니다.

- 첫 번째 방법은 11개의 칸을 지나서 상대 팀 진영에 도착했습니다.

![최단거리2_hnjd3b.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/9d909e5a-ca95-4088-9df9-d84cb804b2b0/%E1%84%8E%E1%85%AC%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A5%E1%84%85%E1%85%B52_hnjd3b.png)

- 두 번째 방법은 15개의 칸을 지나서 상대팀 진영에 도착했습니다.

![최단거리3_ntxygd.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/4b7cd629-a3c2-4e02-b748-a707211131de/%E1%84%8E%E1%85%AC%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A5%E1%84%85%E1%85%B53_ntxygd.png)

위 예시에서는 첫 번째 방법보다 더 빠르게 상대팀 진영에 도착하는 방법은 없으므로, 이 방법이 상대 팀 진영으로 가는 가장 빠른 방법입니다.

만약, 상대 팀이 자신의 팀 진영 주위에 벽을 세워두었다면 상대 팀 진영에 도착하지 못할 수도 있습니다. 예를 들어, 다음과 같은 경우에 당신의 캐릭터는 상대 팀 진영에 도착할 수 없습니다.

![최단거리4_of9xfg.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/d963b4bd-12e5-45da-9ca7-549e453d58a9/%E1%84%8E%E1%85%AC%E1%84%83%E1%85%A1%E1%86%AB%E1%84%80%E1%85%A5%E1%84%85%E1%85%B54_of9xfg.png)

게임 맵의 상태 maps가 매개변수로 주어질 때, 캐릭터가 상대 팀 진영에 도착하기 위해서 지나가야 하는 칸의 개수의 **최솟값**을 return 하도록 solution 함수를 완성해주세요. 단, 상대 팀 진영에 도착할 수 없을 때는 -1을 return 해주세요.

##### 제한사항

- maps는 n x m 크기의 게임 맵의 상태가 들어있는 2차원 배열로, n과 m은 각각 1 이상 100 이하의 자연수입니다.
    - n과 m은 서로 같을 수도, 다를 수도 있지만, n과 m이 모두 1인 경우는 입력으로 주어지지 않습니다.
- maps는 0과 1로만 이루어져 있으며, 0은 벽이 있는 자리, 1은 벽이 없는 자리를 나타냅니다.
- 처음에 캐릭터는 게임 맵의 좌측 상단인 (1, 1) 위치에 있으며, 상대방 진영은 게임 맵의 우측 하단인 (n, m) 위치에 있습니다.

---

##### 입출력 예

|maps|answer|
|---|---|
|[[1,0,1,1,1],[1,0,1,0,1],[1,0,1,1,1],[1,1,1,0,1],[0,0,0,0,1]]|11|
|[[1,0,1,1,1],[1,0,1,0,1],[1,0,1,1,1],[1,1,1,0,0],[0,0,0,0,1]]|-1|

---

### 문제 풀이
#### 풀이 과정
**아이디어**
n x m 크기의 사각형에서 0,0시작점에서부터 n-1,m-1까지 최단 거리를 구하여라. **=>** `bfs를 활용한 풀이.`

n과 m의 크기를 정의해준다.
x와 y의 이동방향을 담은 변수를 만들어준다.
maps의 크기와 동일한 방문 여부 확인 사각형을 만든다.
초기값을 할당해준다. (시작점, queue)

queue가 빌 때 까지 while문을 반복해준다. `(while문 시작)`
queue에 담긴 칸에 대한 정보를 변수로 할당해준다. (해당 칸에 대한 정보를 가지고 동작)

`종료조건(n-1, m-1에 도착)`을 할당해준다.

현재의 칸에서 `동서남북으로 각각 이동`한다. (동서남북 각각 총 4번 반복)
칸에 이동할 수 있을 경우 방문 처리하고, 해당 칸에 대한 정보를 queue에 담는다.

while문 처음으로 돌아가서 queue에 담긴 해당 칸의 정보를 shift해서 해당 칸으로부터 다시 이동을 반복 한다.

`queue가 모두 비었을 경우`, 모든 칸을 이동할 동안 종료조건(도착지점에 도달)을 만족하지 못했으므로
-1(불가능)을 반환한다.

#### 답안 코드
```
function solution(maps) {

    // 맵의 크기를 지정해준다.
    const n = maps.length
    const m = maps[0].length
    
    // x,y좌표가 이동할 방향을 지정해준다.
    const dx = [0, 1, 0, -1]
    const dy = [1, 0, -1, 0]
    
    // [x좌표,y좌표,이동거리]로 queue의 초기값을 넣어준다.
    const queue = [[0, 0, 1]]
    
    // n x m 형태의 visited 배열에 false를 채워준다.
    const visited = Array.from({ length : n }, () => Array(m).fill(false))
    
    // 시작지점 방문처리
    visited[0][0] = true
  
    // queue가 없어질 때 까지 그래프 탐색
    while (queue.length > 0) {
      const [x, y, distance] = queue.shift()
  
      // 종료 지점에 도달할 시 거리 반환
      if (x === n - 1 && y === m - 1) {
        return distance
      }

	 // 한 칸에서 동,남,서,북 순으로 모두 이동
      for (let i = 0; i < 4; i ++) {
        const nx = x + dx[i]
        const ny = y + dy[i]

        // 이동할 수 있는 칸인지 판별
        if (nx >= 0 && ny >= 0 && nx < n && ny < m &&
            maps[nx][ny] === 1 && !visited[nx][ny]) {

		  // 방문시 방문처리
          visited[nx][ny] = true

		  // 방문한 위치와 해당 위치의 거리 queue에 저장
          queue.push([nx, ny, distance + 1])
        }
          
      }
    }
	
	return -1
}
```

각각의 칸에서 동,서,남,북 으로 모두 이동을 진행하고, 이동한 칸들의 위치를 queue에 저장해가면서 계속 이동한다. 만약 해당 칸에서 이동할 수 없으면 queue에 push하지 못하므로 칸에 대한 정보가 그대로 사라짐.

## Lv. 2 압축
### 문제
신입사원 어피치는 카카오톡으로 전송되는 메시지를 압축하여 전송 효율을 높이는 업무를 맡게 되었다. 메시지를 압축하더라도 전달되는 정보가 바뀌어서는 안 되므로, 압축 전의 정보를 완벽하게 복원 가능한 무손실 압축 알고리즘을 구현하기로 했다.

어피치는 여러 압축 알고리즘 중에서 성능이 좋고 구현이 간단한 **LZW**(Lempel–Ziv–Welch) 압축을 구현하기로 했다. LZW 압축은 1983년 발표된 알고리즘으로, 이미지 파일 포맷인 GIF 등 다양한 응용에서 사용되었다.

LZW 압축은 다음 과정을 거친다.

1. 길이가 1인 모든 단어를 포함하도록 사전을 초기화한다.
2. 사전에서 현재 입력과 일치하는 가장 긴 문자열 `w`를 찾는다.
3. `w`에 해당하는 사전의 색인 번호를 출력하고, 입력에서 `w`를 제거한다.
4. 입력에서 처리되지 않은 다음 글자가 남아있다면(`c`), `w+c`에 해당하는 단어를 사전에 등록한다.
5. 단계 2로 돌아간다.

압축 알고리즘이 영문 대문자만 처리한다고 할 때, 사전은 다음과 같이 초기화된다. 사전의 색인 번호는 정수값으로 주어지며, 1부터 시작한다고 하자.

|색인 번호|1|2|3|...|24|25|26|
|---|---|---|---|---|---|---|---|
|단어|A|B|C|...|X|Y|Z|

예를 들어 입력으로 `KAKAO`가 들어온다고 하자.

1. 현재 사전에는 `KAKAO`의 첫 글자 `K`는 등록되어 있으나, 두 번째 글자까지인 `KA`는 없으므로, 첫 글자 `K`에 해당하는 색인 번호 11을 출력하고, 다음 글자인 `A`를 포함한 `KA`를 사전에 27 번째로 등록한다.
2. 두 번째 글자 `A`는 사전에 있으나, 세 번째 글자까지인 `AK`는 사전에 없으므로, `A`의 색인 번호 1을 출력하고, `AK`를 사전에 28 번째로 등록한다.
3. 세 번째 글자에서 시작하는 `KA`가 사전에 있으므로, `KA`에 해당하는 색인 번호 27을 출력하고, 다음 글자 `O`를 포함한 `KAO`를 29 번째로 등록한다.
4. 마지막으로 처리되지 않은 글자 `O`에 해당하는 색인 번호 15를 출력한다.

|현재 입력(w)|다음 글자(c)|출력|사전 추가(w+c)|
|---|---|---|---|
|K|A|11|27: KA|
|A|K|1|28: AK|
|KA|O|27|29: KAO|
|O||15||

이 과정을 거쳐 다섯 글자의 문장 `KAKAO`가 4개의 색인 번호 [11, 1, 27, 15]로 압축된다.

입력으로 `TOBEORNOTTOBEORTOBEORNOT`가 들어오면 다음과 같이 압축이 진행된다.

|현재 입력(w)|다음 글자(c)|출력|사전 추가(w+c)|
|---|---|---|---|
|T|O|20|27: TO|
|O|B|15|28: OB|
|B|E|2|29: BE|
|E|O|5|30: EO|
|O|R|15|31: OR|
|R|N|18|32: RN|
|N|O|14|33: NO|
|O|T|15|34: OT|
|T|T|20|35: TT|
|TO|B|27|36: TOB|
|BE|O|29|37: BEO|
|OR|T|31|38: ORT|
|TOB|E|36|39: TOBE|
|EO|R|30|40: EOR|
|RN|O|32|41: RNO|
|OT||34||

#### 입력 형식

입력으로 영문 대문자로만 이뤄진 문자열 `msg`가 주어진다. `msg`의 길이는 1 글자 이상, 1000 글자 이하이다.

#### 출력 형식

주어진 문자열을 압축한 후의 사전 색인 번호를 배열로 출력하라.

#### 입출력 예제

| msg                        | answer                                                         |
| -------------------------- | -------------------------------------------------------------- |
| `KAKAO`                    | [11, 1, 27, 15]                                                |
| `TOBEORNOTTOBEORTOBEORNOT` | [20, 15, 2, 5, 15, 18, 14, 15, 20, 27, 29, 31, 36, 30, 32, 34] |
| `ABABABABABABABAB`         | [1, 2, 27, 29, 28, 31, 30]                                     |

---

### 문제 풀이
#### 풀이 과정
문자를 하나씩 순회하면서 사전에 있으면, 사전에 없을 때 까지 다음 문자를 포함시킨다.
사전에 포함되지 않은 문자가 나오면 사전에 포함된 문자까지 포함된 문자의 번호를 출력하고,
포함되지 않은 문자까지 사전에 추가한다.
문자가 끝날 때 까지 해당 작업을 반복.

#### 답안 코드
```
function solution(msg) {
    let answer = [];
    
    // 사전 정의
    const dict = new Map()
    // A ~ Z 사전에 추가
    for (let i = 65; i <= 90; i ++) {
        dict.set(String.fromCharCode(i), i - 64)
    }
    
    let index = 26
    let words = msg.split("").reverse() // 스택 자료구조로 만들기
    let char = words.pop() // char 초기값 부여
    
    while (words.length > 0) {
        index ++ // 새로 추가할 사전 번호 업데이트
        char += words.pop() // 비교할 문자 추가
           
        // 사전에 포함된 문자일경우, 포함되지 않은 문자가 나올 때 까지 char 업데이트
        if (dict.has(char)) {
            while (words.length > 0) {
                char += words.pop()
                if (!dict.has(char)) break
            }
        }
        
        if (words.length == 0) break // char 업데이트를 끝내고, 남아있는 문자가 없으면 종료
        dict.set(char, index) // 사전에 문자 새로 추가
        answer.push(dict.get(char.slice(0,-1))) // 마지막 문자 제외하고 사전에서 번호 추가
        char = char[char.length-1] // char에 마지막 문자만 남겨두기
    }

    // while문 종료 후 남아있는 문자 처리 로직
    if (dict.get(char)) {
        answer.push(dict.get(char))    
    } else {
        answer.push(dict.get(char.slice(0,-1)))
        answer.push(dict.get(char[char.length-1]))
    }
    
    return answer;
}
```

## Lv. 2 [완전 탐색] 모음 사전
### 문제
사전에 알파벳 모음 'A', 'E', 'I', 'O', 'U'만을 사용하여 만들 수 있는, 길이 5 이하의 모든 단어가 수록되어 있습니다. 사전에서 첫 번째 단어는 "A"이고, 그다음은 "AA"이며, 마지막 단어는 "UUUUU"입니다.

단어 하나 word가 매개변수로 주어질 때, 이 단어가 사전에서 몇 번째 단어인지 return 하도록 solution 함수를 완성해주세요.

##### 제한사항

- word의 길이는 1 이상 5 이하입니다.
- word는 알파벳 대문자 'A', 'E', 'I', 'O', 'U'로만 이루어져 있습니다.

---

##### 입출력 예

| word      | result |
| --------- | ------ |
| `"AAAAE"` | 6      |
| `"AAAE"`  | 10     |
| `"I"`     | 1563   |
| `"EIO"`   | 1189   |

---

### 문제 풀이
#### 풀이 과정
사전에서 해당하는 문자가 몇번 째에 위치하는지 반환하여라.

완전탐색 => DFS를 활용하여 사전을 채우고, 해당 단어의 index찾기.

roop돌릴 문자열 모음 배열 생성
빈 사전 생성.
dfs 함수 정의.
길이와 문자를 인수로 받음

종료 조건 설정
길이가 5를 달성할 시 종료

aeiou를 roop돌리면서 dfs함수 호출
dfs함수 호출될 때마다 문자열을 추가해주고, 길이 +1

#### 답안 코드
```
function solution(word) {
    const chars = ["A", "E", "I", "O", "U"]
    const dict = new Map()
    
    let index = 0
    function dfs(cur, len) {
        if (len > 5) return
        dict.set(cur, index++)
        
        for(let i = 0; i < 5; i ++) {
            dfs(cur + chars[i], len + 1)
        }
  
    }
    dfs("", 0)
    
    return dict.get(word)
}
```

DFS 함수를 호출하는 반복문을 어떻게 작동시키는지와 자료구조에 따라 유의미한 시간차이가 발생한다.

**반복문 구현**
`Array 자료구조 기준`
`for문 구현` : 평균 1.8초
`forEach() 구현` : 평균 3초
`for of 구현` : 평균 3.1초

**자료 구조**
`for문 기준`
`Array []` : 평균 1.8초
`Map 객체` : 평균 2.2초
`Object 객체` : 평균 3.5

**반복문 구현 방식**
`for문 >> forEach > for of`

**자료구조**
`Array > Map >> Object`

다만, `Array`와 `Map 객체`를 비교했을 때 단어를 생성하는 시간은 `O(5^5)`로 동일하지만 단어를 검색하는 시간은 Array가 `O(n)`, Map 객체가 `O(1)`로 Map이 우세하다. 해당 문제는 길이가 5로 매우 짧고 검색 횟수가 1회이기 때문에 Array가 약간 더 우세하게 보일 수 있다.

하지만 `단어의 길이와 검색 횟수가 증가할 수록 Map 객체로 구현하는 것이 더욱 효율적이다.`

## Lv. 2 롤케이크 자르기
### 문제
철수는 롤케이크를 두 조각으로 잘라서 동생과 한 조각씩 나눠 먹으려고 합니다. 이 롤케이크에는 여러가지 토핑들이 일렬로 올려져 있습니다. 철수와 동생은 롤케이크를 공평하게 나눠먹으려 하는데, 그들은 롤케이크의 크기보다 롤케이크 위에 올려진 토핑들의 종류에 더 관심이 많습니다. 그래서 잘린 조각들의 크기와 올려진 토핑의 개수에 상관없이 각 조각에 동일한 가짓수의 토핑이 올라가면 공평하게 롤케이크가 나누어진 것으로 생각합니다.

예를 들어, 롤케이크에 4가지 종류의 토핑이 올려져 있다고 합시다. 토핑들을 1, 2, 3, 4와 같이 번호로 표시했을 때, 케이크 위에 토핑들이 [1, 2, 1, 3, 1, 4, 1, 2] 순서로 올려져 있습니다. 만약 세 번째 토핑(1)과 네 번째 토핑(3) 사이를 자르면 롤케이크의 토핑은 [1, 2, 1], [3, 1, 4, 1, 2]로 나뉘게 됩니다. 철수가 [1, 2, 1]이 놓인 조각을, 동생이 [3, 1, 4, 1, 2]가 놓인 조각을 먹게 되면 철수는 두 가지 토핑(1, 2)을 맛볼 수 있지만, 동생은 네 가지 토핑(1, 2, 3, 4)을 맛볼 수 있으므로, 이는 공평하게 나누어진 것이 아닙니다. 만약 롤케이크의 네 번째 토핑(3)과 다섯 번째 토핑(1) 사이를 자르면 [1, 2, 1, 3], [1, 4, 1, 2]로 나뉘게 됩니다. 이 경우 철수는 세 가지 토핑(1, 2, 3)을, 동생도 세 가지 토핑(1, 2, 4)을 맛볼 수 있으므로, 이는 공평하게 나누어진 것입니다. 공평하게 롤케이크를 자르는 방법은 여러가지 일 수 있습니다. 위의 롤케이크를 [1, 2, 1, 3, 1], [4, 1, 2]으로 잘라도 공평하게 나뉩니다. 어떤 경우에는 롤케이크를 공평하게 나누지 못할 수도 있습니다.

롤케이크에 올려진 토핑들의 번호를 저장한 정수 배열 `topping`이 매개변수로 주어질 때, 롤케이크를 공평하게 자르는 방법의 수를 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 1 ≤ `topping`의 길이 ≤ 1,000,000
    - 1 ≤ `topping`의 원소 ≤ 10,000

---

##### 입출력 예

|topping|result|
|---|---|
|[1, 2, 1, 3, 1, 4, 1, 2]|2|
|[1, 2, 3, 1, 4]|0|

---

### 문제 풀이
#### 풀이 과정
토핑 종류 수를 반으로 나누는 방법의 수를 반환

빼는 건 map 객체에서
추가 하는 건 Set 객체에서
값을 추가하는 건 Set이 유용하고, 값을 하나 씩 빼면서 확인하는 건 Map이 유용하다.

#### 답안 코드
```
function solution(topping) {
    let count = 0
    const typeMap = new Map()
    const typeSet = new Set()

	// Map에 토핑 별 개수 추가
    topping.forEach((el) => typeMap.set(el, (typeMap.get(el) + 1 || 1)))
    
    let various = typeMap.size // 종류 수 담기

	// 토핑 개수 확인 로직
    topping.forEach((el) => {
        typeSet.add(el)
        typeMap.set(el, (typeMap.get(el) -1))

		// Map에서 토핑 개수 0개되면 종류수 빼주기
        if (typeMap.get(el) === 0) various --
        
        if (typeSet.size === various) count ++
        
    })    
    return count;
}
```

## Lv. 2 [스택] 뒤에 있는 큰 수 찾기
### 문제
정수로 이루어진 배열 `numbers`가 있습니다. 배열 의 각 원소들에 대해 자신보다 뒤에 있는 숫자 중에서 자신보다 크면서 가장 가까이 있는 수를 뒷 큰수라고 합니다.  
정수 배열 `numbers`가 매개변수로 주어질 때, 모든 원소에 대한 뒷 큰수들을 차례로 담은 배열을 return 하도록 solution 함수를 완성해주세요. 단, 뒷 큰수가 존재하지 않는 원소는 -1을 담습니다.

---

##### 제한사항

- 4 ≤ `numbers`의 길이 ≤ 1,000,000
    - 1 ≤ `numbers[i]` ≤ 1,000,000

---

##### 입출력 예

|numbers|result|
|---|---|
|[2, 3, 3, 5]|[3, 5, 5, -1]|
|[9, 1, 5, 3, 6, 2]|[-1, 5, 6, 6, -1, -1]|

---

### 문제 풀이
#### 풀이 과정
자신보다 뒤에 있으면서 큰 수를 반환해라. 큰 수가 없으면 -1 리턴.

투 포인터로 해결 ? => **시간초과**

**스택을 활용한 풀이**
`numbers`배열을 순회하면서 이전 값들을 index형태로 `stack`에 저장해둔다.
다음 값인 `numbers[i]`의 값이 스택에 있는 값보다 큰 경우 해당 원소의 위치에 `numbers[i]`값을 넣어주는 과정을 stack이 빌 때 까지 while문으로 반복.

`numbers` 배열을 전부 순환할 때 까지 더 큰 값이 나오지 않은 값들은, 인덱스 상태로 stack에 남아있음.
result에 디폴트값으로 -1을 넣어놨기 때문에 stack에서 빠져나가지(뒷 큰수가 없는 값) 않은 값들은 -1을 가진다.

원소로 저장하지 않고 인덱스로 저장하는 이유 => 원소로 저장하게 되면 스택의 값과 `numbers[i]`의 값의 순서 비교가 불가하다.

#### 답안 코드
```
function solution(numbers) {

    let result = Array(numbers.length).fill(-1)
    let stack = []
    for (let i = 0; i < numbers.length; i ++) {
        while(stack.length > 0 && numbers[stack[stack.length-1]] < numbers[i]) {
            result[stack.pop()] = numbers[i]
        }
        stack.push(i)
    }
    return result
}
```

## Lv. 2 [DP] 땅따먹기
### 문제
땅따먹기 게임을 하려고 합니다. 땅따먹기 게임의 땅(land)은 총 N행 4열로 이루어져 있고, 모든 칸에는 점수가 쓰여 있습니다. 1행부터 땅을 밟으며 한 행씩 내려올 때, 각 행의 4칸 중 한 칸만 밟으면서 내려와야 합니다. **단, 땅따먹기 게임에는 한 행씩 내려올 때, 같은 열을 연속해서 밟을 수 없는 특수 규칙이 있습니다.**

예를 들면,

| 1 | 2 | 3 | 5 |

| 5 | 6 | 7 | 8 |

| 4 | 3 | 2 | 1 |

로 땅이 주어졌다면, 1행에서 네번째 칸 (5)를 밟았으면, 2행의 네번째 칸 (8)은 밟을 수 없습니다.

마지막 행까지 모두 내려왔을 때, 얻을 수 있는 점수의 최대값을 return하는 solution 함수를 완성해 주세요. 위 예의 경우, 1행의 네번째 칸 (5), 2행의 세번째 칸 (7), 3행의 첫번째 칸 (4) 땅을 밟아 16점이 최고점이 되므로 16을 return 하면 됩니다.

##### 제한사항

- 행의 개수 N : 100,000 이하의 자연수
- 열의 개수는 4개이고, 땅(land)은 2차원 배열로 주어집니다.
- 점수 : 100 이하의 자연수

##### 입출력 예

|land|answer|
|---|---|
|[[1,2,3,5],[5,6,7,8],[4,3,2,1]]|16|

---

### 문제 풀이
#### 풀이 과정
DFS를 통한 풀이 -> 조합의 개수가 너무 많아 시간초과
시간 복잡도가 (4^10)^5이므로 초과

DP를 활용한 풀이

문제 작게 쪼개기
land배열을 복사한 dp테이블 만들어준다.

다음 방식으로 dp배열을 모두 채워준다.
land배열을 복사한 dp테이블에 2중 for문으로 dp i행 j번째 값에 이전 행의 j번째 값을 제외한 값 중 최대값을 더해준다.

dp테이블의 마지막 행 최대값 반환

#### 답안 코드
```
function solution(land) {
    
    // 행 크기 정의
    const N = land.length
    // DP테이블 생성
    let dp = []
    
    //DP테이블에 land복사해서 초기값 채우기
    for (let i = 0; i < N; i ++ ) {
        dp[i] = land[i].slice()    
    }
    
    // 각 행을 이전 행의 같은 위치를 제외한 최대값에 더해줘서 채워나가기
    for(let i = 1; i < N; i ++) {
        for (let j = 0; j < 4; j ++) {
            // 각각 1,2,3씩 더하고 %4를 해줌으로써 같은 열의 값을 더해주는 것을 방지.
            // ex j가 2일 때 1, 2, 3을 더해주면 => 3,4,5 4로 나눈 나머지 값 => 3, 0, 1
            dp[i][j] += Math.max(dp[i-1][(j + 1) % 4], dp[i-1][(j + 2) % 4], dp[i-1][(j + 3) % 4])
        }
    }
    
    return Math.max(...dp[N-1])
}
```

DP테이블 값을 채워주는 과정에서 각 숫자 더하고 최대값의 나머지를 구함으로써 같은 열의 값을 피할 수 있다.

## Lv. 2 [스택/큐] 주식가격
### 문제
초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때, 가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.

##### 제한사항

- prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.
- prices의 길이는 2 이상 100,000 이하입니다.

##### 입출력 예

|prices|return|
|---|---|
|[1, 2, 3, 2, 3]|[4, 3, 1, 1, 0]|

---

### 문제 풀이
#### 풀이 과정
**각 가격 별로 몇 초간 가격이 떨어지지 않았는지 반환.**

**비교 방법**
해당 가격을 쭉 돌면서 자신보다 낮아지는 지점을 찾는다.
해당 지점까지의 거리를 `answer`배열에 추가한다.
모든 가격에 대해 해당 작업 반복.

**스택을 통한 비교방법**
`prices`를 돌면서 `stack`에 추가한다.
`stack`의 마지막 값이 추가할 값보다 작거나 같다면 계속 추가한다.
`stack`의 마지막 값이 추가할 값보다 크다면 가격이 떨어진 것이므로 `.pop()`을 하면서 answer배열에 시간을 추가한다.`(시간을 알아내는 방법? stack에 추가할 때 원소 말고 index로 저장한다.)`
가격이 한 번 떨어지면 stack의 마지막 값과 계속 비교하면서 또 떨어진 값이있나 찾아낸다. 
`떨어진 값이 있으면` 해당 값을 pop하고 시간을 추가한다.
`떨어진 값이 없으면` 계속해서 마지막 값과 비교하면서 값을 추가한다.

마지막에 stack에 값이 남은 index들은, 해당 시간부터 종료 시점까지 살아남았으므로 `길이 - (index + 1)`만큼 해당 index를 추가한다.
맨 마지막 값은 0이므로 비교하지 않는다.

#### 답안 코드
```
function solution(prices) {
    let result = new Array(prices.length).fill(0)
    let stack = [0]
    let idx = 0
    for(let i = 1; i < prices.length-1; i++) {
        while (stack.length > 0 && prices[stack[stack.length-1]] > prices[i]) {
            idx = stack.pop()
            result[idx] = i - idx
        }
        stack.push(i)
    }
    stack.forEach((el) => {
        result[el] = prices.length - (el + 1)
    })
    return result;
}
```


## Lv. 2 [스택/큐] 다리를 지나는 트럭
### 문제
트럭 여러 대가 강을 가로지르는 일차선 다리를 정해진 순으로 건너려 합니다. 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다. 다리에는 트럭이 최대 bridge_length대 올라갈 수 있으며, 다리는 weight 이하까지의 무게를 견딜 수 있습니다. 단, 다리에 완전히 오르지 않은 트럭의 무게는 무시합니다.

예를 들어, 트럭 2대가 올라갈 수 있고 무게를 10kg까지 견디는 다리가 있습니다. 무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.

|경과 시간|다리를 지난 트럭|다리를 건너는 트럭|대기 트럭|
|---|---|---|---|
|0|[]|[]|[7,4,5,6]|
|1~2|[]|[7]|[4,5,6]|
|3|[7]|[4]|[5,6]|
|4|[7]|[4,5]|[6]|
|5|[7,4]|[5]|[6]|
|6~7|[7,4,5]|[6]|[]|
|8|[7,4,5,6]|[]|[]|

따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

solution 함수의 매개변수로 다리에 올라갈 수 있는 트럭 수 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭 별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.

##### 제한 조건

- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.

##### 입출력 예

|bridge_length|weight|truck_weights|return|
|---|---|---|---|
|2|10|[7,4,5,6]|8|
|100|100|[10]|101|
|100|100|[10,10,10,10,10,10,10,10,10,10]|110|

---

### 문제 풀이
#### 풀이 과정
다리의 길이를 1당 1칸이라고 생각하고, 1칸 이동하는데 1초가 소요된다.
트럭을 올릴 다리를 `queue`구조로 구성.
트럭의 무게, 탈출까지 남은 시간을 배열로 담아준다.
트럭을 올림과 동시에 현재 무게를 나타내는 변수 currWeight변수를 업데이트 해준다.
트럭을 더 올릴 수 있을 경우, 트럭을 계속 올림과 동시에 대기시간을 1씩 빼준다.
대기시간이 0이 되면 트럭은 탈출한다.

`트럭은 한 대씩 순차적으로 올라가므로, 남아있는 시간이 동일할 수는 없다.`

#### 답안 코드
```
function solution(bridge_length, weight, truck_weights) {
    // 총 소요 시간
    let time = 0 
    // 트럭을 담을 스택
    let stack = []
    // 현재 올라와있는 트럭들의 무게를 나타내는 변수
    let currWeight = 0

    while (truck_weights.length > 0) {
        let leftTime = 0
        
        // [무게,남은 시간]으로 트럭을 계속 담아주면서 1초씩 +
        while (weight >= currWeight + truck_weights[0] && bridge_length > stack.length) {
            //  stack에 트럭이 이미 올라와 있으면 남은 시간 1초 빼주기
            if (stack.length > 0) {
                stack.map((el) => el[1] -= 1)
                // 남은시간 0이 되면 탈출
                if(stack[0][1] <= 0) {
                    currWeight -= stack[0][0]
                    stack.shift()
                }
            }
            time += 1
            currWeight += truck_weights[0]
            stack.push([truck_weights.shift(),bridge_length])
        }
        // 트럭을 더 올릴 수 없으면, 맨 앞차가 빠져나갈 때 까지의 시간을 모두 빼줌.
        
        leftTime = stack[0][1] // 첫 번째 트럭이 나가기까지 남은시간
        stack.map((el) => {
            el[1] -= leftTime
        })
        currWeight -= stack[0][0]
        stack.shift()
        
        // 첫 번째 트럭이 나가면서 새로 트럭이 들어올 수 있으면 추가
        if (truck_weights.length > 0 && weight >= currWeight + truck_weights[0] && bridge_length > stack.length) {
            currWeight += truck_weights[0]
            stack.push([truck_weights.shift(), bridge_length])
        }
        
        // 시간에 첫 번째 트럭이 나간 시간 추가
        time += leftTime
    } // while문 종료
    
    if(stack.length > 0) time += stack[stack.length-1][1]
  
    return time;
}
```

무게를 업데이트 하는 부분에서 stack의 마지막 트럭을 추가해 주는 게 아니라,
맨 앞 트럭의 무게를 추가해 주는 바람에 해당 문제를 해결하느라 시간이 많이 소요되었다.
**오류 발생 시 사용한 변수들을 모두 확인해보는 습관을 들이자.**

## Lv. 2 스킬트리
### 문제
선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.

예를 들어 선행 스킬 순서가 `스파크 → 라이트닝 볼트 → 썬더`일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.

위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 `스파크 → 힐링 → 라이트닝 볼트 → 썬더`와 같은 스킬트리는 가능하지만, `썬더 → 스파크`나 `라이트닝 볼트 → 스파크 → 힐링 → 썬더`와 같은 스킬트리는 불가능합니다.

선행 스킬 순서 skill과 유저들이 만든 스킬트리[1](https://school.programmers.co.kr/learn/courses/30/lessons/49993#fn1)를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.

##### 제한 조건

- 스킬은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있습니다.
- 스킬 순서와 스킬트리는 문자열로 표기합니다.
    - 예를 들어, `C → B → D` 라면 "CBD"로 표기합니다
- 선행 스킬 순서 skill의 길이는 1 이상 26 이하이며, 스킬은 중복해 주어지지 않습니다.
- skill_trees는 길이 1 이상 20 이하인 배열입니다.
- skill_trees의 원소는 스킬을 나타내는 문자열입니다.
    - skill_trees의 원소는 길이가 2 이상 26 이하인 문자열이며, 스킬이 중복해 주어지지 않습니다.

##### 입출력 예

|skill|skill_trees|return|
|---|---|---|
|`"CBD"`|`["BACDE", "CBADF", "AECB", "BDA"]`|2|

---

### 문제 풀이
#### 풀이 과정
유저들이 만든 스킬트리를 보고, 가능한 스킬트리 개수를 반환

스킬 트리에서 skill에 포함된 문자 말고는 필요 X
skill의 문자를 dict에 넣고, 포함 여부를 통해 skill_trees의 문자를 걸러냄.
포함되는 문자만 dict와 비교해 index가 순차적으로 올라가지 않으면 false.

#### 답안 코드
```
function solution(skill, skill_trees) {
    let result = 0;
    const skillDict = new Map()
    for(let i = 0; i < skill.length; i ++) {
        skillDict.set(skill[i], i)
    }
    
    for (let i = 0; i < skill_trees.length; i++ ) {
        let index = 0
        let avaliable = true
        for(let j = 0; j < skill_trees[i].length; j ++) {
            let skill = skill_trees[i][j]
            if(skillDict.has(skill)) {
                if (skillDict.get(skill) === index) index += 1
                else {
                    avaliable = false
                    break
                }
            }
        }
        if (avaliable) result += 1
    }
    
    return result;
}
```


## Lv. 2 방문 길이
### 문제
게임 캐릭터를 4가지 명령어를 통해 움직이려 합니다. 명령어는 다음과 같습니다.

- U: 위쪽으로 한 칸 가기
    
- D: 아래쪽으로 한 칸 가기
    
- R: 오른쪽으로 한 칸 가기
    
- L: 왼쪽으로 한 칸 가기
    

캐릭터는 좌표평면의 (0, 0) 위치에서 시작합니다. 좌표평면의 경계는 왼쪽 위(-5, 5), 왼쪽 아래(-5, -5), 오른쪽 위(5, 5), 오른쪽 아래(5, -5)로 이루어져 있습니다.

![방문길이1_qpp9l3.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/ace0e7bc-9092-4b95-9bfb-3a55a2aa780e/%E1%84%87%E1%85%A1%E1%86%BC%E1%84%86%E1%85%AE%E1%86%AB%E1%84%80%E1%85%B5%E1%86%AF%E1%84%8B%E1%85%B51_qpp9l3.png)

예를 들어, "ULURRDLLU"로 명령했다면

![방문길이2_lezmdo.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/668c7458-e184-472d-9d32-f5d2acca759a/%E1%84%87%E1%85%A1%E1%86%BC%E1%84%86%E1%85%AE%E1%86%AB%E1%84%80%E1%85%B5%E1%86%AF%E1%84%8B%E1%85%B52_lezmdo.png)

- 1번 명령어부터 7번 명령어까지 다음과 같이 움직입니다.

![방문길이3_sootjd.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/08558e36-d667-4160-bfec-b754c78a7d85/%E1%84%87%E1%85%A1%E1%86%BC%E1%84%86%E1%85%AE%E1%86%AB%E1%84%80%E1%85%B5%E1%86%AF%E1%84%8B%E1%85%B53_sootjd.png)

- 8번 명령어부터 9번 명령어까지 다음과 같이 움직입니다.

![방문길이4_hlpiej.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/a52af28e-5835-438b-9f40-5467ebf9bf03/%E1%84%87%E1%85%A1%E1%86%BC%E1%84%86%E1%85%AE%E1%86%AB%E1%84%80%E1%85%B5%E1%86%AF%E1%84%8B%E1%85%B54_hlpiej.png)

이때, 우리는 게임 캐릭터가 지나간 길 중 **캐릭터가 처음 걸어본 길의 길이**를 구하려고 합니다. 예를 들어 위의 예시에서 게임 캐릭터가 움직인 길이는 9이지만, 캐릭터가 처음 걸어본 길의 길이는 7이 됩니다. (8, 9번 명령어에서 움직인 길은 2, 3번 명령어에서 이미 거쳐 간 길입니다)

단, 좌표평면의 경계를 넘어가는 명령어는 무시합니다.

예를 들어, "LULLLLLLU"로 명령했다면

![방문길이5_nitjwj.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/f631f005-f8de-4392-a76c-a9ef64b6de08/%E1%84%87%E1%85%A1%E1%86%BC%E1%84%86%E1%85%AE%E1%86%AB%E1%84%80%E1%85%B5%E1%86%AF%E1%84%8B%E1%85%B55_nitjwj.png)

- 1번 명령어부터 6번 명령어대로 움직인 후, 7, 8번 명령어는 무시합니다. 다시 9번 명령어대로 움직입니다.

![방문길이6_nzhumd.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/35e62f0a-43c6-4142-bec6-6d28fbc57216/%E1%84%87%E1%85%A1%E1%86%BC%E1%84%86%E1%85%AE%E1%86%AB%E1%84%80%E1%85%B5%E1%86%AF%E1%84%8B%E1%85%B56_nzhumd.png)

이때 캐릭터가 처음 걸어본 길의 길이는 7이 됩니다.

명령어가 매개변수 dirs로 주어질 때, 게임 캐릭터가 처음 걸어본 길의 길이를 구하여 return 하는 solution 함수를 완성해 주세요.

##### 제한사항

- dirs는 string형으로 주어지며, 'U', 'D', 'R', 'L' 이외에 문자는 주어지지 않습니다.
- dirs의 길이는 500 이하의 자연수입니다.

##### 입출력 예

|dirs|answer|
|---|---|
|"ULURRDLLU"|7|
|"LULLLLLLU"|7|

---

### 문제 풀이
#### 풀이 과정
10 * 10 좌표평면에서 캐릭터가 처음 이동한 길의 길이 총 합을 구해라.

왔던 길인지 판별하는 방법
하나의 길을 이동하는 방법은 총 두 가지
한 번의 이동마다 두 가지 경로를 모두 문자열 형태로 저장.
해당 경로가 저장되어 있으면 횟수 추가 x

#### 답안 코드
```
function solution(dirs) {
    let distance = 0;
    const pathMap = new Map()
    pathMap.set("R", 0)
    pathMap.set("D", 1)
    pathMap.set("L", 2)
    pathMap.set("U", 3)
    
    const dx = [0, 1, 0, -1]
    const dy = [1, 0, -1, 0]
    let x = 0
    let y = 0
    let route1 = ""
    let route2 = ""
    let pathList = []
    for(let i = 0; i < dirs.length; i ++) {
        let nx = x + dx[pathMap.get(dirs[i])]
        let ny = y + dy[pathMap.get(dirs[i])]
        if (nx > 5 || ny > 5 || nx < -5 || ny < -5 ) {
            continue
        }
        route1 = x.toString() + y.toString() + nx.toString() + ny.toString()
        route2 = nx.toString() + ny.toString() + x.toString() + y.toString()
        x = nx
        y = ny
        if (pathList.includes(route1)) continue
        pathList.push(route1)
        pathList.push(route2)
        distance ++
    }
    return distance;
}
```

문제 풀기에 집중하다보니 변수가 너무 많고, 가독성이 떨어진다.

#### 코드 리팩토링
```
function solution(dirs) {
    let distance = 0;
    const directions = {
        R: [0, 1],
        D: [1, 0],
        L: [0, -1],
        U: [-1, 0]
    };
    
    const pathSet = new Set();
    let x = 0, y = 0;
    
    for (const dir of dirs) {
        const [dx, dy] = directions[dir];
        const nx = x + dx;
        const ny = y + dy;
        
        if (nx > 5 || ny > 5 || nx < -5 || ny < -5) {
            continue;
        }
        
        const route1 = `${x},${y},${nx},${ny}`;
        const route2 = `${nx},${ny},${x},${y}`;
        
        if (!pathSet.has(route1)) {
            pathSet.add(route1);
            pathSet.add(route2);
            distance++;
        }
        
        x = nx;
        y = ny;
    }
    
    return distance;
}

```

방향별 이동거리를 나타내는 directions를 객체로 정의한 뒤 `[dx,dy]`로 꺼내서 사용.
경로를 담아두는 배열을 set로 만들어서 중복 방지.
문자열로 저장하는 과정을 백틱을 사용하여 간결화.

## Lv. 2 주차 요금 계산
### 문제
주차장의 요금표와 차량이 들어오고(입차) 나간(출차) 기록이 주어졌을 때, 차량별로 주차 요금을 계산하려고 합니다. 아래는 하나의 예시를 나타냅니다.

- **요금표**

|기본 시간(분)|기본 요금(원)|단위 시간(분)|단위 요금(원)|
|---|---|---|---|
|180|5000|10|600|

- **입/출차 기록**

|시각(시:분)|차량 번호|내역|
|---|---|---|
|05:34|5961|입차|
|06:00|0000|입차|
|06:34|0000|출차|
|07:59|5961|출차|
|07:59|0148|입차|
|18:59|0000|입차|
|19:09|0148|출차|
|22:59|5961|입차|
|23:00|5961|출차|

- **자동차별 주차 요금**

|차량 번호|누적 주차 시간(분)|주차 요금(원)|
|---|---|---|
|0000|34 + 300 = 334|5000 + `⌈`(334 - 180) / 10`⌉` x 600 = 14600|
|0148|670|5000 +`⌈`(670 - 180) / 10`⌉`x 600 = 34400|
|5961|145 + 1 = 146|5000|

- 어떤 차량이 입차된 후에 출차된 내역이 없다면, 23:59에 출차된 것으로 간주합니다.
    - `0000`번 차량은 18:59에 입차된 이후, 출차된 내역이 없습니다. 따라서, 23:59에 출차된 것으로 간주합니다.
- 00:00부터 23:59까지의 입/출차 내역을 바탕으로 차량별 누적 주차 시간을 계산하여 요금을 일괄로 정산합니다.
- 누적 주차 시간이 `기본 시간`이하라면, `기본 요금`을 청구합니다.  
    
- 누적 주차 시간이 `기본 시간`을 초과하면, `기본 요금`에 더해서, 초과한 시간에 대해서 `단위 시간` 마다 `단위 요금`을 청구합니다.
    - 초과한 시간이 `단위 시간`으로 나누어 떨어지지 않으면, `올림`합니다.  
        
    - `⌈`a`⌉` : a보다 작지 않은 최소의 정수를 의미합니다. 즉, `올림`을 의미합니다.

주차 요금을 나타내는 정수 배열 `fees`, 자동차의 입/출차 내역을 나타내는 문자열 배열 `records`가 매개변수로 주어집니다. **차량 번호가 작은 자동차부터** 청구할 주차 요금을 차례대로 정수 배열에 담아서 return 하도록 solution 함수를 완성해주세요.

##### 제한사항

- `fees`의 길이 = 4
    
    - fees[0] = `기본 시간(분)`
    - 1 ≤ fees[0] ≤ 1,439
    - fees[1] = `기본 요금(원)`
    - 0 ≤ fees[1] ≤ 100,000
    - fees[2] = `단위 시간(분)`
    - 1 ≤ fees[2] ≤ 1,439
    - fees[3] = `단위 요금(원)`
    - 1 ≤ fees[3] ≤ 10,000
- 1 ≤ `records`의 길이 ≤ 1,000
    
    - `records`의 각 원소는 `"시각 차량번호 내역"` 형식의 문자열입니다.
    - `시각`, `차량번호`, `내역`은 하나의 공백으로 구분되어 있습니다.
    - `시각`은 차량이 입차되거나 출차된 시각을 나타내며, `HH:MM` 형식의 길이 5인 문자열입니다.
        - `HH:MM`은 00:00부터 23:59까지 주어집니다.
        - 잘못된 시각("25:22", "09:65" 등)은 입력으로 주어지지 않습니다.
    - `차량번호`는 자동차를 구분하기 위한, `0'~'9'로 구성된 길이 4인 문자열입니다.  
        
    - `내역`은 길이 2 또는 3인 문자열로, `IN` 또는 `OUT`입니다. `IN`은 입차를, `OUT`은 출차를 의미합니다.
    - `records`의 원소들은 시각을 기준으로 오름차순으로 정렬되어 주어집니다.
    - `records`는 하루 동안의 입/출차된 기록만 담고 있으며, 입차된 차량이 다음날 출차되는 경우는 입력으로 주어지지 않습니다.
    - 같은 시각에, 같은 차량번호의 내역이 2번 이상 나타내지 않습니다.
    - 마지막 시각(23:59)에 입차되는 경우는 입력으로 주어지지 않습니다.
    - 아래의 예를 포함하여, 잘못된 입력은 주어지지 않습니다.
        - 주차장에 없는 차량이 출차되는 경우
        - 주차장에 이미 있는 차량(차량번호가 같은 차량)이 다시 입차되는 경우

---

##### 입출력 예

|fees|records|result|
|---|---|---|
|[180, 5000, 10, 600]|`["05:34 5961 IN", "06:00 0000 IN", "06:34 0000 OUT", "07:59 5961 OUT", "07:59 0148 IN", "18:59 0000 IN", "19:09 0148 OUT", "22:59 5961 IN", "23:00 5961 OUT"]`|[14600, 34400, 5000]|
|[120, 0, 60, 591]|`["16:00 3961 IN","16:00 0202 IN","18:00 3961 OUT","18:00 0202 OUT","23:58 3961 IN"]`|[0, 591]|
|[1, 461, 1, 10]|`["00:00 1234 IN"]`|[14841]|

---

### 문제 풀이
#### 풀이 과정
fees에 담긴 데이터
기본시간, 기본 요금, t, m (t분당 m원 부여)

먼저 `records에서` 데이터를 추출한다.
enterMap에 입차 데이터 번호(string): 시간(int)으로 map객체 구성
한 차량에 대해서 입차 -> 출차 순으로 이루어지므로
출차하는 차량이 나오면 객체에 대조해서 주차시간 누적 후 출차처리.
대조가 모두 끝나고 객체에 남은 값은 23:59 출차이므로, 해당 시간에 맞춰 주차시간 누적.
요금 계산을 누적주차시간으로 계산하므로, 누적 시간을 담아 둘 공간이 필요.

차량 번호순대로 순서를 정렬하고 누적된 시간에 따라 요금을 계산하여 반환.

**소요시간** : `2시간 30분`

#### 답안 코드
```
function solution(fees, records) {
    let result = [];
    let enterMap = new Map(), timeMap = new Map(), carData = [], currTime = 0, charge = 0
    
    // 시간 저장 함수
    const accuTime = (carNum, outTime) => {
        let hour = 0, minute = 0, totalMinute = 0, charge = fees[1]
        hour = parseInt(outTime[0]) - parseInt(enterMap.get(carNum)[0])
        minute = parseInt(outTime[1]) - parseInt(enterMap.get(carNum)[1])
        if (minute < 0) {
            hour -= 1
            minute += 60
        }
        totalMinute = (hour * 60 + minute)
        return totalMinute
    }
    
    // 출차, 입차 데이터 저장
    records.forEach((car) => {
        carData = car.split(" ")
        currTime = carData[0].split(":")
        // 입차하는 차량 데이터 저장
        if (carData[2] === "IN") {
            enterMap.set(carData[1], currTime)
            // 출차하는 차량 시간 누적
        } else {
            // 누적시간
            charge = accuTime(carData[1], currTime)
            // 차 별로 시간 누적
            timeMap.set(carData[1], (timeMap.get(carData[1]) + charge) || charge)
            // 출차 처리
            enterMap.delete(carData[1])
        }
    })
    
    // 출차하지 않은 차 시간 누적
    if (enterMap.size > 0) {
        for (let number of enterMap.keys()) {
            charge = accuTime(number, ["23", "59"])    
            timeMap.set (number, (timeMap.get(number) + charge) || charge)
        }
    }
    let timeOfCar = []
    for (let [key, value] of timeMap.entries()) {
        timeOfCar.push([key, value])        
    }
    let fee = 0
    timeOfCar.sort((a, b) => parseInt(a[0]) - parseInt(b[0])).forEach((totalMinute) => {
        fee = fees[1]
        totalMinute = totalMinute[1] - fees[0]
        if (totalMinute > 0) {
            fee += totalMinute % fees[2] === 0 ? (totalMinute / fees[2]) * fees[3] :
            (Math.floor(totalMinute / fees[2]) + 1) * fees[3]
        }
        result.push(fee)
    })

    return result;
}
```
코드가 너무 길고, 변수가 너무 많으며 선언이 뒤죽박죽 되어 있어 찾기가 힘들다.

#### 코드 리팩토링 
```
function solution(fees, records) {
    let result = [];
    let enterMap = new Map();
    let timeMap = new Map();

    // 입차 시간과 출차 시간을 계산하여 총 주차 시간을 반환하는 함수
    const calculateParkingTime = (inTime, outTime) => {
        let [inHour, inMinute] = inTime.map(Number);
        let [outHour, outMinute] = outTime.map(Number);
        let totalMinutes = (outHour * 60 + outMinute) - (inHour * 60 + inMinute);

        return totalMinutes;
    };

    // 주차 요금을 계산하는 함수
    const calculateFee = (totalMinutes) => {
        const [baseTime, baseFee, unitTime, unitFee] = fees;
        if (totalMinutes <= baseTime) return baseFee;

        return baseFee + Math.ceil((totalMinutes - baseTime) / unitTime) * unitFee;
    };

    // 출입 기록을 처리하여 주차 시간을 계산
    records.forEach((record) => {
        let [time, carNum, action] = record.split(" ");
        let [hour, minute] = time.split(":");

        if (action === "IN") {
            enterMap.set(carNum, [hour, minute]);
        } else {
            let inTime = enterMap.get(carNum);
            let parkingTime = calculateParkingTime(inTime, [hour, minute]);
            enterMap.delete(carNum);

            if (timeMap.has(carNum)) {
                timeMap.set(carNum, timeMap.get(carNum) + parkingTime);
            } else {
                timeMap.set(carNum, parkingTime);
            }
        }
    });

    // 출차 기록이 없는 차량 처리
    enterMap.forEach((inTime, carNum) => {
        let parkingTime = calculateParkingTime(inTime, ["23", "59"]);
        if (timeMap.has(carNum)) {
            timeMap.set(carNum, timeMap.get(carNum) + parkingTime);
        } else {
            timeMap.set(carNum, parkingTime);
        }
    });

    // 차량 번호 순으로 정렬하고 요금 계산
    let sortedCars = [...timeMap.entries()].sort((a, b) => a[0] - b[0]);
    sortedCars.forEach(([carNum, totalMinutes]) => {
        result.push(calculateFee(totalMinutes));
    });

    return result;
}
```

### 문제 풀이를 마치고
처음에 로직을 설계할 때는 20분만에 완료 되어 오래 걸릴 것이라고 생각하지 않았는데, 지문을 급하게 읽고 설계하려다 보니 여러 문제가 발생했다.

**시간을 시와 분을 합쳐 4자리 숫자로 연산 하여 연산이 제대로 이루어지지 않았다.**
- 시,분을 각각 배열로 저장하여 시간 계산과 분 계산을 따로 나누어 주었다.

- `해결 방안` : 연산이 제대로 이루어 질지 먼저 테스트해보고 진행하자.

**누적 출차시간이 아닌 출차마다 요금을 계산**
- 주차 시간을 누적 한 뒤, 한 번에 계산하는 것이 아니라 차가 출차할 때마다 요금을 계산하여 아예 다른 값이 나오게 되었다.

- `해결 방안` : 지문을 꼼곰히 읽고 예제가 해결되는 로직을 자세히 살펴보아서 처음 로직을 설계할 때 어떤 기능을 어느 순서에 배치할 지 명확히 구성하자.

**변수 이름을 알아보기가 힘들고 선언된 위치를 찾기 힘듬**
- 변수를 반복만이나 if문 위에 선언하게 되면 코드가 길어지는 것은 물론이고, 선언된 위치를 찾기 힘들다. 해당 변수를 사용하는 위치에서 let이나 const를 통해 선언하고 사용하자.
- 변수 이름이 명확하지 못해 코드를 작성 하면서도 어떤 기능을 하는지 알아보기가 힘들었다. 너무 짧게 선언하려고 해서 생긴 문제.
- 주어진 예시 데이터에서 변수를 선언하지 않고 index를 통해 사용하려고 했더니 어떤 데이터인지 명확히 알아볼 수가 없다.

- `해결 방안` : **변수는 사용하는 곳에서 선언**, **변수 이름은 기능을 이해할 수 있게끔 명확히 선언**, **index를 통해 데이터를 사용하지 말고 변수로 선언해서 어떤 데이터인지 명시**


## Lv. 2 택배상자
### 문제

### 문제 풀이
#### 풀이 과정
order에 놓인 박스의 순서가 직관적이지 못하다고 생각하여, 컨베이어 벨트에 놓인 대로 순서를 배치한 priority를 만들어주었다.
shift를 통해 박스를 빼오면 시간복잡도가 초과되므로, pop을 통해 박스를 빼오며 해당 인덱스와 맞는지 확인하고, 만약 임시 보관함의 박스가 인덱스와 일치하면, 일치하지 않을 때 까지 계속해서 박스를 빼준다.
더이상 보관함에 넣을 박스가 없으면 보관함에 있는 박스를 확인하고 종료.

#### 답안 코드
```
function solution(order) {
    let priority = []
    let length = order.length
    // 맨 뒤부터 시작해서 박스가 놓인 순서대로, 해당 박스에 순서를 담아 정렬
    for (let i = 0; i < order.length; i ++) {
        priority[length - order[i]] = i+1
    }
    // 임시 보관함 생성
    let temp = []
    // 순서를 나타내는 변수
    let index = 1
    // 컨베이어 벨트가 빌 때 까지 박스 분류
    while (priority.length > 0) {
        let box = priority.pop()
        if (box === index) {
            index ++
            // 보조 컨베이어 벨트 마지막 박스가 해당하면 빼주기
            while (temp.length > 0) {
                if(temp[temp.length-1] === index) {
                    temp.pop()
                    index++
                } else break
            }
        }
        else {
            temp.push(box)
        }
    }
    
    return index - 1
}
```

#### 다른 풀이
```
function solution(order) {
    const stack = [];
    let currentBox = 1;
    let index = 0;
    const n = order.length;

    for (let i = 0; i < n; i++) {
        const targetBox = order[i];

        while (currentBox <= targetBox) {
            stack.push(currentBox++);
        }

        if (stack[stack.length - 1] === targetBox) {
            stack.pop();
            index++;
        } else {
            break;
        }
    }

    return index;
}
```
박스를 재정렬하지 않고 그대로 풀면 시간복잡도는 O(n)으로 동일하지만, 조금 더 효율적으로 나온다.

## Lv. 2 가장 큰 수
### 문제
0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.

##### 제한 사항

- numbers의 길이는 1 이상 100,000 이하입니다.
- numbers의 원소는 0 이상 1,000 이하입니다.
- 정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.

##### 입출력 예

|numbers|return|
|---|---|
|[6, 10, 2]|"6210"|
|[3, 30, 34, 5, 9]|"9534330"|

---

### 문제 풀이
#### 풀이 과정
a와 b가 있을 때  a&b와 b&a중 앞에 왔을 때 큰 수를 만드는 순서가 되도록 정렬한다. (&는 두 수를 문자열로 붙이는걸 의미)
반복문으로 모든 수를 비교하면서 구현하기에는 시간복잡도가 초과되므로, sort메서드를 사용해 정렬한다. sort는 Timesort 정렬 알고리즘을 사용하므로, 시간 복잡도가 O(n log n)이다. Timesort를 직접 구현하기에는 매우 복잡하다.

**정렬 알고리즘**
`sort((a, b) => (b + a) - (a + b))`
a와 b를 각각 문자열로 받아서 문자열로 더한 값을 숫자로 변환해서 계산한다.
음수가 나오면 b가 앞으로 양수가 나오면 a가 앞으로오게 정렬.

#### 답안 코드
```
function solution(numbers) {
    numbers = numbers.map((num) => num.toString()).sort((a,b) => (b + a) - (a + b)).join("")
    if (numbers[0] === "0") return "0"
    return numbers
}
```

### 풀이를 마치고
`sort() 메서드`가 숫자를 연산해서 순서를 정하는 것은 알고 있었지만, 괄호안에 `(b + a)`연산까지 문자열로 계산한다는 사실은 모르고 있었다. 이후 `-`는 숫자로 변환해서 연산하는 사실은 동일하다.

## Lv. 2 [힙(heap)] 더 맵게
### 문제
매운 것을 좋아하는 Leo는 모든 음식의 스코빌 지수를 K 이상으로 만들고 싶습니다. 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 Leo는 스코빌 지수가 가장 낮은 두 개의 음식을 아래와 같이 특별한 방법으로 섞어 새로운 음식을 만듭니다.

```
섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
```

Leo는 모든 음식의 스코빌 지수가 K 이상이 될 때까지 반복하여 섞습니다.  
Leo가 가진 음식의 스코빌 지수를 담은 배열 scoville과 원하는 스코빌 지수 K가 주어질 때, 모든 음식의 스코빌 지수를 K 이상으로 만들기 위해 섞어야 하는 최소 횟수를 return 하도록 solution 함수를 작성해주세요.

##### 제한 사항

- scoville의 길이는 2 이상 1,000,000 이하입니다.
- K는 0 이상 1,000,000,000 이하입니다.
- scoville의 원소는 각각 0 이상 1,000,000 이하입니다.
- 모든 음식의 스코빌 지수를 K 이상으로 만들 수 없는 경우에는 -1을 return 합니다.

##### 입출력 예

| scoville             | K   | return |
| -------------------- | --- | ------ |
| [1, 2, 3, 9, 10, 12] | 7   | 2      |
### 문제 풀이
#### 풀이 과정
최소 힙(Min Heap)으로 구현.

**힙 알고리즘이란 ?**
이진 트리의 구조로써, 루트 노드에는 최대값(Max heap 기준)이 위치하고,
리프 노드를 제외한 모든 노드는 자신보다 낮은 값을 가진 2개의 자식노드를 가지고 있는 형태이다.

**필요한 메서드 목록**
사이즈 확인
삽입 (heapifyup)
삭제 (heapifydown)
index 교체
index 구하기

#### 답안 코드
```
function solution(scoville, K) {
    let minHeap = new MinHeap(scoville)
    
    let count = 0
    while (minHeap.peak() < K && minHeap.size() >= 2) {
        let first = minHeap.remove()
        let second = minHeap.remove()
        
        
        minHeap.insert(first + (second * 2))
        count ++
    }
    
    if(minHeap.peak() < K) {
        return -1
    }
    return count
}

class MinHeap {
    constructor (values = []) {
        this.heap = []
        
        for (let value of values) {
            this.insert(value)
        }
    }
    
    getParentIdx (index) {
        return Math.floor((index - 1) / 2)
    }
    
    getLeftIdx (index) {
        return index * 2 + 1
    }
    
    getRightIdx (index) {
        return index * 2 + 2
    }
    
    swap (index1, index2) {
        [this.heap[index1], this.heap[index2]] = [this.heap[index2], this.heap[index1]]
    }
    
    insert (value) {
        this.heap.push(value)
        this.heapifyUp()
    }
    
    heapifyUp () {
        let index = this.heap.length - 1
        while (index > 0){
            let parentIdx = this.getParentIdx(index)
            if (this.heap[index] < this.heap[parentIdx]) {
                this.swap(index, parentIdx)
                index = parentIdx    
            } else {
                break
            }
        }
    }
    
    remove () {
        if (this.size() === 0) return null
        if (this.size() === 1) return this.heap.pop()
        
        let root = this.heap[0]
        this.heap[0] = this.heap.pop()
        this.heapifyDown()
        return root
    }
    
    heapifyDown () {
        let index = 0
        const length = this.heap.length
        while (this.getLeftIdx(index) < length) {
            let smallest = this.getLeftIdx(index)
            let rightIdx = this.getRightIdx(index)
            
            if (rightIdx < length && this.heap[rightIdx] < this.heap[smallest]) {
                smallest = rightIdx
            }
            if (this.heap[index] > this.heap[smallest]) {
                this.swap(index, smallest)
                index = smallest
            } else {
                break
            }
        }
    }
    
    peak () {
        return this.heap[0]
    }
    
    size () {
        return this.heap.length
    }
}
```

### 풀이를 마치고
문제를 풀기 전에는 클래스에 대한 이해도가 많이 부족했지만 heap을 직접 구현하고 수정해보면서 클래스에 좀 더 익숙해졌다. 다른 알고리즘 문제에도 자주 활용해보자.

무언가를 구현할 때 머릿속으로 상상해서 하는 것 보다, 직접 그리거나 적어서 시각화해서 진행하면 실수할 확률도 적고 구현하기 더욱 쉽다.

**힙 구현할 때 시각화 예시**
![[첨부 파일 소스/Image File 1/Pasted image 20240712204013.png]]
자식, 부모 노드의 index를 계산할 때 직접 시각화한 것을 보면서 하니 계산이 바로 되어 보다 수월하게 구현했다.


## Lv. 2 파일명 정렬
### 문제
세 차례의 코딩 테스트와 두 차례의 면접이라는 기나긴 블라인드 공채를 무사히 통과해 카카오에 입사한 무지는 파일 저장소 서버 관리를 맡게 되었다.

저장소 서버에는 프로그램의 과거 버전을 모두 담고 있어, 이름 순으로 정렬된 파일 목록은 보기가 불편했다. 파일을 이름 순으로 정렬하면 나중에 만들어진 ver-10.zip이 ver-9.zip보다 먼저 표시되기 때문이다.

버전 번호 외에도 숫자가 포함된 파일 목록은 여러 면에서 관리하기 불편했다. 예컨대 파일 목록이 ["img12.png", "img10.png", "img2.png", "img1.png"]일 경우, 일반적인 정렬은 ["img1.png", "img10.png", "img12.png", "img2.png"] 순이 되지만, 숫자 순으로 정렬된 ["img1.png", "img2.png", "img10.png", img12.png"] 순이 훨씬 자연스럽다.

무지는 단순한 문자 코드 순이 아닌, 파일명에 포함된 숫자를 반영한 정렬 기능을 저장소 관리 프로그램에 구현하기로 했다.

소스 파일 저장소에 저장된 파일명은 100 글자 이내로, 영문 대소문자, 숫자, 공백(" "), 마침표("."), 빼기 부호("-")만으로 이루어져 있다. 파일명은 영문자로 시작하며, 숫자를 하나 이상 포함하고 있다.

파일명은 크게 HEAD, NUMBER, TAIL의 세 부분으로 구성된다.

- HEAD는 숫자가 아닌 문자로 이루어져 있으며, 최소한 한 글자 이상이다.
- NUMBER는 한 글자에서 최대 다섯 글자 사이의 연속된 숫자로 이루어져 있으며, 앞쪽에 0이 올 수 있다. `0`부터 `99999` 사이의 숫자로, `00000`이나 `0101` 등도 가능하다.
- TAIL은 그 나머지 부분으로, 여기에는 숫자가 다시 나타날 수도 있으며, 아무 글자도 없을 수 있다.

| 파일명                | HEAD  | NUMBER | TAIL         |
| ------------------ | ----- | ------ | ------------ |
| `foo9.txt`         | `foo` | `9`    | `.txt`       |
| `foo010bar020.zip` | `foo` | `010`  | `bar020.zip` |
| `F-15`             | `F-`  | `15`   | (빈 문자열)      |

### 문제 풀이
#### 풀이 과정
**문제 정리**
파일 정렬 방식을 문자 -> 숫자
파일은 HEAD, NUMBER, TAIL으로 이루어져 있음 (대소문자 구분 X)

**정렬 기준**
HEAD기준으로 사전순 정렬
HEAD부분이 같을 경우 숫자순으로 정렬(앞자리 0은 무시 )
HEAD, NUMBER 모두 동일할 경우 주어진 순서 유지

**시간 복잡도**
files의 최대 길이 1000
파일명은 최대 100글자
각각 파일을 문자별로 모두 순회해도 1000 x 100 = 십만으로 충분히 가능.

**풀이**
for문을 통해 문자열마다 순회하면서 
file을 head, number, tail로 나누어 배열로 담아준다.
중간에 숫자가 시작하고 끝나는 부분만 알아내면 되므로,
투포인터 알고리즘을 통해 중간 숫자 구간을 판별한다.

구간별로 나눈 배열 모음을
sort메서드에 인수로 조건문을 넣어서 조건에 맞게 정렬한다.

#### 답안 코드
```
function solution(files) {
    let newFiles = []
    
    for(let i = 0; i < files.length; i ++) {
        let file = files[i]
        let prevType = Number.isInteger(parseInt(file[0]))
        let currType = ""
        let seperateFile = []
        let strIdx = 0
        for(let j = 1; j < file.length; j++) {
            currType = Number.isInteger(parseInt(file[j]))
            if (j === file.length - 1) {
                if (seperateFile.length > 0) {
                    seperateFile.push(file.slice(strIdx, file.length))
                    newFiles.push(seperateFile)
                    break
                } else {
                    seperateFile.push(file.slice(0, j))
                    seperateFile.push(file[j])
                    newFiles.push(seperateFile)
                    break
                }
            }
            
            if(prevType === false && currType === true) {
                seperateFile.push(file.slice(0,j))
                strIdx = j
            } else if (prevType === true && currType === false) {
                seperateFile.push(file.slice(strIdx, j))
                seperateFile.push(file.slice(j, file.length))
                newFiles.push(seperateFile)
                break
            }
            
            prevType = currType
        }
    }
    
    newFiles.sort((a,b) => {
        if (a[0].toUpperCase() < b[0].toUpperCase()) return -1
        if (a[0].toUpperCase() > b[0].toUpperCase()) return 1
        
        if (parseInt(a[1]) < parseInt(b[1])) return -1
        if (parseInt(a[1]) > parseInt(b[1])) return 1
        return
    })
    newFiles = newFiles.map((el) => el.join(""))
    return newFiles
}
```

### 풀이를 마치고
시간복잡도에 구애받지 않고 단순 정렬방식을 구현하는 문제라 크게 어렵지 않았다.

`풀이 시간` : 1시간 10분


## Lv. 2 오픈채팅방
### 문제
카카오톡 오픈채팅방에서는 친구가 아닌 사람들과 대화를 할 수 있는데, 본래 닉네임이 아닌 가상의 닉네임을 사용하여 채팅방에 들어갈 수 있다.

신입사원인 김크루는 카카오톡 오픈 채팅방을 개설한 사람을 위해, 다양한 사람들이 들어오고, 나가는 것을 지켜볼 수 있는 관리자창을 만들기로 했다. 채팅방에 누군가 들어오면 다음 메시지가 출력된다.

"[닉네임]님이 들어왔습니다."

채팅방에서 누군가 나가면 다음 메시지가 출력된다.

"[닉네임]님이 나갔습니다."

채팅방에서 닉네임을 변경하는 방법은 다음과 같이 두 가지이다.

- 채팅방을 나간 후, 새로운 닉네임으로 다시 들어간다.
- 채팅방에서 닉네임을 변경한다.

닉네임을 변경할 때는 기존에 채팅방에 출력되어 있던 메시지의 닉네임도 전부 변경된다.

예를 들어, 채팅방에 "Muzi"와 "Prodo"라는 닉네임을 사용하는 사람이 순서대로 들어오면 채팅방에는 다음과 같이 메시지가 출력된다.

"Muzi님이 들어왔습니다."  
"Prodo님이 들어왔습니다."

채팅방에 있던 사람이 나가면 채팅방에는 다음과 같이 메시지가 남는다.

"Muzi님이 들어왔습니다."  
"Prodo님이 들어왔습니다."  
"Muzi님이 나갔습니다."

Muzi가 나간후 다시 들어올 때, Prodo 라는 닉네임으로 들어올 경우 기존에 채팅방에 남아있던 Muzi도 Prodo로 다음과 같이 변경된다.

"Prodo님이 들어왔습니다."  
"Prodo님이 들어왔습니다."  
"Prodo님이 나갔습니다."  
"Prodo님이 들어왔습니다."

채팅방은 중복 닉네임을 허용하기 때문에, 현재 채팅방에는 Prodo라는 닉네임을 사용하는 사람이 두 명이 있다. 이제, 채팅방에 두 번째로 들어왔던 Prodo가 Ryan으로 닉네임을 변경하면 채팅방 메시지는 다음과 같이 변경된다.

"Prodo님이 들어왔습니다."  
"Ryan님이 들어왔습니다."  
"Prodo님이 나갔습니다."  
"Prodo님이 들어왔습니다."

채팅방에 들어오고 나가거나, 닉네임을 변경한 기록이 담긴 문자열 배열 record가 매개변수로 주어질 때, 모든 기록이 처리된 후, 최종적으로 방을 개설한 사람이 보게 되는 메시지를 문자열 배열 형태로 return 하도록 solution 함수를 완성하라.

##### 제한사항

- record는 다음과 같은 문자열이 담긴 배열이며, 길이는 `1` 이상 `100,000` 이하이다.
- 다음은 record에 담긴 문자열에 대한 설명이다.
    - 모든 유저는 [유저 아이디]로 구분한다.
    - [유저 아이디] 사용자가 [닉네임]으로 채팅방에 입장 - "Enter [유저 아이디] [닉네임]" (ex. "Enter uid1234 Muzi")
    - [유저 아이디] 사용자가 채팅방에서 퇴장 - "Leave [유저 아이디]" (ex. "Leave uid1234")
    - [유저 아이디] 사용자가 닉네임을 [닉네임]으로 변경 - "Change [유저 아이디] [닉네임]" (ex. "Change uid1234 Muzi")
    - 첫 단어는 Enter, Leave, Change 중 하나이다.
    - 각 단어는 공백으로 구분되어 있으며, 알파벳 대문자, 소문자, 숫자로만 이루어져있다.
    - 유저 아이디와 닉네임은 알파벳 대문자, 소문자를 구별한다.
    - 유저 아이디와 닉네임의 길이는 `1` 이상 `10` 이하이다.
    - 채팅방에서 나간 유저가 닉네임을 변경하는 등 잘못 된 입력은 주어지지 않는다.

##### 입출력 예

|record|result|
|---|---|
|`["Enter uid1234 Muzi", "Enter uid4567 Prodo","Leave uid1234","Enter uid1234 Prodo","Change uid4567 Ryan"]`|`["Prodo님이 들어왔습니다.", "Ryan님이 들어왔습니다.", "Prodo님이 나갔습니다.", "Prodo님이 들어왔습니다."]`|

---

### 문제 풀이
#### 풀이 과정
**문제 정리**
채팅방 입장과 닉네임 변경 기록이 담긴 배열이 주어질 때 최종 메시지를 출력해라.

**풀이**
입장, 퇴장 기록을 id에맞춰 기록해놓고, 마지막에 최종 id별 닉네임을 대입해서 출력한다.
명령을 `[행동, id, 닉네임]`형태의 배열로 나눈다.
입장, 닉네임 변경시 맵 객체에 `ID : 닉네임` 형태로 기록한다.
입장, 퇴장시 messages에 `[id, 행동]`형태로 담아준다.

마지막에 id로 최종 닉네임을 가져오고 행동으로 메시지를 가져와서 출력해준다.

#### 답안 코드
```
function solution(record) {
    let messages = [];
    const idMap = new Map()
    idMap.set("Enter", "님이 들어왔습니다.")
    idMap.set("Leave", "님이 나갔습니다.")
    record = record.map((el) => el.split(" "))
    for (let item of record) {
        let [act, id, name] = item
        if (act === "Enter"){
            idMap.set(id, name)
            messages.push([id,act])  
        } else if (act === "Leave") {
            messages.push([id,act])  
        } else {
            idMap.set(id, name)    
        }
        
    }
    let result = []
    for (let item of messages) {
        let finalName = idMap.get(item[0])
        let text = idMap.get(item[1])
        result.push(finalName + text)
    }
    return result;
}
```

### 풀이를 마치고
지문이 좀 길었을 뿐 문제만 이해하고 나면 객체에 데이터 저장하고 꺼내오는게 다라서 따로 주의해야 할 부분도 없고 매우 간단한 문제였다. 

`풀이 시간` : 30분

## Lv. 2  숫자 변환하기
### 문제
자연수 `x`를 `y`로 변환하려고 합니다. 사용할 수 있는 연산은 다음과 같습니다.

- `x`에 `n`을 더합니다
- `x`에 2를 곱합니다.
- `x`에 3을 곱합니다.

자연수 `x`, `y`, `n`이 매개변수로 주어질 때, `x`를 `y`로 변환하기 위해 필요한 최소 연산 횟수를 return하도록 solution 함수를 완성해주세요. 이때 `x`를 `y`로 만들 수 없다면 -1을 return 해주세요.

---

##### 제한사항

- 1 ≤ `x` ≤ `y` ≤ 1,000,000
- 1 ≤ `n` < `y`

---

##### 입출력 예

| x   | y   | n   | result |
| --- | --- | --- | ------ |
| 10  | 40  | 5   | 2      |
| 10  | 40  | 30  | 1      |
| 2   | 5   | 4   | -1     |


---

### 문제 풀이
#### 풀이 과정
처음에는 dfs를 활용하여 풀었지만, 중복값을 처리하지 못해 연산이 너무 많아 런타임 에러가 발생했다.
이후 bfs를 활용하여 방문처리를 해주며 해결.

#### 답안 코드
```
function solution(x, y, n) {
    function calc(num, i) {
        switch(i) {
            case 1 :
                return num - n
            case 2 :
                if(num % 2 === 0) return num / 2
                else return 0
            case 3 :
                if (num % 3 === 0) return num / 3
                else return 0
        }
    }
    
    function bfs() {
        let queue = [[y,0]]
        const visit = {}
        visit[y] = 1
        while (queue.length) {
            let [curValue, count] = queue.shift()
            if(curValue === x) return count
            for(let i = 1; i <= 3; i ++) {
                let nextValue = calc(curValue, i)
                if(nextValue >= x && visit[nextValue] !== 1) {
                    visit[nextValue] = 1
                    queue.push([nextValue, count+1])
                }
            }
        }
        return -1
    }
    
    return bfs()
}
```

#### DP를 활용한 풀이
```
function solution(x, y, n) {
    // 숫자 같은 경우 0 반환
    if(x === y) return 0
    // dp테이블 생성
    const dp = {}
    //dp테이블에 연산해서 나온 값을 index로 count횟수를 넣어준다.
    dp[x] = 0
    
    // 연산해서 나온 값들로 계속해서 연산 작업
    let datas = [x]
    // 목표값인 y를 넘어가는 값들로 이루어질 때까지 진행
    while(datas.length) {
        const temp = []
        // 이전 연산의 결과값들로 다시 연산 진행
        for(const data of datas) {
            // 연산한 값을 value에 해당
            for(const value of [data + n, data * 2, data * 3]) {
                // y를 넘어가는 경우 패스
                if (value > y || dp[value])  continue
                // 목표값과 일치할 경우 이전 연산횟수에 1을 더해준 값 반환
                if (value === y) return dp[data] + 1
                // dp[값] = count횟수로 dp테이블에 저장
                dp[value] = dp[data] + 1
                // 연산해서 나온 값들을 data에 넣어주기 위해 temp에 임시 저장
                temp.push(value)
            }
        }
        datas = temp
    }
    return -1
}
```

### 풀이를 마치고
중복값을 계산하는 것을 신경쓰고 방지하도록 코드를 짜자

## Lv. 2 2 x n 타일링
### 문제
가로 길이가 2이고 세로의 길이가 1인 직사각형모양의 타일이 있습니다. 이 직사각형 타일을 이용하여 세로의 길이가 2이고 가로의 길이가 n인 바닥을 가득 채우려고 합니다. 타일을 채울 때는 다음과 같이 2가지 방법이 있습니다.

- 타일을 가로로 배치 하는 경우
- 타일을 세로로 배치 하는 경우

예를들어서 n이 7인 직사각형은 다음과 같이 채울 수 있습니다.

![Imgur](https://i.imgur.com/29ANX0f.png)

직사각형의 가로의 길이 n이 매개변수로 주어질 때, 이 직사각형을 채우는 방법의 수를 return 하는 solution 함수를 완성해주세요.

##### 제한사항

- 가로의 길이 n은 60,000이하의 자연수 입니다.
- 경우의 수가 많아 질 수 있으므로, 경우의 수를 1,000,000,007으로 나눈 나머지를 return해주세요.

---

##### 입출력 예

|n|result|
|---|---|
|4|5|

---

### 문제 풀이
#### 풀이 과정
피보나치 수열을 활용한 풀이

#### 답안 코드
```
function solution(n) {
    let fib = [0, 0, 2, 3]
    for(let i = 4; i <= n; i ++) {
            fib[i] = (fib[i-1] + fib[i-2]) % 1000000007
    }
    return fib[n]
}
```

### 풀이를 마치고
처음에 dfs로 구현했다가 시간초과가 발생하여, 반복문을 통한 피보나치수열로 해결. 어떤 방식의 알고리즘을 사용해야 하는지 잘 판단하자.


## Lv. 2 프렌즈4블록
### 문제
#### 프렌즈4블록

블라인드 공채를 통과한 신입 사원 라이언은 신규 게임 개발 업무를 맡게 되었다. 이번에 출시할 게임 제목은 "프렌즈4블록".  
같은 모양의 카카오프렌즈 블록이 2×2 형태로 4개가 붙어있을 경우 사라지면서 점수를 얻는 게임이다.

![board map](http://t1.kakaocdn.net/welcome2018/pang1.png "Friends 4 block!")  
만약 판이 위와 같이 주어질 경우, 라이언이 2×2로 배치된 7개 블록과 콘이 2×2로 배치된 4개 블록이 지워진다. 같은 블록은 여러 2×2에 포함될 수 있으며, 지워지는 조건에 만족하는 2×2 모양이 여러 개 있다면 한꺼번에 지워진다.

![board map](http://t1.kakaocdn.net/welcome2018/pang2.png "Friends 4 block!")

블록이 지워진 후에 위에 있는 블록이 아래로 떨어져 빈 공간을 채우게 된다.

![board map](http://t1.kakaocdn.net/welcome2018/pang3.png "Friends 4 block!")

만약 빈 공간을 채운 후에 다시 2×2 형태로 같은 모양의 블록이 모이면 다시 지워지고 떨어지고를 반복하게 된다.  
![board map](http://t1.kakaocdn.net/welcome2018/pang4.png "Friends 4 block!")

위 초기 배치를 문자로 표시하면 아래와 같다.

```
TTTANT
RRFACC
RRRFCC
TRRRAA
TTMMMF
TMMTTJ
```

각 문자는 라이언(R), 무지(M), 어피치(A), 프로도(F), 네오(N), 튜브(T), 제이지(J), 콘(C)을 의미한다

입력으로 블록의 첫 배치가 주어졌을 때, 지워지는 블록은 모두 몇 개인지 판단하는 프로그램을 제작하라.

##### 입력 형식

- 입력으로 판의 높이 `m`, 폭 `n`과 판의 배치 정보 `board`가 들어온다.
- 2 ≦ `n`, `m` ≦ 30
- `board`는 길이 `n`인 문자열 `m`개의 배열로 주어진다. 블록을 나타내는 문자는 대문자 A에서 Z가 사용된다.

##### 출력 형식

입력으로 주어진 판 정보를 가지고 몇 개의 블록이 지워질지 출력하라.

##### 입출력 예제

| m   | n   | board                                                        | answer |
| --- | --- | ------------------------------------------------------------ | ------ |
| 4   | 5   | ["CCBDE", "AAADE", "AAABF", "CCBBF"]                         | 14     |
| 6   | 6   | ["TTTANT", "RRFACC", "RRRFCC", "TRRRAA", "TTMMMF", "TMMTTJ"] | 15     |

---

### 문제 풀이
#### 풀이 과정
**문제 정리**
n x m 보드의 지워지는 블록 총 개수 반환
최대 30 x 30

블록을 오른쪽으로 90도 회전한 모양으로 바꿔 배열로 만든다.
(블록이 터지면서 위에 있는 블록이 아래로 내려오는 성질과 배열의 성질이 일치하기 때문)

**블록 확인**
한 행씩 순회하면서 같은거 2개 연속이면 다음 행으로 가서 확인.
모든 칸을 다 돌 때 까지 정보 기억하고 있음.
맞는 경우 false로 바꿔줌

**블록 터뜨리는 로직**
filter로 false가 아닌 값들로만 재구성

#### 풀이 코드
```
function solution(m, n, board) {
    let newBoard = Array.from({length : n}, () => Array(m).fill(false))
    let index = m  - 1
    // array와 동일한 성질이 되도록 요소 재배치
    for(let y = 0; y < m; y++) {
        for (let x = 0; x < n; x++) {
            newBoard[x][y] = board[index][x]
        }
        index --
    }
    
    let count = 0
    // 블록게임 작동 로직
    while (true) {
        let temp = []
        // 터뜨릴 블록 찾기
        for(let x = 0; x < newBoard.length -1; x ++) {
            for(let y = 0; y < newBoard[x].length -1; y ++) {
                let curr = newBoard[x][y]
                if (newBoard[x][y+1] === curr &&
                    newBoard[x+1][y] === curr &&
                    newBoard[x+1][y+1] === curr) {
                    temp.push([x,y])
                }
            }
        }
        if(temp.length === 0) break
        
        // 터뜨릴 블록들 false로 값 바꾸기
        temp.forEach(([x,y]) => {
            if(newBoard[x][y]) {
                newBoard[x].splice(y, 1, false)
                count ++
            }
            if(newBoard[x][y+1]) {
                newBoard[x].splice(y+1, 1, false)
                count ++
            }
            if(newBoard[x+1][y]) {
                newBoard[x+1].splice(y, 1, false)
                count ++
            }
            if(newBoard[x+1][y+1]) {
                newBoard[x+1].splice(y+1, 1, false)
                count ++
            }
        })
        
        // 블록 삭제함으로써 위 블록이 아래로 자동으로 내려오도록, 개수 카운팅
        for(let i = 0; i < newBoard.length; i ++) {
            newBoard[i] = newBoard[i].filter((el) => el !== false)
        }
    }
    
    return count;
}
```

#### 풀이 코드2
```
function solution(m, n, board) {
    let boardArray = board.map((el) => el.split(""))
    
    // 지울 블럭 찾는 함수
    function findRemove() {
        let removeMap = Array.from({length : m}, () => Array(n).fill(false))        
        let found = false
        
        for(let y = 0; y < m - 1; y ++) {
            for (let x = 0; x < n - 1; x ++) {
                let cur = boardArray[y][x]
                if (cur &&
                    cur === boardArray[y][x + 1] &&
                    cur === boardArray[y + 1][x] &&
                    cur === boardArray[y + 1][x + 1]) {
                    removeMap[y][x] = removeMap[y][x + 1] = removeMap[y + 1][x] = removeMap[y + 1][x + 1] = true
                    found = true
                }
            }
        }
        return found ? removeMap : ''
    }
    
    // 블럭 지우고 지운 개수 반환 힘수
    function removeBlocks(removeMap) {
        let count = 0
        for (let y = 0; y < m; y ++) {
            for (let x = 0; x < n ; x ++) {
                if (removeMap[y][x]) {
                    boardArray[y][x] = ''
                    count ++
                }
            }
        }
        return count
    }
    
    // 블록 떨어뜨리는 함수
    function dropBlocks() {
        for (let x = 0; x < n; x ++) {
            let emptyRow = m - 1
            for (let y = m - 1; y >= 0; y --) {
                if (boardArray[y][x] !== '') {
                    if (y !== emptyRow) {
                        boardArray[emptyRow][x] = boardArray[y][x]
                        boardArray[y][x] = ''
                    }
                    emptyRow --
                }
            }
        }
        return boardArray
    }

    let totalRemoved = 0
    // 메인 게임 로직
    while (true) {
        let removeMap = findRemove()
        if (!removeMap) break
        totalRemoved += removeBlocks(removeMap)
        dropBlocks()
    }
    
    return totalRemoved
}
```
**필요한 기능들을 정의하고, 각 기능별 함수를 만들어준다.**

1. 지울 블록을 찾는 함수
- board와 동일한 크기의 map에 false로 채워주고, 터지는 블럭일 경우 true로 바꿔준다.

2. 블록 지우고 개수 세는 함수
- 블록 찾는 함수에서 map을 받아오고, true로 되어있는 값을 board에서 ''로 바꿔준다.

3. 블록 떨어뜨리는 함수
- 같은 행의 맨 아래부터 위로 올라가면서 비어있는 칸에 위의 값을 채워준다.

4. 메인 게임 로직
- 각 기능별 함수를 실행

### 풀이를 마치고
`첫 번째 풀이`
처음에는 배열을 원본에서 array의 성질과 비슷하게 변경해서 해결했다. 이렇게 풀이 하니 예제나 테스트 케이스와 비교해보기는 약간 헷갈린다는 단점이 있고, 코드 자체로만 보면 array의 성질을 계승하여 작동하므로 좀 더 간단하다는 장점이 있다.

`두 번째 풀이`
함수를 정의해가며 해결한 풀이는 원본 배열 그대로 두고 로직을 짰고, 함수를 통해 기능을 정의하는 방법이 나중에 사용하기도, 알아보기도 더욱 좋은 것 같다. 로직 자체로만 놓고 보면 첫 번째 풀이보다 코드가 좀 더 길어지지만 예제와 테스트 케이스와 배열이 동일하므로 비교하기 쉽다.

효율성에서 첫 번째와 두 번째가 차이가 많이 날 것으로 예상했지만, 최악의 경우 10ms정도로 두 번째 풀이가 약간 우세했다.

**가급적 필요한 기능을 먼저 정의하고 함수를 활용하여 풀이를 해결하자**

## Lv. 2 2개 이하로 다른 비트
### 문제
양의 정수 `x`에 대한 함수 `f(x)`를 다음과 같이 정의합니다.

- `x`보다 크고 `x`와 **비트가 1~2개 다른** 수들 중에서 제일 작은 수

예를 들어,

- `f(2) = 3` 입니다. 다음 표와 같이 2보다 큰 수들 중에서 비트가 다른 지점이 2개 이하이면서 제일 작은 수가 3이기 때문입니다.

|수|비트|다른 비트의 개수|
|---|---|---|
|2|`000...0010`||
|3|`000...0011`|1|

- `f(7) = 11` 입니다. 다음 표와 같이 7보다 큰 수들 중에서 비트가 다른 지점이 2개 이하이면서 제일 작은 수가 11이기 때문입니다.

|수|비트|다른 비트의 개수|
|---|---|---|
|7|`000...0111`||
|8|`000...1000`|4|
|9|`000...1001`|3|
|10|`000...1010`|3|
|11|`000...1011`|2|

정수들이 담긴 배열 `numbers`가 매개변수로 주어집니다. `numbers`의 모든 수들에 대하여 각 수의 `f` 값을 배열에 차례대로 담아 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 1 ≤ `numbers`의 길이 ≤ 100,000
- 0 ≤ `numbers`의 모든 수 ≤ 1015

---

##### 입출력 예

|numbers|result|
|---|---|
|`[2,7]`|`[3,11]`|

---

### 문제 풀이
#### 풀이 과정
**주어진 수보다 크면서 비트 수가 2개 이하로 다른 수 중 가장 작은 수**

**로직**
주어진 수의 2진수 가장 뒤에 있는 0이 1이 됨과 동시에 바로 뒤 1이 0이 되는 2진수. (비트가 2개까지 달라도 되므로)
0이 없는 경우 맨 앞의 1이 0이 되고 앞에 1이 추가되는 2진수 값.

각 값을 2진변환하여 배열로 만들어준 뒤 pop해가며 비교.
pop할 때마다 1씩 더하면서 자릿수 기록.

#### 답안 코드
```
function solution(numbers) {
    let result = [];
    for (let number of numbers) {
        if (number <= 2) {
            result.push(number + 1)
            continue
        }
        // console.log(number.toString(2))
        let numArray = number.toString(2).split("")
        let index = 0
        while(numArray.length > 0) {
            if (numArray.pop() === "0") {
                if (index === 0) {
                    result.push(number + (2 ** index))
                } else {
                    result.push(number + (2 ** index) - (2 ** (index - 1)))
                }
                break
            }
            index ++
        }
        // 값을 모두 비교해도 0이 나오지 않는 경우
        if(numArray.length === 0) {
            result.push(number + (2 ** index) - (2 ** (index -1)))    
        }
    }
    
    // 정답 확인용 테스트 코드
//     for (let i = 0; i < numbers.length; i ++) {
//         console.log("10진수    ",numbers[i])
//         console.log("다음 10진수", result[i])
//         console.log("2진수    ",numbers[i].toString(2))
//         console.log("다음 2진수",result[i].toString(2))
//         console.log("---------------")
//     }
    
    return result;
}
```

### 풀이를 마치고
중간에 자리수가 늘어나면서 1이 되는걸 비트값이 달라지는 경우와, 7이하의 값을 모두 해당 숫자 + 1의 값으로 리턴하는 바람에 계속 헤맸다.

헤메던 와중에 숫자 판별용 테스트 코드를 작성해 해당 숫자와, 답으로 나오는 숫자의 2진수 10진수 값을 모두 확인하며 테스트 케이스를 추가하니 문제를 알아차릴 수 있었다.
이렇게 테스트 코드를 작성한 적은 없었는데 앞으로도 작성하면서 문제를 풀면 실수를 줄일 수 있을 것 같다.
특히나 실제 코딩테스트의 경우에는 테스트 케이스가 많이 주어지지 않으므로,  **정답 확인용 테스트 코드를 작성함은 물론이고,  직접 테스트케이스를 만드는 코드까지 필요할 수  있다.**

**내가 짠 코드에 문제가 없는데 답이 틀리게 나온다면, 확인용 코드를 만들고 테스트 케이스를 추가하자 !!**

## Lv. 2 소수 찾기 [복습 완료]
### 문제
한자리 숫자가 적힌 종이 조각이 흩어져있습니다. 흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.

각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

##### 제한사항

- numbers는 길이 1 이상 7 이하인 문자열입니다.
- numbers는 0~9까지 숫자만으로 이루어져 있습니다.
- "013"은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.

##### 입출력 예

|numbers|return|
|---|---|
|"17"|3|
|"011"|2|

---

### 문제 풀이
#### 풀이 과정
>1. DFS를 통해 모든 숫자 조합의 경우의 수를 조합한다.
>2. 숫자를 소수 판별 함수에 넣어 확인한다.
>3. 총 소수의 개수를 반환한다.

#### 풀이 코드
```
function solution(numbers) {
    let visited = new Array(numbers.length).fill(false)
    let numSet = new Set()
    let count = 0
    
    // 소수 판별 함수
    const isPrime = (num) => {
        if (num <= 1) return false
        for(let i = 2; i <= Math.sqrt(num); i++ ) {
            if (num % i === 0) return false
        }
        return true
    }
    
    // dfs 함수
    const dfs = (visited, num) => {
        if (num.length === numbers.length) return
        
        for (let i = 0; i < numbers.length; i ++) {
            if (!visited[i]) {
                let cur = parseInt(num + numbers[i])
                if (!numSet.has(cur) && isPrime(cur)) {
                    count ++
                }
                numSet.add(cur)
                visited[i] = true
                dfs(visited, cur)
                visited[i] = false
            }
        }
    }
    
    dfs(visited, "")
    
    return count
}
```

### 풀이를 마치고
문제 자체는 `소수판별`, 간단한 `dfs`가 복합된 문제이다. 두 부분 모두 완벽하게 알고있지 않아서 소수판별 하는 부분에서 오류가 발생하고, dfs구현 과정에서 방문처리를 안해주어 계속해서 같은 값을 꺼내서 사용했다.
방문 배열을 만들었지만 마지막에 방문 처리를 false해야 된다는 사실을 잊고 구현이 잘 되지 않았다.

모두 소수를 판별하는 로직, DFS가 작동하는 로직에 대해서 깊이 이해하고 있지 않기때문에 헷갈리게 느껴졌다.

**알고리즘을 구현할 줄 아는게 중요한 것이 아니라 알고리즘을 이해하고 상황에 맞춰 구현할 줄 아는지가 중요하다**
 
## Lv. 2 삼각 달팽이
### 문제
정수 n이 매개변수로 주어집니다. 다음 그림과 같이 밑변의 길이와 높이가 n인 삼각형에서 맨 위 꼭짓점부터 반시계 방향으로 달팽이 채우기를 진행한 후, 첫 행부터 마지막 행까지 모두 순서대로 합친 새로운 배열을 return 하도록 solution 함수를 완성해주세요.

![examples.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/e1e53b93-dcdf-446f-b47f-e8ec1292a5e0/examples.png)

---

##### 제한사항

- n은 1 이상 1,000 이하입니다.

---

##### 입출력 예

| n   | result                                                    |
| --- | --------------------------------------------------------- |
| 4   | `[1,2,9,3,10,8,4,5,6,7]`                                  |
| 5   | `[1,2,12,3,13,11,4,14,15,10,5,6,7,8,9]`                   |
| 6   | `[1,2,15,3,16,14,4,17,21,13,5,18,19,20,12,6,7,8,9,10,11]` |

---

### 문제 풀이
#### 풀이 과정
n개의 행과 행마다 열이 1개씩 늘어나는 2차원 배열을 만든다.
아래로 내려가면서 맨 앞에 값들을 채워준다.
마지막 행에 도달하면 n개만큼 채워준다.
그 뒤로 위로 올라가면서, 맨 뒤에 값을 채워준다.
한 바퀴를 돌면 round + 1해주고 앞에서 `[행][round]`에 값을 채워준다.
`[행-round]`에 도달하면 해당 행의 길이에 빈 값을 모두 채워준다.

#### 풀이 코드
```
function solution(n) {
    let answer = [];
    let snailMap = Array.from({length : n}, () => [])
    
    // 달팽이맵 생성
    for (let i = 0; i < n; i ++) {
        snailMap[i] = Array(i+1).fill(false)
    }
    // 마지막 숫자 구하기
    let lastNum = n % 2 === 0 ? (n + 1) * (n / 2) : n * ((n - 1) / 2) + n
    
    let last = n - 1
    let round = 0
    let num = 1

	// 달팽이맵 채우는 로직
    while (num <= lastNum) {
    
        // 내려가면서 채우기
        for (let y = round * 2; y < n - round; y ++) {
                snailMap[y][round] = num
                num ++
            if (num > lastNum) break
        }
        // 가장 아래 행 다 채우기
        for (let x = round + 1; x < n - round * 2; x ++) {
                snailMap[n - 1 - round][x] = num
                num ++
                if (num > lastNum) break
        }
        // 올라가면서 채우기
        for (let y = n - round - 2; y >= 1 + (round * 2); y --) {
                snailMap[y][y - round] = num
                num ++
                if (num > lastNum) break    
        }
        round ++
    }
    
    let result = []
    for (let i = 0; i < n; i ++) {
        for (let j = 0; j < snailMap[i].length; j ++) {
            result.push(snailMap[i][j])
        }
    }
    return result;
}
```

### 풀이를 마치고
문제를 풀면서 끝나는 지점, 시작하는 지점을 생각하면서 구했더니 복잡하고 실수가 발생할 확률이 높아진다. 미리 풀기 전에 한 바퀴 돌고 난 뒤 시작하는 지점, 끝나는 지점을 구해놓고 풀이를 들어가면 더욱 수월할 것 같다.
문제를 다 풀고 나니 각 기능 별로 함수를 만들어 하는 방법이 코드를 짜기 더 쉽고 가독성이 좋아 보인다 .

**코드를 적는 것은 단지 생각을 컴퓨터 언어로 바꾸는 것에 불과하다 !! 미리 생각을 끝내놓고 코드를 짜자.**

**!!함수 단위의 기능 구현**

`풀이 시간 : 1시간 10분`

## Lv. 2 쿼드압축 후 개수 세기 [복습 완료]
### 문제
0과 1로 이루어진 2n x 2n 크기의 2차원 정수 배열 arr이 있습니다. 당신은 이 arr을 [쿼드 트리](https://en.wikipedia.org/wiki/Quadtree)와 같은 방식으로 압축하고자 합니다. 구체적인 방식은 다음과 같습니다.

1. 당신이 압축하고자 하는 특정 영역을 S라고 정의합니다.
2. 만약 S 내부에 있는 모든 수가 같은 값이라면, S를 해당 수 하나로 압축시킵니다.
3. 그렇지 않다면, S를 정확히 4개의 균일한 정사각형 영역(입출력 예를 참고해주시기 바랍니다.)으로 쪼갠 뒤, 각 정사각형 영역에 대해 같은 방식의 압축을 시도합니다.

arr이 매개변수로 주어집니다. 위와 같은 방식으로 arr을 압축했을 때, 배열에 최종적으로 남는 0의 개수와 1의 개수를 배열에 담아서 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- arr의 행의 개수는 1 이상 1024 이하이며, 2의 거듭 제곱수 형태를 하고 있습니다. 즉, arr의 행의 개수는 1, 2, 4, 8, ..., 1024 중 하나입니다.
    - arr의 각 행의 길이는 arr의 행의 개수와 같습니다. 즉, arr은 정사각형 배열입니다.
    - arr의 각 행에 있는 모든 값은 0 또는 1 입니다.

---

##### 입출력 예

| arr                                                                                                                                                 | result    |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | --------- |
| `[[1,1,0,0],[1,0,0,0],[1,0,0,1],[1,1,1,1]]`                                                                                                         | `[4,9]`   |
| `[[1,1,1,1,1,1,1,1],[0,1,1,1,1,1,1,1],[0,0,0,0,1,1,1,1],[0,1,0,0,1,1,1,1],[0,0,0,0,0,0,1,1],[0,0,0,0,0,0,0,1],[0,0,0,0,1,0,0,1],[0,0,0,0,1,1,1,1]]` | `[10,15]` |

---

### 문제 풀이
#### 풀이 과정
원본 배열에서 재귀 함수를 통해 압축이 가능하거나, 크기가 1이 될 때 까지 4등분하면서 나눈다.

#### 풀이 코드
```
function solution(arr) {
    
    // 압축 여부 판단 함수
    const isUniform = (x, y, size) => {
        let value = arr[x][y]
        for (let i = x; i < x + size; i++) {
            for (let j = y; j < y + size; j++) {
                if (arr[i][j] !== value) {
                    return false
                }
            }
        }
        return true
    }
    
    // 압축이 가능할 때 까지 4등분하는 재귀함수
    const compress = (x, y, size) => {
        if(size === 1 || isUniform(x, y, size)) {
            return arr[x][y] === 0 ? [1, 0] : [0, 1]
        }
        let harfSize = size / 2
        let topLeft = compress(x, y, harfSize)
        let topRight = compress(x, y + harfSize, harfSize)
        let bottomLeft = compress(x + harfSize, y, harfSize)
        let bottomRight = compress(x + harfSize, y + harfSize, harfSize)
        
        return [topLeft[0] + topRight[0] + bottomLeft[0] + bottomRight[0],
                topLeft[1] + topRight[1] + bottomLeft[1] + bottomRight[1]
               ]
    }
    
    return compress(0, 0, arr.length)
}
    
```

### 풀이를 마치고
재귀 함수는 아직 전체적인 로직이 완벽하게 이해가 가지 않아 사용 가능한 상황이나, 반환하는 값의 경우에 익숙해질 필요가 있다.

## Lv. 2 두 큐 합 같게 만들기 [복습 완료]
### 문제
길이가 같은 두 개의 큐가 주어집니다. 하나의 큐를 골라 원소를 추출(pop)하고, 추출된 원소를 **다른 큐**에 집어넣는(insert) 작업을 통해 각 큐의 원소 합이 같도록 만들려고 합니다. 이때 필요한 작업의 최소 횟수를 구하고자 합니다. 한 번의 pop과 한 번의 insert를 합쳐서 작업을 1회 수행한 것으로 간주합니다.

큐는 먼저 집어넣은 원소가 먼저 나오는 구조입니다. 이 문제에서는 큐를 배열로 표현하며, 원소가 배열 앞쪽에 있을수록 먼저 집어넣은 원소임을 의미합니다. 즉, pop을 하면 배열의 첫 번째 원소가 추출되며, insert를 하면 배열의 끝에 원소가 추가됩니다. 예를 들어 큐 `[1, 2, 3, 4]`가 주어졌을 때, pop을 하면 맨 앞에 있는 원소 1이 추출되어 `[2, 3, 4]`가 되며, 이어서 5를 insert하면 `[2, 3, 4, 5]`가 됩니다.

다음은 두 큐를 나타내는 예시입니다.

```
queue1 = [3, 2, 7, 2]
queue2 = [4, 6, 5, 1]
```

두 큐에 담긴 모든 원소의 합은 30입니다. 따라서, 각 큐의 합을 15로 만들어야 합니다. 예를 들어, 다음과 같이 2가지 방법이 있습니다.

1. queue2의 4, 6, 5를 순서대로 추출하여 queue1에 추가한 뒤, queue1의 3, 2, 7, 2를 순서대로 추출하여 queue2에 추가합니다. 그 결과 queue1은 [4, 6, 5], queue2는 [1, 3, 2, 7, 2]가 되며, 각 큐의 원소 합은 15로 같습니다. 이 방법은 작업을 7번 수행합니다.
2. queue1에서 3을 추출하여 queue2에 추가합니다. 그리고 queue2에서 4를 추출하여 queue1에 추가합니다. 그 결과 queue1은 [2, 7, 2, 4], queue2는 [6, 5, 1, 3]가 되며, 각 큐의 원소 합은 15로 같습니다. 이 방법은 작업을 2번만 수행하며, 이보다 적은 횟수로 목표를 달성할 수 없습니다.

따라서 각 큐의 원소 합을 같게 만들기 위해 필요한 작업의 최소 횟수는 2입니다.

길이가 같은 두 개의 큐를 나타내는 정수 배열 `queue1`, `queue2`가 매개변수로 주어집니다. 각 큐의 원소 합을 같게 만들기 위해 필요한 작업의 최소 횟수를 return 하도록 solution 함수를 완성해주세요. 단, 어떤 방법으로도 각 큐의 원소 합을 같게 만들 수 없는 경우, -1을 return 해주세요.

---

##### 제한사항

- 1 ≤ `queue1`의 길이 = `queue2`의 길이 ≤ 300,000
- 1 ≤ `queue1`의 원소, `queue2`의 원소 ≤ 109
- 주의: 언어에 따라 합 계산 과정 중 산술 오버플로우 발생 가능성이 있으므로 long type 고려가 필요합니다.

---

##### 입출력 예

|queue1|queue2|result|
|---|---|---|
|[3, 2, 7, 2]|[4, 6, 5, 1]|2|
|[1, 2, 1, 2]|[1, 10, 1, 2]|7|
|[1, 1]|[1, 5]|-1|

---

### 문제 풀이
#### 풀이 과정
queue자료구조 자체가 원형으로 되어있는 형식이므로 투 포인터를 활용해서 해결

#### 풀이 코드
```
function solution(queue1, queue2) {
    let sum1 = queue1.reduce((sum,el) => sum + el)
    let sum2 = queue2.reduce((sum,el) => sum + el)
    const half = (sum1 + sum2) /  2
    const q = [...queue1, ...queue2]
    let q1Pointer = 0
    let q2Pointer = queue1.length
    for(let cnt = 0; cnt < queue1.length * 3; cnt++) {
        if (sum1 === half) {
            return cnt
        }
        sum1 = sum1 > half ? sum1 - q[q1Pointer++ % q.length] : sum1 + q[q2Pointer++ % q.length]
    }
    
    return -1
}
```

### 풀이를 마치고
처음에 했던 풀이는 가장 먼저 불가능 여부를 판별하는 것이였다.

가장 큰 값이 총 합의 절반을 넘는 경우
총 합이 홀수인 경우
두 배열이 서로 바뀔 때 까지 안되는 경우
총 세 가지 경우에서 성립이 안 된다고 판단하고, 해당 조건을 먼저 계산해준 뒤에 shift와 pop을 통해서 합을 계산해 주었다.

해당 풀이가 문제인 부분이 크게 두 가지 존재했다.
1. 먼저 불가능 경우를 판별하는 부분에서 불가능한 경우는 계산이 빨리 끝날 수 있지만, 판별이 가능한 대부분의 경우에선 불필요한 연산이 추가되는 것이므로 최악의 경우에선 불리하게 작용할 수 있다는 사실.
2. shift를 연산마다 해주어 해당 문제와 같이 배열의 길이가 큰 상황에서는 시간초과가 발생한다는 사실.

두 가지 문제점을 해결하기 위한 풀이 방법은 다음과 같다.
1. 연산 종료 시점을 해당 queue의 최대 이동거리로 설정해 모든 케이스에서 for문을 똑같이 수행하게 만들 것. 반복문이 끝날 동안 정답을 반환하지 못하면 불가능인 경우로 설정.
2. shift와 pop말고 queue형식으로 해결할 것. queue를 구현하기 위해 투 포인터를 통해 값을 추가하거나 빼주고 index가 길이를 초과하는 경우에도 뒤에 queue1과 queue2의 값이 계속해서 있어야 하므로, index % q.length의 값을 index로 사용해 배열을 넘어가면 처음 지점으로 돌아오게 만들어준다.

**문제를 풀 때 캐치하지 못한 부분**
queue자료구조는 두 배열을 이어 붙인 원모양으로 생겨있기 때문에 , 값을 shift하고 pop하는 부분이 원모양 막대에서 해당 배열이 가지고 있는 영역을 한 칸씩 이동하는 것과 동일하다.
ex) queue1에서 queue2로 값이 이동하는 과정
`queue1 = [1,2,3,4]`
`queue2 = [5,6,7,8]`
![[첨부 파일 소스/Image File 1/Pasted image 20240722131320.png]]

이러한 queue의 성질만 알고 있다면 투 포인터를 활용해서 간단하게 구현할 수 있다.

### 복습 풀이 [8/5]
```
/*
두 큐를 이어붙인 뒤, 두 개의 포인터를 통해 한쪽의 합산을 계산한다.
*/

function solution(queue1, queue2) {
    let q1 = queue1.reduce((total,el) => {
        return total += el}, 0)
    let q2 = queue2.reduce((total,el) => {
        return total += el}, 0)
    let goal = (q1 + q2) / 2
    
    let queue = [...queue1, ...queue2]
    let start = 0
    let end = queue1.length-1
    let sum = q1
    let count = 0
    while(sum !== goal && count <= queue1.length * 3) {
        if (sum > goal) {
            sum -= queue[start]
            start ++
            count ++
        } else {
            sum += queue[end+1]
            end ++
            count ++
        }
    }
    const answer = sum === goal ? count : -1
    
    return answer
}


```


## Lv. 2 큰 수 만들기 [복습 완료]
### 문제
어떤 숫자에서 k개의 수를 제거했을 때 얻을 수 있는 가장 큰 숫자를 구하려 합니다.

예를 들어, 숫자 1924에서 수 두 개를 제거하면 [19, 12, 14, 92, 94, 24] 를 만들 수 있습니다. 이 중 가장 큰 숫자는 94 입니다.

문자열 형식으로 숫자 number와 제거할 수의 개수 k가 solution 함수의 매개변수로 주어집니다. number에서 k 개의 수를 제거했을 때 만들 수 있는 수 중 가장 큰 숫자를 문자열 형태로 return 하도록 solution 함수를 완성하세요.

##### 제한 조건

- number는 2자리 이상, 1,000,000자리 이하인 숫자입니다.
- k는 1 이상 `number의 자릿수` 미만인 자연수입니다.

##### 입출력 예

|number|k|return|
|---|---|---|
|"1924"|2|"94"|
|"1231234"|3|"3234"|
|"4177252841"|4|"775841"|

---

### 📌 풀이 방법 (1차 시도 -> 시간 초과)

> 1. 그리디 알고리즘으로 **앞의 작은 숫자를 제거하고 큰 숫자를 선택** 하는 로직으로 진행한다.
> 2. k를 남아있는 횟수라고 생각하고, number의 앞에서부터 k만큼 쭉 간다.
> 3. 중간에 9가 나타나면 해당 index앞까지 글자를 지운다.
> 4. 9가 나타나지 않으면 k까지 중 가장 큰 수 앞까지 글자를 지운다.
> 5. 지운 글자만큼 k에서 차감한다.

### 📌 풀이 코드
```
function solution(number, k) {
    let answer = '';
    number = number.split("")
    let index = 0
    while (k > 0 || index < number.length - 1) {
        let largestIndex = 0
        let largestNum = 0
        for(let i = index; i <= index + k; i ++) {
            if (number[i] === 9) {
                number.splice(index,i)
                largestNum = 0
                k -= i
                break
            } else if(number[i] > largestNum) {
                largestNum = number[i]
                largestIndex = i
            }
        }
        
        if (largestNum > 0 && largestIndex > index) {
            number.splice(index, largestIndex - index)
            k -= largestIndex - index
        }
        index ++
    }
    
    return number.join("")
}
```

### 📌 생각한 개선 방법 및 힌트

> 1. splice를 계속 사용하니 연산이 너무길어짐.
> 2. 원본 배열에서 값을 지우지 말고 큰 값을 새로운 배열에 추가하는 방식으로 진행

### 📌 풀이 방법 (2차 시도 -> 시간 초과)

> 1.  앞에서 부터 k만큼 비교하면서 가장 큰 값이 나오면 해당 값을 새로운 배열에 push해준다.
> 2. 해당 값을 시작지점으로 설정하고 다시 큰 값을 찾는다.

### 📌 풀이 코드
```
function solution(number, k) {
    let answer = '';
    number = number.split("")
    let newNumber = []
    let startPoint = 0
    let largeIdx = 0
    let largeNum = 0
    
    while (k > 0) {
        largeNum = 0
        largeIdx = 0
        for (let j = startPoint; j <= startPoint + k; j ++) {
            if (number[j] === 9) {
                newNumber.push(9)
                k -= j - startPoint
                startPoint = j
                break
            }
            if (number[j] > largeNum) {
                largeNum = number[j]
                largeIdx = j
            }
        }
        
        newNumber.push(largeNum)
        k -= (largeIdx - startPoint)
        startPoint = largeIdx + 1
    }
    if (largeIdx < number.length) {
        newNumber.push(...number.splice(largeIdx + 1, number.length))
    }
    
    return newNumber.join("")
}
```

### 📌 생각한 개선 방법 및 힌트

> 1. 최악의 경우 k만큼 배열의 수를 비교해봐도 숫자 한 개를 지울 수 있으므로, 더욱 효율적인 연산이 필요하다.

### 📌 풀이 방법 (3차 시도 -> 성공)

**전제 조건**
>큰 수가 만들어지기 위해서는 앞자리 숫자가 제일 커야 한다.

**로직**
>number를 순회하면서 stack에 숫자를 추가한다. stack에 추가된 숫자(= 앞 자리 숫자)와 해당 차례의 number 숫자와 비교하여 해당 차례의 숫자보다 작은 숫자는 모두 stack에서 제거하는 로직.

### 📌 풀이 코드
```
function solution(number, k) {
    let stack = []
    for (let i = 0; i < number.length; i ++) {
        // stack이 비었으면 채우고 다음 number 요소로 이동
        if (stack.length === 0) {
            stack.push(number[i])
            continue
        }
        // number의 요소가 stack의 마지막 요소보다 크면 stack pop해주고 k --
        while (number[i] > stack[stack.length - 1]) {
            k --
            stack.pop()
            
            // k가 0이 되면 더 제거를 못하므로 정답 반환
            if (k === 0) return stack.join("") + number.slice(i)
            
            // stack이 모두 비면 종료
            if (stack.length === 0) break
        }
        
        // 비교를 위해 number[i] stack에 채워줌
        stack.push(number[i])
        
    }
    // k가 남아있으면 뒤에서 k만큼 제거
    return stack.join("").slice(0, stack.length - k)
}
```


## Lv. 2 연속된 부분 수열의 합
### 📖  문제
비내림차순으로 정렬된 수열이 주어질 때, 다음 조건을 만족하는 부분 수열을 찾으려고 합니다.

- 기존 수열에서 임의의 두 인덱스의 원소와 그 사이의 원소를 모두 포함하는 부분 수열이어야 합니다.
- 부분 수열의 합은 `k`입니다.
- 합이 `k`인 부분 수열이 여러 개인 경우 길이가 짧은 수열을 찾습니다.
- 길이가 짧은 수열이 여러 개인 경우 앞쪽(시작 인덱스가 작은)에 나오는 수열을 찾습니다.

수열을 나타내는 정수 배열 `sequence`와 부분 수열의 합을 나타내는 정수 `k`가 매개변수로 주어질 때, 위 조건을 만족하는 부분 수열의 시작 인덱스와 마지막 인덱스를 배열에 담아 return 하는 solution 함수를 완성해주세요. 이때 수열의 인덱스는 0부터 시작합니다.

---

##### 제한사항

- 5 ≤ `sequence`의 길이 ≤ 1,000,000
    - 1 ≤ `sequence`의 원소 ≤ 1,000
    - `sequence`는 비내림차순으로 정렬되어 있습니다.
- 5 ≤ `k` ≤ 1,000,000,000
    - `k`는 항상 `sequence`의 부분 수열로 만들 수 있는 값입니다.

---

##### 입출력 예

| sequence              | k   | result |
| --------------------- | --- | ------ |
| [1, 2, 3, 4, 5]       | 7   | [2, 3] |
| [1, 1, 1, 2, 3, 4, 5] | 5   | [6, 6] |
| [2, 2, 2, 2, 2]       | 6   | [0, 2] |

---

### 📌 풀이 방법 (1차 시도 -> 성공)
**만족하는 수열이 여러개인 경우 우선순위**
> 1.  길이가 짧은 수열 
> 2. 앞쪽에서 시작하는 수열

`자료구조` - **스택**
> 1.  숫자를 담아줄 배열 stck
> 2. index를 저장할 배열 indexList
> 3. 숫자 합 계산할 변수 sum

**로직**
> 1. k를 만족할 때 까지, 맨 뒤에서부터 pop하며 비교 배열에 추가.
> 2. k를 만족할 경우 합이 k보다 작아질 때 까지 값을 sum에 더해준 뒤, stck의 값을 앞에서부터 sum에서 뺴준다.
> 3. k와 같거나 큰 경우 indexList[0]과 [1]을 1씩빼준다.
> 4. 합이 k보다 작아질 경우, indexList 빼준 값을 1씩 더해준다.

### 🖥️ 풀이 코드
```
function solution(sequence, k) {
    let stck = [];
    let indexList = [0,sequence.length-1]
    let sum = 0
    let front = 0
    for (let i = sequence.length - 1; i >= 0; i --) {
        let value = sequence.pop()
        stck.push(value)
        sum += value
        indexList[0] = i
        if (sum > k) {
            indexList[1] --
            sum -= stck[front]
            front++
        }
        if(sum === k) break
    }
    
    while (sequence.length > 0) {
        let value = sequence.pop()
        stck.push(value)
        
        sum -= (stck[front] - value)
        front ++
        if (sum < k) break
        indexList[1] --
        indexList[0] --
    }
    
    return indexList;
}
```


## Lv. 2 124 나라의 숫자
### 📖  문제
124 나라가 있습니다. 124 나라에서는 10진법이 아닌 다음과 같은 자신들만의 규칙으로 수를 표현합니다.

1. 124 나라에는 자연수만 존재합니다.
2. 124 나라에는 모든 수를 표현할 때 1, 2, 4만 사용합니다.

예를 들어서 124 나라에서 사용하는 숫자는 다음과 같이 변환됩니다.

|10진법|124 나라|10진법|124 나라|
|---|---|---|---|
|1|1|6|14|
|2|2|7|21|
|3|4|8|22|
|4|11|9|24|
|5|12|10|41|

자연수 n이 매개변수로 주어질 때, n을 124 나라에서 사용하는 숫자로 바꾼 값을 return 하도록 solution 함수를 완성해 주세요.

##### 제한사항

- n은 50,000,000이하의 자연수 입니다.

---

##### 입출력 예

|n|result|
|---|---|
|1|1|
|2|2|
|3|4|
|4|11|


---

### 📌 풀이 방법 (1차 시도 -> 성공)

>  3^n을 더해줄 때마다 앞자리가 1씩 추가된다.
	3^0 = 1자리
	3^0 + 3^1 = 2자리
	3^0 + 3^1 + 3^2 = 3자리


>1. 주어진 값에서 3의 n제곱만큼 n을 1씩 늘려주며 빼준다.
>2. 값을 0미만으로 만들기 이전의 n이 해당 수의 자리수이다.
>3. 3^n에서 n+1이 뒤에서 n번째 자리수의 숫자에 해당한다.
>4. 남은 값을 다시 가까운 3^n값으로 나누고 몫이 1이면 1칸 올려주고, 2이면 2칸 올려준다.
>5. 해당 나머지로 계속해서 앞의 자리부터 숫자를 변경해준다.

### 🖥️ 풀이 코드
```
function solution(n) {
    let number = n
    let index = 0
    let array = []
    // 자릿수 계산
    while (true) {
        number -= (3 ** index)
        if (number < 0) {
            number += 3 ** index
            break
        }
        index ++
    }
    
    // 자리수에 맞춰 초기값 채워주기
    for(let i = 0; i < index; i++) {
        array.push(1)
    }
    let length = array.length
    
    // 메인 로직. 앞에서부터 자릿수마다 숫자 업데이트 해주기
    while (number >= 3) {
        let tempNum = number
        index = 0
        
        while (tempNum >= 3) {
            tempNum = tempNum / 3
            index ++
        }
        // 자릿수에서 올려줘야 할 수 게산
        let value = Math.floor(number / (3 ** index))
        
        // 해당 자릿수 수 계산해주기
        array[length - (index + 1)] = value * 2
        
        number -= (3 ** index) * value
    }
    if (number > 0) {
        array[length-1] = number * 2
    }
    
    return array.join("")
}
```

### 🔎 코드 리팩토링

```
function solution(n) {
    let result = '';

    while (n > 0) {
        let remainder = n % 3;
        n = Math.floor(n / 3);

        if (remainder === 0) {
            remainder = 4;
            n -= 1;
        }

        result = remainder + result;
    }

    return result;
}
```

10진법 숫자를 124나라 숫자로 변환하는 과정은 3진법으로 변환하는 과정을 기반으로 한다. 단, 0대신 4를 사용하고, 3의 배수에서 자릿수를 하나씩 올려준다.

## Lv. 2 전력망을 둘로 나누기
### 📖  문제
n개의 송전탑이 전선을 통해 하나의 [트리](https://en.wikipedia.org/wiki/Tree_(data_structure)) 형태로 연결되어 있습니다. 당신은 이 전선들 중 하나를 끊어서 현재의 전력망 네트워크를 2개로 분할하려고 합니다. 이때, 두 전력망이 갖게 되는 송전탑의 개수를 최대한 비슷하게 맞추고자 합니다.

송전탑의 개수 n, 그리고 전선 정보 wires가 매개변수로 주어집니다. 전선들 중 하나를 끊어서 송전탑 개수가 가능한 비슷하도록 두 전력망으로 나누었을 때, 두 전력망이 가지고 있는 송전탑 개수의 차이(절대값)를 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- n은 2 이상 100 이하인 자연수입니다.
- wires는 길이가 `n-1`인 정수형 2차원 배열입니다.
    - wires의 각 원소는 [v1, v2] 2개의 자연수로 이루어져 있으며, 이는 전력망의 v1번 송전탑과 v2번 송전탑이 전선으로 연결되어 있다는 것을 의미합니다.
    - 1 ≤ v1 < v2 ≤ n 입니다.
    - 전력망 네트워크가 하나의 트리 형태가 아닌 경우는 입력으로 주어지지 않습니다.

---

##### 입출력 예

| n   | wires                                               | result |
| --- | --------------------------------------------------- | ------ |
| 9   | `[[1,3],[2,3],[3,4],[4,5],[4,6],[4,7],[7,8],[7,9]]` | 3      |
| 4   | `[[1,2],[2,3],[3,4]]`                               | 0      |
| 7   | `[[1,2],[2,7],[3,7],[3,4],[4,5],[6,7]]`             | 1      |


---

### 📌 풀이 방법 (1차 시도 - 실패)

> 1.  주어진 배열을 트리 형태로 변환한다.
> `[[1,3],[2,3],[3,4],[4,5],[4,6],[4,7],[7,8],[7,9]]`
>  => `[[], [3], [3], [1,2,4], [3,5,6,7], [4], [4], [4,8,9], [7], [7]]`
> 2. 간선을 가장 많이 가지고 있는 노드를 꼭대기 노드(topNode)로 지정한다.
> 3. topNode의 자식 노드별로 자식의 개수를 저장한다.
    - 자식 개수를 반환하는 함수를 만든다.
    - (tree, node)를 인수로 받아서 node부터 방문 처리를 해가며 tree를 순환하여 총 자식 수 반환.  
> 4. 전체 노드의 절반과 가장 근접한 자식 개수를 가진 노드와 연결을 끊는다.


### 🖥️ 풀이 코드
```
function solution(n, wires) {
    // 트리 형태로 변환
    let tree = Array.from({length : n + 1}, () => Array())
    for (let node of wires) {
        tree[node[0]].push(node[1])
        tree[node[1]].push(node[0])
    }
	// 꼭대기 노드 정하기
    let topNode = [0,0]
    for(let i = 0; i < tree.length; i ++) {
        if (tree[i].length > topNode[1]) {
            topNode = [i,tree[i].length]
        }
    }
    
    const countChildNode = (nodeNum) => {
        let visited = new Array(n+1).fill(false)
        visited[nodeNum] = true
        visited[topNode[0]] = true
        let queue = tree[nodeNum]
        let countChild = 1
        while (queue.length > 0) {
            let childNode = queue.shift()
            if (visited[childNode]) continue
            visited[childNode] = true
            countChild ++
            
            for(let child of tree[childNode]) {
                if (!visited[child]) {
                    visited[child] = true
                    countChild ++
                    tree[child].forEach((el) => queue.push(el))
                }
            }
        }
        return countChild
    }
    
    let answer = n
    for(let node of tree[topNode[0]]) {
        let value = countChildNode(node)
        console.log("value", value)
        if (Math.abs(n - value * 2) < answer) {
            answer = Math.abs(n - value * 2)
        }
    }
    
    return answer
}
```

### 🔎 생각한 개선 방법 및 힌트

> 1. 단순히 간선을 많이 가지고 있는 노드를 부모 노드로 지정하면 안된다. 그렇기 때문에 꼭대기 노드를 지정할 마땅한 기준이 없으며, 모든 노드마다 연결된 노드의 자식 수를 비교해봐야 한다.


### 📌 풀이 방법 (2차 시도 -> 성공)

> 1. 최상단 노드를 따로 지정하지 않고, 각 노드마다 연결된 노드의 자식 개수가 정답과 가장 근접한 값만 찾기.

### 🖥️ 풀이 코드
```
function solution(n, wires) {
    // 트리 형태로 변환
    const tree = Array.from({length : n + 1}, () => Array())
    for (let node of wires) {
        tree[node[0]].push(node[1])
        tree[node[1]].push(node[0])
    }
    
    // 해당 노드와 연결된 노드의 자식 노드 개수 세는 함수
    const countChildNode = (parentNode, nodeNum) => {
        let visited = new Array(n+1).fill(false)
        visited[nodeNum] = true
        visited[parentNode] = true
        let queue = JSON.parse(JSON.stringify(tree[nodeNum]))
        let countChild = 1
        while (queue.length > 0) {
            let childNode = queue.shift()
            if (visited[childNode]) continue
            visited[childNode] = true
            countChild ++
            
            for(let child of tree[childNode]) {
                if (!visited[child]) {
                    visited[child] = true
                    countChild ++
                    for (let item of tree[child]) {
                        queue.push(item)
                    }
                }
            }
        }
        return countChild
    }
    
    let answer = n
    // 자식 노드 개수중 정답과 가장 근접한 값 찾기
    for(let i = 1; i <= n; i++) {
        for (let node of tree[i]) {
            let value = Math.abs(n - countChildNode(i, node) * 2)
            if (value < answer ) answer = value
        }
    }
    
    return answer
}
```

## Lv. 2 시소 짝
### 📖  문제
어느 공원 놀이터에는 시소가 하나 설치되어 있습니다. 이 시소는 중심으로부터 2(m), 3(m), 4(m) 거리의 지점에 좌석이 하나씩 있습니다.  
이 시소를 두 명이 마주 보고 탄다고 할 때, 시소가 평형인 상태에서 각각에 의해 시소에 걸리는 토크의 크기가 서로 상쇄되어 완전한 균형을 이룰 수 있다면 그 두 사람을 시소 짝꿍이라고 합니다. 즉, 탑승한 사람의 무게와 시소 축과 좌석 간의 거리의 곱이 양쪽 다 같다면 시소 짝꿍이라고 할 수 있습니다.  
사람들의 몸무게 목록 `weights`이 주어질 때, 시소 짝꿍이 몇 쌍 존재하는지 구하여 return 하도록 solution 함수를 완성해주세요.

---

##### 제한 사항

- 2 ≤ `weights`의 길이 ≤ 100,000
- 100 ≤ `weights`[i] ≤ 1,000
    - 몸무게 단위는 N(뉴턴)으로 주어집니다.
    - 몸무게는 모두 정수입니다.

---

##### 입출력 예

|weights|result|
|---|---|
|[100,180,360,100,270]|4|

---

### 📌 풀이 방법 (1차 시도 -> 성공)

> 1. map객체에 무게(key) : 개수(value)로 weights를 담아준다.
> 2. weights 배열에 비율대로 배수를 곱해주면서 사전에 있는지 확인한다.
> 3. 비율을 곱해준 값을 확인하면서 같은 값이 map에 있을 경우 count 해준다.
> 4. 1 : 1 비율은 따로 계산해준다.

### 🖥️ 풀이 코드
```
function solution(weights) {
    // 해당 값의 배수와 같은 값 찾는 함수 
    const findMatch = (weightsArray) => {
        weightsArray.forEach((weight) => {
            if (weightsMap.get(weight)) {
                count += weightsMap.get(weight)
            }
        })
        return
    }
    
    let count = 0
    // weightsMap생성
    let weightsMap = new Map()
    weights.forEach((w) => {
        weightsMap.set(w, (weightsMap.get(w) + 1) || 1)
    })
    
    // 같은 수가 n개 있으면 (n * (n-1)) / 2 만큼 조합 가능
    for(let value of weightsMap.values()) {
        if (value > 1) count += (value * (value - 1)) / 2 // 1 : 1 비율
    }
    findMatch(weights.map(w => w * 1.5))     // 2 : 3 비율
    findMatch(weights.map(w => w * 2))       // 2 : 4 비율
    findMatch(weights.map(w => w * (4 / 3))) // 3 : 4 비율

    return count
}
```

### 🔎 생각한 개선 방법 및 힌트

> 1.  처음에 1 : 1 비율 계산을 !(n-1)로 계산해서 복잡했는데, (n * (n-1)) / 2 로 계산하니 한 줄로 작성할 수 있어 더욱 간단하게 작성할 수 있었다.
> 2. 처음 풀이 때 문제를 잘못 읽어서 쌍을 만든 값을 제거하는 걸로 로직을 짜서, 아예 새로 풀게 되었다.

**생각한 로직이 맞는지 문제의 예시와 한 번 더 비교해보자**

`풀이 시간 : 2시간`

## Lv. 2 호텔 대실
### 📖  문제
호텔을 운영 중인 코니는 최소한의 객실만을 사용하여 예약 손님들을 받으려고 합니다. 한 번 사용한 객실은 퇴실 시간을 기준으로 10분간 청소를 하고 다음 손님들이 사용할 수 있습니다.  
예약 시각이 문자열 형태로 담긴 2차원 배열 `book_time`이 매개변수로 주어질 때, 코니에게 필요한 최소 객실의 수를 return 하는 solution 함수를 완성해주세요.

---

##### 제한사항

- 1 ≤ `book_time`의 길이 ≤ 1,000
    - `book_time[i]`는 ["HH:MM", "HH:MM"]의 형태로 이루어진 배열입니다
        - [대실 시작 시각, 대실 종료 시각] 형태입니다.
    - 시각은 HH:MM 형태로 24시간 표기법을 따르며, "00:00" 부터 "23:59" 까지로 주어집니다.
        - 예약 시각이 자정을 넘어가는 경우는 없습니다.
        - 시작 시각은 항상 종료 시각보다 빠릅니다.

---

##### 입출력 예

|book_time|result|
|---|---|
|[["15:00", "17:00"], ["16:40", "18:20"], ["14:20", "15:20"], ["14:10", "19:20"], ["18:20", "21:20"]]|3|
|[["09:10", "10:10"], ["10:20", "12:20"]]|1|
|[["10:20", "12:30"], ["10:20", "12:30"], ["10:20", "12:30"]]|3|


---

### 📌 풀이 방법 (1차 시도 -> 성공)

> **최소 객실의 수를 반환.**
	객실당 퇴실 10분 후 사용 가능.
> **필요한 자료**
	Map 입실시간 순으로 예약 순번 : 입실시간 형태의 inMap
	Map 입실과 같은 형태로(퇴실시간은 10분 추가해서 담아주기) outMap
	Array 방에 예약 순번으로 예약정보를 담는 rooms
>**방의 정보를 담은 배열 생성.**
	첫번째 예약을 방에 넣고, 다음 예약이 퇴실시간 이전이라면 새로 추가. 아니라면 교체.
	방이 새로 추가될 경우 다음 예약부터 모든 방을 확인하면서 들어갈 수 있는지 판단. 아니면 추가.
>**방 배열의 길이반환.** 

### 🖥️ 풀이 코드
```
function solution(book_time) {
    let inMap = new Map()
    let outMap = new Map()
    let rooms = new Array()
    // 시간을 문자열에서 숫자로 변환, 퇴실시간에 10분 더해줌.
    book_time.forEach((el) => {
        el[0] = parseInt(el[0].split(":").join(""))
        
        if (el[1][3] >= 5) {
            el[1] = parseInt(el[1].split(":").join("")) + 100 - 50
        }
        else {
            el[1] = parseInt(el[1].split(":").join("")) + 10
        }
    })
    // 입실 시간 순서대로 원본 배열 정렬
    book_time.sort((a,b) => a[0] - b[0])
    let test = new Array()
    
    // 입실,퇴실 시간별로 map생성.
    for (let i = 0; i < book_time.length; i ++) {
        inMap.set(i, book_time[i][0])
        outMap.set(i, book_time[i][1])
    }

    rooms.push(0) // 첫 번째 방 삽입

	// 기존 방에 입실 가능하면 입실, 아니면 새로운 방에 입실
    for(let i = 1; i < book_time.length; i ++) {
        let entrance = false
        for (let j = 0; j < rooms.length; j ++) {
            if (outMap.get(rooms[j]) <= inMap.get(i)) {
                rooms[j] = i
                entrance = true
                break
            }
        }
        if (!entrance) rooms.push(i)
    }
    
    // console.log("rooms : ", rooms)
    // console.log("원본 배열", book_time)
    // console.log("Map 데이터", inMap, outMap)
    return rooms.length
}
```

### 🔎 생각한 개선 방법 및 힌트

1. 시간 바꾸는 과정 단순화
```
function makeMinStamp(time) {
    const [hour, min] = time.split(":").map(v => Number(v));
    return hour * 60 + min;
}
```
위의 함수를 만들어 문자열의 시간을 더욱 간단하게 변경할 수 있다.

2.  간단하게 최소 힙을 통한 더욱 효율적인 처리
```
// 최소 힙을 사용하여 객실 배정
    for (const [start, end] of bookings) {
        if (minHeap.length && minHeap[0] <= start) {
            // 가장 빨리 끝나는 예약을 제거
            minHeap.shift();
        }
        // 새로운 예약의 종료 시간을 추가
        minHeap.push(end);
        // 종료 시간을 정렬하여 가장 빨리 끝나는 시간을 항상 앞에 두도록 유지
        minHeap.sort((a, b) => a - b);
    }
```

최소 힙을 떠올리지 못한 이유 => 코드로만 기억하고 있었기 때문.
**해당 알고리즘의 코드 예시보다 본질을 생각하자**

`풀이시간 : 1시간`

## Lv. 2 메뉴 리뉴얼 [복습 완료]
### 📖  문제
레스토랑을 운영하던 `스카피`는 코로나19로 인한 불경기를 극복하고자 메뉴를 새로 구성하려고 고민하고 있습니다.  
기존에는 단품으로만 제공하던 메뉴를 조합해서 코스요리 형태로 재구성해서 새로운 메뉴를 제공하기로 결정했습니다. 어떤 단품메뉴들을 조합해서 코스요리 메뉴로 구성하면 좋을 지 고민하던 "스카피"는 이전에 각 손님들이 주문할 때 가장 많이 함께 주문한 단품메뉴들을 코스요리 메뉴로 구성하기로 했습니다.  
단, 코스요리 메뉴는 최소 2가지 이상의 단품메뉴로 구성하려고 합니다. 또한, 최소 2명 이상의 손님으로부터 주문된 단품메뉴 조합에 대해서만 코스요리 메뉴 후보에 포함하기로 했습니다.

예를 들어, 손님 6명이 주문한 단품메뉴들의 조합이 다음과 같다면,  
(각 손님은 단품메뉴를 2개 이상 주문해야 하며, 각 단품메뉴는 A ~ Z의 알파벳 대문자로 표기합니다.)

|손님 번호|주문한 단품메뉴 조합|
|---|---|
|1번 손님|A, B, C, F, G|
|2번 손님|A, C|
|3번 손님|C, D, E|
|4번 손님|A, C, D, E|
|5번 손님|B, C, F, G|
|6번 손님|A, C, D, E, H|

가장 많이 함께 주문된 단품메뉴 조합에 따라 "스카피"가 만들게 될 코스요리 메뉴 구성 후보는 다음과 같습니다.

|코스 종류|메뉴 구성|설명|
|---|---|---|
|요리 2개 코스|A, C|1번, 2번, 4번, 6번 손님으로부터 총 4번 주문됐습니다.|
|요리 3개 코스|C, D, E|3번, 4번, 6번 손님으로부터 총 3번 주문됐습니다.|
|요리 4개 코스|B, C, F, G|1번, 5번 손님으로부터 총 2번 주문됐습니다.|
|요리 4개 코스|A, C, D, E|4번, 6번 손님으로부터 총 2번 주문됐습니다.|

---

#### **[문제]**

각 손님들이 주문한 단품메뉴들이 문자열 형식으로 담긴 배열 orders, "스카피"가 `추가하고 싶어하는` 코스요리를 구성하는 단품메뉴들의 갯수가 담긴 배열 course가 매개변수로 주어질 때, "스카피"가 새로 추가하게 될 코스요리의 메뉴 구성을 문자열 형태로 배열에 담아 return 하도록 solution 함수를 완성해 주세요.

#### **[제한사항]**

- orders 배열의 크기는 2 이상 20 이하입니다.
- orders 배열의 각 원소는 크기가 2 이상 10 이하인 문자열입니다.
    - 각 문자열은 알파벳 대문자로만 이루어져 있습니다.
    - 각 문자열에는 같은 알파벳이 중복해서 들어있지 않습니다.
- course 배열의 크기는 1 이상 10 이하입니다.
    - course 배열의 각 원소는 2 이상 10 이하인 자연수가 `오름차순`으로 정렬되어 있습니다.
    - course 배열에는 같은 값이 중복해서 들어있지 않습니다.
- 정답은 각 코스요리 메뉴의 구성을 문자열 형식으로 배열에 담아 사전 순으로 `오름차순` 정렬해서 return 해주세요.
    - 배열의 각 원소에 저장된 문자열 또한 알파벳 `오름차순`으로 정렬되어야 합니다.
    - 만약 가장 많이 함께 주문된 메뉴 구성이 여러 개라면, 모두 배열에 담아 return 하면 됩니다.
    - orders와 course 매개변수는 return 하는 배열의 길이가 1 이상이 되도록 주어집니다.

---

##### **[입출력 예]**

|orders|course|result|
|---|---|---|
|`["ABCFG", "AC", "CDE", "ACDE", "BCFG", "ACDEH"]`|[2,3,4]|`["AC", "ACDE", "BCFG", "CDE"]`|
|`["ABCDE", "AB", "CD", "ADE", "XYZ", "XYZ", "ACD"]`|[2,3,5]|`["ACD", "AD", "ADE", "CD", "XYZ"]`|
|`["XYZ", "XWY", "WXA"]`|[2,3,4]|`["WX", "XY"]`|


---

### 📌 풀이 방법 (1차 시도 - 실패)

> 1. 재귀함수로 완전탐색을 구현하여 모든 조합을 사전에 넣는다.
> 2. 사전에 있는 메뉴조합 중 조건에 맞는 메뉴조합을 course별로 모아 놓은 배열에 넣는다.
> 3. 메뉴 조합의 주문 횟수가 담아놓은 메뉴 조합보다 클 경우 배열을 비우고 해당 메뉴만 채워준다. 횟수가 같은 경우에는 push해준다.

### 🖥️ 풀이 코드
```
function solution(orders, course) {
    // 메뉴 조합 알파벳 순서대로 정렬
    orders = orders.map((el) => el.split("").sort().join(""))
    let menuDict = new Map()
    
    const visited = Array(20).fill(false)
    
    // 메뉴 조합 사전에 담는 dfs함수
    const dfs = (comb, len, menu) => {
        if (len === menu.length) {
            menuDict.set(comb, (menuDict.get(comb) + 1) || 1)
            return
        }
        if (len >= 2) {
            menuDict.set(comb, (menuDict.get(comb) + 1) || 1)
        }
        
        for (let i = len; i < menu.length; i ++) {
            if (!visited[i]) {
                visited[i] = true
                dfs(comb + menu[i], len + 1, menu)
                visited[i] = false
            }
        }
    }
    
    // 주문별로 dfs함수 실행
    orders.forEach((menu) => {
        dfs("", 0, menu)
    })
    
    let combsArray = Array.from({length : course.length}, () => [])
    
    // 사전의 데이터들을 순회하면서 추가
    for(let [comb, cnt] of menuDict) {
        // 등장 횟수가 2회 미만일 경우 패스
        if (cnt === 1) continue
        for (let i = 0; i < course.length; i ++) {
            if (comb.length === course[i]) {
                let rightCourse = combsArray[i]
                if (combsArray[i].length === 0 || cnt === menuDict.get(combsArray[i][combsArray[i].length-1])) {
                    combsArray[i].push(comb)  
                }
                else if (cnt > menuDict.get(combsArray[i][combsArray[i].length-1])) {
                    combsArray[i] = [comb]
                }
            }
        }
    }
    
    return combsArray.flat().sort()
}
```

### 🔎 생각한 개선 방법 및 힌트

> 1. 조합을 모두 사전에 등록할 필요 없이, course에 있는 길이에 해당하는 조합들만 사전에 등록.
> 2. 완전탐색을 재귀함수로 구현하기보다, 백트래킹으로 구현하는게 더욱 효율적.

### 📌📌 풀이 방법 (2차 시도 -> 성공)

>**문제 정리**
>2명 이상이 주문한 조합을 목록에 포함하여 반환.
>조합을 만들고 싶은 요리의 개수가 course에 담겨있고, 가장 많이 주문 된 조합을 추가한다. (동률이면 모두 추가)

>**풀이 과정**
>1. 각 주문마다 만들 수 있는 조합을 모두 만들고, 객체에 추가한다.
>2. 객체를 순회하면서 corse의 길이만큼, 개수가 높은 조합을 result에 추가한다.

>**조합 만들기**
>1. **모든 길이를 만들 필요 없고 필요한 길이의 단어들만 만들어준다.**
>2. (주문, 시작 지점, 길이, 단어)를 인자로 받아서 해당 길이를 충족하면 조합>에 추가한다.
>3. 해당 코스의 주문 수가 2를 넘으면 후보에 등록시켜주고, 해당 길이 최대 갯수를 업데이트 해준다.
>4. 코스 후보에서 각 길이별 최대 개수의 메뉴를 정렬하여 결과에 추가한다.
>5. 결과에 있는 코스들을 오름차순으로 정렬해준다.

### 🖥️ 풀이 코드
```
function solution(orders, course) {
  const ordered = {};
  const candidates = {};
  const maxNum = Array(10 + 1).fill(0);
  const createSet = (arr, start, len, foods) => {
    if (len === 0) {
      ordered[foods] = (ordered[foods] || 0) + 1;
      if (ordered[foods] > 1) candidates[foods] = ordered[foods];
      maxNum[foods.length] = Math.max(maxNum[foods.length], ordered[foods]);
      return;
    }

    for (let i = start; i < arr.length; i++) {
      createSet(arr, i + 1, len - 1, foods + arr[i]);
    }
  };

  orders.forEach((od) => {
    // arr.sort는 기본적으로 사전식 배열
    const sorted = od.split('').sort();
    // 주문한 음식을 사전순으로 배열해서 문자열을 만든다.
    // course에 있는 길이만 만들면 된다.
    course.forEach((len) => {
      createSet(sorted, 0, len, '');
    });
  });

  const launched = Object.keys(candidates).filter(
    (food) => maxNum[food.length] === candidates[food]
  );

  return launched.sort();
}
```

**완전탐색관련 문제를 풀어보면서 더 익숙해지기**
## Lv. 2 [수학] 숫자 카드 나누기
### 📖  문제
철수와 영희는 선생님으로부터 숫자가 하나씩 적힌 카드들을 절반씩 나눠서 가진 후, 다음 두 조건 중 하나를 만족하는 가장 큰 양의 정수 a의 값을 구하려고 합니다.

1. 철수가 가진 카드들에 적힌 모든 숫자를 나눌 수 있고 영희가 가진 카드들에 적힌 모든 숫자들 중 하나도 나눌 수 없는 양의 정수 a
2. 영희가 가진 카드들에 적힌 모든 숫자를 나눌 수 있고, 철수가 가진 카드들에 적힌 모든 숫자들 중 하나도 나눌 수 없는 양의 정수 a

예를 들어, 카드들에 10, 5, 20, 17이 적혀 있는 경우에 대해 생각해 봅시다. 만약, 철수가 [10, 17]이 적힌 카드를 갖고, 영희가 [5, 20]이 적힌 카드를 갖는다면 두 조건 중 하나를 만족하는 양의 정수 a는 존재하지 않습니다. 하지만, 철수가 [10, 20]이 적힌 카드를 갖고, 영희가 [5, 17]이 적힌 카드를 갖는다면, 철수가 가진 카드들의 숫자는 모두 10으로 나눌 수 있고, 영희가 가진 카드들의 숫자는 모두 10으로 나눌 수 없습니다. 따라서 철수와 영희는 각각 [10, 20]이 적힌 카드, [5, 17]이 적힌 카드로 나눠 가졌다면 조건에 해당하는 양의 정수 a는 10이 됩니다.

철수가 가진 카드에 적힌 숫자들을 나타내는 정수 배열 `arrayA`와 영희가 가진 카드에 적힌 숫자들을 나타내는 정수 배열 `arrayB`가 주어졌을 때, 주어진 조건을 만족하는 가장 큰 양의 정수 a를 return하도록 solution 함수를 완성해 주세요. 만약, 조건을 만족하는 a가 없다면, 0을 return 해 주세요.

---

##### 제한사항

제한사항

- 1 ≤ `arrayA`의 길이 = `arrayB`의 길이 ≤ 500,000
- 1 ≤ `arrayA`의 원소, `arrayB`의 원소 ≤ 100,000,000
- `arrayA`와 `arrayB`에는 중복된 원소가 있을 수 있습니다.

---

##### 입출력 예

|arrayA|arrayB|result|
|---|---|---|
|[10, 17]|[5, 20]|0|
|[10, 20]|[5, 17]|10|
|[14, 35, 119]|[18, 30, 102]|7|


---

### 📌 풀이 방법 (1차 시도 -> 성공)

> 1. 유클리드 호제법을 통해 각 배열의 최대 공약수를 구한다.
> 2. 최대 공약수의 약수들을 구하고, 큰 값부터 반대쪽 배열의 값을 나눈다.
> 3. 모든 값이 나눠지지 않는 경우, 해당 값을 반환한다.
> 4. 양쪽 배열 모두 해당 과정을 진행하고, 큰 값을 정답으로 반환한다.

### 🖥️ 풀이 코드
```
function solution(arrayA, arrayB) {
    // 최대 공약수 구하는 함수
    const gcd = (num1,num2) => {
        let a = num1
        let b = num2
        if (num1 < num2) {
            a = num1
            b = num2
        }
    
        let r = 1
        while (r > 0) {
            r = a % b
            a = b
            b = r
        }
        return a
    }
    
    // 배열의 모든 값 중에서 최대 공약수 구하는 함수
    const gcdArray = (arr) => {
        let tempA = [...arr]
        let tempB = []
        while (true) {
            if (tempA.length % 2 !== 0) tempA.push(tempA[0])
            for (let i = 0; i < tempA.length - 1; i += 2) {
                tempB.push(gcd(tempA[i], tempA[i+1]))
            }
            if (tempB.length === 1) return tempB[0]
            if (tempB.length % 2 !== 0) tempB.push(tempB[0])
            tempA = []
            for (let i = 0; i < tempB.length - 1; i += 2) {
                tempA.push(gcd(tempB[i], tempB[i+1]))
            }
            if (tempA.length === 1) return tempA[0]
            tempB = []
        }
    }
    
    // 최대 공약수의 모든 약수 구하는 함수
    const divisors = (a) => {
        let result = []
        for (let i = 2 ; i <= Math.sqrt(a); i++) {
            if (a % i === 0) result.push(i)
        }
        result.push(a)
        return result
    }
    
    // 한 쪽의 최대 공약수의 약수들로 다른 배열의 모든 값들과 나눠지지 않는 값 찾는 함수
    const correctValue = (divisors,otherArr) => {
        // 최대공약수의 약수들의 모음인 divisors의 최대값부터 비교.
        for (let i = divisors.length - 1; i >= 0; i --) {
        let value = divisors[i]
            for (let i = 0; i < otherArr.length; i ++) {
                if (otherArr[i] % value === 0) break
                if (i === otherArr.length-1) return value
            }
        }
        return 0
    }
    
    // 메인 로직
    const gcdA = gcdArray(arrayA)
    const gcdB = gcdArray(arrayB)
    const divisorsA = divisors(gcdA)
    const divisorsB = divisors(gcdB)
    const answer = Math.max(correctValue(divisorsA,arrayB), correctValue(divisorsB,arrayA))
    
    return answer
}
```

### 🔎 생각한 개선 방법 및 힌트
**다른사람의 좋은 풀이**
```
function solution(arrayA, arrayB) {
    const aResult = getAnswer(arrayA, arrayB)
    const bResult = getAnswer(arrayB, arrayA)

    return aResult > bResult ? aResult : bResult
}

function getAnswer (A, B) {
    A.sort((a, b) => a - b)
    for (let i = A[0]; i > 1; i--) {
        if (A.every(a => a % i === 0) && !B.some(b => b % i === 0)) return i
    }
    return 0
}
```

> 1. 해당 배열의 약수는 해당 배열의 최소값보다 같거나 작다는 사실을 활용.
> 2. `every메서드` => 배열의 모든 요소가 주어진 조건을 만족하면 true 아니면 false반환.
> 3. `some메서드` => 배열의 한 요소라도 주어진 조건을 만족하면 true, 아니면 false반환.

1번같은 조건 활용은 여러 수의 공약수에 대해서 조금 더 고민해보면 도출해낼 수 있다.

`every`와 `some`메서드를 새로 알게 되어 앞으로 반복문을 사용하는 대신 유용하게 활용할 수 있을 것 같다.

`풀이시간 : 1시간 30분`

## Lv. 2 [수학] 마법의 엘리베이터
### 📖  문제
마법의 세계에 사는 민수는 아주 높은 탑에 살고 있습니다. 탑이 너무 높아서 걸어 다니기 힘든 민수는 마법의 엘리베이터를 만들었습니다. 마법의 엘리베이터의 버튼은 특별합니다. 마법의 엘리베이터에는 -1, +1, -10, +10, -100, +100 등과 같이 절댓값이 10c (c ≥ 0 인 정수) 형태인 정수들이 적힌 버튼이 있습니다. 마법의 엘리베이터의 버튼을 누르면 현재 층 수에 버튼에 적혀 있는 값을 더한 층으로 이동하게 됩니다. 단, 엘리베이터가 위치해 있는 층과 버튼의 값을 더한 결과가 0보다 작으면 엘리베이터는 움직이지 않습니다. 민수의 세계에서는 0층이 가장 아래층이며 엘리베이터는 현재 민수가 있는 층에 있습니다.

마법의 엘리베이터를 움직이기 위해서 버튼 한 번당 마법의 돌 한 개를 사용하게 됩니다.예를 들어, 16층에 있는 민수가 0층으로 가려면 -1이 적힌 버튼을 6번, -10이 적힌 버튼을 1번 눌러 마법의 돌 7개를 소모하여 0층으로 갈 수 있습니다. 하지만, +1이 적힌 버튼을 4번, -10이 적힌 버튼 2번을 누르면 마법의 돌 6개를 소모하여 0층으로 갈 수 있습니다.

마법의 돌을 아끼기 위해 민수는 항상 최소한의 버튼을 눌러서 이동하려고 합니다. 민수가 어떤 층에서 엘리베이터를 타고 0층으로 내려가는데 필요한 마법의 돌의 최소 개수를 알고 싶습니다. 민수와 마법의 엘리베이터가 있는 층을 나타내는 정수 `storey` 가 주어졌을 때, 0층으로 가기 위해 필요한 마법의 돌의 최소값을 return 하도록 solution 함수를 완성하세요.

---

##### 제한사항

- 1 ≤ `storey` ≤ 100,000,000

---

##### 입출력 예

|storey|result|
|---|---|
|16|6|
|2554|16|

---

### 📌 풀이 방법 (1차 시도 -> 성공)
>1. 현재 층에서 가장 가까운 10의 제곱의 배수인 층인 goal으로 이동.
>2. goal으로 이동하기 위해, 끝자리 수를 계속해서 0으로 만들어야 한다.
>3. 해당 층을 0으로 만드는 최소한의 횟수로 해당 층을 0으로 만들고, 해당 수가 5일 경우만 앞자리를 보고 판단.
>4. 앞자리가 5미만이면 -를 5이상이면 +를 해준다.
>5. 해당 자리가 9일 경우 앞에 9가 나오지 않을 때 까지 1씩 올려준다.
>6. 맨 앞자리를 제외한 뒤자릿수의 수가 0이 될 경우 맨 앞자리 수만큼 이동하고 정답 반환.


### 🖥️ 풀이 코드
```
function solution(storey) {
    let count = 0;
    // 배열로 변환
    storey = storey.toString().split("").map(el => parseInt(el))
    
    // 메인 로직
    for (let i = storey.length - 1; i > 0; i --) {
        let currValue = storey[i]
        if (currValue === 0) continue
        // 5일 경우
        if (currValue === 5) {
            if (storey[i-1] >= 5) {
                if (storey[i-1] === 9) {
                    isNine(storey, i)
                }
                else {
                    storey[i-1] ++    
                }
                count += (10 - currValue)
            }
            else {
                count += currValue    
            }
        }
        // 5보다 클 경우
        else if (currValue > 5) {
            if (storey[i-1] === 9) {
                isNine(storey, i)    
            }
            else {
                storey[i-1] ++
            }
            count += (10 - currValue)
        }
        // 5보다 작을 경우
        else {
            count += currValue
        }
    }
    
    // 맨 앞자리 수 더해줌
    let firstValue = storey[0]
    if (firstValue > 5) {
        count += (10 - firstValue) + 1
    }
    else {
        count += firstValue
    }
        
    return count
}

// 9일 경우 앞자리 수를 올려주는 함수
function isNine(arr, i) {
    let idx = 1            
    while ((i - idx) > 0 && arr[i-idx] === 9) {
        arr[i - idx] = 0
        idx ++
    }
    if (i === idx) {
        arr[0] ++
    } else {
        arr[i- (idx+1) ] ++
    }
    return
}
```

### 🔎 생각한 개선 방법 및 힌트

> 재귀적으로 푸는 방법도 있다.

**다른 좋은 풀이**
```
function solution(storey) {
    if (storey < 5) return storey;
    const r = storey % 10;
    const m = (storey - r) / 10;
    return Math.min(r + solution(m), 10 - r + solution(m + 1));
}
```

>1. 1의자리 숫자와 10의자리 숫자를 통해 올릴지 내릴지 판단하고, 계산이 끝나면 1의자리 숫자를 없애고 10의자리 숫자가 1의자리로 오게 하여 반복.
>2. 0층으로 가는 것과, 10층으로 올리는 것 중 최소 값을 반환하여 재귀적으로 풀이.

`풀이 시간 : 1시간`

## Lv. 2 [다익스트라] 배달 [복습 완료]
### 📖  문제

N개의 마을로 이루어진 나라가 있습니다. 이 나라의 각 마을에는 1부터 N까지의 번호가 각각 하나씩 부여되어 있습니다. 각 마을은 양방향으로 통행할 수 있는 도로로 연결되어 있는데, 서로 다른 마을 간에 이동할 때는 이 도로를 지나야 합니다. 도로를 지날 때 걸리는 시간은 도로별로 다릅니다. 현재 1번 마을에 있는 음식점에서 각 마을로 음식 배달을 하려고 합니다. 각 마을로부터 음식 주문을 받으려고 하는데, N개의 마을 중에서 K 시간 이하로 배달이 가능한 마을에서만 주문을 받으려고 합니다. 다음은 N = 5, K = 3인 경우의 예시입니다.

![배달_1_uxun8t.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/d7779d88-084c-4ffa-ae9f-2a42f97d3bbf/%E1%84%87%E1%85%A2%E1%84%83%E1%85%A1%E1%86%AF_1_uxun8t.png)

위 그림에서 1번 마을에 있는 음식점은 [1, 2, 4, 5] 번 마을까지는 3 이하의 시간에 배달할 수 있습니다. 그러나 3번 마을까지는 3시간 이내로 배달할 수 있는 경로가 없으므로 3번 마을에서는 주문을 받지 않습니다. 따라서 1번 마을에 있는 음식점이 배달 주문을 받을 수 있는 마을은 4개가 됩니다.  
마을의 개수 N, 각 마을을 연결하는 도로의 정보 road, 음식 배달이 가능한 시간 K가 매개변수로 주어질 때, 음식 주문을 받을 수 있는 마을의 개수를 return 하도록 solution 함수를 완성해주세요.

##### 제한사항

- 마을의 개수 N은 1 이상 50 이하의 자연수입니다.
- road의 길이(도로 정보의 개수)는 1 이상 2,000 이하입니다.
- road의 각 원소는 마을을 연결하고 있는 각 도로의 정보를 나타냅니다.
- road는 길이가 3인 배열이며, 순서대로 (a, b, c)를 나타냅니다.
    - a, b(1 ≤ a, b ≤ N, a != b)는 도로가 연결하는 두 마을의 번호이며, c(1 ≤ c ≤ 10,000, c는 자연수)는 도로를 지나는데 걸리는 시간입니다.
    - 두 마을 a, b를 연결하는 도로는 여러 개가 있을 수 있습니다.
    - 한 도로의 정보가 여러 번 중복해서 주어지지 않습니다.
- K는 음식 배달이 가능한 시간을 나타내며, 1 이상 500,000 이하입니다.
- 임의의 두 마을간에 항상 이동 가능한 경로가 존재합니다.
- 1번 마을에 있는 음식점이 K 이하의 시간에 배달이 가능한 마을의 개수를 return 하면 됩니다.

---

##### 입출력 예

| N   | road                                                      | K   | result |
| --- | --------------------------------------------------------- | --- | ------ |
| 5   | [[1,2,1],[2,3,3],[5,2,2],[1,4,2],[5,3,1],[5,4,2]]         | 3   | 4      |
| 6   | [[1,2,1],[1,3,2],[2,3,2],[3,4,3],[3,5,2],[3,5,3],[5,6,1]] | 4   | 4      |

---

### 📌 풀이 방법 (1차 시도 -> 시간 초과)

> 1. DFS를 통해 구현
>2. 재귀함수를 통해 시작지점, 목표지점이 일치하는 곳이 나오면 방문하지 않았을 경우 방문하고 재귀함수 호출.

### 🖥️ 풀이 코드
```
function generateTestCase(N, numRoads) {
    const road = [];
    const maxRoadWeight = 10;
    const maxRoadsPerNode = Math.min(N - 1, 10);

    // 생성된 도로를 확인하기 위해 사용되는 set
    const usedRoads = new Set();

    for (let i = 1; i <= N; i++) {
        for (let j = i + 1; j <= N; j++) {
            if (road.length < numRoads) {
                const weight = Math.floor(Math.random() * maxRoadWeight) + 1;
                road.push([i, j, weight]);
                usedRoads.add(`${i}-${j}`);
                usedRoads.add(`${j}-${i}`);
            }
        }
    }

    // 추가 도로 생성하여 2000개 맞추기
    while (road.length < numRoads) {
        const a = Math.floor(Math.random() * N) + 1;
        const b = Math.floor(Math.random() * N) + 1;
        if (a !== b && !usedRoads.has(`${a}-${b}`)) {
            const weight = Math.floor(Math.random() * maxRoadWeight) + 1;
            road.push([a, b, weight]);
            usedRoads.add(`${a}-${b}`);
            usedRoads.add(`${b}-${a}`);
        }
    }

    return road;
}

const N = 50;
const numRoads = 2000;
const K = 10; // 적절한 배달 시간

const testCaseRoads = generateTestCase(N, numRoads);


function solution(N, testCaseRoads, K) {
    if (N === 1) return 1
    
    let towns = new Array(N + 1).fill(false)
    const visited = new Array(road.length).fill(false)
    
    // dfs 함수
    const dfs = (start, target, time) => {
        // 시간이 초과되거나 이미 해당 마을은 배달이 가능한 경우 종료
        if (time > K || towns[target]) return
        // 목표 지점에 도착하면 해당 마을 true처리
        if (start === target) {
            towns[target] = true
            return
        }
        // 길을 중복해서 방문하지 않도록, 방문처리 하면서 이동
        for (let i = 0; i < road.length; i ++) {
            if (!visited[i] && (road[i][0] === start || road[i][1] === start)) {
                visited[i] = true
                if (road[i][0] === start) {
                    dfs(road[i][1], target, time + road[i][2])    
                }
                else {
                    dfs(road[i][0], target, time + road[i][2])    
                }
                visited[i] = false
            }
        }
    }
    
    // 모든 마을마다 dfs함수 실행
    for (let i = 2; i <= N; i ++) {
        dfs(1, i, 0)
    }
    
    towns = towns.filter(el => el)
    return towns.length + 1
}
```

### 🔎 생각한 개선 방법 및 힌트

> 1. DFS로 구현 시에 모든 도로와 마을을 탐색해야 하므로 비효율적.
> 2. 다익스트라 알고리즘을 통해 각 마을까지의 최단 경로를 계산.

### 📌 풀이 방법 (2차 시도 -> 성공)

**다익스트라로 알고리즘으로 구현.**
>다익스트라 알고리즘이란 ?
>`시작 노드에서 다른 모든 노드까지의 최단 거리를 구하는 알고리즘.`

**동작 과정**
>1. 시작 노드에서 각 노드까지의 비용을 배열에 저장한다.
>2. 비용을 저장한 배열에서 가장 가까운 노드로 방문 후 방문처리를 해주고, 해당 노드를 거쳐 다른 노드로 이동하는 비용이 더욱 가까울 경우 비용을 저장한 배열을 업데이트 해준다.
>3. 2의 과정을 모든 노드를 방문할 때 까지 반복하며 비용을 저장한 배열을 업데이트 해준다.

### 🖥️ 풀이 코드
```
function solution(N, road, K) {
    // 저장할 때 편의를 위해 0번 노드는 비워놓는다.
    const visited = new Array(N + 1).fill(false)
    visited[0] = true
    const nodeCosts = new Array(N + 1).fill(Infinity)
    nodeCosts[1] = 0
    
    let targetNode = 1 // 시작 노드 설정
    let count = 1
    // 모든 노드 방문할 때 까지 비용 업데이트
    while (count <= N) {
        visited[targetNode] = true // 노드 방문처리
        
        for (let r of road) {
            let [nodeA, nodeB, cost] = r
            if (nodeA === targetNode && nodeCosts[nodeA] + cost < nodeCosts[nodeB]) {
                nodeCosts[nodeB] = nodeCosts[nodeA] + cost
            }
            else if (nodeB === targetNode && nodeCosts[nodeB] + cost < nodeCosts[nodeA]) {
                nodeCosts[nodeA] = nodeCosts[nodeB] + cost
            }
        }
        // 가장 가까운 노드 타겟으로 설정
        targetNode = 0
        for (let i = 2; i <= N; i ++) {
            if (!visited[i] && nodeCosts[i] <= nodeCosts[targetNode]) {
                targetNode = i
            }
        }
        count ++
    }
    
    return nodeCosts.filter((el) => el <= K).length
}
```

### 🔎 생각한 개선 방법 및 힌트

>1. road를 for문으로 순회하는 과정을 forEach로 더욱 깔끔하게 구현 가능
```
road.forEach(([nodeA, nodeB, cost]) => {

})
```

`풀이 시간 : 35분`

## Lv. 2 [문자열 처리] 방금 그곡
### 📖  문제
라디오를 자주 듣는 네오는 라디오에서 방금 나왔던 음악이 무슨 음악인지 궁금해질 때가 많다. 그럴 때 네오는 다음 포털의 '방금그곡' 서비스를 이용하곤 한다. 방금그곡에서는 TV, 라디오 등에서 나온 음악에 관해 제목 등의 정보를 제공하는 서비스이다.

네오는 자신이 기억한 멜로디를 가지고 방금그곡을 이용해 음악을 찾는다. 그런데 라디오 방송에서는 한 음악을 반복해서 재생할 때도 있어서 네오가 기억하고 있는 멜로디는 음악 끝부분과 처음 부분이 이어서 재생된 멜로디일 수도 있다. 반대로, 한 음악을 중간에 끊을 경우 원본 음악에는 네오가 기억한 멜로디가 들어있다 해도 그 곡이 네오가 들은 곡이 아닐 수도 있다. 그렇기 때문에 네오는 기억한 멜로디를 재생 시간과 제공된 악보를 직접 보면서 비교하려고 한다. 다음과 같은 가정을 할 때 네오가 찾으려는 음악의 제목을 구하여라.

- 방금그곡 서비스에서는 음악 제목, 재생이 시작되고 끝난 시각, 악보를 제공한다.
- 네오가 기억한 멜로디와 악보에 사용되는 음은 C, C#, D, D#, E, F, F#, G, G#, A, A#, B 12개이다.
- 각 음은 1분에 1개씩 재생된다. 음악은 반드시 처음부터 재생되며 음악 길이보다 재생된 시간이 길 때는 음악이 끊김 없이 처음부터 반복해서 재생된다. 음악 길이보다 재생된 시간이 짧을 때는 처음부터 재생 시간만큼만 재생된다.
- 음악이 00:00를 넘겨서까지 재생되는 일은 없다.
- 조건이 일치하는 음악이 여러 개일 때에는 라디오에서 재생된 시간이 제일 긴 음악 제목을 반환한다. 재생된 시간도 같을 경우 먼저 입력된 음악 제목을 반환한다.
- 조건이 일치하는 음악이 없을 때에는 “`(None)`”을 반환한다.

### 입력 형식

입력으로 네오가 기억한 멜로디를 담은 문자열 `m`과 방송된 곡의 정보를 담고 있는 배열 `musicinfos`가 주어진다.

- `m`은 음 `1`개 이상 `1439`개 이하로 구성되어 있다.
- `musicinfos`는 `100`개 이하의 곡 정보를 담고 있는 배열로, 각각의 곡 정보는 음악이 시작한 시각, 끝난 시각, 음악 제목, 악보 정보가 '`,`'로 구분된 문자열이다.
- 음악의 시작 시각과 끝난 시각은 24시간 `HH:MM` 형식이다.
- 음악 제목은 '`,`' 이외의 출력 가능한 문자로 표현된 길이 `1` 이상 `64` 이하의 문자열이다.
- 악보 정보는 음 `1`개 이상 `1439`개 이하로 구성되어 있다.

### 출력 형식

조건과 일치하는 음악 제목을 출력한다.

### 입출력 예시

| m                  | musicinfos                                                 | answer  |
| ------------------ | ---------------------------------------------------------- | ------- |
| "ABCDEFG"          | ["12:00,12:14,HELLO,CDEFGAB", "13:00,13:05,WORLD,ABCDEF"]  | "HELLO" |
| "CC#BCC#BCC#BCC#B" | ["03:00,03:30,FOO,CC#B", "04:00,04:08,BAR,CC#BCC#BCC#B"]   | "FOO"   |
| "ABC"              | ["12:00,12:14,HELLO,C#DEFGAB", "13:00,13:05,WORLD,ABCDEF"] | "WORLD" |


---

### 📌 풀이 방법 (1차 시도 -> 성공)

> 1. 곡마다 데이터를 , 기준으로 나눠준다.
> 2. 시간 차이를 계산해서 재생 시간을 구한다.
> 3. 코드의 길이를 재생 시간에 맞춰 조정해준다.
> 4. 코드를 처음부터 순회하면서 멜로디의 첫 음이 나오면 멜로디가 모두 나오는지 확인한다.
> 5. 멜로디가 포함되면 결과에 추가해주고 최종적으로 재생 길이가 긴 노래를 반환한다.

### 🖥️ 풀이 코드
```
function solution(m, musicinfos) {
    let result = []
    // 메인 로직
    for(let i = 0; i < musicinfos.length; i ++) {
        // 곡 별로 데이터 구분
        let song = musicinfos[i].split(",")
        
        // 코드길이를 재생 시간만큼 늘이거나 줄여줌
        let code = codeToArray(song[3])
        let playTime = timeCheck(song)
        let songTime = code.length
        if (playTime >= songTime) {
            // Case 1 재생 시간 >= 곡 시간 * 2
            if (playTime >= songTime * 2) {
                let count = Math.floor(playTime / songTime)
                let baseCode = [...code]
                let r = playTime % songTime
                for (let i = 1; i < count; i ++) {
                    code = code.concat(baseCode)
                }
                code = code.concat(baseCode.slice(0,r))
            }
            // Case 2 곡 시간 <= 재생 시간 < 곡 시간 * 2
            else {
                code = code.concat(code.slice(0, playTime - songTime))
            }
        }
        // Case 3 재생 시간 < 곡 시간
        else {
            code = code.slice(0, playTime)
        }
        
        // 코드 포함 여부 확인
        let melody = codeToArray(m)
        let firstCode = melody[0]
        let isIncludes = false
        for (let i = 0; i < code.length; i ++) {
            if (code[i] === firstCode) {
                let idx = 1
                if (melody.length === 1) result.push([playTime,song[2]])  
                while (melody[idx] === code[i + idx]) {
                    idx ++
                    if (idx >= melody.length) {
                        isIncludes = true
                        break
                    }
                }
                if (isIncludes) {
                    result.push([playTime,song[2]])  
                    break
                }
            }
        }
    }
    
    // 결과 반환
    if (result.length === 0) return "(None)"
    let max = 0
    for(let i = 0; i < result.length; i ++) {
        if (result[i][0] > result[max][0]) {
            max = i
        }
    }
    return result[max][1]
}

// 재생시간 계산하는 함수
function timeCheck(arr) {
    let start = arr[0].split(":").map(el => parseInt(el))
    let end = arr[1].split(":").map(el => parseInt(el))
    let h = 0
    let m = 0
    // 시 단위 계산
    // 분 단위 계산
    if (start[1] > end[1]) {
        m = end[1] + (60 - start[1])
        h = (end[0] - start[0]) - 1
        
    } else {
        h = end[0] - start[0]
        m = end[1] - start[1]
        
    }
    
    return h * 60 + m
}

// 문자열 코드 배열로 변환하는 함수
function codeToArray(code) {
    let codeArr = []
    for(let i = 0; i < code.length; i ++) {
        if (code[i] === "#") codeArr[codeArr.length-1] += "#"
        else codeArr.push(code[i])
    }
    return codeArr
}
```

### 🔎 생각한 개선 방법 및 힌트

> 1. `11:50 -> 12:10` 처럼 시간이 넘어가는 경우를 1시간이 넘어간 걸로 계산해서 오류를 해결하느라 1시간 가까이 소요되었다.
> 	ㄴ> **함수 체크를 꼼꼼히 하자**

`풀이시간 : 2시간 30분`

## Lv. 2 행렬 테두리 회전하기
### 📖  문제

rows x columns 크기인 행렬이 있습니다. 행렬에는 1부터 rows x columns까지의 숫자가 한 줄씩 순서대로 적혀있습니다. 이 행렬에서 직사각형 모양의 범위를 여러 번 선택해, 테두리 부분에 있는 숫자들을 시계방향으로 회전시키려 합니다. 각 회전은 (x1, y1, x2, y2)인 정수 4개로 표현하며, 그 의미는 다음과 같습니다.

- x1 행 y1 열부터 x2 행 y2 열까지의 영역에 해당하는 직사각형에서 테두리에 있는 숫자들을 한 칸씩 시계방향으로 회전합니다.

다음은 6 x 6 크기 행렬의 예시입니다.

![grid_example.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/ybm/4c3c0fab-11f4-43b6-b290-6f4017e9379f/grid_example.png)

이 행렬에 (2, 2, 5, 4) 회전을 적용하면, 아래 그림과 같이 2행 2열부터 5행 4열까지 영역의 테두리가 시계방향으로 회전합니다. 이때, 중앙의 15와 21이 있는 영역은 회전하지 않는 것을 주의하세요.

![rotation_example.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/ybm/962df137-5c71-4091-ad9f-8e322910c1ab/rotation_example.png)

행렬의 세로 길이(행 개수) rows, 가로 길이(열 개수) columns, 그리고 회전들의 목록 queries가 주어질 때, 각 회전들을 배열에 적용한 뒤, 그 회전에 의해 위치가 바뀐 숫자들 중 **가장 작은 숫자들을 순서대로 배열에 담아** return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- rows는 2 이상 100 이하인 자연수입니다.
- columns는 2 이상 100 이하인 자연수입니다.
- 처음에 행렬에는 가로 방향으로 숫자가 1부터 하나씩 증가하면서 적혀있습니다.
    - 즉, 아무 회전도 하지 않았을 때, i 행 j 열에 있는 숫자는 ((i-1) x columns + j)입니다.
- queries의 행의 개수(회전의 개수)는 1 이상 10,000 이하입니다.
- queries의 각 행은 4개의 정수 [x1, y1, x2, y2]입니다.
    - x1 행 y1 열부터 x2 행 y2 열까지 영역의 테두리를 시계방향으로 회전한다는 뜻입니다.
    - 1 ≤ x1 < x2 ≤ rows, 1 ≤ y1 < y2 ≤ columns입니다.
    - 모든 회전은 순서대로 이루어집니다.
    - 예를 들어, 두 번째 회전에 대한 답은 첫 번째 회전을 실행한 다음, 그 상태에서 두 번째 회전을 실행했을 때 이동한 숫자 중 최솟값을 구하면 됩니다.

---

##### 입출력 예시

| rows  | columns | queries                                     | result         |
| ----- | ------- | ------------------------------------------- | -------------- |
| `6`   | `6`     | `[[2,2,5,4],[3,3,6,6],[5,1,6,3]]`           | `[8, 10, 25]`  |
| `3`   | `3`     | `[[1,1,2,2],[1,2,2,3],[2,1,3,2],[2,2,3,3]]` | `[1, 1, 5, 3]` |
| `100` | `97`    | `[[1,1,100,97]]`                            | `[1]`          |

---

### 📌 풀이 방법 (1차 시도 -> 성공)

> **행렬 회전 방법**
>1. 좌 상단부터 시작하고, 시작하는 좌상단 값은 자신의 오른쪽으로 넘겨준다.
>2. 아래로 쭉 내려가면서 아래 값을 자신의 값에 지정한다.
>3. 직사각형의 맨 아래 행에 도달하면 열을 한 칸씩 이동하면서 다시 값을 교체한다.
>4. 맨 오른쪽 열에 도달하면 위로 올라가면서 앞의 과정을 반복한다.
>5. 맨 위 행에 도달하면 왼쪽 열로 이동하면서 다음 값을 자신에게 지정한다.
>
>회전할 때마다 최소값을 구해 result에 저장하고, 과정이 끝나면 반환한다.

### 🖥️ 풀이 코드
```
function solution(rows, columns, queries) {
    // 초기 행렬 생성
    let board = Array.from({length : rows}, () => Array())
    for(let row = 0; row < rows; row ++) {
        let n = row * columns
        for (let col = 1; col <= columns; col ++) {
            board[row].push(n + col)
        }    
    }
    
    //행렬 회전하는 함수
    const rotateBoard = (query) => {
        let originBoard = JSON.parse(JSON.stringify(board))
        let x1 = query[0] - 1
        let y1 = query[1] - 1
        let x2 = query[2] - 1
        let y2 = query[3] - 1
        let min = Infinity
        let time = 0
        
        // 좌변 계산
        for (let row = x1; row < x2; row ++) {
            // 좌하단 값 제외한 좌변 값 교체
            let nextValue = originBoard[row + 1][y1]
            board[row][y1] = nextValue
            if (nextValue < min) min = nextValue
        }
        
        // 우변 계산
        for (let row = x2; row > x1; row --) {
            let nextValue = originBoard[row -1][y2]
            board[row][y2] = nextValue
            if (nextValue < min) min = nextValue
        }
        // 윗변 계산
        for (let col = y2; col > y1; col --) {
            let nextValue = originBoard[x1][col - 1]
            board[x1][col] = nextValue
            if (nextValue < min) min = nextValue
        }
        // 밑변 계산
        for (let col = y1; col < y2; col ++) {
            let nextValue = originBoard[x2][col + 1]
            board[x2][col] = nextValue
            if (nextValue < min) min = nextValue
        }
        
        return min
    }
    
    const result = []
    queries.forEach(query => {
        result.push(rotateBoard(query))
    })
    
    return result
}
```

### 🔎 생각한 개선 방법 및 힌트
최대 2000ms로 연산속도가 너무 느리다. 원본 배열을 복사해와서 회전을 진행한게 원인인 것 같아 보인다. 이렇게 했던 이유는, 이미 교체한 값이 다른 값으로 들어가는 경우가 생겨서 인데, 교체 순서를 반 시계방향으로 진행하면 중복될 일이 없다.

**해결방안**
> 1. 굳이 원본 배열을 복사해와서 값을 변경할 필요 없이, 첫 시작 값을 따로 저장해두고 최소값에 할당한다. 회전을 왼쪽 -> 밑 -> 오른쪽 -> 위 로 **반 시계방향으로 진행**하고, 마치면 마지막 값에 첫 시작 값을 배정해준다.
> 2. query에서 x와 y를 가져오는 과정을 map을 통해 간략화.
> 3. 초기 행렬 생성하는 과정을 map을 통해 간략화.

// 수정된 코드
```
function solution(rows, columns, queries) {
    // 초기 행렬 생성
    const board = [...Array(rows)].map((_, r)=>[...Array(columns)].map((_, c)=> r * columns + c + 1));
    
    //행렬 회전하는 함수
    const rotateBoard = (query) => {
        let [x1, y1, x2, y2] = query.map(n => n - 1)
        let min = board[x1][y1]
        let startValue = board[x1][y1]
        
        // 좌변 계산
        for (let row = x1; row < x2; row ++) {
            board[row][y1] = board[row + 1][y1]
            min = Math.min(min, board[row][y1])
        }
        // 밑변 계산
        for (let col = y1; col < y2; col ++) {
            board[x2][col] = board[x2][col + 1]
            min = Math.min(min, board[x2][col])
        }
        // 우변 계산
        for (let row = x2; row > x1; row --) {
            board[row][y2] = board[row -1][y2]
            min = Math.min(min, board[row][y2])
        }
        // 윗변 계산
        for (let col = y2; col > y1; col --) {
            board[x1][col] = board[x1][col - 1]
            min = Math.min(min, board[x1][col])
        }
        board[x1][y1 + 1] = startValue
        
        return min
    }
    
    const result = []
    queries.forEach(query => {
        result.push(rotateBoard(query))
    })
    
    return result
}
```

최대 23ms로 이전보다 훨씬 개선되었다.

`풀이시간 : 1시간 20분`

## Lv. 2 [bfs] 무인도 여행
### 📖  문제
메리는 여름을 맞아 무인도로 여행을 가기 위해 지도를 보고 있습니다. 지도에는 바다와 무인도들에 대한 정보가 표시돼 있습니다. 지도는 1 x 1크기의 사각형들로 이루어진 직사각형 격자 형태이며, 격자의 각 칸에는 'X' 또는 1에서 9 사이의 자연수가 적혀있습니다. 지도의 'X'는 바다를 나타내며, 숫자는 무인도를 나타냅니다. 이때, 상, 하, 좌, 우로 연결되는 땅들은 하나의 무인도를 이룹니다. 지도의 각 칸에 적힌 숫자는 식량을 나타내는데, 상, 하, 좌, 우로 연결되는 칸에 적힌 숫자를 모두 합한 값은 해당 무인도에서 최대 며칠동안 머물 수 있는지를 나타냅니다. 어떤 섬으로 놀러 갈지 못 정한 메리는 우선 각 섬에서 최대 며칠씩 머물 수 있는지 알아본 후 놀러갈 섬을 결정하려 합니다.

지도를 나타내는 문자열 배열 `maps`가 매개변수로 주어질 때, 각 섬에서 최대 며칠씩 머무를 수 있는지 배열에 오름차순으로 담아 return 하는 solution 함수를 완성해주세요. 만약 지낼 수 있는 무인도가 없다면 -1을 배열에 담아 return 해주세요.

---

##### 제한사항

- 3 ≤ `maps`의 길이 ≤ 100
    - 3 ≤ `maps[i]`의 길이 ≤ 100
    - `maps[i]`는 'X' 또는 1 과 9 사이의 자연수로 이루어진 문자열입니다.
    - 지도는 직사각형 형태입니다.

---

##### 입출력 예

| maps                               | result     |
| ---------------------------------- | ---------- |
| ["X591X","X1X5X","X231X", "1XXX1"] | [1, 1, 27] |
| ["XXX","XXX","XXX"]                | [-1]       |


---

### 📌 풀이 방법 (1차 시도 -> 성공)

> 1. 땅의 넓이 측정하는 문제이니 bfs로 해결
> 2. 반복문을 통해 처음 땅이 나오면 bfs함수를 실행해서 해당 땅에서 상,하,좌,우로 이동하면서 인접 땅에 이동하면 해당 위치 방문처리하고 땅의 넓이 측정.
> 3. 상,하,좌,우로 이동하는 과정을 더 이상 이동하지 못할 때 까지 반복.

### 🖥️ 풀이 코드
```
function solution(maps) {
    // maps를 통해 방문처리를 진행하기 위해 배열로 split 처리
    maps = maps.map(el => el.split(""))
    const n = maps.length
    const m = maps[0].length
    
    // bfs 함수
    function bfs(x,y) {
        let queue = [[x,y]]
        let total = parseInt(maps[x][y])
        maps[x][y] = "X"
        
        const dx = [0,1,0,-1]
        const dy = [1,0,-1,0]
        
        // queue가 빌 때 까지 진행
        while (queue.length > 0) {
            let q = queue.shift()
            for (let i = 0; i < 4; i ++) {
                let nx = q[0] + dx[i]
                let ny = q[1] + dy[i]
                if (nx < n && ny < m && nx >= 0 && ny >= 0 &&
                    maps[nx][ny] !== "X") {
                    total += parseInt(maps[nx][ny])
                    maps[nx][ny] = "X"
                    queue.push([nx,ny])
                }
            }    
        }
        return total
    }
    // 땅이 나오면 해당 땅에서 bfs로 땅 크기 측정
    const result = []
    for(let x = 0; x < n; x ++) {
        for (let y = 0; y < m; y ++) {
            if (maps[x][y] !== "X") {
                result.push(bfs(x,y))
            }
        }
    }
    
    if (result.length === 0) return [-1]
    return result.sort((a,b) => a-b)
}
```

### 🔎 생각한 개선 방법 및 힌트

> 1.  마지막 결과 반환하는 부분을 result의 길이를 통해 삼항 연산자로 표현 가능하다
```
return result.length ? result.sort((a,b) => a - b) : [-1]
```

`풀이시간 : 30분`

## Lv. 2 [재귀] 괄호 변환
### 📖  문제
카카오에 신입 개발자로 입사한 **"콘"**은 선배 개발자로부터 개발역량 강화를 위해 다른 개발자가 작성한 소스 코드를 분석하여 문제점을 발견하고 수정하라는 업무 과제를 받았습니다. 소스를 컴파일하여 로그를 보니 대부분 소스 코드 내 작성된 괄호가 개수는 맞지만 짝이 맞지 않은 형태로 작성되어 오류가 나는 것을 알게 되었습니다.  
수정해야 할 소스 파일이 너무 많아서 고민하던 "콘"은 소스 코드에 작성된 모든 괄호를 뽑아서 올바른 순서대로 배치된 괄호 문자열을 알려주는 프로그램을 다음과 같이 개발하려고 합니다.

### 용어의 정의

**'('** 와 **')'** 로만 이루어진 문자열이 있을 경우, '(' 의 개수와 ')' 의 개수가 같다면 이를 **`균형잡힌 괄호 문자열`**이라고 부릅니다.  
그리고 여기에 '('와 ')'의 괄호의 짝도 모두 맞을 경우에는 이를 **`올바른 괄호 문자열`**이라고 부릅니다.  
예를 들어, `"(()))("`와 같은 문자열은 "균형잡힌 괄호 문자열" 이지만 "올바른 괄호 문자열"은 아닙니다.  
반면에 `"(())()"`와 같은 문자열은 "균형잡힌 괄호 문자열" 이면서 동시에 "올바른 괄호 문자열" 입니다.

'(' 와 ')' 로만 이루어진 문자열 w가 "균형잡힌 괄호 문자열" 이라면 다음과 같은 과정을 통해 "올바른 괄호 문자열"로 변환할 수 있습니다.

```
1. 입력이 빈 문자열인 경우, 빈 문자열을 반환합니다. 
2. 문자열 w를 두 "균형잡힌 괄호 문자열" u, v로 분리합니다. 단, u는 "균형잡힌 괄호 문자열"로 더 이상 분리할 수 없어야 하며, v는 빈 문자열이 될 수 있습니다. 
3. 문자열 u가 "올바른 괄호 문자열" 이라면 문자열 v에 대해 1단계부터 다시 수행합니다. 
  3-1. 수행한 결과 문자열을 u에 이어 붙인 후 반환합니다. 
4. 문자열 u가 "올바른 괄호 문자열"이 아니라면 아래 과정을 수행합니다. 
  4-1. 빈 문자열에 첫 번째 문자로 '('를 붙입니다. 
  4-2. 문자열 v에 대해 1단계부터 재귀적으로 수행한 결과 문자열을 이어 붙입니다. 
  4-3. ')'를 다시 붙입니다. 
  4-4. u의 첫 번째와 마지막 문자를 제거하고, 나머지 문자열의 괄호 방향을 뒤집어서 뒤에 붙입니다. 
  4-5. 생성된 문자열을 반환합니다.
```

**"균형잡힌 괄호 문자열"** p가 매개변수로 주어질 때, 주어진 알고리즘을 수행해 **"올바른 괄호 문자열"**로 변환한 결과를 return 하도록 solution 함수를 완성해 주세요.

### 매개변수 설명

- p는 '(' 와 ')' 로만 이루어진 문자열이며 길이는 2 이상 1,000 이하인 짝수입니다.
- 문자열 p를 이루는 '(' 와 ')' 의 개수는 항상 같습니다.
- 만약 p가 이미 "올바른 괄호 문자열"이라면 그대로 return 하면 됩니다.

---

### 입출력 예

| p            | result       |
| ------------ | ------------ |
| `"(()())()"` | `"(()())()"` |
| `")("`       | `"()"`       |
| `"()))((()"` | `"()(())()"` |


---
### 📌 풀이 방법 (1차 시도 -> 구현 실패)

> 1. 예시에 나와있는 과정을 직접 구현하려니, 재귀하는 과정과 반환하는 요소들이 헷갈려서 이해하면서 코드를 짤 수 없었다.


### 📌 풀이 방법 (2차 시도 -> 성공)

> 1. 문제에 나와있는 예시대로 코드를 그대로 작성했다.

### 🖥️ 풀이 코드
```
function solution(p) {
    return problemSolve(p)
}

// 올바른 괄호 판별 함수
function isCorrect(w) {
    let count = 0
    for (let i = 0; i < w.length; i ++) {
        w[i] === '(' ? count -- : count ++
        if (count >= 1) return false
    }
    return true
}

// 메인 로직
function problemSolve(w) {
    // 1. 입력이 빈 문자열인 경우, 빈 문자열을 반환합니다.
    if (w.length === 0) {
        return ""
    }
    // 2. 문자열 w를 두 "균형잡힌 괄호 문자열" u, v로 분리합니다.
    //단, u는 "균형잡힌 괄호 문자열"로 더 이상 분리할 수 없어야 하며, v는 빈 문자열이 될 수 있습니다. 
    let u = ""
    let v = ""
    let count = 0
    for (let i = 0; i < w.length; i ++) {
        u += w[i]
        w[i] === '(' ? count -- : count ++
        if (count === 0) {
            v = w.slice(i + 1)
            break
        }
    }
    
    // 3. 문자열 u가 "올바른 괄호 문자열" 이라면 문자열 v에 대해 1단계부터 다시 수행합니다. 
    // 3-1. 수행한 결과 문자열을 u에 이어 붙인 후 반환합니다.
    if (isCorrect(u)) {
        return u + problemSolve(v)
    }
    
    // 4. 문자열 u가 "올바른 괄호 문자열"이 아니라면 아래 과정을 수행합니다.
    // 4-1. 빈 문자열에 첫 번째 문자로 '('를 붙입니다. 
    // 4-2. 문자열 v에 대해 1단계부터 재귀적으로 수행한 결과 문자열을 이어 붙입니다. 
    // 4-3. ')'를 다시 붙입니다
    // 4-5. 생성된 문자열을 반환합니다.
    return '(' + problemSolve(v) + ')' + transformU(u)
}

// 4-4. u의 첫 번째와 마지막 문자를 제거하고, 나머지 문자열의 괄호 방향을 뒤집어서 뒤에 붙입니다.
function transformU (u) {
    u = u.split("").slice(1)
    u.pop()
    
    if (u.length === 0) return ''
    for (let i = 0 ; i < u.length; i ++) {
        u[i] = u[i] === '(' ? ')' : '('
    }
    return u.join("")
}
```

### 🔎 생각한 개선 방법 및 힌트

>1. 해당 문제는 주어진 지시를 코드로 옮길 수 있는지 판별하는 문제이다. 
>2.  재귀함수는 안에서 일어나는 일을 이해하면서 짜려하기 보다, 코드가 돌아가는 전체적인 프로세스를 알고 짜야 한다.
>3. 재귀함수에 겁먹지 말자.

`풀이시간 : 1시간 20분`

## Lv. 2 [bfs] 미로 탈출
### 📖  문제
1 x 1 크기의 칸들로 이루어진 직사각형 격자 형태의 미로에서 탈출하려고 합니다. 각 칸은 통로 또는 벽으로 구성되어 있으며, 벽으로 된 칸은 지나갈 수 없고 통로로 된 칸으로만 이동할 수 있습니다. 통로들 중 한 칸에는 미로를 빠져나가는 문이 있는데, 이 문은 레버를 당겨서만 열 수 있습니다. 레버 또한 통로들 중 한 칸에 있습니다. 따라서, 출발 지점에서 먼저 레버가 있는 칸으로 이동하여 레버를 당긴 후 미로를 빠져나가는 문이 있는 칸으로 이동하면 됩니다. 이때 아직 레버를 당기지 않았더라도 출구가 있는 칸을 지나갈 수 있습니다. 미로에서 한 칸을 이동하는데 1초가 걸린다고 할 때, 최대한 빠르게 미로를 빠져나가는데 걸리는 시간을 구하려 합니다.

미로를 나타낸 문자열 배열 `maps`가 매개변수로 주어질 때, 미로를 탈출하는데 필요한 최소 시간을 return 하는 solution 함수를 완성해주세요. 만약, 탈출할 수 없다면 -1을 return 해주세요.

---

##### 제한사항

- 5 ≤ `maps`의 길이 ≤ 100
    - 5 ≤ `maps[i]`의 길이 ≤ 100
    - `maps[i]`는 다음 5개의 문자들로만 이루어져 있습니다.
        - S : 시작 지점
        - E : 출구
        - L : 레버
        - O : 통로
        - X : 벽
    - 시작 지점과 출구, 레버는 항상 다른 곳에 존재하며 한 개씩만 존재합니다.
    - 출구는 레버가 당겨지지 않아도 지나갈 수 있으며, 모든 통로, 출구, 레버, 시작점은 여러 번 지나갈 수 있습니다.

---

##### 입출력 예

| maps                                      | result |
| ----------------------------------------- | ------ |
| ["SOOOL","XXXXO","OOOOO","OXXXX","OOOOE"] | 16     |
| ["LOOXS","OOOOX","OOOOO","OOOOO","EOOOO"] | -1     |


---

### 📌 풀이 방법 (1차 시도 -> 성공)

> 1. 방문 여부 변수를 만들어준다.
>2. bfs를 통해서 레버까지의 최단 경로를 찾고, 소요 시간, 좌표를 저장한다.
>3. 레버부터 출구까지 최단 경로를 찾고, 레버까지의 소요 시간을 더해준다.

### 🖥️ 풀이 코드
```
function solution(maps) {
    const bfs = (x, y, goal) => {
        // 방문 여부 판별
        const visited = Array.from({length : maps.length}, () => Array(maps[0].length).fill(false))
        // 이동 방향 정의
        const dx = [0, 1, 0, -1]
        const dy = [1, 0, -1, 0]
        // 시작 지점 방문 처리
        visited[x][y] = true
        // 시작지점 queue에 삽입 
        let queue = [[x, y, 0]]
        // 다음 이동할 곳이 없을 때 까지 이동
        while (queue.length > 0) {
            let [cx, cy, distance] = queue.shift()
            // 방향 별로 이동
            for (let i = 0; i < 4; i ++) {
                let nx = cx + dx[i] // 다음 x 좌표
                let ny = cy + dy[i] // 다음 y 좌표
                // 이동 가능여부 판별
                if (nx >= 0 && ny >= 0 && nx < maps.length && ny < maps[0].length &&
                    maps[nx][ny] !== "X" && !visited[nx][ny]) {
                    // 목표지점 도달 시 좌표, 거리 반환
                    if (maps[nx][ny] === goal) return [nx, ny, distance + 1]
                    
                    visited[nx][ny] = true
                    queue.push([nx, ny, distance + 1])
                }
            }
        }
        // 목표 도달하지 못했을 경우 false 반환
        return [false, false, false]
    }
    // 시작 좌표 찾
    let startX, startY
    for (let i = 0; i < maps.length; i ++) {
        for (let j = 0; j < maps[0].length; j ++) {
            if (maps[i][j] === "S") {
                startX = i
                startY = j
            }
        }
    }
    
    const [x, y, distance] = bfs(startX, startY, "L")
    if (x === false) return -1
    const [x2, y2, distance2] = bfs(x, y, "E")
    if (x2 === false) return -1
    
    return distance + distance2
}
```

### 🔎 생각한 개선 방법 및 힌트

> 1. bfs함수에서 queue를 `shift()`하는 대신 `for of...`문으로 루프를 진행 시 유의미한 성능 개선을 기대할 수 있다.
```
// 이전 코드
while (queue.length > 0) {
	let [cx, cy, distance] = queue.shift()
}
// 개선 코드
for (let [cx, cy, distance] of queue)
```

> 2. 목표에 도달하지 못할 시 false보다 null을 반환하는게 더 명확하다.
> 3. 시작 좌표를 반환하는 것 보다, 시작 좌표를 따로 찾고 함수에서 인자로 `(시작 좌표,목표 좌표)`만 전달하는 것이 더욱 직관적이다.

```
// 이전 실행 로직
const [x, y, distance] = bfs(startX, startY, "L")
if (x === false) return -1
const [x2, y2, distance2] = bfs(x, y, "E")
if (x2 === false) return -1

// 개선된 실행 로직
const lever = bfs(findPosition("S"), "L")
if (lever === null) return -1
const exit = bfs(findPosition("L"), "E")
if (exit === null) return -1
```

`풀이 시간 : 1시간`

## Lv. 2 수식 최대
### 📖  문제
IT 벤처 회사를 운영하고 있는 `라이언`은 매년 사내 해커톤 대회를 개최하여 우승자에게 상금을 지급하고 있습니다.  
이번 대회에서는 우승자에게 지급되는 상금을 이전 대회와는 다르게 다음과 같은 방식으로 결정하려고 합니다.  
해커톤 대회에 참가하는 모든 참가자들에게는 숫자들과 3가지의 연산문자(`+, -, *`) 만으로 이루어진 연산 수식이 전달되며, 참가자의 미션은 전달받은 수식에 포함된 연산자의 우선순위를 자유롭게 재정의하여 만들 수 있는 가장 큰 숫자를 제출하는 것입니다.  
단, 연산자의 우선순위를 새로 정의할 때, 같은 순위의 연산자는 없어야 합니다. 즉, `+` > `-` > `*` 또는 `-` > `*` > `+` 등과 같이 연산자 우선순위를 정의할 수 있으나 `+,*` > `-` 또는 `*` > `+,-`처럼 2개 이상의 연산자가 동일한 순위를 가지도록 연산자 우선순위를 정의할 수는 없습니다. 수식에 포함된 연산자가 2개라면 정의할 수 있는 연산자 우선순위 조합은 2! = 2가지이며, 연산자가 3개라면 3! = 6가지 조합이 가능합니다.  
만약 계산된 결과가 음수라면 해당 숫자의 절댓값으로 변환하여 제출하며 제출한 숫자가 가장 큰 참가자를 우승자로 선정하며, 우승자가 제출한 숫자를 우승상금으로 지급하게 됩니다.

예를 들어, 참가자 중 `네오`가 아래와 같은 수식을 전달받았다고 가정합니다.

`"100-200*300-500+20"`

일반적으로 수학 및 전산학에서 약속된 연산자 우선순위에 따르면 더하기와 빼기는 서로 동등하며 곱하기는 더하기, 빼기에 비해 우선순위가 높아 `*` > `+,-` 로 우선순위가 정의되어 있습니다.  
대회 규칙에 따라 `+` > `-` > `*` 또는 `-` > `*` > `+` 등과 같이 연산자 우선순위를 정의할 수 있으나 `+,*` > `-` 또는 `*` > `+,-` 처럼 2개 이상의 연산자가 동일한 순위를 가지도록 연산자 우선순위를 정의할 수는 없습니다.  
수식에 연산자가 3개 주어졌으므로 가능한 연산자 우선순위 조합은 3! = 6가지이며, 그 중 `+` > `-` > `*` 로 연산자 우선순위를 정한다면 결괏값은 22,000원이 됩니다.  
반면에 `*` > `+` > `-` 로 연산자 우선순위를 정한다면 수식의 결괏값은 -60,420 이지만, 규칙에 따라 우승 시 상금은 절댓값인 60,420원이 됩니다.

참가자에게 주어진 연산 수식이 담긴 문자열 expression이 매개변수로 주어질 때, 우승 시 받을 수 있는 가장 큰 상금 금액을 return 하도록 solution 함수를 완성해주세요.

##### **[제한사항]**

- expression은 길이가 3 이상 100 이하인 문자열입니다.
- expression은 공백문자, 괄호문자 없이 오로지 숫자와 3가지의 연산자(`+, -, *`) 만으로 이루어진 올바른 중위표기법(연산의 두 대상 사이에 연산기호를 사용하는 방식)으로 표현된 연산식입니다. 잘못된 연산식은 입력으로 주어지지 않습니다.
    - 즉, `"402+-561*"`처럼 잘못된 수식은 올바른 중위표기법이 아니므로 주어지지 않습니다.  
        
- expression의 피연산자(operand)는 0 이상 999 이하의 숫자입니다.
    - 즉, `"100-2145*458+12"`처럼 999를 초과하는 피연산자가 포함된 수식은 입력으로 주어지지 않습니다.
    - `"-56+100"`처럼 피연산자가 음수인 수식도 입력으로 주어지지 않습니다.
- expression은 적어도 1개 이상의 연산자를 포함하고 있습니다.
- 연산자 우선순위를 어떻게 적용하더라도, expression의 중간 계산값과 최종 결괏값은 절댓값이 263 - 1 이하가 되도록 입력이 주어집니다.
- 같은 연산자끼리는 앞에 있는 것의 우선순위가 더 높습니다.

---

##### **입출력 예**

| expression             | result |
| ---------------------- | ------ |
| `"100-200*300-500+20"` | 60420  |
| `"50*6-3*2"`           | 300    |


---

### 📌 풀이 방법 (1차 시도 -> 실패)

>모든 경우의 수 시도
>1. 연산자를 기준으로 문자열을 배열로 나눈다.
>2. 연산자의 index에 따라, 계산 여부를 확인한다.

계산할 순서인 경우
>1. 다음 연산자 계산 O : 객체에서 다음 연산자 계산 결과를 통해 값을 객체에 저장한다.
>2. 다음 연산자 계산 X : 이전 index 값과 다음 index값을 계산해서 객체에 {index : 값}으로 저장.

### 🖥️ 풀이 코드
```
function solution(expression) {
    let stack = []
    let expressionArr = []
    expression = expression.split("")
    for (let i = 0; i < expression.length; i ++) {
        let cur = expression[i]
        if (cur !== "*" && cur !== "+" && cur !== "-") {
            stack.push(cur)
            continue
        }
        expressionArr.push(parseInt(stack.join("")))
        expressionArr.push(cur)
        stack = []
    }
    // 마지막 값 추가 
    expressionArr.push(parseInt(stack.join("")))
    let values = {}
    let results = []
    
    const multiply = (a, b) => {
        return a * b
    }
    const plus = (a, b) => {
        return a + b
    }
    
    const minus = (a,b) => {
        return a - b
    }
    
    const firstCal = (operator, cal) => {
        let lastIdx = 0
        for (let i = 1; i < expressionArr.length; i += 2) {
            if (expressionArr[i] === operator) {
                values[i] = cal(expressionArr[i-1], expressionArr[i+1])
            }
            lastIdx = i
        }
        return values[lastIdx]
    }
    
    const calculator = (operator, cal) => {
        let lastIdx = 0
        for (let i = 1; i < expressionArr.length; i += 2) {
            if (expressionArr[i] === operator) {
                if ((i + 2) in values) {
                    let value = cal(expressionArr[i-1], values[i + 2])
                    values[i] = value
                    values[i+2] = value
                }
                else if ((i - 2) in values) {
                    let value = cal(values[i-2], expressionArr[i + 1])
                    values[i] = value
                    value[i-2] = value
                }
                else {
                    values[i] = cal(expressionArr[i-1], expressionArr[i+1])
                }
                lastIdx = i
            }
        }
        return lastIdx ? values[lastIdx] : null
    }
    
    let operators = [["*", multiply], ["+", plus], ["-", minus]]
    
    for (let i = 0; i < 3; i ++) {
        let operator1 = operators[i][0]
        let cal1 = operators[i][1]
        let calResult = 0
        
        let j = (i + 1) % 3
        let operator2 = operators[j][0]
        let cal2 = operators[j][1]
        let operator3 = operators[(j + 1) % 3][0]
        let cal3 = operators[(j + 1) % 3][1]
        let result1 = firstCal(operator1, cal1)
        let result2 = calculator(operator2, cal2)
        let result3 = calculator(operator3, cal3)
        
        calResult = result3 === null ? (result2 === null ? result1 : result2) : result3
        results.push(calResult)
        values = {}
        
        let temp = [operator2, cal2]
        operator2 = operator3
        cal2 = cal3
        operator3 = temp[0]
        cal3 = temp[1]
        
        result1 = firstCal(operator1, cal1)
        result2 = calculator(operator2, cal2)
        result3 = calculator(operator3, cal3)
        
        calResult = result3 === null ? (result2 === null ? result1 : result2) : result3
        results.push(calResult)
        values = {}
    }
    
    results.map((num) => Math.abs(num))
    return Math.max([...results])
}
```

---

### 🔎🔎 생각한 개선 방법 및 힌트

> 1. 돌아가지도 않는 쓰레기 완성.
> 2. 코드가 너무 복잡하고 많으며, 계산하는 로직이 잘못되었다. 이전에 계산한 값을 제대로 반영하여 이어서 계산하지 못한다.
> 3. 시작부터 구현에만 집중하다 보니 너무 복잡해짐. 필요한 부분만 최대한 깔끔하게 짜보자.

### 📌📌 풀이 방법 (2차 시도 -> 성공)

> 1. 정규 표현식으로 숫자와 연산자 분리.
> 2. calculating함수에서 while 반복문으로 계산.
> 3. 경우의 수 별로 한 번씩 총 6번 계산

### 🖥️🖥️ 풀이 코드
```
function solution(expression) {
    let nums = expression.split(/[\+\-\*]/).map(Number); // 숫자들만 분리
    let operators = expression.match(/[\+\-\*]/g); // 연산자들만 분리
    
    const calculator = (a, b, operator) => {
        if (operator === "*") return a * b;
        if (operator === "+") return a + b;
        if (operator === "-") return a - b;
    }

    const calculating = (n, o, priority) => {
        let nums = n.slice();
        let operators = o.slice();
        for (let operator of priority) {
            while (operators.includes(operator)) {
                const index = operators.indexOf(operator);
                nums[index] = calculator(nums[index], nums[index + 1], operator);
                nums.splice(index + 1, 1);
                operators.splice(index, 1);
            }
        }
        return Math.abs(nums[0]);
    }

    const orders = [
        ["*", "+", "-"], ["*", "-", "+"], 
        ["+", "*", "-"], ["+", "-", "*"], 
        ["-", "*", "+"], ["-", "+", "*"]
    ];
    
    let maxResult = 0;
    for (let order of orders) {
        const result = calculating(nums, operators, order);
        maxResult = Math.max(maxResult, result);
    }

    return maxResult;
}
```

---

### 🔎🔎 생각한 개선 방법 및 힌트

> 1. 


카카오에서 나오는 문제 처럼 구현이 까다롭고 설정해야 할 조건들이 많아질 경우, 정리가 안되고 코드가 점점 지저분해지며 구현에 실패하는 경우가 많아진다. 그 이유는, 먼저 계획을 세우고 계획대로 하는 것이 아니라 일단 코드를 작성 하면서 조건에 맞춰 코드를 짜다 보니 코드를 짜면서 계속 바뀌고 명확한 계획에 따라 짜지 못해 테스트 케이스도 확인 못하고 복잡해진다.
**계획을 정말 세세하게 코드로 테스트해보면서 짜고, 그대로 깔끔하게 코드로 작성하자.**

## Lv. 2 줄 서는 방법[복습 완료]
### 📖  문제
n명의 사람이 일렬로 줄을 서고 있습니다. n명의 사람들에게는 각각 1번부터 n번까지 번호가 매겨져 있습니다. n명이 사람을 줄을 서는 방법은 여러가지 방법이 있습니다. 예를 들어서 3명의 사람이 있다면 다음과 같이 6개의 방법이 있습니다.

- [1, 2, 3]
- [1, 3, 2]
- [2, 1, 3]
- [2, 3, 1]
- [3, 1, 2]
- [3, 2, 1]

사람의 수 n과, 자연수 k가 주어질 때, 사람을 나열 하는 방법을 사전 순으로 나열 했을 때, k번째 방법을 return하는 solution 함수를 완성해주세요.

###### 제한사항

- n은 20이하의 자연수 입니다.
- k는 n! 이하의 자연수 입니다.

---

##### 입출력 예

| n   | k   | result  |
| --- | --- | ------- |
| 3   | 5   | [3,1,2] |


---

### 📌 풀이 방법 (1차 시도 -> 실패)

> 1. visited로 방문처리 하면서 for문으로 n만큼 반복.

### 🖥️ 풀이 코드
```
function solution(n, k) {
    const visited = new Array(n + 1).fill(false)
    let answer = 0
    let index = 1
    const makeComb = (n, arr, len) => {
        if (index > k) return
        
        if (len === n) {
            if (index === k) answer = arr
            index ++
            return
        }
        
        for (let i = 1; i <= n; i ++) {
            if (!visited[i]) {
                visited[i] = true
                makeComb(n, arr + String(i) + '.', len + 1)    
                visited[i] = false
            }
        }
    }
    makeComb(n, "", 0)
    answer = answer.split(".").map(el => parseInt(el))
    answer.pop()
    return answer
}
```

---

### 🔎 생각한 개선 방법 및 힌트

> 1. 경우의 수는 피보나치 n이 아니라 팩토리얼 n이므로 최대 2432902008176640000이므므로 모든 조합을 구하는 건 당연히도 시간초과 발생.
> 2. 팩토리얼과 k를 통해 자리수를 유추하여 해당 수 구하기.

---

### 📌📌 풀이 방법 (2차 시도 -> 성공)

> 1. n 번째 자리수는 k-1 / factorial(n-1)
> 2. 1부터 n까지 있는 배열에서 자리수에 해당하는 index의 값을 splice로 빼와서 결과에 추가해준다.
> 3. 자리수 하나를 구해준 다음에는 k = k * factorial(n-1)를 대입해줌.

### 🖥️🖥️ 풀이 코드
```
function solution(n, k) {
    let factorial = [1,1,2,6,24]
    function makeFactorial(n) {
        if (factorial[n]) return factorial[n]
        factorial[n] = makeFactorial(n-1) * n
        return factorial[n]
    }
    makeFactorial(n)
    let result = []
    let nums = []
    for(let i = 1; i <= n; i ++) {
        nums.push(i)
    }
    
    while (n > 0) {
        let index = Math.floor((k-1) / factorial[n-1])
        if (index === n) index --
        result.push(nums.splice(index,1)[0])
        k = k % factorial[n-1]
        n --
    }
    
    return result
}
```

---

`풀이시간 : 30분`

## Lv. 2 거리두기 확인하기
### 📖  문제
개발자를 희망하는 죠르디가 카카오에 면접을 보러 왔습니다.  
  
코로나 바이러스 감염 예방을 위해 응시자들은 거리를 둬서 대기를 해야하는데 개발 직군 면접인 만큼  
아래와 같은 규칙으로 대기실에 거리를 두고 앉도록 안내하고 있습니다.

> 1. 대기실은 5개이며, 각 대기실은 5x5 크기입니다.
> 2. 거리두기를 위하여 응시자들 끼리는 맨해튼 거리[1](https://school.programmers.co.kr/learn/courses/30/lessons/81302#fn1)가 2 이하로 앉지 말아 주세요.
> 3. 단 응시자가 앉아있는 자리 사이가 파티션으로 막혀 있을 경우에는 허용합니다.

예를 들어,

|![PXP.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/8c056cac-ec8f-435c-a49a-8125df055c5e/PXP.png)|![PX_XP.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/d611f66e-f9c4-4433-91ce-02887657fe7f/PX_XP.png)|![PX_OP.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/ed707158-0511-457b-9e1a-7dbf34a776a5/PX_OP.png)|
|---|---|---|
|위 그림처럼 자리 사이에 파티션이 존재한다면 맨해튼 거리가 2여도 거리두기를 **지킨 것입니다.**|위 그림처럼 파티션을 사이에 두고 앉은 경우도 거리두기를 **지킨 것입니다.**|위 그림처럼 자리 사이가 맨해튼 거리 2이고 사이에 빈 테이블이 있는 경우는 거리두기를 **지키지 않은 것입니다.**|
|![P.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/4c548421-1c32-4947-af9e-a45c61501bc4/P.png)|![O.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/ce799a38-668a-4038-b32f-c515b8701262/O.png)|![X.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/91e8f98b-baeb-4f81-8cb6-5bafebebdcc7/X.png)|
|응시자가 앉아있는 자리(`P`)를 의미합니다.|빈 테이블(`O`)을 의미합니다.|파티션(`X`)을 의미합니다.|

5개의 대기실을 본 죠르디는 각 대기실에서 응시자들이 거리두기를 잘 기키고 있는지 알고 싶어졌습니다. 자리에 앉아있는 응시자들의 정보와 대기실 구조를 대기실별로 담은 2차원 문자열 배열 `places`가 매개변수로 주어집니다. 각 대기실별로 거리두기를 지키고 있으면 1을, 한 명이라도 지키지 않고 있으면 0을 배열에 담아 return 하도록 solution 함수를 완성해 주세요.

---

##### 제한사항

- `places`의 행 길이(대기실 개수) = 5
    - `places`의 각 행은 하나의 대기실 구조를 나타냅니다.
- `places`의 열 길이(대기실 세로 길이) = 5
- `places`의 원소는 `P`,`O`,`X`로 이루어진 문자열입니다.
    - `places` 원소의 길이(대기실 가로 길이) = 5
    - `P`는 응시자가 앉아있는 자리를 의미합니다.
    - `O`는 빈 테이블을 의미합니다.
    - `X`는 파티션을 의미합니다.
- 입력으로 주어지는 5개 대기실의 크기는 모두 5x5 입니다.
- return 값 형식
    - 1차원 정수 배열에 5개의 원소를 담아서 return 합니다.
    - `places`에 담겨 있는 5개 대기실의 순서대로, 거리두기 준수 여부를 차례대로 배열에 담습니다.
    - 각 대기실 별로 모든 응시자가 거리두기를 지키고 있으면 1을, 한 명이라도 지키지 않고 있으면 0을 담습니다.

---

##### 입출력 예

| places                                                                                                                                                                                                                                        | result |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| `[["POOOP", "OXXOX", "OPXPX", "OOXOX", "POXXP"], ["POOPX", "OXPXP", "PXXXO", "OXXXO", "OOOPP"], ["PXOPX", "OXOXP", "OXPOX", "OXXOP", "PXPOX"], ["OOOXX", "XOOOX", "OOOXX", "OXOOX", "OOOOO"], ["PXPXP", "XPXPX", "PXPXP", "XPXPX", "PXPXP"]]` |        |

---

### 📌 풀이 방법 (1차 시도 -> 성공)

>1. 대기실을 순회하며 P를 찾는다.
>2. P가 나오면, 상하좌우 대각선을 조건에 맞춰 확인한다.
>3. 해당 과정을 5개의 대기실에 모두 적용하여 result에 추가한다.

### 🖥️ 풀이 코드
```
function solution(places) {
    const result = []
    for(let i = 0; i < 5; i ++) {
        result.push(checkPlace(places[i]))
    }
    return result
}

function checkPlace(place) {
        // 1. 대기실을 순회하며 P를 찾는다.
        for (let row = 0; row < 5; row ++) {
            for (let col = 0; col < 5; col ++) {
                // 2. P가 나오면, 상하좌우 대각선 확인
                if (place[row][col] === "P")  {
                    // 상
                    if (row - 1 >= 0 && place[row-1][col] === "P") return 0
                    if (row - 2 >= 0 && place[row-2][col] === "P" && place[row-1][col] === "O") return 0
                    // 하
                    if (row + 1 < 5 && place[row+1][col] === "P") return 0
                    if (row + 2 < 5 && place[row+2][col] === "P" && place[row+1][col] === "O") return 0
                    // 좌
                    if (col - 1 >= 0 && place[row][col-1] === "P") return 0
                    if (col - 2 >= 0 && place[row][col-2] === "P" && place[row][col-1] !== "X") return 0
                    // 우
                    if (col + 1 < 5 && place[row][col+1] === "P") return 0
                    if (col + 2 < 5 && place[row][col+2] === "P" && place[row][col+1] !== "X") return 0
                    // 왼쪽 위
                    if (row - 1 >= 0 && col - 1 >= 0 && place[row-1][col-1] === 'P') {
                        if (place[row-1][col] === 'O' || place[row][col-1] === 'O') return 0
                    }
                    // 오른쪽 위
                    if (row - 1 >= 0 && col + 1 < 5 && place[row-1][col+1] === 'P') {
                        if (place[row-1][col] === 'O' || place[row][col+1] === 'O') return 0
                    }
                    // 왼쪽 아래
                    if (row + 1 < 5 && col - 1 >= 0 && place[row+1][col-1] === 'P') {
                        if (place[row+1][col] === 'O' || place[row][col-1] === 'O') return 0
                    }
                    // 오른쪽 아래
                    if (row + 1 < 5 && col + 1 < 5 && place[row+1][col+1] === 'P') {
                        if (place[row+1][col] === 'O' || place[row][col+1] === 'O') return 0
                    }
                }
            }
        }
        return 1
    }
```

---

### 🔎 생각한 개선 방법 및 힌트

> 직접 하드코딩하여 풀었지만, dfs를 통해서 같은 로직으로 풀이 가능.

`풀이 시간 : 45분`

---

## Lv. 2 [bfs] 리코쳇 로봇
### 📖  문제
리코쳇 로봇이라는 보드게임이 있습니다.

이 보드게임은 격자모양 게임판 위에서 말을 움직이는 게임으로, 시작 위치에서 목표 위치까지 최소 몇 번만에 도달할 수 있는지 말하는 게임입니다.

이 게임에서 말의 움직임은 상, 하, 좌, 우 4방향 중 하나를 선택해서 게임판 위의 장애물이나 맨 끝에 부딪힐 때까지 미끄러져 이동하는 것을 한 번의 이동으로 칩니다.

다음은 보드게임판을 나타낸 예시입니다.

```
...D..R
.D.G...
....D.D
D....D.
..D....
```

여기서 "."은 빈 공간을, "R"은 로봇의 처음 위치를, "D"는 장애물의 위치를, "G"는 목표지점을 나타냅니다.  
위 예시에서는 "R" 위치에서 아래, 왼쪽, 위, 왼쪽, 아래, 오른쪽, 위 순서로 움직이면 7번 만에 "G" 위치에 멈춰 설 수 있으며, 이것이 최소 움직임 중 하나입니다.

게임판의 상태를 나타내는 문자열 배열 `board`가 주어졌을 때, 말이 목표위치에 도달하는데 최소 몇 번 이동해야 하는지 return 하는 solution함수를 완성하세요. 만약 목표위치에 도달할 수 없다면 -1을 return 해주세요.

---

##### 제한 사항

- 3 ≤ `board`의 길이 ≤ 100
    - 3 ≤ `board`의 원소의 길이 ≤ 100
    - `board`의 원소의 길이는 모두 동일합니다.
    - 문자열은 ".", "D", "R", "G"로만 구성되어 있으며 각각 빈 공간, 장애물, 로봇의 처음 위치, 목표 지점을 나타냅니다.
    - "R"과 "G"는 한 번씩 등장합니다.

---

##### 입출력 예

|board|result|
|---|---|
|["...D..R", ".D.G...", "....D.D", "D....D.", "..D...."]|7|
|[".D.R", "....", ".G..", "...D"]|-1|

---

### 📌 풀이 방법 (1차 시도 -> 성공)

>  BFS로 구현
>1. 방문처리할 배열 생성
>2. BFS 함수 구현
>	2.1 R의 위치로 시작지점 설정.
>	2.2 queue가 빌 때 까지 이동
>	2.3 상하좌우 4가지 방향을 각각 이동하여, 벽 또는 D에 부딪힐 때 까지 이동.
>	2.4 해당 위치의 방문 여부를 판별하여 queue에 삽입.
>	2.5 목표 위치에 도달하면, 횟수 반환.

### 🖥️ 풀이 코드
```
function solution(board) {
    const visited = Array.from({length : board.length}, () => Array(board[0].length).fill(false))
    let startPoint = []
    let endPoint = []
    for (let i = 0; i < board.length; i ++) {
        for (let j = 0; j < board[0].length; j ++) {
            if (board[i][j] === "R") {
                startPoint.push(i)
                startPoint.push(j)
                startPoint.push(0)
                if (endPoint.length > 0) break
            }
            if (board[i][j] === "G") {
                endPoint.push(i)
                endPoint.push(j)
                if (startPoint.length > 0) break
                
            }
        }
    }
    
    function bfs(board) {
        let queue = []
        visited[startPoint[0]][startPoint[1]] = true
        queue.push(startPoint)
        const directions = [[0,1], [1,0], [0,-1], [-1,0]]
        
        for (let [cx, cy, distance] of queue) {
            for (let direction of directions) {
                let [nx, ny] = [cx, cy]
                let [dx,dy] = direction
                // 끝까지 이동
                while (true) {
                    nx += dx
                    ny += dy
                    if (nx < 0 || ny < 0 || nx >= board.length ||
                        ny >= board[0].length || board[nx][ny] === "D") {
                        nx -= dx
                        ny -= dy
                        break
                    }
                }
                if (nx === endPoint[0] && ny === endPoint[1]) {
                    return distance + 1
                }
                
                if (!visited[nx][ny]) {
                    visited[nx][ny] = true
                    queue.push([nx, ny, distance + 1])
                }
            }
        }
        return -1
    }
    
    return bfs(board)
}
```

---

### 🔎 생각한 개선 방법 및 힌트

> 1. 좌표를 이동하는 과정에서 `nx = cx`로 nx를 새로 할당하지 않고 `cx += dx`로 진행했더니, 다른 방향으로의 이동에서도 cx의 값이 넘어와 오류가 발생했다.

`풀이 시간 : 1시간`

--- 

## Lv. 2 [DP] 가장 큰 정사각형 찾기
### 📖  문제
1와 0로 채워진 표(board)가 있습니다. 표 1칸은 1 x 1 의 정사각형으로 이루어져 있습니다. 표에서 1로 이루어진 가장 큰 정사각형을 찾아 넓이를 return 하는 solution 함수를 완성해 주세요. (단, 정사각형이란 축에 평행한 정사각형을 말합니다.)

예를 들어

|1|2|3|4|
|---|---|---|---|
|0|1|1|1|
|1|1|1|1|
|1|1|1|1|
|0|0|1|0|

가 있다면 가장 큰 정사각형은

|1|2|3|4|
|---|---|---|---|
|0|`1`|`1`|`1`|
|1|`1`|`1`|`1`|
|1|`1`|`1`|`1`|
|0|0|1|0|

가 되며 넓이는 9가 되므로 9를 반환해 주면 됩니다.

##### 제한사항

- 표(board)는 2차원 배열로 주어집니다.
- 표(board)의 행(row)의 크기 : 1,000 이하의 자연수
- 표(board)의 열(column)의 크기 : 1,000 이하의 자연수
- 표(board)의 값은 1또는 0으로만 이루어져 있습니다.

---

##### 입출력 예

|board|answer|
|---|---|
|[[0,1,1,1],[1,1,1,1],[1,1,1,1],[0,0,1,0]]|9|
|[[0,0,1,1],[1,1,1,1]]|4|


---
### 📌 풀이 방법 (1차 시도 -> 실패)

> BFS를 활용하여 풀다가 정사각형 판별 로직을 구현하지 못해서 실패.

---

### 📌 풀이 방법 (2차 시도 -> 성공)

> 1. board를 순회하면서 각 칸마다 오른쪽,아래,오른쪽 아래 총 4칸을 비교한다.
> 2. 사각형이 성립될 경우 오른쪽 아래칸에 해당 칸의 값을 제외한 나머지 칸의 최소값 + 1을 부여(= 정사각형의 한 변의 길이를 의미함).
> 3. 최대값 * 2를 반환한다.

### 🖥️ 풀이 코드
```
function solution(board) {
    let maxNum = 0
    for (let i = 0; i < board.length - 1; i ++) {
        for (let j = 0; j < board[0].length - 1; j ++) {
            if (board[i][j] > 0 && board[i][j+1] > 0 &&
                board[i+1][j] > 0 && board[i+1][j+1] > 0) {
                board[i+1][j+1] = Math.min(board[i][j], board[i][j+1], board[i+1][j]) + 1
                maxNum = Math.max(maxNum, board[i+1][j+1])
            }
        }
    }
    // 사각형을 찾지못했을 경우, 1이 하나라도 있으면 1 반환 아니면 0 반환
    if (maxNum === 0) {
        for(let i = 0; i < board.length; i ++) {
            for (let j = 0; j < board[0].length; j ++) {
                if (board[i][j] === 1) return 1
            }
        }    
    }
    
    return maxNum * 2
```

---

### 🔎 생각한 개선 방법 및 힌트

> **넓이라고 무조건 BFS라는 생각 금물.**
> 이는 다른 경우에서도 문제의 유형과 알고리즘을 섣불리 일치시키지 말고, 조건을 비교하면서 사용할 수 있는 알고리즘을 골라내자. 해당 문제같은 경우는 board의 넓이가 100만이였으므로, 최대 O(n log n)으로 풀어야하는데,  여러 번 비교를 하며 찾는 BFS와는 적합하지 않다.


---

## Lv. 2 [재귀 함수]하노이의 탑
### 📖  문제
하노이 탑(Tower of Hanoi)은 퍼즐의 일종입니다. 세 개의 기둥과 이 기동에 꽂을 수 있는 크기가 다양한 원판들이 있고, 퍼즐을 시작하기 전에는 한 기둥에 원판들이 작은 것이 위에 있도록 순서대로 쌓여 있습니다. 게임의 목적은 다음 두 가지 조건을 만족시키면서, 한 기둥에 꽂힌 원판들을 그 순서 그대로 다른 기둥으로 옮겨서 다시 쌓는 것입니다.

1. 한 번에 하나의 원판만 옮길 수 있습니다.
2. 큰 원판이 작은 원판 위에 있어서는 안됩니다.

하노이 탑의 세 개의 기둥을 왼쪽 부터 1번, 2번, 3번이라고 하겠습니다. 1번에는 n개의 원판이 있고 이 n개의 원판을 3번 원판으로 최소 횟수로 옮기려고 합니다.

1번 기둥에 있는 원판의 개수 n이 매개변수로 주어질 때, n개의 원판을 3번 원판으로 최소로 옮기는 방법을 return하는 solution를 완성해주세요.

##### 제한사항

- n은 15이하의 자연수 입니다.

---

##### 입출력 예

| n   | result                  |
| --- | ----------------------- |
| 2   | [ [1,2], [1,3], [2,3] ] |

---

### 📌 풀이 방법

>**재귀 함수로 해결**
>1. n개의 원판을 1번 -> 3번으로 이동해야 하므로, n-1개는 목적지가 아닌 다른 곳으로 이동 후 마지막 원판을 목적지에 옮겨야 한다.
>2. 원판이 하나 남으면 1 -> 3으로 이동하고, 나머지는 1개씩 줄여가면서 1 -> 2, 2 -> 3으로 이동.

### 🖥️ 풀이 코드
```
function solution(n) {
    let answer = []
    const hanoi = (n, start, goal, passing) => {
        if (n === 1) {
            answer.push([start, goal])
        } else {
            hanoi(n-1, start, passing, goal)
            answer.push([start,goal])
            hanoi(n-1, passing, goal, start)
        }
    }
    
    hanoi(n,1,3,2)
    return answer
}
```

---

### 🔎 생각한 개선 방법 및 힌트

> 1. 처음에는 우선순위를 설정하고, 기둥별 배열을 만들고 원판을 옮기는 형식으로 진행했었는데, 우선순위를 추리기가 너무어렵고 복잡해진다. 직접 옮기지 말고, 재귀 함수를 통해서 이동 경로만 배열에 추가. 

`풀이시간 : 30분분 `

## Lv. 2 [Heap]디펜스 게임
### 📖  문제

준호는 요즘 디펜스 게임에 푹 빠져 있습니다. 디펜스 게임은 준호가 보유한 병사 `n`명으로 연속되는 적의 공격을 순서대로 막는 게임입니다. 디펜스 게임은 다음과 같은 규칙으로 진행됩니다.

- 준호는 처음에 병사 `n`명을 가지고 있습니다.
- 매 라운드마다 `enemy[i]`마리의 적이 등장합니다.
- 남은 병사 중 `enemy[i]`명 만큼 소모하여 `enemy[i]`마리의 적을 막을 수 있습니다.
    - 예를 들어 남은 병사가 7명이고, 적의 수가 2마리인 경우, 현재 라운드를 막으면 7 - 2 = 5명의 병사가 남습니다.
    - 남은 병사의 수보다 현재 라운드의 적의 수가 더 많으면 게임이 종료됩니다.
- 게임에는 `무적권`이라는 스킬이 있으며, `무적권`을 사용하면 병사의 소모없이 한 라운드의 공격을 막을 수 있습니다.
- `무적권`은 최대 `k`번 사용할 수 있습니다.

준호는 `무적권`을 적절한 시기에 사용하여 최대한 많은 라운드를 진행하고 싶습니다.

준호가 처음 가지고 있는 병사의 수 `n`, 사용 가능한 무적권의 횟수 `k`, 매 라운드마다 공격해오는 적의 수가 순서대로 담긴 정수 배열 `enemy`가 매개변수로 주어집니다. 준호가 몇 라운드까지 막을 수 있는지 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 1 ≤ `n` ≤ 1,000,000,000
- 1 ≤ `k` ≤ 500,000
- 1 ≤ `enemy`의 길이 ≤ 1,000,000
- 1 ≤ `enemy[i]` ≤ 1,000,000
- `enemy[i]`에는 i + 1 라운드에서 공격해오는 적의 수가 담겨있습니다.
- 모든 라운드를 막을 수 있는 경우에는 `enemy[i]`의 길이를 return 해주세요.

---

##### 입출력 예

| n   | k   | enemy                 | result |
| --- | --- | --------------------- | ------ |
| 7   | 3   | [4, 2, 4, 5, 3, 3, 1] | 5      |
| 2   | 4   | [3, 3, 3, 3]          | 4      |

---

### 📌 풀이 방법

> enemy배열에서 k개만큼의 최대값을 저장하고, 최대값에 속한 범위의 숫자가 나오면 k 소모.

**로직** (실패)
1. enemy를 복사 후 정렬한 뒤, 0부터 k까지 객체에 추가한다.
2. enemy를 순회하면서 해당 수가 객체에 속하고 0보다 클 경우 무적권 사용.
**실패원인** 
	순서를 고려 안하고 최대값만 막다가는, 무적권을 다 못쓰고 죽는 경우 발생.

>직접 게임을 플레이하면 안되고, 최대 라운드를 판별하는 입장으로 가야한다.

**로직 변경**
쎈적 나오면 무적권 사용 **->** 죽으면 이전에 가장 강한적에서 무적권 썼다 치고 체력회복.

**개선 로직**
1. 최대 힙을 만들어서 배열을 순회하면서 적의 수들을 최대 힙에 넣는다.
2. enemy배열을 순회하고, 체력이 0이하가 되면 최대 힙에서 하나씩 꺼내 체력 회복하고 무적권 소모.

### 🖥️ 풀이 코드
```
function solution(n, k, enemy) {
    const maxHeap = new MaxHeap()
  
    for (let i = 0; i < enemy.length; i ++) {
        let monsters = enemy[i]
        n -= monsters
        maxHeap.insert(monsters)
        
        if (n <= 0) {
            while (n < 0 && maxHeap.size() > 0 && k > 0) {
                n += maxHeap.remove()
                k --
            }
        }
        
        if (n === 0 && k === 0) return i + 1
        if (n < 0) return i
    }
    
    if (n < 0) return enemy.length - 1
    
    return enemy.length
}

class MaxHeap {
    constructor () {
        this.heap = []
    }
    
    getParentIndex (index) {
        return Math.floor((index - 1) / 2)
    }
    
    getLeftChildIndex (index) {
        return index * 2 + 1
    }
    
    getRightChildIndex (index) {
        return index * 2 + 2
    }
    
    swap (index1, index2) {
        [this.heap[index1], this.heap[index2]] = [this.heap[index2], this.heap[index1]]
    }
    
    insert (value) {
        this.heap.push(value)
        this.bubbleUp()
    }
    
    size () {
        return this.heap.length
    }
    
    bubbleUp () {
        let index = this.size() - 1
        while (index > 0) {
            let parentIndex = this.getParentIndex(index)
            if (this.heap[index] > this.heap[parentIndex]) {
                this.swap(index, parentIndex)
                index = parentIndex
            } else {
                break
            }
        }
    }
    
    remove () {
        if (this.size() === 0) return null
        if (this.size() === 1) return this.heap.pop()
        
        let root = this.heap[0]
        this.heap[0] = this.heap.pop()
        this.bubbleDown()
        return root
    }
    
    bubbleDown () {
        let index = 0
        const length = this.size()
        while (this.getLeftChildIndex(index) < length) {
            let largest = this.getLeftChildIndex(index)
            let rightIndex = this.getRightChildIndex(index)
            if (this.heap[rightIndex] > this.heap[largest]) largest = rightIndex
            
            if (this.heap[index] < this.heap[largest]) {
                this.swap(index, largest)
                index = largest
            } else break
        }
    }
    
    peak () {
        return this.heap[0]
    }
}
```

---

### 🔎 생각한 개선 방안 또는 보완할 점

**이진 탐색을 활용한 풀이도 가능**
`heap`을 사용한 풀이와 `이진 탐색`을 사용한 풀이 모두 시간 복잡도는 최악의 경우 **O(n log n)** `n = enemy.length` 으로 동일하다.
하지만 대부분의 경우에서 `heap`을 사용한 풀이의 연산 속도가 압도적으로 더욱빠르다.
`이진 탐색`으로 풀이하는 방법은 구현이 더욱 간단하고 직관적일 수 있다.  

`풀이 시간 : 1시간 20분`

---

## Lv. 2 [수학]멀쩡한 사각형
### 📖  문제

가로 길이가 Wcm, 세로 길이가 Hcm인 직사각형 종이가 있습니다. 종이에는 가로, 세로 방향과 평행하게 격자 형태로 선이 그어져 있으며, 모든 격자칸은 1cm x 1cm 크기입니다. 이 종이를 격자 선을 따라 1cm × 1cm의 정사각형으로 잘라 사용할 예정이었는데, 누군가가 이 종이를 대각선 꼭지점 2개를 잇는 방향으로 잘라 놓았습니다. 그러므로 현재 직사각형 종이는 크기가 같은 직각삼각형 2개로 나누어진 상태입니다. 새로운 종이를 구할 수 없는 상태이기 때문에, 이 종이에서 원래 종이의 가로, 세로 방향과 평행하게 1cm × 1cm로 잘라 사용할 수 있는 만큼만 사용하기로 하였습니다.  
가로의 길이 W와 세로의 길이 H가 주어질 때, 사용할 수 있는 정사각형의 개수를 구하는 solution 함수를 완성해 주세요.

##### 제한사항

- W, H : 1억 이하의 자연수

#### 입출력 예

|W|H|result|
|---|---|---|
|8|12|80|

##### 입출력 예 설명

입출력 예 #1  
가로가 8, 세로가 12인 직사각형을 대각선 방향으로 자르면 총 16개 정사각형을 사용할 수 없게 됩니다. 원래 직사각형에서는 96개의 정사각형을 만들 수 있었으므로, 96 - 16 = 80 을 반환합니다.

![572957326.92.png](https://grepp-programmers.s3.amazonaws.com/files/production/ee895b2cd9/567420db-20f4-4064-afc3-af54c4a46016.png)

---

### 📌 풀이 방법

> 1. w,h의 최대값이 1억이므로, 해당 사각형 크기를 통해서 계산하는 것이 아니라, 해당 사각형과 같은 비율의 가장 작은 사각형을 통해서 배수로 구한다.
> 
> 2. 가장 작은 비율에서 가로 w 세로 h인 사각형의 사용할 수 없는 사각형의 개수는, `(w + h - 1)`. 이 공식을 커지는 비율에도 똑같이 적용하기 위해 -1대신 w와h의 최대 공약수를 대입한다. `= (w + h - gcd(w,h))`
> 
> 3. 총 넓이`(w*h)`에서 해당 개수만큼 빼주면 답이 나온다.


### 🖥️ 풀이 코드
```
function solution(w, h) {
    function gcd(w,h) {
        let a = Math.max(w,h)
        let b = Math.min(w,h)
        
        while (b !== 0) {
            let temp = b
            b = a % b
            a = temp
        }
        return a
    }
    
    return w * h - (w + h - gcd(w,h))
}
```

---

### 🔎 생각한 개선 방안 또는 보완할 점

> 1. 최대공약수, 최소 공배수, 소수판별 등 활용을 많이하는 부분은 항상 숙지하고 있자.

---

`풀이 시간 : 40분`

## Lv. 2 문자열 압축
### 📖  문제
데이터 처리 전문가가 되고 싶은 **"어피치"**는 문자열을 압축하는 방법에 대해 공부를 하고 있습니다. 최근에 대량의 데이터 처리를 위한 간단한 비손실 압축 방법에 대해 공부를 하고 있는데, 문자열에서 같은 값이 연속해서 나타나는 것을 그 문자의 개수와 반복되는 값으로 표현하여 더 짧은 문자열로 줄여서 표현하는 알고리즘을 공부하고 있습니다.  
간단한 예로 "aabbaccc"의 경우 "2a2ba3c"(문자가 반복되지 않아 한번만 나타난 경우 1은 생략함)와 같이 표현할 수 있는데, 이러한 방식은 반복되는 문자가 적은 경우 압축률이 낮다는 단점이 있습니다. 예를 들면, "abcabcdede"와 같은 문자열은 전혀 압축되지 않습니다. "어피치"는 이러한 단점을 해결하기 위해 문자열을 1개 이상의 단위로 잘라서 압축하여 더 짧은 문자열로 표현할 수 있는지 방법을 찾아보려고 합니다.

예를 들어, "ababcdcdababcdcd"의 경우 문자를 1개 단위로 자르면 전혀 압축되지 않지만, 2개 단위로 잘라서 압축한다면 "2ab2cd2ab2cd"로 표현할 수 있습니다. 다른 방법으로 8개 단위로 잘라서 압축한다면 "2ababcdcd"로 표현할 수 있으며, 이때가 가장 짧게 압축하여 표현할 수 있는 방법입니다.

다른 예로, "abcabcdede"와 같은 경우, 문자를 2개 단위로 잘라서 압축하면 "abcabc2de"가 되지만, 3개 단위로 자른다면 "2abcdede"가 되어 3개 단위가 가장 짧은 압축 방법이 됩니다. 이때 3개 단위로 자르고 마지막에 남는 문자열은 그대로 붙여주면 됩니다.

압축할 문자열 s가 매개변수로 주어질 때, 위에 설명한 방법으로 1개 이상 단위로 문자열을 잘라 압축하여 표현한 문자열 중 가장 짧은 것의 길이를 return 하도록 solution 함수를 완성해주세요.

### 제한사항

- s의 길이는 1 이상 1,000 이하입니다.
- s는 알파벳 소문자로만 이루어져 있습니다.

##### 입출력 예

| s                            | result |
| ---------------------------- | ------ |
| `"aabbaccc"`                 | 7      |
| `"ababcdcdababcdcd"`         | 9      |
| `"abcabcdede"`               | 8      |
| `"abcabcabcabcdededededede"` | 14     |
| `"xababcdcdababcdcd"`        | 17     |

---

### 📌 첫 번째 풀이 방법 (실패 -> 문제 착각 )

>**확인 로직**
>문자열 길이의 1/2크기로 시작해 1까지 줄어드는 창문을 통해 한 칸씩 이동하며 확인 후 압축.
>문서에서 단어를 찾는 해쉬 searching알고리즘 참고하여 활용

>시간 복잡도
s의 최대 길이는 1000이므로, 
`[1 3 5 7 ... n-1]` 이므로 평균값 n/2만큼 (log n) - 1)번 비교 = O(n log n)

### 🖥️ 풀이 코드
```
function solution(s) {
    let wLength = Math.floor(s.length / 2)
    let result = []
    while(wLength > 0) {
        for (let i = 0; i + wLength <= s.length; i ++) {
            let startPoint = i
            let count = 1
            let w = s.slice(i,i + wLength)
            let nextW = s.slice(i + wLength,i + wLength + wLength)
            // 같은게 나오면 뒤에 같은게 없을 때 까지 계속 확인
            if (w === nextW && w !== " ") {
                let startPoint = i + wLength
                while (w === nextW) {
                    startPoint += wLength
                    count ++
                    nextW = s.slice(startPoint, startPoint + wLength)
                }
                s = s.slice(0, i) + s.slice(startPoint)
                result.push(count + w)
                i--
            }
            // console.log(s,"길이 :", wLength,'인덱스 :',i)
        }
        wLength --
    }
    console.log(s,result)
    result = result.join("")
    
    return s.length + result.length
}
```

---

### 🔎 생각한 개선 방안 또는 보완할 점

> 1. 가장 효율적인 압축 방법을 작성하는 걸로 생각해 코드를 짜고 나니, 문제에서 제시한 방법과는 달랐다. `(문제에서 제시한 방법은 정해진 길이로 첫 번째부터 압축하는 로직. 구현이 간단한 반면에 기대값이 낮음) `

`풀이 시간 : 1시간 50분`

---

### 📌📌 두 번째 풀이 방법 (성공)

>**확인 로직**
>압축 가능한 문자는 횟수와 함께 다른 배열에 저장해주고, 줄어든 길이를 따로 저장한다. 해당 압축 크기의 비교가 끝나면 따로 저장해둔 배열 + 원본 배열 - 잘려나간 길이 를 통해 결과에 저장하고, 마지막에 길이들 중 최소값을 반환한다. 

### 🖥️🖥️ 풀이 코드
```
function solution(s) {
    if (s.length === 1) return 1
    let wLength = Math.floor(s.length / 2)
    let lengths = []
    while (wLength > 0) {
        let word = s
        let count = 1
        let deleteLength = 0
        let result = []
        for (let i = 0; i + wLength <= word.length; i += wLength) {
            let w = word.slice(i, i + wLength)
            let nextW = word.slice(i + wLength, i + wLength + wLength)
            if (w === nextW) {
                let startIdx = i + wLength
                while (w === nextW) {
                    count ++
                    startIdx += wLength
                    nextW = word.slice(startIdx, startIdx + wLength)
                }
                deleteLength += word.slice(i,startIdx).length
                result.push(count.toString() + w)
                i = startIdx - wLength
            }
            count = 1
        }
        lengths.push(word.length + result.join("").length - deleteLength)
        // console.log('result :', result, 'wLength :', wLength, 'word :', word, '길이 :', lengths[lengths.length-1])
        wLength --
        result = []
    }
    
    return Math.min(...lengths)
}
```

---

### 🔎 생각한 개선 방안 또는 보완할 점

> 문제와 테스트케이스를 꼼꼼히 확인할 필요가 있다.

`풀이 시간 : 50분`

---

## Lv. 2 우박수열 정적분
### 📖  문제

콜라츠 추측이란 로타르 콜라츠(Lothar Collatz)가 1937년에 제기한 추측으로 모든 자연수 k에 대해 다음 작업을 반복하면 항상 1로 만들 수 있다는 추측입니다.

```
1-1. 입력된 수가 짝수라면 2로 나눕니다.
1-2. 입력된 수가 홀수라면 3을 곱하고 1을 더합니다.
2.결과로 나온 수가 1보다 크다면 1번 작업을 반복합니다.
```

예를 들어 주어진 수가 5 라면 5 ⇒ 16 ⇒ 8 ⇒ 4 ⇒2 ⇒ 1 이되어 총 5번만에 1이 됩니다.

수가 커졌다 작아지기를 반복하는 모습이 비구름에서 빗방울이 오르락내리락하며 우박이 되는 모습과 비슷하다고 하여 우박수 또는 우박수열로 불리기도 합니다. 현재 이 추측이 참인지 거짓인지 증명되지 않았지만 약 1해까지의 수에서 반례가 없음이 밝혀져 있습니다.

은지는 우박수열을 좌표 평면 위에 꺾은선 그래프로 나타내보려고 합니다. 초항이 k인 우박수열이 있다면, x = 0일때 y = k이고 다음 우박수는 x = 1에 표시합니다. 이런 식으로 우박수가 1이 될 때까지 점들을 찍고 인접한 점들끼리 직선으로 연결하면 다음과 같이 꺾은선 그래프를 만들 수 있습니다.  
![그림.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/2d71eb1d-3d66-4046-93ce-2e8b7586bb96/%EA%B7%B8%EB%A6%BC.png)

은지는 이렇게 만든 꺾은선 그래프를 정적분 해보고 싶어졌습니다. x에 대한 어떤 범위 [a, b]가 주어진다면 이 범위에 대한 정적분 결과는 꺾은선 그래프와 x = a, x = b, y = 0 으로 둘러 쌓인 공간의 면적과 같습니다. 은지는 이것을 우박수열 정적분이라고 정의하였고 다양한 구간에 대해서 우박수열 정적분을 해보려고 합니다. 0 이상의 수 b에 대해 [a, -b]에 대한 정적분 결과는 x = a, x = n - b, y = 0 으로 둘러 쌓인 공간의 면적으로 정의하며, 이때 n은 k가 초항인 우박수열이 1이 될때 까지의 횟수를 의미합니다.

예를 들어, 5를 초항으로 하는 우박수열은 5 ⇒ 16 ⇒ 8 ⇒ 4 ⇒ 2 ⇒ 1 입니다. 이를 좌표 평면으로 옮기면 (0, 5), (1, 16), (2, 8), (3, 4), (4, 2), (5, 1) 에 점이 찍히고 점들을 연결하면 꺾은선 그래프가 나옵니다. 이를 [0,0] 구간에 대해 정적분 한다면 전체 구간에 대한 정적분이며, [1,-2] 구간에 대해 정적분 한다면 1 ≤ x ≤ 3인 구간에 대한 정적분입니다.

우박수의 초항 `k`와, 정적분을 구하는 구간들의 목록 `ranges`가 주어졌을 때 정적분의 결과 목록을 return 하도록 solution을 완성해주세요. 단, 주어진 구간의 시작점이 끝점보다 커서 유효하지 않은 구간이 주어질 수 있으며 이때의 정적분 결과는 -1로 정의합니다.

---

##### 제한사항

- 2 ≤ `k` ≤ 10,000
- 1 ≤ `ranges`의 길이 ≤ 10,000
    - `ranges`의 원소는 [a, b] 형식이며 0 ≤ a < 200, -200 < b ≤ 0 입니다.
- 주어진 모든 입력에 대해 정적분의 결과는 227 을 넘지 않습니다.
- 본 문제는 정답에 실수형이 포함되는 문제입니다. 입출력 예의 소수 부분 `.0`이 코드 실행 버튼 클릭 후 나타나는 결괏값, 기댓값 표시와 다를 수 있습니다.

---

##### 입출력 예

|k|ranges|result|
|---|---|---|
|5|[[0,0],[0,-1],[2,-3],[3,-3]]|[33.0,31.5,0.0,-1.0]|
|3|[[0,0], [1,-2], [3,-3]]|[47.0,36.0,12.0]|

---

### 📌 풀이 방법

>arr은 콜라츠 배열을 의미.
>구간 [a,b]가 주어졌을 떄, 해당 구간은 [a,arr.length + b - 1]

>풀이 로직
>1. k에 해당하는 콜라츠 배열 먼저 생성.
>2. y좌표를 저장하는 배열, 구간 별 넓이를 저장해놓는 배열 총 두개 생성.
>3. 구간에 따라 넓이를 result에 추가.

### 🖥️ 풀이 코드
```
function solution(k, ranges) {
    let result = []
    let areas = []
    let yValues = [k]
    while (k > 1) {
        k = k % 2 === 0 ? k / 2 : k * 3 + 1
        yValues.push(k)
    }
    // 넓이 구해서 배열에 추가
    for (let i = 0; i < yValues.length - 1; i++) {
        let y1= yValues[i]
        let y2= yValues[i+1]
        areas.push((Math.max(y1, y2) - Math.min(y1, y2)) / 2 + Math.min(y1,y2))
    }
    
    for(let i = 0; i < ranges.length; i ++) {
        let a  = ranges[i][0]
        let b = yValues.length + ranges[i][1] - 1
        
        if (a === b)
        {
            result.push(0)    
            continue
        }
        if (a > b)
        {
            result.push(-1)    
            continue
        }
        let area = 0
        for (let j = a; j < b; j ++) {
            area = area + areas[j]
        }
        result.push(area)
    }
    
    return result
}
```

---

`풀이 시간 : 40분`

---

## Lv. 2 광물 캐기
### 📖  문제
마인은 곡괭이로 광산에서 광석을 캐려고 합니다. 마인은 다이아몬드 곡괭이, 철 곡괭이, 돌 곡괭이를 각각 0개에서 5개까지 가지고 있으며, 곡괭이로 광물을 캘 때는 피로도가 소모됩니다. 각 곡괭이로 광물을 캘 때의 피로도는 아래 표와 같습니다.

![image](https://user-images.githubusercontent.com/62426665/217975815-63c58d04-0421-4c39-85ce-17613b9c9389.png)

예를 들어, 철 곡괭이는 다이아몬드를 캘 때 피로도 5가 소모되며, 철과 돌을 캘때는 피로도가 1씩 소모됩니다. 각 곡괭이는 종류에 상관없이 광물 5개를 캔 후에는 더 이상 사용할 수 없습니다.

마인은 다음과 같은 규칙을 지키면서 최소한의 피로도로 광물을 캐려고 합니다.

- 사용할 수 있는 곡괭이중 아무거나 하나를 선택해 광물을 캡니다.
- 한 번 사용하기 시작한 곡괭이는 사용할 수 없을 때까지 사용합니다.
- 광물은 주어진 순서대로만 캘 수 있습니다.
- 광산에 있는 모든 광물을 캐거나, 더 사용할 곡괭이가 없을 때까지 광물을 캡니다.

즉, 곡괭이를 하나 선택해서 광물 5개를 연속으로 캐고, 다음 곡괭이를 선택해서 광물 5개를 연속으로 캐는 과정을 반복하며, 더 사용할 곡괭이가 없거나 광산에 있는 모든 광물을 캘 때까지 과정을 반복하면 됩니다.

마인이 갖고 있는 곡괭이의 개수를 나타내는 정수 배열 `picks`와 광물들의 순서를 나타내는 문자열 배열 `minerals`가 매개변수로 주어질 때, 마인이 작업을 끝내기까지 필요한 최소한의 피로도를 return 하는 solution 함수를 완성해주세요.

---

##### 제한사항

- `picks`는 [dia, iron, stone]과 같은 구조로 이루어져 있습니다.
    - 0 ≤ dia, iron, stone ≤ 5
    - dia는 다이아몬드 곡괭이의 수를 의미합니다.
    - iron은 철 곡괭이의 수를 의미합니다.
    - stone은 돌 곡괭이의 수를 의미합니다.
    - 곡괭이는 최소 1개 이상 가지고 있습니다.
- 5 ≤ `minerals`의 길이 ≤ 50
    - `minerals`는 다음 3개의 문자열로 이루어져 있으며 각각의 의미는 다음과 같습니다.
    - diamond : 다이아몬드
    - iron : 철
    - stone : 돌

---

##### 입출력 예

|picks|minerals|result|
|---|---|---|
|[1, 3, 2]|["diamond", "diamond", "diamond", "iron", "iron", "diamond", "iron", "stone"]|12|
|[0, 1, 1]|["diamond", "diamond", "diamond", "diamond", "diamond", "iron", "iron", "iron", "iron", "iron", "diamond"]|50|

---

### 📌 풀이 방법

>곡괭이 개수 총 합 * 5 까지 광물 캘 수 있음.
>해당 길이만큼 5씩 끊어가면서, 광물 포인트의 총 합이 높은 순으로 좋은 곡괭이 배치.
>광물 포인트 : 다이아 : 25, 철 : 5, 돌 : 1

>로직
>1. 곡괭이 개수를 토대로 최대로 캘 수 있는 개수를 정한다.
>2. 5개씩 끊어가면서, 순서별 광물 포인트를 합산하여 index : 점수 형태의 객체로 저장한다.
>3. 점수 순으로 오름차순 정렬하고, index : 곡괭이 종류 형태로 값을 변경한다.
>4. minerals배열을 순회하면서 index에 맞는 곡괭이를 배정하고, 광물을 캐 피로도를 저장한다.

### 🖥️ 풀이 코드
```
function solution(picks, minerals) {
    // 1. 최대로 캘 수 있는 광물의 개수 구하기
    let maximum = picks.reduce((total, el) => total += el) * 5
    minerals = minerals.splice(0, maximum)
    
    const pointMap = new Map()
    let count = 0
    let point = 0 
    let index = 0
    let diaCount = 0
    // 2. 광물 포인트 index : point 형태로 저장하기
    for (let i = 0; i < minerals.length; i ++)
    {
        if (minerals[i] === "diamond")
        {
            point += 25
        }
        else if (minerals[i] === 'iron')
        {
            point += 5
        }
        else
        {
            point += 1    
        }
        count ++
        
        if (count === 5 || i === minerals.length - 1)
        {
            pointMap.set(index, point)
            count = 0
            point = 0
            index ++
        }
    }
    
    const sortedMap = new Map([...pointMap.entries()].sort((a,b) => b[1] - a[1]))
    
    let pick = ''
    for (let key of sortedMap.keys())
    {
        if (picks[0])
        {
            pick = 'diamond'
            picks[0] --
        }
        else if(picks[1])
        {
            pick = 'iron'
            picks[1] --
        }
        else
        {
            pick = 'stone'
            picks[2] --
        }
        sortedMap.set(key, pick)
    }
    
    let order = 0
    let energy = 0
    for (let i = 0; i < minerals.length; i += 5)
    {
        for (let j = i; j < i + 5; j ++)
        {
            if (j === minerals.length)
            {
                break
            }
            energy += mining(sortedMap.get(order), minerals[j])
        }
        order ++
    }
    
    return energy
}

function mining(pick, mineral)
{
    if (pick === 'diamond')
    {
        return 1
    }
    else if (pick === 'iron')
    {
        if (mineral === 'diamond')
        {
            return 5
        }
        else
        {
            return 1
        }
    }
    else {
        if (mineral === 'diamond')
        {
            return 25
        }
        else if (mineral === 'iron')
        {
            return 5
        }
        else
        {
            return 1
        }
    }
}
```

---

### 🔎 생각한 개선 방안 또는 보완할 점

> 1. 마지막 index 계산을 잘못해서 처음에 오류가 발생했다. 처음과 끝의 index 계산을 꼼꼼히 하자.
> 2. 중괄호 작성을 BSD스타일로 작성해보았다. 한 문단만 보았을 때는 가독성이 좋게 느껴지지만, 스크롤을 내릴수록 한 화면에 코드가 적게 들어와서 큰 장점을 느끼기 어려운 듯 하다.

`풀이시간 : 1시간 20분`

---

## Lv. 2 [수학] 점 찍기
### 📖 문제  

좌표평면을 좋아하는 진수는 x축과 y축이 직교하는 2차원 좌표평면에 점을 찍으면서 놀고 있습니다. 진수는 두 양의 정수 `k`, `d`가 주어질 때 다음과 같이 점을 찍으려 합니다.

- 원점(0, 0)으로부터 x축 방향으로 `a*k`(a = 0, 1, 2, 3 ...), y축 방향으로 `b*k`(b = 0, 1, 2, 3 ...)만큼 떨어진 위치에 점을 찍습니다.
- 원점과 거리가 `d`를 넘는 위치에는 점을 찍지 않습니다.

예를 들어, `k`가 2, `d`가 4인 경우에는 (0, 0), (0, 2), (0, 4), (2, 0), (2, 2), (4, 0) 위치에 점을 찍어 총 6개의 점을 찍습니다.

정수 `k`와 원점과의 거리를 나타내는 정수 `d`가 주어졌을 때, 점이 총 몇 개 찍히는지 return 하는 solution 함수를 완성하세요.

---

##### 제한사항

- 1 ≤ `k` ≤ 1,000,000
- 1 ≤ `d` ≤ 1,000,000

---

##### 입출력 예

|k|d|result|
|---|---|---|
|2|4|6|
|1|5|26

---  

### 📌 풀이 방법  

>row column 방향으로 d거리 이하까지 k 칸마다 점을 찍음  
>점의 총 개수 반환  

>**한 줄씩 점의 개수를 계산**  
>피타고라스 정리에 따라 삼각형의 대각선의 길이 즉, 거리는 a^2 + b^2 = c^2 이므로  
>양 변에 루트를 씌워주면, 한 줄당 c의 최대 값은 루트(a^2 + b^2)이다.  
>x를 k씩 증가시키면서, 한 줄당 점의 개수를 계산하여 추가.  

---

### 🖥️ 풀이 코드  

```  
function solution(k, d) {  
	let result = 0  
	for (let x = 0; x <= d; x += k) {  
		const max_y = Math.sqrt((d** 2) - (x ** 2))  
		result += Math.floor(max_y / k) + 1  
	}  

	return result  
}  
```  

---  

### 🔎 생각한 개선 방안 또는 보완할 점

> 전체 범위에서 규칙을 찾기 보다, 규칙이 성립되는 가장 작은 범위에서 개수를 세서 전체 범위의 개수를 구하는게 더욱 간단하다.

---

## Lv. 2 [정렬] 후보키
### 📖  문제

프렌즈대학교 컴퓨터공학과 조교인 제이지는 네오 학과장님의 지시로, 학생들의 인적사항을 정리하는 업무를 담당하게 되었다.

그의 학부 시절 프로그래밍 경험을 되살려, 모든 인적사항을 데이터베이스에 넣기로 하였고, 이를 위해 정리를 하던 중에 후보키(Candidate Key)에 대한 고민이 필요하게 되었다.

후보키에 대한 내용이 잘 기억나지 않던 제이지는, 정확한 내용을 파악하기 위해 데이터베이스 관련 서적을 확인하여 아래와 같은 내용을 확인하였다.

- 관계 데이터베이스에서 릴레이션(Relation)의 튜플(Tuple)을 유일하게 식별할 수 있는 속성(Attribute) 또는 속성의 집합 중, 다음 두 성질을 만족하는 것을 후보 키(Candidate Key)라고 한다.
    - 유일성(uniqueness) : 릴레이션에 있는 모든 튜플에 대해 유일하게 식별되어야 한다.
    - 최소성(minimality) : 유일성을 가진 키를 구성하는 속성(Attribute) 중 하나라도 제외하는 경우 유일성이 깨지는 것을 의미한다. 즉, 릴레이션의 모든 튜플을 유일하게 식별하는 데 꼭 필요한 속성들로만 구성되어야 한다.

제이지를 위해, 아래와 같은 학생들의 인적사항이 주어졌을 때, 후보 키의 최대 개수를 구하라.

![cand_key1.png](https://grepp-programmers.s3.amazonaws.com/files/production/f1a3a40ede/005eb91e-58e5-4109-9567-deb5e94462e3.jpg)

위의 예를 설명하면, 학생의 인적사항 릴레이션에서 모든 학생은 각자 유일한 "학번"을 가지고 있다. 따라서 "학번"은 릴레이션의 후보 키가 될 수 있다.  
그다음 "이름"에 대해서는 같은 이름("apeach")을 사용하는 학생이 있기 때문에, "이름"은 후보 키가 될 수 없다. 그러나, 만약 ["이름", "전공"]을 함께 사용한다면 릴레이션의 모든 튜플을 유일하게 식별 가능하므로 후보 키가 될 수 있게 된다.  
물론 ["이름", "전공", "학년"]을 함께 사용해도 릴레이션의 모든 튜플을 유일하게 식별할 수 있지만, 최소성을 만족하지 못하기 때문에 후보 키가 될 수 없다.  
따라서, 위의 학생 인적사항의 후보키는 "학번", ["이름", "전공"] 두 개가 된다.

릴레이션을 나타내는 문자열 배열 relation이 매개변수로 주어질 때, 이 릴레이션에서 후보 키의 개수를 return 하도록 solution 함수를 완성하라.

##### 제한사항

- relation은 2차원 문자열 배열이다.
- relation의 컬럼(column)의 길이는 `1` 이상 `8` 이하이며, 각각의 컬럼은 릴레이션의 속성을 나타낸다.
- relation의 로우(row)의 길이는 `1` 이상 `20` 이하이며, 각각의 로우는 릴레이션의 튜플을 나타낸다.
- relation의 모든 문자열의 길이는 `1` 이상 `8` 이하이며, 알파벳 소문자와 숫자로만 이루어져 있다.
- relation의 모든 튜플은 유일하게 식별 가능하다.(즉, 중복되는 튜플은 없다.)

##### 입출력 예

| relation                                                                                                                                                                      | result |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| `[["100","ryan","music","2"],["200","apeach","math","2"],["300","tube","computer","3"],["400","con","computer","4"],["500","muzi","music","3"],["600","apeach","music","2"]]` | 2      |

---

### 📌 풀이 방법

>**문제 정리**
>데이터의 최대 개수 : 8개
>속성의 최대 개수 : 20개
>
>유일성 : 데이터 중복이 없어야 함.
>최소성 : 데이터 식별을 가능케 하는 속성의 최소 개수.

>**시간 복잡도**
 속성 n개가 있을 때, n개의 속성들로 만들 수 있는 조합의 개수는 ? (중복 허용 X, 순서 상관 X) 
 >$2^n$개이다. (공집합 포함)
 >각 단계는 $2^n$번의 연산이 필요하므로 총 $n$번 실행하게 되면 전체 시간복잡도는 $O(n \cdot 2^n)$
 >이를 통해 최대 연산 횟수를 계산해보면, n = 8일 때, 2048이다.
 >그러므로 모든 조합을 구하여 해결한다. 

>로직
>1. 속성별 정보를 index로 구분하고, 가능한 모든 조합을 만든다.
>2. 유일성과 최소성을 체크할 수 있는 함수를 각각 만든다.
>3. 모든 조합에서 유일성과 최소성을 각각 위반하는 경우의 조합을 제거해 가면서 남아있는 조합의 개수를 반환한다.

### 🖥️ 풀이 코드
```
function solution(relation) {
    const arr = []
    for (let i = 0; i < relation[0].length ; i++) {
        arr.push(i)
    }
    let candidates = getCandidates(arr)
    // 길이 순으로 정렬
    candidates.sort((a,b) => a.length - b.length)
    candidates = checkUniqueness(relation, candidates)
    candidates = checkMinimality(candidates)
    
    return candidates.length
}

function getCandidates(arr) {
    const result = []
    function dfs(curr, start) {
        if (curr.length > 0) {
            result.push([...curr])
        }
        for (let i = start; i < arr.length; i ++) {
            curr.push(arr[i])
            dfs(curr, i + 1)
            curr.pop()
        }
    }
    dfs([], 0)
    return result
}

function checkUniqueness(relation, candidates) {
    const result = []
    
    for (let candidate of candidates) {
        let set = new Set()
        for (let rel of relation) {
            set.add(candidate.map((el) => rel[el]).join(','))
        }
        if (set.size === relation.length) {
            result.push(candidate)
        }
        
    }
    return result
}

function checkMinimality(candidates) {
    function checkContains(arr, subArr) {
        for (let item of subArr) {
            if (!arr.includes(item)) {
                return false
            }
        }
        return true
    }
    let prev = 0
    let curr = 1
    while (prev < candidates.length - 1) {
        if (checkContains(candidates[curr], candidates[prev])) {
            candidates.splice(curr, 1)
        }
        else {
            curr ++
        }
        
        if (curr > candidates.length - 1) {
            prev ++
            curr = prev + 1
        }
    }
    
    return candidates
}
```

---

### 🔎 생각한 개선 방안 또는 보완할 점

> 1.  정렬에 대해 더욱 빠삭하게 숙지하기


`풀이 시간 : 5시간`

---

## Lv. 2 [정렬, 스택] 과제 진행하기
### 📖  문제

과제를 받은 루는 다음과 같은 순서대로 과제를 하려고 계획을 세웠습니다.

- 과제는 시작하기로 한 시각이 되면 시작합니다.
- 새로운 과제를 시작할 시각이 되었을 때, 기존에 진행 중이던 과제가 있다면 진행 중이던 과제를 멈추고 새로운 과제를 시작합니다.
- 진행중이던 과제를 끝냈을 때, 잠시 멈춘 과제가 있다면, 멈춰둔 과제를 이어서 진행합니다.
    - 만약, 과제를 끝낸 시각에 새로 시작해야 되는 과제와 잠시 멈춰둔 과제가 모두 있다면, 새로 시작해야 하는 과제부터 진행합니다.
- 멈춰둔 과제가 여러 개일 경우, 가장 최근에 멈춘 과제부터 시작합니다.

과제 계획을 담은 이차원 문자열 배열 `plans`가 매개변수로 주어질 때, 과제를 끝낸 순서대로 이름을 배열에 담아 return 하는 solution 함수를 완성해주세요.

---

##### 제한사항

- 3 ≤ `plans`의 길이 ≤ 1,000
    - `plans`의 원소는 [name, start, playtime]의 구조로 이루어져 있습니다.
        - name : 과제의 이름을 의미합니다.
            - 2 ≤ name의 길이 ≤ 10
            - name은 알파벳 소문자로만 이루어져 있습니다.
            - name이 중복되는 원소는 없습니다.
        - start : 과제의 시작 시각을 나타냅니다.
            - "hh:mm"의 형태로 "00:00" ~ "23:59" 사이의 시간값만 들어가 있습니다.
            - 모든 과제의 시작 시각은 달라서 겹칠 일이 없습니다.
            - 과제는 "00:00" ... "23:59" 순으로 시작하면 됩니다. 즉, 시와 분의 값이 작을수록 더 빨리 시작한 과제입니다.
        - playtime : 과제를 마치는데 걸리는 시간을 의미하며, 단위는 분입니다.
            - 1 ≤ playtime ≤ 100
            - playtime은 0으로 시작하지 않습니다.
        - 배열은 시간순으로 정렬되어 있지 않을 수 있습니다.
- 진행중이던 과제가 끝나는 시각과 새로운 과제를 시작해야하는 시각이 같은 경우 진행중이던 과제는 끝난 것으로 판단합니다.

---

##### 입출력 예

| plans                                                                                                            | result                                      |
| ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------- |
| [["korean", "11:40", "30"], ["english", "12:10", "20"], ["math", "12:30", "40"]]                                 | ["korean", "english", "math"]               |
| [["science", "12:40", "50"], ["music", "12:20", "40"], ["history", "14:00", "30"], ["computer", "12:30", "100"]] | ["science", "history", "computer", "music"] |
| [["aaa", "12:00", "20"], ["bbb", "12:10", "30"], ["ccc", "12:40", "10"]]                                         | ["bbb", "ccc", "aaa"]                       |

---

### 📌 풀이 방법  
>if 종료 시간이 다음 과제 시작 시간보다 이르면, result에 추가.  
>else 다음 과제 시작 시간까지 진행시간 줄이고, stack에 추가.  

>새로운 과제 종료 후, 다음 과제 시작 시간까지 stack의 마지막 과제를 진행하고, 과제가 완료되면 pop한 뒤에 stack의 다음 과제 진행.  

>로직  
>1. plans 데이터를 시작시간이 빠른 순으로 정렬한다.  
>2. 다음 과제 시작 시간까지 남는 시간을 계산해서, 해당 시간을 과제에 소모시키며 0이 되면 다음 과제로 넘어간다.  

---

### 🖥️ 풀이 코드  

```  
function solution(plans) {
    const result = []
    // 문자열 시간 숫자로 변경하고 시작 시간 순으로 정렬.
    for (let i = 0; i < plans.length; i ++) {
        plans[i][1] = plans[i][1].slice(0,2) + plans[i][1].slice(3)
        plans[i][2] = parseInt(plans[i][2])
    }
    plans.sort((a, b) => parseInt(a[1]) - parseInt(b[1]))
    
    const stack = []
    for (let i = 0; i < plans.length; i ++) {
        let [curPlan, curStart, curSpend] = plans[i]
        if (i === plans.length - 1) {
            result.push(curPlan)
            break
        }
        let remainTime = timeDiff(curStart, plans[i + 1][1])
        // console.log(curPlan, '에서 남은시간', remainTime)
        if (remainTime >= curSpend) {
            remainTime -= curSpend
            result.push(curPlan)
            while (remainTime > 0 && stack.length > 0) {
                [curPlan, curStart, curSpend] = stack.pop()
                if (remainTime >= curSpend) {
                    remainTime -= curSpend
                    result.push(curPlan)
                }
                else {
                    curSpend -= remainTime
                    remainTime = 0
                    stack.push([curPlan, curStart, curSpend])
                }
            }
        }
        else {
            curSpend -= remainTime
            remainTime = 0
            stack.push([curPlan, curStart, curSpend])
        }
    }
    
    // plans배열 다 돌고 남아있는 과제들 차례대로 추가
    while (stack.length > 0) {
        result.push(stack.pop()[0])
    }
    
    return result
}

function timeDiff(curr, next) {
    let hour = Number(next.slice(0,2)) - Number(curr.slice(0,2))
    let currM = Number(curr.slice(2))
    let nextM = Number(next.slice(2))
    let minute = 0
    if (currM > nextM) {
        hour --
        minute = (60 - currM) + nextM
    }
    else {
        minute = nextM - currM
    }
    
    return (hour * 60) + minute
}
```  

  

---  

  

### 🔎 생각한 개선 방안 또는 보완할 점  
> 1. 시간 계산에 아직 익숙치 않아 이 부분에서 많이 헤맸다.  

`풀이 시간 : 1시간 20분`

---

## Lv. 2 [수학] 두 원 사이의 정수 쌍
### 📖  문제
x축과 y축으로 이루어진 2차원 직교 좌표계에 중심이 원점인 서로 다른 크기의 원이 두 개 주어집니다. 반지름을 나타내는 두 정수 `r1`, `r2`가 매개변수로 주어질 때, 두 원 사이의 공간에 x좌표와 y좌표가 모두 정수인 점의 개수를 return하도록 solution 함수를 완성해주세요.  
※ 각 원 위의 점도 포함하여 셉니다.

---

##### 제한 사항

- 1 ≤ `r1` < `r2` ≤ 1,000,000

---

##### 입출력 예

| r1  | r2  | result |
| --- | --- | ------ |
| 2   | 3   | 20     |

---

### 📌 풀이 방법

>1. 삼각함수를 활용해 원에서 하나의 사분면만 계산한다.
>2. 높이 1씩 올라가면서 r2 크기 원의 점의 개수 - r1 크기 원의 점의 개수를 세준다.
>3. r2의 높이까지 올라갔으면 점의 총 합에 * 4를 해주어 총 개수를 구한다.

---

### 🖥️ 풀이 코드
```
function solution(r1, r2) {
    let y1 = 0
    let y2 = 0
    let answer = 0
    for (let i = 1; i <= r2; i ++) {
        y2 = Math.sqrt(Math.pow(r2, 2) - Math.pow(i, 2))
        y1 = Math.sqrt(Math.pow(r1, 2) - Math.pow(i, 2))
        if (isNaN(y1)) {
            y1 = 0
        }
        
        answer += Math.floor(y2) - Math.ceil(y1) + 1
    }
    
    return answer * 4
}
```

---

### 🔎 생각한 개선 방안 또는 보완할 점

> 1. 필요한 기초 식을 먼저 적어두고 계산하기. ex) a2+b2=c2

`풀이 시간 : 30분`

---

## Lv. 2 [완전 탐색] 이모티콘 할인행사
### 📖  문제

카카오톡에서는 이모티콘을 무제한으로 사용할 수 있는 이모티콘 플러스 서비스 가입자 수를 늘리려고 합니다.  
이를 위해 카카오톡에서는 이모티콘 할인 행사를 하는데, 목표는 다음과 같습니다.

1. 이모티콘 플러스 서비스 가입자를 최대한 늘리는 것.
2. 이모티콘 판매액을 최대한 늘리는 것.

**1번 목표가 우선이며, 2번 목표가 그 다음입니다.**

이모티콘 할인 행사는 다음과 같은 방식으로 진행됩니다.

- `n`명의 카카오톡 사용자들에게 이모티콘 `m`개를 할인하여 판매합니다.
- 이모티콘마다 할인율은 다를 수 있으며, 할인율은 10%, 20%, 30%, 40% 중 하나로 설정됩니다.

카카오톡 사용자들은 다음과 같은 기준을 따라 이모티콘을 사거나, 이모티콘 플러스 서비스에 가입합니다.

- 각 사용자들은 자신의 기준에 따라 일정 비율 이상 할인하는 이모티콘을 모두 구매합니다.
- 각 사용자들은 자신의 기준에 따라 이모티콘 구매 비용의 합이 일정 가격 이상이 된다면, 이모티콘 구매를 모두 취소하고 이모티콘 플러스 서비스에 가입합니다.

다음은 2명의 카카오톡 사용자와 2개의 이모티콘이 있을때의 예시입니다.

|사용자|비율|가격|
|---|---|---|
|1|40|10,000|
|2|25|10,000|

|이모티콘|가격|
|---|---|
|1|7,000|
|2|9,000|

1번 사용자는 40%이상 할인하는 이모티콘을 모두 구매하고, 이모티콘 구매 비용이 10,000원 이상이 되면 이모티콘 구매를 모두 취소하고 이모티콘 플러스 서비스에 가입합니다.  
2번 사용자는 25%이상 할인하는 이모티콘을 모두 구매하고, 이모티콘 구매 비용이 10,000원 이상이 되면 이모티콘 구매를 모두 취소하고 이모티콘 플러스 서비스에 가입합니다.

1번 이모티콘의 가격은 7,000원, 2번 이모티콘의 가격은 9,000원입니다.

만약, 2개의 이모티콘을 모두 40%씩 할인한다면, 1번 사용자와 2번 사용자 모두 1,2번 이모티콘을 구매하게 되고, 결과는 다음과 같습니다.

|사용자|구매한 이모티콘|이모티콘 구매 비용|이모티콘 플러스 서비스 가입 여부|
|---|---|---|---|
|1|1, 2|9,600|X|
|2|1, 2|9,600|X|

이모티콘 플러스 서비스 가입자는 0명이 늘어나고 이모티콘 판매액은 19,200원이 늘어납니다.

하지만, 1번 이모티콘을 30% 할인하고 2번 이모티콘을 40% 할인한다면 결과는 다음과 같습니다.

|사용자|구매한 이모티콘|이모티콘 구매 비용|이모티콘 플러스 서비스 가입 여부|
|---|---|---|---|
|1|2|5,400|X|
|2|1, 2|10,300|O|

2번 사용자는 이모티콘 구매 비용을 10,000원 이상 사용하여 이모티콘 구매를 모두 취소하고 이모티콘 플러스 서비스에 가입하게 됩니다.  
따라서, 이모티콘 플러스 서비스 가입자는 1명이 늘어나고 이모티콘 판매액은 5,400원이 늘어나게 됩니다.

카카오톡 사용자 `n`명의 구매 기준을 담은 2차원 정수 배열 `users`, 이모티콘 `m`개의 정가를 담은 1차원 정수 배열 `emoticons`가 주어집니다. 이때, 행사 목적을 최대한으로 달성했을 때의 이모티콘 플러스 서비스 가입 수와 이모티콘 매출액을 1차원 정수 배열에 담아 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- 1 ≤ `users`의 길이 = `n` ≤ 100
    - `users`의 원소는 [`비율`, `가격`]의 형태입니다.
    - `users[i]`는 `i+1`번 고객의 구매 기준을 의미합니다.
    - `비율`% 이상의 할인이 있는 이모티콘을 모두 구매한다는 의미입니다.
        - 1 ≤ `비율` ≤ 40
    - `가격`이상의 돈을 이모티콘 구매에 사용한다면, 이모티콘 구매를 모두 취소하고 이모티콘 플러스 서비스에 가입한다는 의미입니다.
        - 100 ≤ `가격` ≤ 1,000,000
        - `가격`은 100의 배수입니다.
- 1 ≤ `emoticons`의 길이 = `m` ≤ 7
    - `emoticons[i]`는 `i+1`번 이모티콘의 정가를 의미합니다.
    - 100 ≤ `emoticons`의 원소 ≤ 1,000,000
    - `emoticons`의 원소는 100의 배수입니다.

---

##### 입출력 예

| users                                                                                | emoticons                | result     |
| ------------------------------------------------------------------------------------ | ------------------------ | ---------- |
| [[40, 10000], [25, 10000]]                                                           | [7000, 9000]             | [1, 5400]  |
| [[40, 2900], [23, 10000], [11, 5200], [5, 5900], [40, 3100], [27, 9200], [32, 6900]] | [1300, 1500, 1600, 4900] | [4, 13860] |

---

### 📌 풀이 방법
>우선순위
>1. 이모티콘 플러스 가입자 수 증가
>2. 이모티콘 판매액 증가

>유저의 수가 최대 100명, 이모티콘의 개수가 최대 7개이므로 완전탐색으로 해결.
>이모티콘이 7가지, 할인율의 종류 4가지의 모든 조합을 생성하고, 조합마다 비교

>중복조합으로 이모티콘 할인율 설정하여 가입자 수, 판매 금액 비교하여 최대값 리턴

### 🖥️ 풀이 코드
```
function solution(users, emoticons) {
    
    return saleCombination(users, emoticons)
}

function salePrice(price, percentage) {
    return price * ((100 - percentage) / 100)
}

function saleCombination(users, emoticons) {
    let result = [0, 0]
    const arr = [10, 20, 30, 40]
    function dfs(sales, len) {
        if (sales.length === len) {
        const buyingPrice = new Array(users.length).fill(0)
            const candidates = [0, 0]
            for (let i = 0; i < users.length; i ++) {
                let [limitPercentage, limitPrice] = users[i]
                for (let j = 0; j < len; j ++) {
                    if (limitPercentage <= sales[j]) {
                        buyingPrice[i] += salePrice(emoticons[j], sales[j])
                        if (buyingPrice[i] >= users[i][1]) {
                            break
                        }
                    }
                }
                if (buyingPrice[i] >= limitPrice) {
                    buyingPrice[i] = Infinity
                }
            }
            for (let price of buyingPrice) {
                if (price === Infinity) {
                    candidates[0] ++
                }
                else {
                    candidates[1] += price
                }
            }
            
            if (candidates[0] > result[0]) {
                result = candidates
            }
            else if (candidates[0] === result[0] && candidates[1] > result[1]) {
                result = candidates
            }
            return
        }
        
        for (let i = 0; i < arr.length; i ++) {
            sales.push(arr[i])
            dfs(sales, len)
            sales.pop()
        }
    }
    dfs([], emoticons.length)
    
    return result
}
    dfs([], emoticons.length)
    
    return result
}
```

---

### 🔎 생각한 개선 방안 또는 보완할 점

> 1.  가독성 개선 필요

`풀이 시간 : 55분`

---

## Lv. 2 [수학] N-Queen
### 📖  문제

가로, 세로 길이가 n인 정사각형으로된 체스판이 있습니다. 체스판 위의 n개의 퀸이 서로를 공격할 수 없도록 배치하고 싶습니다.

예를 들어서 n이 4인경우 다음과 같이 퀸을 배치하면 n개의 퀸은 서로를 한번에 공격 할 수 없습니다.

![Imgur](https://i.imgur.com/lt2zdK6.png)  
![Imgur](https://i.imgur.com/5c5EUrq.png)

체스판의 가로 세로의 세로의 길이 n이 매개변수로 주어질 때, n개의 퀸이 조건에 만족 하도록 배치할 수 있는 방법의 수를 return하는 solution함수를 완성해주세요.

##### 제한사항

- 퀸(Queen)은 가로, 세로, 대각선으로 이동할 수 있습니다.
- n은 12이하의 자연수 입니다.

---

##### 입출력 예

| n   | result |
| --- | ------ |
| 4   | 2      |

---

### 📌 풀이 방법

>고려할 부분
>전체 n * n 크기의 공간을 만들지 않아도 된다.
>어차피 row를 통해 방문하므로 row의 방문을 체크하지 않아도 된다.
>column 방문은 공통되므로 배열의 크기는 column개수 만큼만.

>로직 (재귀를 통해 구현)
>1. row를 하나씩 증가시키면서, 놓을 수 있는 곳에 Q를 놓는다.
>2. Q를 놓으면, column방문 처리 배열에 column에 해당하는 index에 row를 저장한다.
>3. row + 1을 전달받아 다음 열로 넘어가 재귀를 시작한다.
>4. 해당 재귀가 끝나면 다시 해당 column의 방문을 취소처리하고 위의 과정을 반복한다.
>5. 맨 마지막 열까지 도달할 경우 result += 1을 해준다.

>**Q를 놓을 수 있는지 판별**
>**세로줄(Column)**
>- 해당 column이 방문하지 않은 상태일 경우
>**가로줄(Row)**
>- row를 증가시키며 확인하므로 겹칠 일 X
>**대각선**
>- column 방문 처리 배열에 각 column에 놓여져 있는 Queen의 row를 저장함으로써, 해당 row와 현재 확인하는 row의 차이만큼 column을 더하고, 빼고 두 가지 경우를 통해 양쪽 대각선을 확인한다.
	EX) 이미 놓여진 Queen의 row,와 column이 (2,3)에 놓여져 있고, 현재 확인하는 칸이 (5, 6)일 경우
	3 - (5 - 2) = 0 (좌쪽 대각선)
	3 + (5 - 2) = 6 (우측 대각선)
	현재 확인하는 column이 6이므로 해당 칸은 Queen을 놓을 수 없다.

---

### 🖥️ 풀이 코드
```
function solution(n) {
    
    return checkQueen(n)
}

function checkQueen(n) {
    const colVisited = new Array(n).fill(false)
    let result = 0
    function dfs(row) {
        if (row === n) {
            result += 1    
            return
        }
        
        for (let col = 0; col < n; col ++) {
            if (typeof colVisited[col] !== 'number') {
                let check = true
                for (let c = 0; c < n; c ++) {
                    let r = colVisited[c]
                    if (typeof r === "number") {
                    if (c + (row - r) === col ||
                        c - (row - r) === col) {
                            check = false
                            break
                        }
                    }
                }
                
                if (check) {
                    colVisited[col] = row
                    dfs(row + 1)
                    colVisited[col] = false
                }
            }
        }
    }
    dfs(0)
    
    return result
}
```

---

### 🔎 생각한 개선 방안 또는 보완할 점

> 1. 0에 false로 작용되는 사실을 캐치하지 못하여 계속 틀린 답이 나왔다.
> 2. 재귀를 싱글스레드처럼 하나의 작업이 실행되다 재귀가 호출되면 해당 재귀로 들어가 작업을 시작하는... 이런 일련의 과정을 머릿속으로 한 단계씩 생각해보니 재귀를 이해하는데 도움이 괴었다.

`풀이 시간 : 3시간`

---

## Lv. 2 혼자 놀기의 달인
### 📖  문제

혼자서도 잘 노는 범희는 어느 날 방구석에 있는 숫자 카드 더미를 보더니 혼자 할 수 있는 재미있는 게임을 생각해냈습니다.

숫자 카드 더미에는 카드가 총 100장 있으며, 각 카드에는 1부터 100까지 숫자가 하나씩 적혀있습니다. 2 이상 100 이하의 자연수를 하나 정해 그 수보다 작거나 같은 숫자 카드들을 준비하고, 준비한 카드의 수만큼 작은 상자를 준비하면 게임을 시작할 수 있으며 게임 방법은 다음과 같습니다.

준비된 상자에 카드를 한 장씩 넣고, 상자를 무작위로 섞어 일렬로 나열합니다. 상자가 일렬로 나열되면 상자가 나열된 순서에 따라 1번부터 순차적으로 증가하는 번호를 붙입니다.

그 다음 임의의 상자를 하나 선택하여 선택한 상자 안의 숫자 카드를 확인합니다. 다음으로 확인한 카드에 적힌 번호에 해당하는 상자를 열어 안에 담긴 카드에 적힌 숫자를 확인합니다. 마찬가지로 숫자에 해당하는 번호를 가진 상자를 계속해서 열어가며, 열어야 하는 상자가 이미 열려있을 때까지 반복합니다.

이렇게 연 상자들은 1번 상자 그룹입니다. 이제 1번 상자 그룹을 다른 상자들과 섞이지 않도록 따로 둡니다. 만약 1번 상자 그룹을 제외하고 남는 상자가 없으면 그대로 게임이 종료되며, 이때 획득하는 점수는 0점입니다.

그렇지 않다면 남은 상자 중 다시 임의의 상자 하나를 골라 같은 방식으로 이미 열려있는 상자를 만날 때까지 상자를 엽니다. 이렇게 연 상자들은 2번 상자 그룹입니다.

1번 상자 그룹에 속한 상자의 수와 2번 상자 그룹에 속한 상자의 수를 곱한 값이 게임의 점수입니다.

상자 안에 들어있는 카드 번호가 순서대로 담긴 배열 `cards`가 매개변수로 주어질 때, 범희가 이 게임에서 얻을 수 있는 최고 점수를 구해서 return 하도록 solution 함수를 완성해주세요.

---

##### 제한사항

- `2` ≤ `cards`의 길이 ≤ `100`
- `cards`의 원소는 `cards`의 길이 이하인 임의의 자연수입니다.
- `cards`에는 중복되는 원소가 존재하지 않습니다.
- `cards[i]`는 i + 1번 상자에 담긴 카드에 적힌 숫자를 의미합니다.

---

##### 입출력 예

| cards             | result |
| ----------------- | ------ |
| [8,6,3,7,2,5,1,4] | 12     |

---

### 📌 풀이 방법

>**문제 정리**
>임의의 수 n이하의 모든 카드를 각자 상자에 넣음.
>상자를 열어서 안에 있는 카드의 번호에 해당하는 index를 가진 상자 오픈.
>열어야 하는 상자가 이미 열려있으면 1그룹에 배정. (모두 열리면 0점)
>2그룹도 똑같이 진행해서 상자 배정.
>1그룹 상자 수 x 2그룹 상자 수 의 최대값 구하기.

>**로직 (그리디)**
>1. 시작점을 index 1 부터 끝까지 모든 경우의 수에 맞춰 group1 상자 오픈
>2. group1의 상자가 정해졌으면, 남아있는 박스의 개수만큼 group2 상자 오픈 반복

---

### 🖥️ 풀이 코드
```
function solution(cards) {
    // index 계산을 편리하게 하기 위해 cards 앞에 0추가
    cards.unshift(0)
    let maxPoint = 0
    
    
    for (let i = 1; i < cards.length; i ++) {
        let index = i
        let visited = new Array(cards.length).fill(false)
        let group1 = 0
        let group2 = 0
        // group1의 박스 개수 카운팅
        while (!visited[index]) {
            visited[index] = true
            group1 ++
            index = cards[index]
        }
        
        // group1에서 모든 박스를 오픈했다면 다시 처음으로
        if (group1 === cards.length - 1) {
            continue
        }
        
        // 남아있는 박스만큼 group2 박수 개수 카운팅 반복
        for (let j = 1; j < cards.length - 1; j ++) {
            if (!visited[j]) {
                let visited2 = [...visited]
                index = j
                while(!visited2[index]) {
                    visited2[index] = true
                    group2 ++
                    index = cards[index]
                }
            }
            maxPoint = group1 * group2 > maxPoint ? group1 * group2 : maxPoint
            group2 = 0
        }
    }
        
    return maxPoint
}
```

---

### 🔎 생각한 개선 방안 또는 보완할 점

> 1. 데이터의 범위가 작기때문에 문제 이해만 하면 모든 경우의 수를 비교하면서 해결 가능.

`풀이 시간 : 30분`

---


## Lv. 2 혼자서 하는 틱택토
### 📖  문제

틱택토는 두 사람이 하는 게임으로 처음에 3x3의 빈칸으로 이루어진 게임판에 선공이 "O", 후공이 "X"를 번갈아가면서 빈칸에 표시하는 게임입니다. 가로, 세로, 대각선으로 3개가 같은 표시가 만들어지면 같은 표시를 만든 사람이 승리하고 게임이 종료되며 9칸이 모두 차서 더 이상 표시를 할 수 없는 경우에는 무승부로 게임이 종료됩니다.

할 일이 없어 한가한 머쓱이는 두 사람이 하는 게임인 틱택토를 다음과 같이 혼자서 하려고 합니다.

- 혼자서 선공과 후공을 둘 다 맡는다.
- 틱택토 게임을 시작한 후 "O"와 "X"를 혼자서 번갈아 가면서 표시를 하면서 진행한다.

틱택토는 단순한 규칙으로 게임이 금방 끝나기에 머쓱이는 한 게임이 종료되면 다시 3x3 빈칸을 그린 뒤 다시 게임을 반복했습니다. 그렇게 틱택토 수 십 판을 했더니 머쓱이는 게임 도중에 다음과 같이 규칙을 어기는 실수를 했을 수도 있습니다.

- "O"를 표시할 차례인데 "X"를 표시하거나 반대로 "X"를 표시할 차례인데 "O"를 표시한다.
- 선공이나 후공이 승리해서 게임이 종료되었음에도 그 게임을 진행한다.

게임 도중 게임판을 본 어느 순간 머쓱이는 본인이 실수를 했는지 의문이 생겼습니다. 혼자서 틱택토를 했기에 게임하는 과정을 지켜본 사람이 없어 이를 알 수는 없습니다. 그러나 게임판만 봤을 때 실제로 틱택토 규칙을 지켜서 진행했을 때 나올 수 있는 상황인지는 판단할 수 있을 것 같고 문제가 없다면 게임을 이어서 하려고 합니다.

머쓱이가 혼자서 게임을 진행하다 의문이 생긴 틱택토 게임판의 정보를 담고 있는 문자열 배열 `board`가 매개변수로 주어질 때, 이 게임판이 규칙을 지켜서 틱택토를 진행했을 때 나올 수 있는 게임 상황이면 1을 아니라면 0을 return 하는 solution 함수를 작성해 주세요.

---

##### 제한사항

- `board`의 길이 = `board[i]`의 길이 = 3
    - `board`의 원소는 모두 "O", "X", "."으로만 이루어져 있습니다.
- `board[i][j]`는 `i` + 1행 `j` + 1열에 해당하는 칸의 상태를 나타냅니다.
    - "."은 빈칸을, "O"와 "X"는 해당 문자로 칸이 표시되어 있다는 의미입니다.

---

##### 입출력 예

|board|result|
|---|---|
|["O.X", ".O.", "..X"]|1|
|["OOO", "...", "XXX"]|0|
|["...", ".X.", "..."]|0|
|["...", "...", "..."]|1|

---

### 📌 풀이 방법

>머쓱이가 실수할 수 있는 모든 경우의 수를 종합하고. 해당 조건을 체크

**머쓱이가 실수하는 모든 경우의 수**
>순서 헷갈리는 경우
>1. X가 O보다 많을 때
>2. O가 X보다 2개 이상 많을 때

>둘다 승리하는 경우
>1. 불가능

>게임이 종료되었는데 진행하는 경우
>1. X가 승리했는데, O의 개수가 X보다 많을 때
>2 O가 승리했는데, X의 개수가 O와 같거나 많을 때

---

### 🖥️ 풀이 코드
```
function solution(board) {
    const winO = checkWinning(board, 'O')
    const winX = checkWinning(board, 'X')
    const countO = countStone(board, 'O')
    const countX = countStone(board, 'X')
    // console.log(winO, winX, countO, countX)
    // 1. 순서 헷갈리는 경우
    if (countX > countO || countO >= countX + 2) {
        return 0
    }
    
    // 2. 둘다 승리
    if (winO && winX) {
        return 0
    }
    
    // 3. 게임이 종료되었는데 진행하는 경우
    // O가 승리
    if (winO && countX >= countO) {
        return 0
    }
    
    // X가 승리
    if (winX && countO > countX) {
        return 0
    }

	// 모든 실수를 안했을 경우 1 반환환
    return 1
}

function checkWinning(board, p) {
    // 대각선 승리 판독
    if (board[0][0] === p && board[1][1] === p && board[2][2] === p) {
        return true
    }
    if (board[0][2] === p && board[1][1] === p && board[2][0] === p) {
        return true
    }
    
    let line = p + p + p
    for (let i = 0; i < 3; i ++) {
        // 가로줄 승리 판독
        if (board[i] === line) {
            return true
        }
        
        // 세로줄 승리 판독
        if (board[0][i] === p && board[1][i] === p && board[2][i] === p) {
            return true
        }
    }
    return false
}

function countStone(board, p) {
    let count = 0
    for (let i = 0; i < 3; i ++) {
        for (let j = 0; j < 3; j ++) {
            if (board[i][j] === p) {
                count ++
            }
        }
    }
    
    return count    
}
```

---

### 🔎 생각한 개선 방안 또는 보완할 점

> 1. 실수할 수 있는 모든 경우의 수를 찾아내기만 하면 간단한 구현으로 풀이 가능.

`풀이시간 : 30분`

---


## Lv. 2 요격 시스템
### 📖  문제

A 나라가 B 나라를 침공하였습니다. B 나라의 대부분의 전략 자원은 아이기스 군사 기지에 집중되어 있기 때문에 A 나라는 B 나라의 아이기스 군사 기지에 융단폭격을 가했습니다.  
A 나라의 공격에 대항하여 아이기스 군사 기지에서는 무수히 쏟아지는 폭격 미사일들을 요격하려고 합니다. 이곳에는 백발백중을 자랑하는 요격 시스템이 있지만 운용 비용이 상당하기 때문에 미사일을 최소로 사용해서 모든 폭격 미사일을 요격하려 합니다.  
A 나라와 B 나라가 싸우고 있는 이 세계는 2 차원 공간으로 이루어져 있습니다. A 나라가 발사한 폭격 미사일은 x 축에 평행한 직선 형태의 모양이며 개구간을 나타내는 정수 쌍 (s, e) 형태로 표현됩니다. B 나라는 특정 x 좌표에서 y 축에 수평이 되도록 미사일을 발사하며, 발사된 미사일은 해당 x 좌표에 걸쳐있는 모든 폭격 미사일을 관통하여 한 번에 요격할 수 있습니다. 단, 개구간 (s, e)로 표현되는 폭격 미사일은 s와 e에서 발사하는 요격 미사일로는 요격할 수 없습니다. 요격 미사일은 실수인 x 좌표에서도 발사할 수 있습니다.  
각 폭격 미사일의 x 좌표 범위 목록 `targets`이 매개변수로 주어질 때, 모든 폭격 미사일을 요격하기 위해 필요한 요격 미사일 수의 최솟값을 return 하도록 solution 함수를 완성해 주세요.

---

##### 제한 사항

- 1 ≤ `targets`의 길이 ≤ 500,000
- targets의 각 행은 [s,e] 형태입니다.
    - 이는 한 폭격 미사일의 x 좌표 범위를 나타내며, 개구간 (s, e)에서 요격해야 합니다.
    - 0 ≤ s < e ≤ 100,000,000

---

##### 입출력 예

| targets                                          | result |
| ------------------------------------------------ | ------ |
| [[4,5],[4,8],[10,14],[11,13],[5,12],[3,7],[1,4]] | 3      |

---

### 📌 풀이 방법

>**겹치는 구간인지 판별**
	앞의 구간을 a 뒤의 구간을 b라고 가정.
	b의 시작점이 a의 종료지점보다 작으면 겹치는 구간.

>**로직**
>1. 미사일을 종료 지점 기준으로 내림차순 정렬한다.
>2. 다음 미사일이 겹치는 구간일 경우, 겹치는 구간 미사일의 종료지점을 c, c보다 작은 시작지점의 미사일들을 찾는다.
>3. 해당 미사일들을 1번의 요격으로 제거하고, 다음 미사일부터 다시 찾아나간다.

---

### 🖥️ 풀이 코드
```
function solution(targets) {
    targets.sort((a,b) => a[1] - b[1])
    let count = 0
    for (let i = 0; i < targets.length; i ++) {
        let endPoint = targets[i][1]
        while (i < targets.length - 1 && targets[i + 1][0] < endPoint) {
            i ++                        
        }
        count ++
    }
    
    return count
}
```

---

### 🔎 풀이를 마치고

> 1. 끝나는 지점을 기점으로 체크해나가면, 아무리 긴 구간을 가진 막대라도 결국 마지막에 같이 제거된다.

`풀이시간 : 25분`

---

## Lv. 2 숫자 블록
### 📖  문제

그렙시에는 숫자 0이 적힌 블록들이 설치된 도로에 다른 숫자가 적힌 블록들을 설치하기로 하였습니다. 숫자 블록을 설치하는 규칙은 다음과 같습니다.

블록에 적힌 번호가 n 일 때, 가장 첫 블록은 n * 2번째 위치에 설치합니다. 그 다음은 n * 3, 그 다음은 n * 4, ...위치에 설치합니다. 기존에 설치된 블록은 빼고 새로운 블록을 집어넣습니다.

블록은 1이 적힌 블록부터 숫자를 1씩 증가시키며 순서대로 설치합니다. 예를 들어 1이 적힌 블록은 2, 3, 4, 5, ... 인 위치에 우선 설치합니다. 그 다음 2가 적힌 블록은 4, 6, 8, 10, ... 인 위치에 설치하고, 3이 적힌 블록은 6, 9, 12... 인 위치에 설치합니다.

이렇게 3이 적힌 블록까지 설치하고 나면 첫 10개의 블록에 적힌 번호는 [0, 1, 1, 2, 1, 3, 1, 2, 3, 2]가 됩니다.

그렙시는 길이가 1,000,000,000인 도로에 1부터 10,000,000까지의 숫자가 적힌 블록들을 이용해 위의 규칙대로 모두 설치 했습니다.

그렙시의 시장님은 특정 구간에 어떤 블록이 깔려 있는지 알고 싶습니다.

구간을 나타내는 두 정수 `begin`, `end` 가 매개변수로 주어 질 때, 그 구간에 깔려 있는 블록의 숫자 배열을 return하는 solution 함수를 완성해 주세요.

---

##### 제한 사항

- 1 ≤ `begin` ≤ `end` ≤ 1,000,000,000
- `end` - `begin` ≤ 5,000

---

##### 입출력 예

| begin | end | result                         |
| ----- | --- | ------------------------------ |
| 1     | 10  | [0, 1, 1, 2, 1, 3, 1, 4, 3, 5] |

---

### 📌 풀이 방법

>설계 과정
>1. 해당 칸의 숫자 판별하는 함수 만들기
    1.1 n이 1이면 0반환
    1.2 2부터 루트n 까지 n을 나눠서, 몫이 1e7보다 작으면 해당 목 반환.
    1.3 몫이 1e7보다 클 경우 n이 나뉘어지는 수(= 약수)를 스택에 넣어줌.
    1.4 스택에 숫자가 있따면 가장 큰 약수 (스택의 맨 뒤 숫자)를 반환
    1.5 스택에 아무 숫자도 없다면, 해당 수는 소수이므로 1 반환.
  >
>2. begin 부터 end까지 순회하면서 함수를 통해 판별한 값을 결과에 추가해준다.

---

### 🖥️ 풀이 코드
```
function solution(begin, end) {
    const result = []
    for (let i = begin; i <= end; i ++) {
        result.push(checkNum(i))
    }

    return result
}

function checkNum(n) {
    if (n === 1) {
        return 0
    }

    let stack = []
    for (let i = 2; i <= Math.sqrt(n); i ++) {
        if (n % i === 0) {
            if (n / i <= 1e7) {
                return n / i
            }
            stack.push(i)
        }
    }
    
    if (stack.length) {
        return stack[stack.length - 1]
    }
    
    return 1
}
```

---

### 🔎 풀이를 마치고

> 1. 처음에는 소수를 먼저 판별했는데, 모든 수마다 소수 판별을 진행하니 비효율적으로 작동.
> 2. 몫의 범위를 1e7 까지로 제한했는데, 그보다 1e7까지의 숫자를 넣는게 아니라 1e7까지의 숫자의 배수들로 값을 채우는 것이므로 1e7 이하의 가장 큰 약수를 반환하면 된다.

`풀이 시간 : 1시간 반`

---

## Lv. 2 퍼즐 게임 챌린지
### 📖  문제

당신은 순서대로 `n`개의 퍼즐을 제한 시간 내에 풀어야 하는 퍼즐 게임을 하고 있습니다. 각 퍼즐은 난이도와 소요 시간이 정해져 있습니다. 당신의 숙련도에 따라 퍼즐을 풀 때 틀리는 횟수가 바뀌게 됩니다. 현재 퍼즐의 난이도를 `diff`, 현재 퍼즐의 소요 시간을 `time_cur`, 이전 퍼즐의 소요 시간을 `time_prev`, 당신의 숙련도를 `level`이라 하면, 게임은 다음과 같이 진행됩니다.

- `diff` ≤ `level`이면 퍼즐을 틀리지 않고 `time_cur`만큼의 시간을 사용하여 해결합니다.
- `diff` > `level`이면, 퍼즐을 총 `diff` - `level`번 틀립니다. 퍼즐을 틀릴 때마다, `time_cur`만큼의 시간을 사용하며, 추가로 `time_prev`만큼의 시간을 사용해 이전 퍼즐을 다시 풀고 와야 합니다. **이전 퍼즐을 다시 풀 때는 이전 퍼즐의 난이도에 상관없이 틀리지 않습니다.** `diff` - `level`번 틀린 이후에 다시 퍼즐을 풀면 `time_cur`만큼의 시간을 사용하여 퍼즐을 해결합니다.

예를 들어 `diff` = 3, `time_cur` = 2, `time_prev` = 4인 경우, `level`에 따라 퍼즐을 푸는데 걸리는 시간은 다음과 같습니다.

- `level` = 1이면, 퍼즐을 3 - 1 = 2번 틀립니다. 한 번 틀릴 때마다 2 + 4 = 6의 시간을 사용하고, 다시 퍼즐을 푸는 데 2의 시간을 사용하므로 총 6 × 2 + 2 = 14의 시간을 사용하게 됩니다.
- `level` = 2이면, 퍼즐을 3 - 2 = 1번 틀리므로, 6 + 2 = 8의 시간을 사용하게 됩니다.
- `level` ≥ 3이면 퍼즐을 틀리지 않으며, 2의 시간을 사용하게 됩니다.

퍼즐 게임에는 전체 제한 시간 `limit`가 정해져 있습니다. 제한 시간 내에 퍼즐을 모두 해결하기 위한 숙련도의 최솟값을 구하려고 합니다. **난이도, 소요 시간은 모두 양의 정수며, 숙련도도 양의 정수여야 합니다.**

퍼즐의 난이도를 순서대로 담은 1차원 정수 배열 `diffs`, 퍼즐의 소요 시간을 순서대로 담은 1차원 정수 배열 `times`, 전체 제한 시간 `limit`이 매개변수로 주어집니다. 제한 시간 내에 퍼즐을 모두 해결하기 위한 숙련도의 최솟값을 정수로 return 하도록 solution 함수를 완성해 주세요.

---

##### 제한사항

- 1 ≤ `diffs`의 길이 = `times`의 길이 = `n` ≤ 300,000
    - `diffs[i]`는 `i`번째 퍼즐의 난이도, `times[i]`는 `i`번째 퍼즐의 소요 시간입니다.
    - `diffs[0]` = 1
    - 1 ≤ `diffs[i]` ≤ 100,000
    - 1 ≤ `times[i]` ≤ 10,000
- 1 ≤ `limit` ≤ 1015
    - 제한 시간 내에 퍼즐을 모두 해결할 수 있는 경우만 입력으로 주어집니다.

---

##### 입출력 예

| diffs                     | times                    | limit      | result |
| ------------------------- | ------------------------ | ---------- | ------ |
| [1, 5, 3]                 | [2, 4, 7]                | 30         | 3      |
| [1, 4, 4, 2]              | [6, 3, 8, 2]             | 59         | 2      |
| [1, 328, 467, 209, 54]    | [2, 7, 1, 4, 3]          | 1723       | 294    |
| [1, 99999, 100000, 99995] | [9999, 9001, 9999, 9001] | 3456789012 | 39354  |

---

### 📌 풀이 방법

diffs는 각 퍼즐의 레벨
times는 각 퍼즐의 소요시간
i번째 퍼즐의 소요시간은 times[i]이고 이전 시간은 times[i-1]
첫 번째 퍼즐은 이전 퍼즐의 시간이 없음.
이전 퍼즐을 다시 풀 때는 무조건 한 번만에 해결.

사용자에게 필요한 최소 레벨 반환.

퍼즐의 개수는 최대 30만개.
N^2 미만으로 풀어야 함.
최대 O(N logN)

결국 제한시간 내에 모든 퍼즐을 해결하는 변곡점을 찾으면 된다.

diffs의 최댓값과 1 사이의 범위로 이진탐색 실행하다보면 n logn으로 해결 가능.

---

### 🖥️ 풀이 코드
```
function solution(diffs, times, limit) {
    let max = diffs.reduce((acc, val) => Math.max(acc, val), -Infinity);
    let min = 1
    let answer = max
    
    while(min <= max) {
        let level = Math.floor((min + max) / 2)
        let spendTime = 0
        for (let i = 0; i < diffs.length; i ++) {
            let levelDifference = diffs[i] - level
            if (levelDifference > 0) {
                spendTime += (levelDifference) * (times[i] + times[i-1]) + times[i]
            }
            else {
                spendTime += times[i]
            }
            
            if (spendTime > limit) {
                break
            }
        }
        
        if(spendTime > limit) {
            min = level + 1
        }
        else {
            answer = level
            max = level - 1
        }
    }
    return answer
}
```

---

### 🔎 풀이를 마치고

> **문제발생** 
> 이진탐색을 활용해 간단하게 해결할 수 있는 문제이지만, 처음 풀이 시도때는 Math.max(...diffs)를 최댓값으로 지정했더니 시간 초과가 발생함.

>**문제 원인**
> max와 spread연산자 모두 각각 N만큼 시간이 걸려서 최댓값을 지정하는 데에만 theta(2N)만큼의 시간이 걸리는 것이 원인.

>**해결 방안**
> 최댓값을 상수 10,000으로 지정하거나 spread연산자를 사용하지 않고 구하는 방법으로 해결.


---


## Lv. 2 [!!작성 양식]
### 📖  문제



---

### 📌 풀이 방법

>

---

### 🖥️ 풀이 코드
```

```

---

### 🔎 풀이를 마치고

> 1. 


---

## Lv. 2 양궁 대회
### 📖  문제



---

### 📌 풀이 방법

>**우승자 선정 방식**
>1. 같은 점수를 더 많이 맞춘 사람이 해당 점수를 가져감.(동률일 경우 도전자가)
>    1.1 10점을 각각 2번씩 맞출 경우 도전자가 10점 획득
  >  1.2 임의의 수 k를 둘 다 0번씩 맞춘 경우 둘다 획득 불가.
>2. 1의 방식으로 모든 점수를 계산하고, 최종 점수가 동률일 경우 도전자가 승리

>**시간 복잡도**
>n이 10이하의 수이므로 시간적 제한은 없다고 봐도 무방함.

>**풀이 방법**
>0점부터 10점까지 점수를 순환하면서 모든 경우의 수를 반영한다.
>
>경우의 수는 총 세 가지 이다.
>1. 라이언이 점수 획득
>2. 어피치가 점수 획득
>3. 무승부
>
>문제에서 구하고자 하는 게임 결과는 라이언이 가장 큰 점수차로 승리한 상황이므로
>각 점수마다 라이언에게 가장 유리한 상황으로 반영한다.
>총 세 가지 경우의 수를 통해 살펴보자.
>
>1. 라이언이 점수 획득
>- 라이언이 이겼을 경우는 화살 1개 차이로 이긴 경우가 가장 유리하다
>
>2. 어피치가 점수 획득
>- 어피치가 이겼을 경우는 화살을 한 개도 사용하지 않은 경우가 가장 유리하다
>
>3. 무승부
>- 무승부는 화살 0개 사용으로 고정되어있다.
>
>각 점수마다 세 가지 상황을 반영하여 나올 수 있는 모든 결과를 재귀적으로 구한다.
>그리고 가장 큰 점수차를 기록한 경기는 게임의 점수판을 저장해둔 뒤, 마지막에 반환한다.
>
>우리가 구해야 할 부분은 점수차 이므로, 라이언과 어피치 각각의 점수를 저장하지 않고, 점수 차만 반영하면서 게임을 진행한다.

>**유의해야 할 부분**
>- 이길 수 없는 경우 [-1] 반환
>- 라이언이 가장 큰 점수 차이로 우승할 수 있는 방법이 여러 가지 일 경우, 가장 낮은 점수를 더 많이 맞힌 경우를 반환

---

### 🖥️ 풀이 코드
```
function solution(n, info) {
    let maxScoreBoard = Array(11).fill(0)
    let maxScoreDifference = 0
    
    const findMaxScore = (scoreDifference, attemptCount, point, scoreBoard) => {        
        if (attemptCount > n) {
            return
        }
        
        if (point > 10) {
            if (scoreDifference > maxScoreDifference) {
                scoreBoard[10] = n - attemptCount
                maxScoreBoard = scoreBoard
                maxScoreDifference = scoreDifference
            }
            return
        }
        
        const index = 10 - point
        // 라이언이 점수 획득
        const updateBoard = [...scoreBoard]
        updateBoard[index] = info[index] + 1
        findMaxScore(scoreDifference + point, attemptCount + info[index] + 1, point + 1, updateBoard)
        // 어피치가 점수 획득
        if (info[index] > 0) {
            findMaxScore(scoreDifference - point, attemptCount, point + 1, scoreBoard )    
        }
        else {
            // 둘다 0점
            findMaxScore(scoreDifference, attemptCount, point + 1, scoreBoard )
        }
    }
    
    findMaxScore(0, 0, 0, maxScoreBoard)
    
    if (maxScoreDifference) {
        return maxScoreBoard
    }
    return [-1]
}
```

---

### 🔎 풀이를 마치고

> 1. 구해야 하는 값의 대상과 어떤 부분을 반복해야 하는지 명확히 하자.


---



# 프로그래머스 Lv. 3
## Lv. 3 [힙(heap)] 이중우선순위큐
### 문제
이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.

|명령어|수신 탑(높이)|
|---|---|
|I 숫자|큐에 주어진 숫자를 삽입합니다.|
|D 1|큐에서 최댓값을 삭제합니다.|
|D -1|큐에서 최솟값을 삭제합니다.|

이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0,0] 비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.

##### 제한사항

- operations는 길이가 1 이상 1,000,000 이하인 문자열 배열입니다.
- operations의 원소는 큐가 수행할 연산을 나타냅니다.
    - 원소는 “명령어 데이터” 형식으로 주어집니다.- 최댓값/최솟값을 삭제하는 연산에서 최댓값/최솟값이 둘 이상인 경우, 하나만 삭제합니다.
- 빈 큐에 데이터를 삭제하라는 연산이 주어질 경우, 해당 연산은 무시합니다.

##### 입출력 예

| operations                                                                  | return     |
| --------------------------------------------------------------------------- | ---------- |
| ["I 16", "I -5643", "D -1", "D 1", "D 1", "I 123", "D -1"]                  | [0,0]      |
| ["I -45", "I 653", "D 1", "I -642", "I 45", "I 97", "D 1", "D -1", "I 333"] | [333, -45] |

### 문제 풀이
#### 풀이 과정
**문제 정리**
주어진 연산(특정 숫자 삽입, 최댓값 삭제, 최솟값 삭제)을 모두 시행하고
최댓값, 최솟값 반환. 비어있으면 0,0반환

**구현**
최소힙에 최대 값 제거 메서드를 추가해서 구현해준다.

#### 답안 코드
```
class MinHeap {
    constructor() {
        this.heap = [];
    }
    
    getParentIndex(index) {
        return Math.floor((index - 1) / 2)
    }
    
    getLeftChildIndex(index) {
        return index * 2 + 1
    }
    
    getRightChildIndex(index) {
        return index * 2 + 2
    }
    
    swap(idx1, idx2) {
        [this.heap[idx1], this.heap[idx2]] = [this.heap[idx2], this.heap[idx1]]
    }
    
    add(value) {
        this.heap.push(value)
        this.heapifyUp()
    }
    
    heapifyUp(idx = this.heap.length - 1) {
        let index = idx
        while (index > 0) {
            let parentIndex = this.getParentIndex(index)
            if (this.heap[index] < this.heap[parentIndex]) {
                this.swap(index, parentIndex)
                index = parentIndex
            } else {
                break
            }
        }
    }
    
    remove() {
        if (this.heap.length === 0) return null
        if (this.heap.length === 1) return this.heap.pop()
        
        const root = this.heap[0]
        this.heap[0] = this.heap.pop()
        this.heapifyDown()
        
        return root
    }
    
    heapifyDown(idx = 0) {
        const length = this.heap.length
        let index = idx
        while(this.getLeftChildIndex(index) < length) {
            let smallest = this.getLeftChildIndex(index)
            let rightIndex = this.getRightChildIndex(index)
            if (rightIndex < length && this.heap[rightIndex] < this.heap[smallest]) {
                smallest = rightIndex
            }
            if (this.heap[index] > this.heap[smallest]) {
                this.swap(index, smallest)
                index = smallest
            } else {
                break
            }
        }
    }
    
    size() {
        return this.heap.length
    }
    
    peak() {
        return this.heap[0]
    }
    
    removeMax() {
        if (this.size() === 0) return null
        if (this.size() <= 2) return this.heap.pop()
        
        let maxIndex = this.size() - 1
        for (let i = Math.floor(this.size() / 2); i < this.size(); i ++) {
            if (this.heap[i] > this.heap[maxIndex]) {
                maxIndex = i
            }
        }
        const max = this.heap[maxIndex]
        if(maxIndex < this.size()) {
            this.heapifyUp(maxIndex)
            this.heapifyDown(maxIndex)
        }
        return max
    }
}

function solution(operations) {
    let answer = []
    let minHeap = new MinHeap()
    for(let i = 0; i < operations.length; i ++) {
        if (operations[i][0] === "I") {
            let num = parseInt(operations[i].slice(2))
            minHeap.add(num)
        } else if(operations[i][2] === "-") {
            minHeap.remove()
        } else {
            minHeap.removeMax()
        }
    }
    
    if(minHeap.size() === 0) {
        answer = [0,0]
    } else if (minHeap.size() >= 2) {
        answer = [minHeap.removeMax(), minHeap.peak()]
    } else {
        answer = [minHeap.peak(), minHeap.peak()]
    }

    return answer
}
```


## Lv. 3 디스크 컨트롤러
### 문제
하드디스크는 한 번에 하나의 작업만 수행할 수 있습니다. 디스크 컨트롤러를 구현하는 방법은 여러 가지가 있습니다. 가장 일반적인 방법은 요청이 들어온 순서대로 처리하는 것입니다.

예를들어

```
- 0ms 시점에 3ms가 소요되는 A작업 요청
- 1ms 시점에 9ms가 소요되는 B작업 요청
- 2ms 시점에 6ms가 소요되는 C작업 요청
```

와 같은 요청이 들어왔습니다. 이를 그림으로 표현하면 아래와 같습니다.  
![Screen Shot 2018-09-13 at 6.34.58 PM.png](https://grepp-programmers.s3.amazonaws.com/files/production/b68eb5cec6/38dc6a53-2d21-4c72-90ac-f059729c51d5.png)

한 번에 하나의 요청만을 수행할 수 있기 때문에 각각의 작업을 요청받은 순서대로 처리하면 다음과 같이 처리 됩니다.  
![Screen Shot 2018-09-13 at 6.38.52 PM.png](https://grepp-programmers.s3.amazonaws.com/files/production/5e677b4646/90b91fde-cac4-42c1-98b8-8f8431c52dcf.png)

```
- A: 3ms 시점에 작업 완료 (요청에서 종료까지 : 3ms)
- B: 1ms부터 대기하다가, 3ms 시점에 작업을 시작해서 12ms 시점에 작업 완료(요청에서 종료까지 : 11ms)
- C: 2ms부터 대기하다가, 12ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 16ms)
```

이 때 각 작업의 요청부터 종료까지 걸린 시간의 평균은 10ms(= (3 + 11 + 16) / 3)가 됩니다.

하지만 A → C → B 순서대로 처리하면  
![Screen Shot 2018-09-13 at 6.41.42 PM.png](https://grepp-programmers.s3.amazonaws.com/files/production/9eb7c5a6f1/a6cff04d-86bb-4b5b-98bf-6359158940ac.png)

```
- A: 3ms 시점에 작업 완료(요청에서 종료까지 : 3ms)
- C: 2ms부터 대기하다가, 3ms 시점에 작업을 시작해서 9ms 시점에 작업 완료(요청에서 종료까지 : 7ms)
- B: 1ms부터 대기하다가, 9ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 17ms)
```

이렇게 A → C → B의 순서로 처리하면 각 작업의 요청부터 종료까지 걸린 시간의 평균은 9ms(= (3 + 7 + 17) / 3)가 됩니다.

각 작업에 대해 [작업이 요청되는 시점, 작업의 소요시간]을 담은 2차원 배열 jobs가 매개변수로 주어질 때, 작업의 요청부터 종료까지 걸린 시간의 평균을 가장 줄이는 방법으로 처리하면 평균이 얼마가 되는지 return 하도록 solution 함수를 작성해주세요. (단, 소수점 이하의 수는 버립니다)

##### 제한 사항

- jobs의 길이는 1 이상 500 이하입니다.
- jobs의 각 행은 하나의 작업에 대한 [작업이 요청되는 시점, 작업의 소요시간] 입니다.
- 각 작업에 대해 작업이 요청되는 시간은 0 이상 1,000 이하입니다.
- 각 작업에 대해 작업의 소요시간은 1 이상 1,000 이하입니다.
- 하드디스크가 작업을 수행하고 있지 않을 때에는 먼저 요청이 들어온 작업부터 처리합니다.

##### 입출력 예

|jobs|return|
|---|---|
|[[0, 3], [1, 9], [2, 6]]|9|

---

### 문제 풀이
#### 풀이 과정
요청부터 작업 완료까지의 시간중에 가장 낮은 평균값을 반환해라.

**우선 순위**
현재 작업 시작이 가능한 작업 중 소요시간이 짧은 작업 실행.

작업이 실행될 때 마다 현재 시간을 업데이트하고, 현재 시간보다 작업 요청시점이 작은 값들을 `heap`에 넣는다.
`heap`에서 값을 빼서, 현재 시간 업데이트하고 총 작업시간 업데이트.

#### 답안 코드
```
function solution(jobs) {
    let totalSpendTime = 0 // 총 소요시간
    let currTime = 0 // 현재 시간
    let totalTask = jobs.length // 작업의 개수
    let taskCount = totalTask // 남아있는 작업 개수 확인 용도
    let taskHeap = new MinHeap() // 실행가능 작업 리스트
    
    // pop으로 비교하기 위해 요청순서대로 역정렬
    jobs.sort((a,b) => b[0] - a[0])
    
    // 작업 처리 로직
    while (taskCount > 0) {
        // 현재 실행 가능한 작업들을 heap에 담아줌
        while (jobs.length > 0 && jobs[jobs.length-1][0] <= currTime) {
            taskHeap.add(jobs.pop())
        }
        // 실행 가능한 작업이 있는 경우 작업 실행하고 시간 업데이트
        if(taskHeap.size() > 0) {
            let [startPoint, spendTime] = taskHeap.runTask()
            currTime += spendTime
            totalSpendTime += currTime - startPoint
            taskCount --
        // 현재 실행 가능한 작업이 없는 경우 가장 가까운 작업을 heap에 담아줌
        } else {
            taskHeap.add(jobs.pop())
            currTime = taskHeap.peek()[0]
        }
    }
    
    return Math.floor(totalSpendTime / totalTask)
}

// 최소 힙으로 디스크 힙 구현
class MinHeap {
    constructor() {
        this.heap = []
    }
    
    getParent(index) {
        return Math.floor((index - 1) / 2)
    }
    
    getLeftChild(index) {
        return index * 2 + 1
    }
    
    getRightChild(index) {
        return index * 2 + 2
    }
    
    swap(index1, index2) {
        [this.heap[index1], this.heap[index2]] = [this.heap[index2], this.heap[index1]]
    }
    
    add(value) {
        this.heap.push(value)
        this.heapifyUp()
    }
    
    heapifyUp() {
        let index = this.size() - 1
        while(index > 0) {
            let parentIndex = this.getParent(index)
            if (this.heap[index][1] < this.heap[parentIndex][1]) {
                this.swap(index, parentIndex)
                index = parentIndex
            } else {
                break
            }
        }
    }
    
    runTask() {
        if (this.size() === 0) return null
        if (this.size() === 1) return this.heap.pop()
        
        const root = this.heap[0]
        this.heap[0] = this.heap.pop()
        this.heapifyDown()
        return root
    }
    
    heapifyDown() {
        const length = this.size()
        let index = 0
        while (this.getLeftChild(index) < length) {
            let smallest = this.getLeftChild(index)
            let rightIndex = this.getRightChild(index)
            if(rightIndex < length && this.heap[rightIndex][1] < this.heap[smallest][1]) {
                smallest = rightIndex
            }
            if (this.heap[index][1] > this.heap[smallest][1]) {
                this.swap(index, smallest)
                index = smallest
            } else {
                break
            }
        }
    }
    
    peek() {
        return this.heap[0]
    }
        
    size() {
        return this.heap.length
    }
}
```

### 풀이를 마치고
처음에는 heap에서 한번에 정렬하고 순차적으로 빼면서 처리할 수 있도록 heap을 구현하려다 보니 어려움을 겪었다.
`해결 방안` : 먼저 작업이 들어온 순으로 정렬하고 조건을 만족(현재 실행 가능)하는 작업들만 heap에 넣어서 새로운 조건에 따라 정렬한 뒤, 가장 우선순위에 있는 작업을 실행.

heap에서 순서를 한 번에 정렬하는 것이 아니라 heap의 본질에 따라
특정 값을 넣어서 최소값이 가장 앞에 올 수 있도록 정렬하는 용도로 사용해야 한다.

**내가 필요한 알고리즘의 본질을 파악하고 용도에 맞게 도구로써 활용하자**

## Lv. 3 기둥과 보 설치
### 문제
빙하가 깨지면서 스노우타운에 떠내려 온 **"죠르디"**는 인생 2막을 위해 주택 건축사업에 뛰어들기로 결심하였습니다. "죠르디"는 **기둥과 보**를 이용하여 벽면 구조물을 자동으로 세우는 로봇을 개발할 계획인데, 그에 앞서 로봇의 동작을 시뮬레이션 할 수 있는 프로그램을 만들고 있습니다.  
프로그램은 **2차원 가상 벽면**에 기둥과 보를 이용한 구조물을 설치할 수 있는데, 기둥과 보는 **길이가 1인 선분**으로 표현되며 다음과 같은 규칙을 가지고 있습니다.

- 기둥은 바닥 위에 있거나 보의 한쪽 끝 부분 위에 있거나, 또는 다른 기둥 위에 있어야 합니다.
- 보는 한쪽 끝 부분이 기둥 위에 있거나, 또는 양쪽 끝 부분이 다른 보와 동시에 연결되어 있어야 합니다.

단, 바닥은 벽면의 맨 아래 지면을 말합니다.

2차원 벽면은 **`n x n`** 크기 정사각 격자 형태이며, 각 격자는 **`1 x 1`** 크기입니다. 맨 처음 벽면은 비어있는 상태입니다. 기둥과 보는 격자선의 교차점에 걸치지 않고, 격자 칸의 각 변에 정확히 일치하도록 설치할 수 있습니다. 다음은 기둥과 보를 설치해 구조물을 만든 예시입니다.

![기둥과보-1.jpg](https://grepp-programmers.s3.amazonaws.com/files/production/c453630fa0/834b86e5-6fd0-4d3c-8023-7f853ea4301f.jpg)

예를 들어, 위 그림은 다음 순서에 따라 구조물을 만들었습니다.

1. (1, 0)에서 위쪽으로 기둥을 하나 설치 후, (1, 1)에서 오른쪽으로 보를 하나 만듭니다.
2. (2, 1)에서 위쪽으로 기둥을 하나 설치 후, (2, 2)에서 오른쪽으로 보를 하나 만듭니다.
3. (5, 0)에서 위쪽으로 기둥을 하나 설치 후, (5, 1)에서 위쪽으로 기둥을 하나 더 설치합니다.
4. (4, 2)에서 오른쪽으로 보를 설치 후, (3, 2)에서 오른쪽으로 보를 설치합니다.

만약 (4, 2)에서 오른쪽으로 보를 먼저 설치하지 않고, (3, 2)에서 오른쪽으로 보를 설치하려 한다면 2번 규칙에 맞지 않으므로 설치가 되지 않습니다. 기둥과 보를 삭제하는 기능도 있는데 기둥과 보를 삭제한 후에 남은 기둥과 보들 또한 위 규칙을 만족해야 합니다. 만약, 작업을 수행한 결과가 조건을 만족하지 않는다면 해당 작업은 무시됩니다.

벽면의 크기 n, 기둥과 보를 설치하거나 삭제하는 작업이 순서대로 담긴 2차원 배열 build_frame이 매개변수로 주어질 때, 모든 명령어를 수행한 후 구조물의 상태를 return 하도록 solution 함수를 완성해주세요.

### 제한사항

- n은 5 이상 100 이하인 자연수입니다.
- build_frame의 세로(행) 길이는 1 이상 1,000 이하입니다.
- build_frame의 가로(열) 길이는 4입니다.
- build_frame의 원소는 [x, y, a, b]형태입니다.
    - x, y는 기둥, 보를 설치 또는 삭제할 교차점의 좌표이며, [가로 좌표, 세로 좌표] 형태입니다.
    - a는 설치 또는 삭제할 구조물의 종류를 나타내며, 0은 기둥, 1은 보를 나타냅니다.
    - b는 구조물을 설치할 지, 혹은 삭제할 지를 나타내며 0은 삭제, 1은 설치를 나타냅니다.
    - 벽면을 벗어나게 기둥, 보를 설치하는 경우는 없습니다.
    - 바닥에 보를 설치 하는 경우는 없습니다.
- 구조물은 교차점 좌표를 기준으로 보는 오른쪽, 기둥은 위쪽 방향으로 설치 또는 삭제합니다.
- 구조물이 겹치도록 설치하는 경우와, 없는 구조물을 삭제하는 경우는 입력으로 주어지지 않습니다.
- 최종 구조물의 상태는 아래 규칙에 맞춰 return 해주세요.
    - return 하는 배열은 가로(열) 길이가 3인 2차원 배열로, 각 구조물의 좌표를 담고있어야 합니다.
    - return 하는 배열의 원소는 [x, y, a] 형식입니다.
    - x, y는 기둥, 보의 교차점 좌표이며, [가로 좌표, 세로 좌표] 형태입니다.
    - 기둥, 보는 교차점 좌표를 기준으로 오른쪽, 또는 위쪽 방향으로 설치되어 있음을 나타냅니다.
    - a는 구조물의 종류를 나타내며, 0은 기둥, 1은 보를 나타냅니다.
    - return 하는 배열은 x좌표 기준으로 오름차순 정렬하며, x좌표가 같을 경우 y좌표 기준으로 오름차순 정렬해주세요.
    - x, y좌표가 모두 같은 경우 기둥이 보보다 앞에 오면 됩니다.

### 입출력 예

|n|build_frame|result|
|---|---|---|
|5|[[1,0,0,1],[1,1,1,1],[2,1,0,1],[2,2,1,1],[5,0,0,1],[5,1,0,1],[4,2,1,1],[3,2,1,1]]|[[1,0,0],[1,1,1],[2,1,0],[2,2,1],[3,2,1],[4,2,1],[5,0,0],[5,1,0]]|
|5|[[0,0,0,1],[2,0,0,1],[4,0,0,1],[0,1,1,1],[1,1,1,1],[2,1,1,1],[3,1,1,1],[2,0,0,0],[1,1,1,0],[2,2,0,1]]|[[0,0,0],[0,1,1],[1,1,1],[2,1,1],[3,1,1],[4,0,0]]|

---

### 문제 풀이
#### 풀이 과정
**조건**
벽면을 벗어나게 설치하는 경우 X => 맵 벗어나는지 체크 안해도 됨
바닥에 보를 설치하는 경우 X => 높이0에서 설치하는 거면 무조건 기둥
겹치는 설치, 없는 구조물 삭제 하는 경우 X

**설치 삭제 로직**
보 : 좌표 기준 오른쪽 방향
기둥 : 좌표 기준 위쪽 방향
기동 아래에 보가 없거나 보 아래에 기둥이 없으면 설치 불가. => 해당 작업 무시

최종 데이터 (각 구조물들의 위치)
`[x좌표, y좌표, 기동0 or 보1]`
구조물이 위치한 좌표만 모아서 2차원 배열로 반환
정렬 : x좌표 낮은 값 -> y좌표 낮은 값 -> 기둥인 값 우선

**풀이**
2중 for문으로 구현
좌표를 나타내는 배열을 만들고,
조건을 만족하면 설치 or 삭제
조건을 만족못하면 무시

**조건 만족하는지 판별**
`기둥인 경우` : 해당 좌표 또는 해당 좌표 x - 1에 보가 있는지 or 해당 좌표 y-1에 기둥이 있는지
`보인 경우` : 해당 좌표y-1 또는 해당 좌표 x + 1에 기둥이 있는지 or 해당 좌표 x-1과 x+1에 보가 있는지

**시간 복잡도**
n이 1000이므로 O(n^2) = 100만. 가능

build_frame
`[x좌표, y좌표, 구조물 종류, 설치 or 삭제]` 기둥0 보1 삭제0 설치1

#### 나의 코드
```
function solution(n, build_frame) {
    let lengthX = 0
    let lengthY = 0
    for (let order of build_frame) {
        if (order[0] > lengthX) lengthX = order[0]
        if (order[1] > lengthY) lengthY = order[1]
    }
    
    let stand = Array.from({ length : lengthX + 2}, () => Array.from({length : lengthY + 2}, () => false))
    let floor = Array.from({ length : lengthX + 2}, () => Array.from({length : lengthY + 2}, () => false))
    
    // 건물에 문제 없는지 검증하는 함수
    function validate(stand,floor) {
        let valid = true
        for(let y = 1; y < lengthY + 2; y ++) {
            for (let x = 1; x < lengthX + 2; x ++) {
                // 기둥 검증
                if (stand[x][y]) {
                    
                    if(y > 1 && !stand[x][y-1] && !floor[x][y] && !floor[x-1][y]) {
                        return false
                    }
                }
                // 바닥 검증
                if (floor[x][y]) {
                    if (!stand[x][y-1] && !stand[x+1][y-1]) {
                        if (!floor[x+1][y] || !floor[x-1][y]) {
                            return false
                        }
                    }
                }
            }
        }
        return true
    } // validate 함수 종료
    
    for(let i = 0; i < build_frame.length; i ++) {
        let [x, y, type, act] = build_frame[i]
        x ++
        y ++
        if (type === 0) stand[x][y] = act === 1 ? true : false
        else floor[x][y] = act === 1 ? true : false
        
        if (validate(stand,floor) === false) {
            if (type === 0) stand[x][y] = act === 1 ? false : true
            else floor[x][y] = act === 1 ? false : true
        }
    }
    
    let result = []
    
    for(let x = 1; x < lengthX + 2; x++) {
        for(let y = 1; y < lengthY + 2; y++) {
            if (stand[x][y]) result.push([x-1, y-1, 0])
            if (floor[x][y]) result.push([x-1, y-1, 1])
        }
    }
    
    return result
}
```


#### 정답 코드
```
function solution(n, build_frame) {
    let structures = new Set();

    // 구조물이 유효한지 검증하는 함수
    function isValid(structures) {
        for (let item of structures) {
            let [x, y, a] = item.split(',').map(Number);
            if (a === 0) { // 기둥
                if (y === 0 || // 바닥 위에 있거나
                    structures.has(`${x},${y-1},0`) || // 다른 기둥 위에 있거나
                    structures.has(`${x-1},${y},1`) || // 보의 오른쪽 끝에 있거나
                    structures.has(`${x},${y},1`) // 보의 왼쪽 끝에 있어야 함
                ) continue;
                return false;
            } else if (a === 1) { // 보
                if (structures.has(`${x},${y-1},0`) || // 한쪽 끝이 기둥 위에 있거나
                    structures.has(`${x+1},${y-1},0`) || // 한쪽 끝이 기둥 위에 있거나
                    (structures.has(`${x-1},${y},1`) && structures.has(`${x+1},${y},1`)) // 양쪽 끝이 다른 보와 동시에 연결되어 있어야 함
                ) continue;
                return false;
            }
        }
        return true;
    }

    // 명령어 처리
    for (let [x, y, a, b] of build_frame) {
        let key = `${x},${y},${a}`;
        if (b === 1) { // 설치
            structures.add(key);
            if (!isValid(structures)) structures.delete(key);
        } else { // 삭제
            structures.delete(key);
            if (!isValid(structures)) structures.add(key);
        }
    }

    // 결과를 배열로 변환하고 정렬
    let answer = Array.from(structures).map(e => e.split(',').map(Number));
    answer.sort((a, b) => a[0] - b[0] || a[1] - b[1] || a[2] - b[2]);

    return answer;
}
```

### 풀이를 마치고
최종으로 푼 풀이는 런타임 에러가 계속 발생해서 정답처리가 되지 않았다. 아무래도 최소값, 최대값을 구하는 과정과 배열의 크기가 커서 발생한 것 같다.
`해결 방안` : 배열에서 index를 통해 처리하는 것이 아니라, 데이터를 수정할 필요가 없기 때문에`set() `을 통해 처리하는게 더욱 효율적이다

x와 y가 0일 경우 x-1을 해줬을 때 오류나는 것을 방지하고자 기둥과 보의 길이를 1씩 늘려주고 한 칸씩 띄워서 계산했다. 이렇게 하니까 테스트 데이터와 비교하기도 복잡하고 로직을 설계하면서도 index가 계속 헷갈려서 골치아팠다. **앞으로 index는 임의로 추가하거나 빼서 계산하지 말고 예외 처리를 추가해주는 식으로 진행하자.**

구현 문제는 확실히 많이 풀어봐야 감이 잡힐 것 같다. 머릿속에서 구현하려고 하다보니 실수도 잦아지고 내가 무슨 로직을 짜고있는지도 헷갈렸다. **시간이 오래 걸리더라도 처음에 예외를 계산하면서 틀을 짜놓고 진행하자.** 처음에 틀을 잡는데 시간을 많이 소요했는데, 몇가지 예외 사항들을 고려하지 못해 다시 짜야하는 경우가 반복되어 시간이 배로 소요되었다.

**총 풀이 시간** `5시간 30분`


## Lv. 3 [최단 경로] 가장 먼 노드 [BFS로 복습 9/30]
### 📖  문제

n개의 노드가 있는 그래프가 있습니다. 각 노드는 1부터 n까지 번호가 적혀있습니다. 1번 노드에서 가장 멀리 떨어진 노드의 갯수를 구하려고 합니다. 가장 멀리 떨어진 노드란 최단경로로 이동했을 때 간선의 개수가 가장 많은 노드들을 의미합니다.

노드의 개수 n, 간선에 대한 정보가 담긴 2차원 배열 vertex가 매개변수로 주어질 때, 1번 노드로부터 가장 멀리 떨어진 노드가 몇 개인지를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 노드의 개수 n은 2 이상 20,000 이하입니다.
- 간선은 양방향이며 총 1개 이상 50,000개 이하의 간선이 있습니다.
- vertex 배열 각 행 [a, b]는 a번 노드와 b번 노드 사이에 간선이 있다는 의미입니다.

##### 입출력 예

|n|vertex|return|
|---|---|---|
|6|[[3, 6], [4, 3], [3, 2], [1, 3], [1, 2], [2, 4], [5, 2]]|3|

---

### 📌 풀이 방법

>주어진 edge배열을 adjency List(인접 리스트) 형태로 만들어준다.

>필요한 자료구조
>Array
>- visted (정점 방문 처리목적)
>- nodeCosts (노드별 비용 저장)
>Object
>- adj List (인접 노드 구분)
>동작 과정
>다익스트라로 최단 경로 모두 구하고 가장 큰 값들만 반환.

---

### 🖥️ 풀이 코드
```
// 다익스트라
function solution(n, edge) {
    const adjList = {}
    const nodeCosts = new Array(n+1).fill(Infinity)
    const visited = new Array(n+1).fill(false)
    for (let i = 1; i <= n; i++ ) {
        adjList[i] = []
        nodeCosts[i] = Infinity
    }
    
    for (let v of edge) {
        adjList[v[0]].push(v[1])
        adjList[v[1]].push(v[0])
    }
    
    // 초기값 설정
    nodeCosts[1] = 0
    let targetNode = 1
    let count = 1
    // 거리 계산
    while (count <= n) {
        visited[targetNode] = true
        let cost = nodeCosts[targetNode] + 1
        // 연결된 노드에 거리 업데이트
        for (let node of adjList[targetNode]) {
            if (nodeCosts[node] > cost) {
                nodeCosts[node] = cost
            }
        }
        targetNode = 0
        for (let i = 2; i <= n; i ++) {
            if (!visited[i] && nodeCosts[i] !== Infinity) {
                if (nodeCosts[targetNode] > nodeCosts[i]) {
                    targetNode = i
                }
            }
        }
        count ++
    }
    
    nodeCosts[0] = 0
    let maxDistance = Math.max(...nodeCosts)
    let result = nodeCosts.reduce((total, el) => {
        if (el === maxDistance) {
            return total + 1
        }
        else return total
    }, 0)
    
    return result
}
```

---

### 🔎 풀이를 마치고

> 1. 처음에 BFS로 해매다 최단 경로를 못구해서 2시간 가까이 걸림.
> 2. 다익스트라 개념을 다시 살펴보고 구현하니 30분 소요.

BFS로도 풀어보고 업로드 !

---

## Lv. 3 [그래프] 순위 [플로이드 - 워셜로 해결]
### 📖  문제



---

### 📌 풀이 방법

>

---

### 🖥️ 풀이 코드
```

```

---

### 🔎 풀이를 마치고

> 1. 


---

## Lv. 3 [BFS/DFS] 네트워크
### 📖  문제
###### 문제 설명

네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

##### 제한사항

- 컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
- 각 컴퓨터는 0부터 `n-1`인 정수로 표현합니다.
- i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
- computer[i][i]는 항상 1입니다.

##### 입출력 예

|n|computers|return|
|---|---|---|
|3|[[1, 1, 0], [1, 1, 0], [0, 0, 1]]|2|
|3|[[1, 1, 0], [1, 1, 1], [0, 1, 1]]|1|


---

### 📌 풀이 방법

>adj리스트로 변환하고, bfs를 통해 해결
>더이상 갈곳이 없을 때 마다, count를 1씩 올리고 새로운 대륙에서 시작.

---

### 🖥️ 풀이 코드
```
function solution(n, computers) {
    // 주어진 데이터 인접 리스트로 변환
    const adj = {}
    for (let r = 0; r < n; r ++) {
        adj[r+1] = []
        for (let c = 0; c < n; c ++) {
            if (c !== r && computers[r][c] === 1) {
                adj[r+1].push(c+1)
            }
        }
    }
    
    // BFS 탐색
    const visited = new Array(n + 1).fill(false)
    const bfs = (s) => {
        let queue = adj[s]
        visited[s] = true
        while (queue.length > 0) {
            let v = queue.shift()
            if (!visited[v]) {
                visited[v] = true
                queue.push(...adj[v])
            }
        }
    }
    
    // 새로운 대륙에서 시작점 찾기
    let result = 0
    for (let i = 1; i <= n; i ++) {
        if (!visited[i]) {
            result ++
            bfs(i)
        }
    }
    
    return result
}
```

---

### 🔎 풀이를 마치고

> 간단한 그래프 탐색 문제이다. 해당 데이터로는 그래프 연결 관계 파악이 헷갈려서 인접 리스트로 변환 후 탐색을 진행했다.

`풀이 시간 : 40분`

---

## Lv. 3 [DP] 정수 삼각형
### 📖  문제

![스크린샷 2018-09-14 오후 5.44.19.png](https://grepp-programmers.s3.amazonaws.com/files/production/97ec02cc39/296a0863-a418-431d-9e8c-e57f7a9722ac.png)

위와 같은 삼각형의 꼭대기에서 바닥까지 이어지는 경로 중, 거쳐간 숫자의 합이 가장 큰 경우를 찾아보려고 합니다. 아래 칸으로 이동할 때는 대각선 방향으로 한 칸 오른쪽 또는 왼쪽으로만 이동 가능합니다. 예를 들어 3에서는 그 아래칸의 8 또는 1로만 이동이 가능합니다.

삼각형의 정보가 담긴 배열 triangle이 매개변수로 주어질 때, 거쳐간 숫자의 최댓값을 return 하도록 solution 함수를 완성하세요.

##### 제한사항

- 삼각형의 높이는 1 이상 500 이하입니다.
- 삼각형을 이루고 있는 숫자는 0 이상 9,999 이하의 정수입니다.

##### 입출력 예

|triangle|result|
|---|---|
|[[7], [3, 8], [8, 1, 0], [2, 7, 4, 4], [4, 5, 2, 6, 5]]|30|

---

### 📌 풀이 방법

**동적 프로그래밍(Dynamic Programming)** 은 총 5가지 단계를 통해 해결할 수 있다.

1. **하위 문제 정의**
2. **해법 일부분 추측**
3. **하위 문제의 풀이 연관짓기** 
4. **상향식 또는 하향식으로 코드 구현(검증)**
5. **원래 문제를 풀 수 있는지 확인**

위의 **5가지 단계**는 반드시 순차적으로 이루어질 필요는 없지만 이번 문제에서는 순차적으로 구현해도 문제가 없기에 5가지 단계를 따라 문제를 살펴보자.

1. **하위 문제 정의하기**
	해당 문제는 삼각형의 맨 꼭대기에서 한 칸씩 내려가거나, 맨 아래부터 한 칸씩 올라오며 최대값을 구하는 문제이다.
	그러므로 **하위 문제는** 현재 위치 `[i, j]`에서 두 가지 선택지(왼쪽or오른쪽 아래)중 더 큰 값을 선택하여 현재 위치의 값과 더하는 것이다.

2. **해법의 일부분 추측하기**
	우리는 최대값을 가지는 `dp[0][0]`의 값을 구할 것이다. 그러기 위해 `dp[i][j]`의 값을 구하기 위해서는 `dp[i+1][j]`와 `dp[i+1][j+1]`의 값이 필요하다. 즉, 한 단계 아래에서 고를 수 있는 두 개의 값 중 최댓값을 현재의 값에 더해주면 된다.

3. **하위 문제의 풀이 연관 짓기**
	이 단계에서 각 하위 문제를 서로 어떻게 연결할 수 있는지 점화식을 구해볼 것이다.
	**점화식** : `dp[i][j] = triangle[i][j] + Math.max(dp[i+1][j], dp[i+1][j+1]`
	- `(i, j)`위치에서의 최댓값은 해당 위치`(i, j)`의 값과 아래의 두 값중 최댓값의 합이다. 이를 통해 꼭대기에서부터 한 칸씩 내려가며 문제를 해결할 수 있다.

4. **코드 구현(검증)**
	 먼저 문제가 올바르게 해결될 수 있는지 두 가지를 검증해야 한다.
	 1) 문제가 비순환적인가 ?
		- 순환 cycle이 있는 경우 코드가 무한으로 반복될 가능성이 있다. 해당 삼각형에서는 아래로만 이동하기 때문에 같은 위치로 다시 되돌아 올 경로가 없어 비순환적이다.
	 2) 올바른 위상학적 순서를 갖고 있는가 ?
		 - 꼭대기에서부터 바닥향하는 경로이므로 순서가 명확하여 위상학적 순서를 만족한다고 볼 수 있다.
	
	 일반적으로 상향식(Bottom - Up)은 for문을 통해, 하향식(Top - Down)은 재귀와 메모이제이션을 통해 구현한다. 그럼 각 방식에 따른 코드를 살펴보자.

*상향식(Bottom - Up) 구현*
```
function solution(triangle) {
    for (let i = triangle.length - 2; i >= 0; i --) {
        for (let j = 0; j < triangle[i].length; j ++) {
            triangle[i][j] += Math.max(triangle[i+1][j], triangle[i+1][j+1])
        }
    }
    
    return triangle[0][0]
}
```

*하향식(Top - Down) 구현*
```
function solution(triangle) {
    const memo = Array.from({ length: triangle.length }, (_, i) => Array(triangle[i].length).fill(-1));
    function dfs(row, col) {
        // 삼각형의 바닥까지 도달했으면 해당 값 반환
        if (row === triangle.length - 1) return triangle[row][col];
        
        // 이미 계산된 값이 있으면 그 값을 사용
        if (memo[row][col] !== -1) return memo[row][col];
        
        // 왼쪽 아래, 오른쪽 아래로 이동하여 최대값을 재귀적으로 계산
        const left = dfs(row + 1, col);
        const right = dfs(row + 1, col + 1);
        
        // 현재 위치에서의 최대 경로 합 저장
        memo[row][col] = triangle[row][col] + Math.max(left, right);
        
        return memo[row][col];
    }
    
    // 꼭대기에서 시작
    return dfs(0, 0);
}
```


5. **원래 문제를 풀 수 있는지 확인**
	 `dp[0][0]`은 삼각형 꼭대기에서 시작해 바닥까지 가는 경로 중 최대 합을 의미한다. 해당 값이 구해지면 원래 문제를 해결한 것이 된다.
	 또한 각 하위 문제의 풀이가 최종적으로 원래 문제의 해답(삼각형의 최댓값)을 찾는데 기여하므로 원래 문제를 해결하기에 적합하다.


---


### 🔎 풀이를 마치고

반복문으로 구현하는 것은 직관적이라 생각하기 어렵지 않지만, 재귀로 구현하는 것은 세부 과정이 명확하게 보이지 않아 조금 더 헷갈리는 경향이 있다.

---

## Lv. 3 [DP] 등굣길
### 📖  문제

계속되는 폭우로 일부 지역이 물에 잠겼습니다. 물에 잠기지 않은 지역을 통해 학교를 가려고 합니다. 집에서 학교까지 가는 길은 m x n 크기의 격자모양으로 나타낼 수 있습니다.

아래 그림은 m = 4, n = 3 인 경우입니다.

![image0.png](https://grepp-programmers.s3.amazonaws.com/files/ybm/056f54e618/f167a3bc-e140-4fa8-a8f8-326a99e0f567.png)

가장 왼쪽 위, 즉 집이 있는 곳의 좌표는 (1, 1)로 나타내고 가장 오른쪽 아래, 즉 학교가 있는 곳의 좌표는 (m, n)으로 나타냅니다.

격자의 크기 m, n과 물이 잠긴 지역의 좌표를 담은 2차원 배열 puddles이 매개변수로 주어집니다. **오른쪽과 아래쪽으로만 움직여** 집에서 학교까지 갈 수 있는 최단경로의 개수를 1,000,000,007로 나눈 나머지를 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 격자의 크기 m, n은 1 이상 100 이하인 자연수입니다.
    - m과 n이 모두 1인 경우는 입력으로 주어지지 않습니다.
- 물에 잠긴 지역은 0개 이상 10개 이하입니다.
- 집과 학교가 물에 잠긴 경우는 입력으로 주어지지 않습니다.

##### 입출력 예

|m|n|puddles|return|
|---|---|---|---|
|4|3|[[2, 2]]|4|

---

### 📌 풀이 방법

**문제 정의**
목표 지점 v까지의 최단 경로 개수

**하위 문제**
i,j의 칸에 해당 칸으로 갈 수 있는 위, 왼쪽칸에 갈 수 있는 경우의 수를 더해준다.

**추측**
도착 지점과 맞 닿아있는 지점의 도착할 수 있는 경우의 수를 구한다.

**하위문제와 해결방안 연결 (점화식 세우기)**
DP(i,j) = DP(i-1, j) + DP(i, j-1)

**알고리즘 구현(검증)**

오른쪽, 아래로만 이동하므로 비순환적인 위상 순서를 만족한다.

**원래 문제 풀기**
도착 지점까지 이동하고, 도착가능한 경우는 모두 최단 경로이다.

---

### 🖥️ 풀이 코드
```
function solution(m, n, puddles) {
    const dp = Array.from({length : n + 1}, () => Array(m + 1).fill(0))
    dp[1][1] = 1
    
    const checkPuddle = (i,j) => {
        for (let [y,x] of puddles) {
            if (i === x && j === y) {
                return true
            }
        }
        return false
    }
    
    for (let i = 1; i < n + 1; i ++) {
        for (let j = 1; j < m + 1; j ++) {
            if (checkPuddle(i,j)) {
                continue
            }
            else {
                dp[i][j] += dp[i - 1][j] + dp[i][j - 1] % 1000000007
            }
            
        }
    }
    return dp[n][m] % 1000000007
}
```

---

### 🔎 풀이를 마치고

> 1. puddles의 좌표가 반대로 되어 있었다는 사실을 알아채지 못해서 꽤나 오랜 시간동안 헤맸다. 처음에 m * n으로 이루어진 보드를 n * m으로 변환할 때 꼼꼼하게 체크했어야 했다. 다음부터 문제의 열, 행과 코드의 열, 행이 달라질 경우 모든 경우를 꼼꼼히 체크하자.


---

## Lv. 3 [DP] N으로 표현 [9/29 복습]
### 📖  문제

아래와 같이 5와 사칙연산만으로 12를 표현할 수 있습니다.

12 = 5 + 5 + (5 / 5) + (5 / 5)  
12 = 55 / 5 + 5 / 5  
12 = (55 + 5) / 5

5를 사용한 횟수는 각각 6,5,4 입니다. 그리고 이중 가장 작은 경우는 4입니다.  
이처럼 숫자 N과 number가 주어질 때, N과 사칙연산만 사용해서 표현 할 수 있는 방법 중 N 사용횟수의 최솟값을 return 하도록 solution 함수를 작성하세요.

##### 제한사항

- N은 1 이상 9 이하입니다.
- number는 1 이상 32,000 이하입니다.
- 수식에는 괄호와 사칙연산만 가능하며 나누기 연산에서 나머지는 무시합니다.
- 최솟값이 8보다 크면 -1을 return 합니다.

##### 입출력 예

|N|number|return|
|---|---|---|
|5|12|4|
|2|11|3|

---

### 📌 풀이 방법

**문제 정의**
N을 사용해서 number를 만들 수 있는 최소 사용 횟수를 구해라.

**하위 문제**
number가 되는 연산이 무엇인가 ?

**추측**
연산을 통해 만들어질 다음 값
추측의 개수는 연산의 개수인 총 4가지 + '-'와 '/'의 반대 순서 2가지 = 총 6가지와
자리수 7자리 부터 1자리까지 하여 7 * 6 = 42가지

**하위 문제와 해 연결(점화식)**
DP(n, count) = n 연산자 n

**알고리즘 구현(검증)**
상향식으로 구현

8번의 연산이 되면 끝이므로 명확한 종료 지점 존재하며, 모든 연산을 통해 위상 순서를 만족한다.

---

### 🖥️ 풀이 코드
```
function solution(N, number) {
    // 연산자와 연산 함수
    const operators = ['*', '+', '/', '-', '--', '//']
    const calculator = (k, op, num) => {
        if (op === '*') return k * num
        if (op === '/') return Math.floor(k / num)
        if (op === '+') return k + num
        if (op === '-') return k - num
        // 빼기와 나누기의 경우 순서에 따라 결과가 달라지는 부분 고려
        if (op === '--') return num - k
        if (op === '//') return Math.floor(num / k)
    }
    
    // N의 개수 별로 배열 생성
    const nArray = [0]
    for (let i = 1; i < 8; i ++) {
        nArray.push(parseInt(N.toString().repeat(i)))
    }
    
    let minCount = 9
    // DP함수 로직
    function dp(k, count) {
        if (k === number) {
            minCount = Math.min(minCount, count)
            return
        }
        if (count > 8) {
            return
        }
        for (let op of operators) {
            for (let j = 1; j < Math.min(9, 9 - count); j ++) {
                let calK = calculator(k,op, nArray[j])
                dp(calK, count + j)
            }
        }
    }
    // DP 실행
    for (let i = 1; i <= 7; i++) {
        dp(nArray[i], i)
    }
    
    // 최솟값이 8 초과인 경우 -1 반환
    if (minCount > 8) minCount = -1
    
    return minCount
}
```

---

### 🔎 풀이를 마치고

연산의 종류가 단순 4가지가 아닌, 순서에 따라 달라지는 경우를 고려하여 총 6가지(나누기와 빼기의 반대 순서 계산 추가)를 파악하는 부분이 중요하다.

---

## Lv. 3 단어 변환
### 📖  문제

두 개의 단어 begin, target과 단어의 집합 words가 있습니다. 아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.

```
1. 한 번에 한 개의 알파벳만 바꿀 수 있습니다.
2. words에 있는 단어로만 변환할 수 있습니다.
```

예를 들어 begin이 "hit", target가 "cog", words가 ["hot","dot","dog","lot","log","cog"]라면 "hit" -> "hot" -> "dot" -> "dog" -> "cog"와 같이 4단계를 거쳐 변환할 수 있습니다.

두 개의 단어 begin, target과 단어의 집합 words가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 begin을 target으로 변환할 수 있는지 return 하도록 solution 함수를 작성해주세요.

##### 제한사항

- 각 단어는 알파벳 소문자로만 이루어져 있습니다.
- 각 단어의 길이는 3 이상 10 이하이며 모든 단어의 길이는 같습니다.
- words에는 3개 이상 50개 이하의 단어가 있으며 중복되는 단어는 없습니다.
- begin과 target은 같지 않습니다.
- 변환할 수 없는 경우에는 0를 return 합니다.

##### 입출력 예

| begin | target | words                                      | return |
| ----- | ------ | ------------------------------------------ | ------ |
| "hit" | "cog"  | ["hot", "dot", "dog", "lot", "log", "cog"] | 4      |
| "hit" | "cog"  | ["hot", "dot", "dog", "lot", "log"]        | 0      |

---

### 📌 풀이 방법

주어진 텍스트를 목표 텍스트로 변환할 수 있는 최소 횟수 반환.
텍스트는 words안에 있는 텍스트로만 하나의 알파벳씩만 변환 가능.

**제한 사항**
주어진 단어의 길이 3 이상 10 이하
words.length <= 50

**풀이**
words배열을 그래프라고 생각해보자.
알파벳을 하나씩만 변경할 수 있으므로, 알파벳 한 개만 다른 노드끼리 연결되어 있는 형식이다.
결과적으로 target에 도달해야 하므로, target으로 갈 수 있는 최소 거리를 찾으면 된다.
만약 목표 지점까지의 그래프가 연결되어 있지 않거나, 목표 지점이 없다면 불가능이므로 0을 반환한다.

단어들 간의 방향 그래프를 만들고, BFS를 통해 해결할 것이다.
코드를 작성하기에 앞서, 시간복잡도를 벗어나지 않는지 확인해보자.

**시간 복잡도 확인**
단어의 개수를 n, 길이를 l로 가정하자.
우선 주어진 배열을 통해 인접 리스트로 만들 것이다.
인접 리스트를 만들기 위해서는, words의 문자를 서로 하나하나 비교해봐야 한다.
단어를 다른 단어와 비교하는데 걸리는 시간은 단어의 길이인 l.
해당 작업을 n개의 단어와 비교하면 하나의 단어에 nl의 시간이 소요된다.
이를 모든 단어에 각각 실행해주면 인접리스트 제작에는 O(n^2 * l)의 시간이 걸린다.

주어진 인접리스트를 통해 그래프의 모든 간선을 탐색하려면 O(V + E)의 시간이 걸리므로
충분히 가능하다.

**의사 코드**
1. 인접 리스트 만들기
    1.1 단어의 알파벳이 하나만 다른 경우만 연결
2. 인접 리스트를 통해 그래프 탐색하며 이동 횟수 저장
3. target을 만나면 최소 이동 횟수 반환
4. 인접 리스트를 모두 방문했는데 target을 만나지 못했을 경우, 0 반환.

---

### 🖥️ 풀이 코드
```
function solution(begin, target, words) {
    // 변환 불가능한 경우 0 반환
    if (!words.includes(target)) {
        return 0
    }
    
    const allWords = [begin, ...words]
    const adjList = buildAdjacencyList(allWords)
    const visited = new Set()
    const queue = [{ word : begin, depth : 0 }]
    
    while (queue.length > 0) {
        const { word, depth } = queue.shift()
        
        if (word === target) {
            return depth
        }
        
        adjList[word].forEach((neighbor) => {
            if (!visited.has(neighbor)) {
                visited.add(neighbor);
                queue.push({ word: neighbor, depth: depth + 1 });
            }
        });
    }
    
    return 0
    
    function buildAdjacencyList(wordsArray) {
        return wordsArray.reduce((acc, word) => {
            acc[word] = wordsArray.filter((otherWord) => (
                word !== otherWord && isTransformed(word, otherWord)
            ));
            return acc
        }, {});
    }
    
    function isTransformed(word1, word2) {
        const diffCount = word1.split('').reduce((count, char, i) => (
            char !== word2[i] ? count + 1 : count
        ), 0) 
            
        return diffCount === 1
    }
}
```

---

### 🔎 풀이를 마치고

코드를 airbnb 스타일 가이드에 맞춰 작성했다.

**평소 작성하던 방식과 다른 부분**
1. for문을 지양하고 forEach, reduce 등 메서드 사용
2. 간단한 로직의 경우 화살표 함수를 사용해도 괜찮다
3. 처음에는 visited를 객체로 만들었는데, set으로 만드는게 로직이 간단하고 가독성이 좋다.

---


## Lv. 3 [!!작성 양식]
### 📖  문제



---

### 📌 풀이 방법

>

---

### 🖥️ 풀이 코드
```

```

---

### 🔎 풀이를 마치고

> 1. 


---


# 프로그래머스 Lv. 4
## Lv. 4 [DP] 도둑질
### 📖  문제
도둑이 어느 마을을 털 계획을 하고 있습니다. 이 마을의 모든 집들은 아래 그림과 같이 동그랗게 배치되어 있습니다.

![image.png](https://grepp-programmers.s3.amazonaws.com/files/ybm/e7dd4f51c3/a228c73d-1cbe-4d59-bb5d-833fd18d3382.png)

각 집들은 서로 인접한 집들과 방범장치가 연결되어 있기 때문에 인접한 두 집을 털면 경보가 울립니다.

각 집에 있는 돈이 담긴 배열 money가 주어질 때, 도둑이 훔칠 수 있는 돈의 최댓값을 return 하도록 solution 함수를 작성하세요.

##### 제한사항

- 이 마을에 있는 집은 3개 이상 1,000,000개 이하입니다.
- money 배열의 각 원소는 0 이상 1,000 이하인 정수입니다.

##### 입출력 예

|money|return|
|---|---|
|[1, 2, 3, 1]|4|

---

### 📌 풀이 방법

**문제 정리**
각각 떨어진 집을 털어서 얻을 수 있는 돈의 최댓값 구하기

>**DP의 5단계**
>1) 하위 문제 정의
>2) 해 일부분 추측
>3) 하위 문제와 해 연결
>4) 알고리즘 구성
>5) 원래 문제와 비교

DP문제를 해결하기 위해서는 위의 5단계를 따르면 보다 간단하게 해결할 수 있다.

5가지 단계는 순차적인 단계가 아니므로 실제 구현 순서로 다음과 같이 나타낼 수 있다.

>1. **문제 분석** : 주어진 문제를 부분 문제로 나누고, 부분 문제의 해결 방법 고민
>2. **점화식 도출** : 부분 문제 간의 관계를 정의하는 점화식 도출.
>3. **메모이제이션 구현 또는 바텀업 방식 구현** : 점화식을 바탕으로 `메모이제이션(재귀 호출)`을 구현하거나, `바텀업(반복문)` 방식으로 해결.
>4. **해결** : 점화식을 이용하여 문제를 해결하고, 필요에 따라 최적화 진행.



#### 1. 문제 분석
문제를 해결하기 위해서 알아야 할 일부분의 해는 무엇일까 ?
문제에서는 money의 최댓값을 얻기 위해 모든 집을 확인해 보아야 한다.
그러기 위해서 집에 방문했을 경우 해당 집을 털지 털지 않을지 결정해야 한다.

#### 2. 점화식 도출
**하위 문제 정의**
하위 문제는 해당 집을 털었을 때의 최적해와 털지 않았을 때의 최적해를 구하는 것이다.
모든 집을 중복 없이 1번씩 방문하므로 하위 문제의 개수 = n이다.

배열을 처음부터 순차적(위상적 순서)으로 방문했을 때,
**해당 집의 위치`i`에서 지금까지 누적된 money의 최대값**을 **`DP[i]`에 담는다**.
이를 점화식으로 표현하면 다음과 같다.
i = 0... n - 1
`DP[i] = Math.max(DP[i - 1], DP[i - 2] + money[i])`

점화식에 대해 설명을 추가하자면, DP[i - 1]은 해당 집을 털 지 않았을 경우의 최댓값이고,
money[i] + DP[i - 2]의 경우 해당 집을 털기로 결정했을 경우 바로 이전 집은 인접한 집이라 못털기 때문에 2칸 뒤의 집의 money 최댓값과 더해준다.

하위 문제당 연산 시간은 배열을 index를 통해 접근(O(1))과 간단한 연산으로 구성되어 있으므로 상수시간에 해결 가능하다.
그러므로 총 연산 시간은 하위 문제의 개수O(n)와 하위 문제의 연산 시간O(1)을 곱하여 O(n)의 시간을 얻을 수 있다.

#### 3. 메모이제이션 구현 또는 바텀업 방식 구현
알고리즘은 상향식(반복문), 하향식(재귀 & 메모이제이션) 두 가지로 구성할 수 있다.
문제에서는 처음 집부터 순차적으로 방문해나갈 것이므로 상향식으로 구현한다.
또한, 해당 알고리즘이 무한으로 반복되는 경우를 방지하기 위해서 비순환적, 위상적 순서를 만족하는지 살펴보아야 한다.

해당 문제에서 data는 배열로 주어지지만, 개념적으로는 원으로 이루어진 집이기 때문에 문제에서는 DP배열 2개를 만들어서 진행할 것이다.
2개를 만드는 이유는 처음 집과 마지막 집을 동시에 방문하는 경우를 방지해주기 위해서이다.
때문에 처음 집을 방문하는 경우에는 마지막 집을 0으로 처리해주고,
마지막 집을 방문하는 경우에는 처음 집을 0으로 처리해준다.

#### 4. 해결
문제에서는 원래 문제의 각 집들에 대해 해당 위치에서의 money의 최댓값을 구하므로,
결국 마지막 집에 도착하게 되면 문제에서 원하던 money의 최댓값을 얻는다.

---

### 🖥️ 풀이 코드
``` javascript
function solution(money) {
    if (money.length <= 3) {
        return Math.max(...money)
    }
    
    // 첫 번째 집 턴 경우 마지막 집 0 처리
    const DP1 = money.slice() // money배열 복사해오기
    DP1.unshift(0)// 배열 맨 앞에 0 삽입
    DP1[DP1.length - 1] = 0
    
    // 마지막 집 턴 경우 첫 번째 집 0 처리
    const DP2 = money.slice()
    DP2.push(0)
    DP2[0] = 0
    
    // DP[i]는 i번째 집의 money값이지만 인덱싱으로 인해 DP[i]로 지칭
    for(let i = 2; i < money.length + 1; i ++) {
        DP1[i] = Math.max(DP1[i - 1], DP1[i - 2] + DP1[i])
        DP2[i] = Math.max(DP2[i - 1], DP2[i - 2] + DP2[i])
    }
    
    return Math.max(DP1[DP1.length - 1], DP2[DP2.length - 1])
}
```

#### Swift 풀이
``` swift
func solution(_ money: [Int]) -> Int {
    if money.count <= 3 {
        return money.max() ?? 0
    }
    
    // 첫 번째 집을 털고 마지막은 안 터는 경우
    var dp1 = Array(money)
	dp2.insert(1, at: 0)
	dp1[dp1.count - 1] = 0  // 마지막 집은 털지 않음
	
    // 마지막 집을 털고 첫 번째는 안 터는 경우
    var dp2 = Array(money)
    dp2.append(o)
    dp2[0] = 0  // 첫 번째 집은 털지 않음
    
    for i in 2..< money.count {
	    dp1[i] = max(dp1[i - 1], dp1[i] + dp1[i - 2])
        dp2[i] = max(dp2[i - 1], dp2[i] + dp2[i - 2])
    }
    
    return max(dp1[dp1.count - 1], dp2[dp2.count - 1])
}
```

---

## Lv. 4 [!!작성 양식]
### 📖  문제



---

### 📌 풀이 방법

>

---

### 🖥️ 풀이 코드
```

```

---

### 🔎 풀이를 마치고

> 1. 


---

