# 모듈



## 표준모듈

* 표준모듈은 python에서 제공하는 모듈이다.



### Import(모듈 호출)

* 다른 파일에 정의된 변수,함수,객체 등을 사용하기 전에 이를 알리는 것

* 구조

  * `import 모듈 [as alias]`여기서 ` as alias`는 너무 긴 모듈이름을 짧게 부르기위해(생략가능)
  * `from 모듈 import 함수명` 모듈에서 필요한 함수만 불러오겠다.

  ```python
  math모듈 전부에서 불러올때
  import math
  print(math.sqrt(2))  # 1.414...
  
  math모듈에서 특정함수만 불러올때
  from math import sqrt, sin, cos
  print(sqrt(2))  # 1.414...
  
  # 서로다른 모듈에 같은이름의 함수를 두개다 쓰고 싶을때
  import A
  import B
  A.sum()
  B.sum()
  
  # 이렇게 많이씀
  imprt random as r
  r.random()
  
  import statistics as st
  
  score = [30, 40, 50, 60, 70, 80, 90]
  print(st.mean(score))
  print(st.harmonic_mean(score))
  print(st.median(score))
  print(st.median_low(score))
  print(st.median_high(score))
  ```



#### math 모듈

| 상수    | 설명                  |
| ------- | --------------------- |
| `pi :`  | 원주율 상수           |
| `tau :` | 원주율의 2배되는 상수 |
| `e :`   | 자연 대수 상수        |
| `inf :` | 무한대 값             |
| `nan :` | 숫자가 아닌 값을 의미 |

| 함수                     | 설명                                                        |
| ------------------------ | ----------------------------------------------------------- |
| `sqrt(x)`                | 제곱근                                                      |
| `pow(x,y)`               | x에 y승한 값                                                |
| `hypot(x,y)`             | `SQRT (x *x + y*y)`즉 지정한 좌표까지의 벡터의 크기         |
| `factorial(x)`           | 팩토리얼                                                    |
| `sin(x), cos(x), tan(x)` | 삼각함수                                                    |
| `degrees(x)`             | 각도                                                        |
| `radians(x)`             | 라디안                                                      |
| `ceil(x)`                | 올림                                                        |
| `floor(x)`               | 내림 0에 가깝게 내리는 것이 아니라 그냥 작은 값으로 내린다. |
| `fabs(x)`                | 절대값                                                      |
| `trunc(x)`               | 내림  0에 가깝게 내림                                       |
| `log(x, base)`           | base를 밑으로 가지는 log a                                  |
| `log10(x)`               | 10을 밑으로 가지는 로그                                     |
| `gcd(a, b)`              | 두수의 최대 공약수를 반환                                   |

#### 통계 모듈

| 함수               | 설명                                  |
| :----------------- | ------------------------------------- |
| `mean()`           | 평균                                  |
| `harmonic_mean()`  | 조화평균                              |
| `median()`         | 중앙값, 짝수인 경우 보간값 계산       |
| `median_low()`     | 중앙값을 구함, 집합 내의 낮은 값 선택 |
| `median_high()`    | 중앙값을 구함, 집합 내의 높은 값 선택 |
| `mdeian_grouped()` | 그룹 연속 중앙값                      |
| `mode()`           | 최빈값                                |
| `pstdev()`         | 모표준편차                            |
| `stddev()`         | 표준편차                              |
| `variance()`       | 분산                                  |



#### Time 모듈

* 1970년 1월 1일 자정을 기준으로 경과한 시간을 초 단위로 표현

```python
import time

t = time.time()
print(t)              # 1610022966.225918
print(time.ctime(t))  # Thu Jan  7 21:36:06 2021
print(time.localtime(t))
# time.struct_time
# (tm_year=2021, tm_mon=1, tm_mday=7, tm_hour=21, tm_min=36, tm_sec=6, tm_wday=3, tm_yday=7, tm_isdst=0)


# 현재시간은 t생략가능
t = time.localtime(t)
print(f'{t.tm_year}-{t.tm_mon}-{t.tm_mday}')  # 2021-1-7
print(f'{t.tm_hour}:{t.tm_min}:{t.tm_sec}')   # 21:36:6


from datetime import datetime as dt

now = dt.now()
print(f'{now.year}년 {now.month}월 {now.day}일')  # 2021년 1월 7일
print(f'{now.hour}:{now.minute}:{now.second}')   # 21:36:6
```

