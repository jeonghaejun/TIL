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

  