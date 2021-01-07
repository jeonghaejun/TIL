# 컬렉션 관리



## 컬렉션 관리 함수



### Enumerate

* 구조 : `enumerate(시퀀스 [, start])`

  * 시퀀스의 인덱스와 요소를 튜플 묶어서 순회

  ```python
  race = ['저그', '테란', '프로토스']
  
  print(list(enumerate(race)))
  # [(0, '저그'), (1, '테란'), (2, '프로토스')]
  
  
  score = [88, 95, 70, 100, 99]
  
  for no, s in enumerate(score, 1):
      print(str(no)+'번 학생의 성적 :', s)
      
  # 1번 학생의 성적 : 88
  # 2번 학생의 성적 : 95
  # 3번 학생의 성적 : 70
  # 4번 학생의 성적 : 100
  # 5번 학생의 성적 : 99
  ```



### Zip

* 구조 : `zip(시퀀스1, 시퀀스2) -> [(값1, 값2), ... ]`

  * 시퀀스의 길이가 다른 경우 가장 짧은 시퀀스의 길이에 맞춤

  ```python
  # zip 두개의 다른 튜플을 서로 대응하는
  # 위치의 요소끼리 묵어서 튜플로 출력하는 함수
  # zip은 루프한번만 돌수있다. 계속 쓸려면 list로 묶어서 사용.(중요)
  
  dates = ['월', '화', '수', '목', '금', '토', '일']
  food = ['갈비탕', '순대국', '칼국수', '삼겹살']
  
  menu = list(zip(dates, food))    # zip를 list화 시킨거
  for d, f in menu:
      print("%s요일 메뉴: %s" % (d, f))
  
  
  # zip을 dict화 시키는거
  
  menu_dic = dict(zip(dates, food))
  print(menu_dic)
  # {'월': '갈비탕', '화': '순대국', '수': '칼국수', '목': '삼겹살'}
  ```

  * 예제 

  ```python
  info = """ 고길동 홍길동 둘리 도우너
  30 40 50 60
  70 90 60 56 78
  80 100 20 90 100
  30 40 50 60"""
  
  info_lines = info.splitlines()
  students = info_lines[0].split()      # key파트
  scores = info_lines[1:]
  print(scores)
  scores = [line.split() for line in scores]  # value파트
  print(scores)
  result = dict(zip(students, scores))
  print(result)
  
  # {'고길동': ['30', '40', '50', '60'],
  # '홍길동': ['70', '90', '60', '56', '78'],
  # '둘리': ['80', '100', '20', '90', '100'],
  # '도우너': ['30', '40', '50', '60']}
  
  # 아직 점수가 문자열이다 숫자로 바까야해 더배워서
  
  # append로도 가능 빈 dic에다가 append와 
  # for문을이용해서 집어넣는 과정 루프가 많아진다.
  ```



### Any,ALL

* 구조 : `any(시퀀스)`

  * 시퀀스에 하나라도 True가 있으면 True 리턴

* 구조 : `all(시퀀스)`

  * 시퀀스의 모든 요소가 True이면 True 리턴

  ```python
  adult = [True, False, True, False]
  
  print(any(adult))  # True
  print(all(adult))  # False
  ```

  

### Filter

* 구조 : `filter(판정함수, 시퀀스) -> 시퀀스`

  * 시퀸스의 각 요소를 판정함수에 전달하여 True를 리턴하는 요소로만 구성된 새로운 시퀸스 리턴

  ```python
  def flunk(s):
      return s < 60
  
  
  score = [45, 89, 72, 53, 94]
  for s in filter(flunk, score):
      print(s)
  
  # 45
  # 53
  ```

* Filter와 람다함수

  ```python
  # 람다함수
  
  score = [45, 89, 72, 53, 94]
  
  for s in filter(lambda s: s < 60, score):
      print(s)
  # 문장(statement)
  # 표현식(expression) --> 값
  
  # 방법.1
  score2 = list(filter(lambda a: a < 60, score)) # 람다함수 사용
  print(score2)
  
  # 방법.2 개인적으로 이게 편한 듯
  score2 = [n for n in score if n < 60]          # for-in-if
  print(score2)
  ```




### Map

* `map`함수는 매개변수로 함수를 넣어 전달하는 기능이 있다.

