# 반복문



## while문

* 조건이 참인 동안 명령 블럭을 실행한다.

  ```python
  student = 1
  while student <= 5:
  print(student, "번 학생의 성정을 처리합니다.")
  student += 1
  
  1 번 학생의 성정을 처리합니다.
  2 번 학생의 성정을 처리합니다.
  3 번 학생의 성정을 처리합니다.
  4 번 학생의 성정을 처리합니다.
  5 번 학생의 성정을 처리합니다.
  
  num = 1
  total = 0
  while num <= 100:
      total += num
      num += 1
  print('total =', total)
  
  total = 5050
  
  # 1에서 100까지의 수에서
  
  # 짝수의 합 : XXXX
  # 홀수의 합 : yyyy
  
  num = 1
  xxxx = 0
  yyyy = 0
  
  # While 루프로 합계구하기
  while num <= 100:
      # num이 짝수인지 홀수인지 판단.
      if num % 2 == 0:  # 짝수이면
          xxxx += num
      else:  # 홀수이면
          yyyy += num
      num += 1
  
  print('짝수의 합 =', xxxx)
  print('홀수의 합 =', yyyy)
  
  while True:  # 무한 루프
      print('Hello world')
      ch = input('입력')
      if ch == 'Exit':
          break
          
  짝수의 합 = 2550
  홀수의 합 = 2500
  ```

  

## for 문

* 컬렉션의 요소를 하나씩 꺼내 명령 블럭을 실행

* 컬렉션의 모든 요소를 다 사용하면 반복을 끝냄

  ```python
  for student in [1, 2, 3, 4, 5]:
  print(student, "번 학생의 성적을 처리한다")
  
  1 번 학생의 성적을 처리한다
  2 번 학생의 성적을 처리한다
  3 번 학생의 성적을 처리한다
  4 번 학생의 성적을 처리한다
  5 번 학생의 성적을 처리한다
  ```

  ```python
  total = 0
  for num in range(1, 101):
      total += num
  
  print('total =', total)
  
  total = 5050
  ```

  ```python
  total = 0
  for num in range(2, 101, 2):
      total += num
  
  print('total =', total)
  
  total = 2550
  ```

  ```python
  for x in range(1, 51):
      if (x % 10) == 0:
          print('+', end='')
      else:
          print('-', end='')
  
  # 위에꺼랑 같은거
  
  for x in range(5):
      print('-'*9, end='')
      print('+', end='')
      
  ---------+---------+---------+---------+---------+
  ```

  

## break

* 반복문을 벗어나게 함

  ```python
  score = [92, 86, 68, 120, 56]
  for s in score:
  if( s < 0 ) or (s > 100):
  break
  print(s)
  print('성적 처리 끝')
  
  92
  86
  68
  성적 처리 끝
  ```



## continue

* continue 이후 명령을 실행하지 않고 다음 반복을 시작

  ```python
  score = [92, 86, 68, -1, 56]
  for s in score:
  	if s == -1:
  		continue
  	print(s)
      
  print('성적 처리 끝')
  
  92
  86
  68
  56
  성적 처리 끝
  ```

  ```python
  score = [92, 86, 68, 120, -20, 40, 68, -1, 56]
  num = 0
  for s in score:
      if (s < 0) or (s > 100):
          num += 1
          continue
      print(s)
  print('성적 처리 끝')
  print('오류데이터는', num, '개 입니다.')
  
  # 들여쓰기 레벨 한번에 바꾸는 법 블럭잡고 탭 누르기 또는 쉬프트 탭
  
  92
  86
  68
  40
  68
  56
  성적 처리 끝
  오류데이터는 3 개 입니다
  ```



## 루프의 활용

* 이중 루프

  * 루프안에 루프를 실행

  ```python
  for dan in range(2, 10):
  	print(dan, "단")
  	for hang in range(2, 10):
  		print(dan, '*', hang , '=', dan * hang)
  	print()
  
  2 단
  2 * 2 = 4
  2 * 3 = 6
  :
  2 * 9 = 18
  3 단
  :
  9 단
  9 * 2 = 18
  9 * 3 = 27
  :
  9 * 9 = 81
  ```

  ```python
  for y in range(1, 10):
  	for x in range(y):
  		print('*', end='')
  	print()
  
  # 위에와 같은 결과 
  
  for y in range(1, 10):
  	print('*'*y)
  
  *
  **
  ***
  ****
  *****
  ******
  *******
  ********
  *********
  ```

* 무한루프

  * `while` 문의 조건이 항상 `True`
  * 반복문에서 조건을 검사하여 `break`로 벗어남

  ```python
  print("3 + 4 = ?")
  while True:
  	a = int(input('정답을 입력하세요: '))
  	if a == 7 : break
          
  print('참 잘했어요')
  
  3 + 4 = ?
  정답을 입력하세요: 6
  정답을 입력하세요: 12
  정답을 입력하세요: 7
  참 잘했어요
  ```

  ```python
  for ten in range(0, 5):
  	for num in range(ten * 10, ten * 10 + 10):
  		print(num, end = ",")
  	print()
  
  0,1,2,3,4,5,6,7,8,9,
  10,11,12,13,14,15,16,17,18,19,
  20,21,22,23,24,25,26,27,28,29,
  30,31,32,33,34,35,36,37,38,39,
  40,41,42,43,44,45,46,47,48,49,
  ```