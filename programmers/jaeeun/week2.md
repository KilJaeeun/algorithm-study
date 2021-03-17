##  월간코드 챌린지 시즌 1 3진법 뒤집기

### 문제 설명

자연수 n이 매개변수로 주어집니다. n을 3진법 상에서 앞뒤로 뒤집은 후, 이를 다시 10진법으로 표현한 수를 return 하도록 solution 함수를 완성해주세요.

------

### 제한사항

- n은 1 이상 100,000,000 이하인 자연수입니다.

------

### 입출력 예

| n    | result |
| ---- | ------ |
| 45   | 7      |



### 구현
```python
NOTATION = '0123456789ABCDEF' 
def numeral_system(number, base): 
    q, r = divmod(number, base) 
    n = NOTATION[r] 
    return numeral_system(q, base) + n if q else n


def solution(n):
    answer=0
    three_num = str(int(str(numeral_system(n, 3))[::-1]))
    for i in range(len(three_num)):
        answer+=int(three_num[i])*3**(len(three_num)-i-1)
    
    
    return answer
```



## 프로그래머스 완주하기 못한 선수



### 문제 설명

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

### 제한사항

- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.

### 입출력 예

| participant                                       | completion                               | return   |
| ------------------------------------------------- | ---------------------------------------- | -------- |
| ["leo", "kiki", "eden"]                           | ["eden", "kiki"]                         | "leo"    |
| ["marina", "josipa", "nikola", "vinko", "filipa"] | ["josipa", "filipa", "marina", "nikola"] | "vinko"  |
| ["mislav", "stanko", "mislav", "ana"]             | ["stanko", "ana", "mislav"]              | "mislav" |


### 구현
```python
import collections
def solution(participant, completion):
    answer = ''
    before = collections.Counter(participant)
    after = collections.Counter(completion)
    answer = list((before - after).elements())
    return answer[0]
```












## 2019 카카오 블라인드 실패율

* 문제 링크: https://programmers.co.kr/learn/courses/30/lessons/42889