* functional programming(함수적 프로그래밍):` filter, map, sort`

  ```python
  def total(s, b):
      return s+b
  
  
  score = [45, 89, 72, 53, 94]
  bonus = [2, 3, 0, 0, 5]
  for s in map(total, score, bonus):
      print(s, end=", ")    # 47, 92, 72, 53, 99,
  ```

  ```python
  # score 리스트의 요소를 int로바꾸기 2가지 방법
  
  # 1. for와 enumerate 이용해서 바꾸기
  
  score = ['20', '30', '50', '90']
  score=[20,30,50,90]
  for ix, s in enumerate(score):
      score[ix] = int(s)
  
  print(score)    # [20, 30, 50, 90]
  
  # 2. map을 사용해서 바꾸기
  
  score = ['20', '30', '50', '90']
  
  score = list(map(int, score))
  print(score)    # [20, 30, 50, 90]
  ```

  

* `map`과 람다함수

  ```python
  # 람다함수
  # 한 줄로 정의되는 함수의 축약표현
  # 함수의 이름이 없다.
  # 변수에 직접 대입하여 사용.
  # 구조 lambda 인수:식
  
  score = [45, 89, 72, 53, 94]
  for s in map(lambda x: x/2, score):
      print(s, end=', ')  # 22.5, 44.5, 36.0, 26.5, 47.0,
  
  
  # 60점 이하인 성적이 포함되어있는지 판단하세요.
  # 과락 여부 판단
  score = [70, 90, 62, 56, 78]
  
  result = list(map(lambda x: x < 60, score))
  
  print(any(result))
  
  # 모든과목이 통과했냐?
  score = [70, 90, 62, 56, 78]
  
  result = list(map(lambda x: x >= 60, score))
  
  print(all(result))
  ```



### 리스트 사본

#### copy

* list는 참조형이기 때문에 전역저장소에 list가 저장되고 데이터는 mm에 heap에 저장된다.
* list를 부르면 참조값을 사용하여 heap에 저장된 데이터를 불러오는 정도이기 때문에 참조형이다.

```python
# 스택에 저장되는 데이터는 한번 저장되면 크기가 지정된다.

list1 = [1, 2, 3]
list2 = list1   # 기존의 list1의 참조값을 list2에 복사한다.
# 데이터를 복사한게 아니라 참조값을 복사한거

print(list1 == list2)  # True

list2[1] = 100    # heap에 있는 데이터를 바꿧다.

# 그러므로 list1의 데이터값이 바꿨기 때문에 밑에와 같은 결과가 나온다
print(list1)           # [1, 100, 3]
print(list2)           # [1, 100, 3]

print(list1 == list2)  # True

# 리스트 사본만들기
# .copy()메소드를 사용하여 만듬

list1 = [1, 2, 3]
list2 = list1.copy()

print(list1 == list2) # True 참조값이 아닌 데이터를 보고 비교한다.

list2[1] = 100
print(list1)  # [1, 2, 3]
print(list2)  # [1, 100, 3]

print(list1 == list2)  # False
```

* 요소하나를 바꾸면 바뀌고 함수를 만들어서 데이터 전체를 바꾸면 안바뀐다.

```python
def test1(a):
    a = 20

# 밑의 a와 위의 a는 다르다.
a = 10
test1(a)  # call by value
print(a)  # 10 -> 함수를 호출하고 계산값만 출력하고 사라지기때문에

def test2(l):
    l[0] = 20

l = [1, 2, 3]
test2(l)   # call by ref 참조를 불러서 요소를 바꿔서 원본이 바꼈다.
print(l)   # [20, 2, 3]
```

* 얕은 복사

```python
list0 = ['a', 'b']
list1 = [list0, 1, 2]
list2 = list1.copy()  # 얕은 복사 
                      # 데이터값이 전부 복사된것이 아니라 
                      # 참조도 있어서 나중에도 영향을 받는다.

list2[0][1] = 'c'
print(list1)  # [['a', 'c'], 1, 2]
print(list2)  # [['a', 'c'], 1, 2]
print(list0)  # ['a', 'c']
```

* 깊은 복사

```python
import copy

list0 = ['a', 'b']
list1 = [list0, 1, 2]
list2 = copy.deepcopy(list1) # 깊은 복사

list2[0][1] = 'c'
print(list1)  # [['a', 'b'], 1, 2]
print(list2)  # [['a', 'c'], 1, 2]


def test(l):
    l=[10,20,30]

l=[1,2,3]
test(l)
print(l)      # [1, 2, 3]
```



#### Is 연산자

* 두 변수가 같은 참조를 가지고 있는지 조사

```python
list1 = ['a', 'b']
list2 = list1
list3 = list1.copy() # 얕은 복사

print("list1 == list2", list1 is list2)
print("list1 == list3", list1 is list3)
print("list2 == list3", list2 is list3)

# list1 == list2 True
# list1 == list3 False
# list2 == list3 False
```



