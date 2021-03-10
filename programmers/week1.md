# 예산
문제 링크 : https://programmers.co.kr/learn/courses/30/lessons/12982  

**문제 내용**  
S사에서는 각 부서에 필요한 물품을 지원해 주기 위해 부서별로 물품을 구매하는데 필요한 금액을 조사했습니다. 그러나, 전체 예산이 정해져 있기 때문에 모든 부서의 물품을 구매해 줄 수는 없습니다. 그래서 최대한 많은 부서의 물품을 구매해 줄 수 있도록 하려고 합니다.

물품을 구매해 줄 때는 각 부서가 신청한 금액만큼을 모두 지원해 줘야 합니다. 예를 들어 1,000원을 신청한 부서에는 정확히 1,000원을 지원해야 하며, 1,000원보다 적은 금액을 지원해 줄 수는 없습니다.

부서별로 신청한 금액이 들어있는 배열 d와 예산 budget이 매개변수로 주어질 때, 최대 몇 개의 부서에 물품을 지원할 수 있는지 return 하도록 solution 함수를 완성해주세요.

**제한사항 **   
d는 부서별로 신청한 금액이 들어있는 배열이며, 길이(전체 부서의 개수)는 1 이상 100 이하입니다.
d의 각 원소는 부서별로 신청한 금액을 나타내며, 부서별 신청 금액은 1 이상 100,000 이하의 자연수입니다.
budget은 예산을 나타내며, 1 이상 10,000,000 이하의 자연수입니다.

**입출력 예**  
d	budget	result  
[1,3,2,5,4]	9	3  
[2,2,3,3]	10	4


**내가 푼 코드**  
주어진 예산에서 최대한 많은 물품을 구매하려면, 신청한 금액이 작은 것부터 처리하면 된다. 시간복잡도는 O(N)
```python
def solution(d, budget):
    answer = 0
    d.sort()
    for x in d:
        if budget >= x:
            answer+=1
            budget-=x
    return answer
```

# [1차] 비밀지도    
문제 링크 : https://programmers.co.kr/learn/courses/30/lessons/17681

**문제 내용**  
네오는 평소 프로도가 비상금을 숨겨놓는 장소를 알려줄 비밀지도를 손에 넣었다. 그런데 이 비밀지도는 숫자로 암호화되어 있어 위치를 확인하기 위해서는 암호를 해독해야 한다. 다행히 지도 암호를 해독할 방법을 적어놓은 메모도 함께 발견했다.

지도는 한 변의 길이가 n인 정사각형 배열 형태로, 각 칸은 "공백"(" ") 또는 "벽"("#") 두 종류로 이루어져 있다.
전체 지도는 두 장의 지도를 겹쳐서 얻을 수 있다. 각각 "지도 1"과 "지도 2"라고 하자. 지도 1 또는 지도 2 중 어느 하나라도 벽인 부분은 전체 지도에서도 벽이다. 지도 1과 지도 2에서 모두 공백인 부분은 전체 지도에서도 공백이다.
"지도 1"과 "지도 2"는 각각 정수 배열로 암호화되어 있다.
암호화된 배열은 지도의 각 가로줄에서 벽 부분을 1, 공백 부분을 0으로 부호화했을 때 얻어지는 이진수에 해당하는 값의 배열이다. 
![image](https://user-images.githubusercontent.com/43433753/110618315-f5ffcb00-81d9-11eb-88c2-ba1f9efce1e4.png)  
네오가 프로도의 비상금을 손에 넣을 수 있도록, 비밀지도의 암호를 해독하는 작업을 도와줄 프로그램을 작성하라.

입출력 예제  
매개변수	값  
n	5  
arr1	[9, 20, 28, 18, 11]  
arr2	[30, 1, 21, 17, 28]  
출력	["#####","# # #", "### #", "# ##", "#####"]  


**내가 푼 코드**  
두 지도에는 2진수로 저장되어 있는데, Input을 보면 10진수로 입력받고 있다.  
그래서 2진수로 변환 시켜줘야 하는데 이때 주의할점은 내장함수 bin()을 썼을 때
앞자리가 0이 오는 경우는 생략된 결과를 반환한다.  
적당한 슬라이싱과 필요한 0의 개수를 앞에 붙여준 뒤, 모두 1일 경우 '#'을, 모두 0일 경우엔 ' '을 넣어주면 된다. 구현한 코드의 시간복잡도는 O(N^2)이다.
```python
def solution(n, arr1, arr2):
    answer = []
    for idx in range(0,n):
        temp = bin(arr1[idx]) 
        arr1[idx] = temp[2:] if len(temp[2:]) == n else '0'*(n-len(temp[2:])) + temp[2:]
    for idx in range(0,n):
        temp = bin(arr2[idx]) 
        arr2[idx] = temp[2:] if len(temp[2:]) == n else '0'*(n-len(temp[2:])) + temp[2:]  
    for i in range(0,n):
        temp = ''
        for j in range(0,n):
            if arr1[i][j] == '1' or arr2[i][j] == '1':
                temp += '#'
            elif arr1[i][j] == '0' and arr2[i][j] == '0':
                temp += ' '
        answer.append(temp)
    return answer
```
**코드 풀이 리뷰**  
C++에서 파이썬으로 넘어온지 얼마 안돼 문법에서 시간을 좀 낭비했다. ㅠㅠ 두 지도의 값을 확인하여 조건을 만족하면 answer[i][j]에 '#' 또는 ' '을 대입할려고 했는데, answer이 빈 1차원 리스트로 정의되어 있기 때문에 index out of range가 발생한다. 그래서 한 줄이 끝날 때 answer리스트에 추가해주는 걸로 해결했다.

**알게된 것**  
파이썬에선 내장함수로 진법 변환 함수를 지원한다.
- 2진수로 변환 : bin() -> '0b'
- 8진수로 변환 : oct() -> '0o'
- 16진수로 변환 : hex() -> '0x'
- 10진수로 변환 : int('변환할 target',[target진법])
    ```python
    >>> print(bin(9))
    '0b1001'
    ```
진법에 따라 앞에 접두사가 붙으며, string type을 반환하기 때문에 필요에 따라 슬라이싱과 정수형변환(int)이 필요하다.
내가 푼 코드에서는 bin연산 뒤에 슬라이싱을 따로 했는데, `bin(값)[슬라이싱]` 도 가능하더라.

비트연산자를 사용한 다른 사람의 풀이도 봤는데, 처음 본 파이썬 내장함수들을 유용하게 사용했다.  

- **zip()**  
동일한 개수의 리스트를 묶어주는 함수
    ```python
    num = [1,2,3,4]
    name = ['su','ye','km','jx']
    for i, j in zip(num,name): #[(1,'su'),(2,'ye'),(3,'km'),(4,'jx')]
        ...
    ```
- **rjust()**  
문자열이 원하는 길이를 갖도록 문자열 앞에 문자 패딩을 추가해주는 함수
    ```python
    >>> val = '100'
    >>> val.rjust(5,'0')
    >>> print(val)
    '00100'
    ```  
- **replace()**  
문자열에서 해당되는 모든 값을 바꾼다.
    ```python
    >>> val = '11010'
    >>> val=val.replace('1','#')
    >>> val=val.replace('0',' ')
    >>> print(val)
    '## # '
    ```