![failture_rate1.png](https://grepp-programmers.s3.amazonaws.com/files/production/bde471d8ac/48ddf1cc-c4ea-499d-b431-9727ee799191.png)

슈퍼 게임 개발자 오렐리는 큰 고민에 빠졌다. 그녀가 만든 프랜즈 오천성이 대성공을 거뒀지만, 요즘 신규 사용자의 수가 급감한 것이다. 원인은 신규 사용자와 기존 사용자 사이에 스테이지 차이가 너무 큰 것이 문제였다.

이 문제를 어떻게 할까 고민 한 그녀는 동적으로 게임 시간을 늘려서 난이도를 조절하기로 했다. 역시 슈퍼 개발자라 대부분의 로직은 쉽게 구현했지만, 실패율을 구하는 부분에서 위기에 빠지고 말았다. 오렐리를 위해 실패율을 구하는 코드를 완성하라.

- 실패율은 다음과 같이 정의한다.
  - 스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수 / 스테이지에 도달한 플레이어 수

전체 스테이지의 개수 N, 게임을 이용하는 사용자가 현재 멈춰있는 스테이지의 번호가 담긴 배열 stages가 매개변수로 주어질 때, 실패율이 높은 스테이지부터 내림차순으로 스테이지의 번호가 담겨있는 배열을 return 하도록 solution 함수를 완성하라.

### 제한사항

- 스테이지의 개수 N은 `1` 이상 `500` 이하의 자연수이다.
- stages의 길이는 `1` 이상 `200,000` 이하이다.
- stages에는 1이상 N + 1이하의 자연수가 담겨있다.
  - 각 자연수는 사용자가 현재 도전 중인 스테이지의 번호를 나타낸다.
  - 단, `N + 1` 은 마지막 스테이지(N 번째 스테이지) 까지 클리어 한 사용자를 나타낸다.
- 만약 실패율이 같은 스테이지가 있다면 작은 번호의 스테이지가 먼저 오도록 하면 된다.
- 스테이지에 도달한 유저가 없는 경우 해당 스테이지의 실패율은 `0` 으로 정의한다.

### 입출력 예

| N    | stages                   | result      |
| ---- | ------------------------ | ----------- |
| 5    | [2, 1, 2, 6, 2, 4, 3, 3] | [3,4,2,1,5] |
| 4    | [4,4,4,4,4]              | [4,1,2,3]   |

### 구현

```python
import collections
def solution(N, stages):
    answer = []
    s=collections.Counter(stages)
    ss=sorted(s.items(),key=lambda a:-a[0])
    gosu=0
    ans=[[i+1,0] for i in range(N)]
    answer
    for i in ss:
        gosu+=i[1]
        if i[0]>N:
            continue
        ans[i[0]-1]= [i[0],i[1]/gosu]
    ans= sorted(ans, key=lambda a:(-a[1],a[0] ))
    answer=[]
    for i in ans:
        answer.append(i[0])
    return answer
```



## 2018 카카오 블라인드 다트 게임

* 문제 링크: https://programmers.co.kr/learn/courses/30/lessons/17682

카카오톡에 뜬 네 번째 별! 심심할 땐? 카카오톡 게임별~

![Game Star](http://t1.kakaocdn.net/welcome2018/gamestar.png)

카카오톡 게임별의 하반기 신규 서비스로 다트 게임을 출시하기로 했다. 다트 게임은 다트판에 다트를 세 차례 던져 그 점수의 합계로 실력을 겨루는 게임으로, 모두가 간단히 즐길 수 있다.
갓 입사한 무지는 코딩 실력을 인정받아 게임의 핵심 부분인 점수 계산 로직을 맡게 되었다. 다트 게임의 점수 계산 로직은 아래와 같다.

1. 다트 게임은 총 3번의 기회로 구성된다.
2. 각 기회마다 얻을 수 있는 점수는 0점에서 10점까지이다.
3. 점수와 함께 Single(`S`), Double(`D`), Triple(`T`) 영역이 존재하고 각 영역 당첨 시 점수에서 1제곱, 2제곱, 3제곱 (점수1 , 점수2 , 점수3 )으로 계산된다.
4. 옵션으로 스타상(`*`) , 아차상(`#`)이 존재하며 스타상(`*`) 당첨 시 해당 점수와 바로 전에 얻은 점수를 각 2배로 만든다. 아차상(`#`) 당첨 시 해당 점수는 마이너스된다.
5. 스타상(`*`)은 첫 번째 기회에서도 나올 수 있다. 이 경우 첫 번째 스타상(`*`)의 점수만 2배가 된다. (예제 4번 참고)
6. 스타상(`*`)의 효과는 다른 스타상(`*`)의 효과와 중첩될 수 있다. 이 경우 중첩된 스타상(`*`) 점수는 4배가 된다. (예제 4번 참고)
7. 스타상(`*`)의 효과는 아차상(`#`)의 효과와 중첩될 수 있다. 이 경우 중첩된 아차상(`#`)의 점수는 -2배가 된다. (예제 5번 참고)
8. Single(`S`), Double(`D`), Triple(`T`)은 점수마다 하나씩 존재한다.
9. 스타상(`*`), 아차상(`#`)은 점수마다 둘 중 하나만 존재할 수 있으며, 존재하지 않을 수도 있다.

0~10의 정수와 문자 S, D, T, *, #로 구성된 문자열이 입력될 시 총점수를 반환하는 함수를 작성하라.

### 입력 형식

"점수|보너스|[옵션]"으로 이루어진 문자열 3세트.
예) `1S2D*3T`

- 점수는 0에서 10 사이의 정수이다.
- 보너스는 S, D, T 중 하나이다.
- 옵선은 *이나 # 중 하나이며, 없을 수도 있다.

### 출력 형식

3번의 기회에서 얻은 점수 합계에 해당하는 정수값을 출력한다.
예) 37

### 입출력 예제

| 예제 | dartResult | answer | 설명                        |
| ---- | ---------- | ------ | --------------------------- |
| 1    | `1S2D*3T`  | 37     | 11 * 2 + 22 * 2 + 33        |
| 2    | `1D2S#10S` | 9      | 12 + 21 * (-1) + 101        |
| 3    | `1D2S0T`   | 3      | 12 + 21 + 03                |
| 4    | `1S*2T*3S` | 23     | 11 * 2 * 2 + 23 * 2 + 31    |
| 5    | `1D#2S*3S` | 5      | 12 * (-1) * 2 + 21 * 2 + 31 |
| 6    | `1T2D3D#`  | -4     | 13 + 22 + 32 * (-1)         |
| 7    | `1D2S3T*`  | 59     | 12 + 21 * 2 + 33 * 2        |


### 구현
```python

def solution(dartResult):
    stack = []
    dartResult = list(dartResult)
    lenDart = len(dartResult)
    index = 0
    answer = 0
    while index < lenDart:
        if dartResult[index] == "*":
            back = []
            if len(stack) > 0:
                back.append(2 * stack.pop())
            if len(stack) > 0:
                back.append(2 * stack.pop())
            while back:
                stack.append(back.pop())
            index += 1
            continue

        elif dartResult[index] == "#":
            if len(stack) > 0:
                stack.append(-1 * stack.pop())
            index += 1
            continue
        else:
            if dartResult[index + 1] != "S" and dartResult[index + 1] != "T" and dartResult[index + 1] != "D":
                index += 1
                dartResult[index] = 10
            if dartResult[index + 1] == "S":
                stack.append(int(dartResult[index]) ** 1)
                index += 2
            elif dartResult[index + 1] == "D":
                stack.append(int(dartResult[index]) ** 2)
                index += 2
            elif dartResult[index + 1] == "T":
                stack.append(int(dartResult[index]) ** 3)
                index += 2
    return sum(stack)
```