* 루프 시간측정

```python
import time

start = time.time()
for a in range(1000):
    print(a)       # I/O 작업 입출력작업은 오래걸림
end = time.time()

print(end-start)  # 0.1360311508178711


# 계산작업은 엄청빠르다.
total = 0
start = time.time()
# 1000번 루프돌며 계산
for a in range(1000):
    total += a
end = time.time()
print(end-start)  # 0.0

# 입출력을 줄여야 처리속도를 빠르게 할수있다.
```

* `time sleep` 실행 멈춤

```python
# 코딩 중간에 시간텀이 필요할 때

import time

print('안녕하세요.')
time.sleep(1)
print('밤에 성시경이 두 명 있으면 뭘까요?')
time.sleep(5)
print('야간투시경입니다.')
```

* time 포맷팅

  * `.strftime(포맷방식,시간함수())`

    | 포맷문자 | 설명       |
    | :------- | :--------- |
    | Y        | 4자리 년도 |
    | y        | 2자리 년도 |
    | m        | 월         |
    | d        | 일         |
    | H        | 시간(24H)  |
    | I        | 시간(12H)  |
    | M        | 분         |
    | S        | 초         |

    

```python
import time

timestr = time.strftime('%Y-%m-%d', time.localtime())
timestrHMS = time.strftime('%H:%M:%S')

print(timestr)    # 2021-01-07
print(timestrHMS) # 21:46:30
```



#### Random 모듈

| 함수                     | 설명                                                      |
| ------------------------ | --------------------------------------------------------- |
| `.random()`              | 0~1 사이의 난수 리턴                                      |
| `.randint(begin, end)`   | begin ~ end 사이의 정수 난수를 리턴 (end도 포함)          |
| `.randrange(begin, end)` | begin ~ end 사이의 정수 난수를 리턴 (end도 포함되지 않음) |
| `.uniform(begin, end)`   | begin ~ end 사이의 실수 난수를 리턴 (end 미포함)          |
| `.choice(시퀀스)`        | 시퀀스에서 랜덤하게 요소 선택하여 리턴                    |
| `.shuffle(시퀀스)`       | 시퀀스의 내용을 랜덤하게 섞음, 원본자체를 섞는다.         |
| `.sample(시퀀스, count)` | 시퀀스에서 랜덤하게 count개의 요소 리턴                   |

```python
1 .random
import random

for i in range(5):
	print(random.random())
# 0.9085194756407313
# 0.5157698060289099
# 0.6511156516629886
# 0.6844494104248139
# 0.07817243576575794

2 .randint(begin, end)
import random

for i in range(5):
	print(random.randint(1, 10))
# 3
# 3
# 10
# 4
# 5

3 .randrange(begin, end)
import random

for i in range(5):
	print(random.randrange(1, 10))
# 2
# 3
# 4
# 4
# 6

4 .choice(시퀸스)
import random

food = ["짜장면", "짬뽕", "탕수육", "군만두"]
print(random.choice(food))  # 탕수육

i = random.randrange(len(food))
print( food[i])   # 짜장면

5 .shuffle(시퀀스)
import random

food = ["짜장면", "짬뽕", "탕수육", "군만두"]
print(food)   # ['짜장면', '짬뽕', '탕수육', '군만두']

random.shuffle(food)
print(food)   # ['군만두', '탕수육', '짜장면', '짬뽕']

6 .sample(시퀀스, count)
import random
food = ["짜장면", "짬뽕", "탕수육", "군만두"]
print(random.sample(food, 2))
# ['짬뽕', '짜장면']

import random
nums = random.sample(range(1, 46), 6)
nums.sort()
print(nums)
# [5, 6, 17, 22, 28, 36]
```



#### sys 모듈

* 서버같은 장비들은 그래픽컬한 인터페이스를 제공 못함 그래서 문자로 입력해야함 그럴때 오류를 나타내준다.
* 입력받는 것들은 다 문자열 출력값도 문자열

```python
import sys

while True:
    ans = input('명령>')
    if ans == 'quit':
        sys.exit(0)       # 종료 상태 0: 정상적인 종료, 1: 메모리 부족, 2:데이터 오류

    print(ans)
    
    
import sys

print(sys.argv)
```