## [카카오 인턴] 키패드 누르기

*  문제 링크 : https://programmers.co.kr/learn/courses/30/lessons/67256
### 문제 설명
스마트폰 전화 키패드의 각 칸에 다음과 같이 숫자들이 적혀 있습니다.

![kakao_phone1.png](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/4b69a271-5f4a-4bf4-9ebf-6ebed5a02d8d/kakao_phone1.png)

이 전화 키패드에서 왼손과 오른손의 엄지손가락만을 이용해서 숫자만을 입력하려고 합니다.
맨 처음 왼손 엄지손가락은 * 키패드에 오른손 엄지손가락은 # 키패드 위치에서 시작하며, 엄지손가락을 사용하는 규칙은 다음과 같습니다.

엄지손가락은 상하좌우 4가지 방향으로만 이동할 수 있으며 키패드 이동 한 칸은 거리로 1에 해당합니다.
왼쪽 열의 3개의 숫자 1, 4, 7을 입력할 때는 왼손 엄지손가락을 사용합니다.
오른쪽 열의 3개의 숫자 3, 6, 9를 입력할 때는 오른손 엄지손가락을 사용합니다.
가운데 열의 4개의 숫자 2, 5, 8, 0을 입력할 때는 두 엄지손가락의 현재 키패드의 위치에서 더 가까운 엄지손가락을 사용합니다.
4-1. 만약 두 엄지손가락의 거리가 같다면, 오른손잡이는 오른손 엄지손가락, 왼손잡이는 왼손 엄지손가락을 사용합니다.
순서대로 누를 번호가 담긴 배열 numbers, 왼손잡이인지 오른손잡이인 지를 나타내는 문자열 hand가 매개변수로 주어질 때, 각 번호를 누른 엄지손가락이 왼손인 지 오른손인 지를 나타내는 연속된 문자열 형태로 return 하도록 solution 함수를 완성해주세요.

### 제한사항
numbers 배열의 크기는 1 이상 1,000 이하입니다.
numbers 배열 원소의 값은 0 이상 9 이하인 정수입니다.
hand는 "left" 또는 "right" 입니다.
"left"는 왼손잡이, "right"는 오른손잡이를 의미합니다.
왼손 엄지손가락을 사용한 경우는 L, 오른손 엄지손가락을 사용한 경우는 R을 순서대로 이어붙여 문자열 형태로 return 해주세요.

### 입출력 예
numbers	hand	result
[1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5]	"right"	"LRLLLRLLRRL"
[7, 0, 8, 2, 8, 3, 1, 5, 7, 6, 2]	"left"	"LRLLRRLLLRR"
[1, 2, 3, 4, 5, 6, 7, 8, 9, 0]	"right"	"LLRLLRLLRL"
### 구현
```python
def solution(numbers, hand):
    cellPhone = {
        1: [0, 0], 2: [0, 1], 3: [0, 2],
        4: [1, 0], 5: [1, 1], 6: [1, 2],
        7: [2, 0], 8: [2, 1], 9: [2, 2],
        '*': [3, 0], 0: [3, 1], '#': [3, 2]}
    person = {'left': [3, 0], 'right': [3, 2]}
    answer = ''

    def countDist(a, b):
        return abs(a[0] - b[0]) + abs(a[1] - b[1])

    for n in numbers:
        if n == 1 or n == 4 or n == 7:
            answer += 'L'
            person["left"] = cellPhone[n]
        elif n == 3 or n == 6 or n == 9:
            answer += "R"
            person["right"] = cellPhone[n]
        else:
            dist = cellPhone[n]
            leftCost = countDist(dist, person["left"])
            rightCost = countDist(dist, person["right"])
            if leftCost < rightCost:
                answer += 'L'
                person["left"] = cellPhone[n]
            elif rightCost < leftCost:
                answer += "R"
                person["right"] = cellPhone[n]
            else:
                if hand == "right":
                    answer += "R"
                    person["right"] = cellPhone[n]
                else:
                    answer += 'L'
                    person["left"] = cellPhone[n]

    return answer
```



---

## 소수 만들기

문제 링크: https://programmers.co.kr/learn/courses/30/lessons/12977

### 문제 설명

주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.

### 제한사항

- nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.
- nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.

### 구현
```python
import itertools
def solution(nums):
    isPrime=findPrime()
    num = itertools.combinations(nums,3)
    answer=0
    # 3000 이하의 소수 찾기
    for i in num:
        if isPrime[i[0]+i[1]+i[2]]:
            answer+=1
    return answer

def findPrime():
    isPrime =[1 for  i in range(3011)]
    isPrime[0],isPrime[1]=0,0
    index=2
    while index<3001:
        while isPrime[index]==0 and  index<3001: 
            index+=1
            
        if isPrime[index]==1:
            for i in range(index*2, 3001, index):
                isPrime[i]=0
        index+=1
    return isPrime
```





