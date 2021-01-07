# 예외 처리



## 예외

* 프로그램 실행 중 발생한 에러 --> 프로그램 실행 종료

```python
# 예외 예시

str = "89점"
score = int(str)
print(score)
print("작업완료")
------------------------------------------------------------
Traceback (most recent call last):
File , line 2, in <module>
score = int(str)
ValueError: invalid literal for int() with base 10: '89점'
```

## 예외 처리(try)

* 예외 발생을 감지하고 복구하는 방법
* 구조

```python
try:
	실행할 명령
except 예외 as 변수:
	오류 처리문
else:
	예외가 발생하지 않을 때의 처리
```



```python
str = '89점'
try:
    score = int(str)
    print(score)
except:
    print('예외가 발생했습니다.')

print('작업완료')

# 예외가 발생했습니다.
# 작업완료


while True:
    str = input('점수를 입력하세요 : ')
    try:
        score = int(str)
        print('입력한 점수 :', score)
        break
    except:
        print('점수 형식이 잘못되었습니다.')
print('작업완료')

# 점수를 입력하세요 : 만점
# 점수 형식이 잘못되었습니다.
# 점수를 입력하세요 : 99
# 입력한 점수 : 99
# 작업완료
```

* 예외의 종류
  * NameError
  * ValueError
  * ZeroDivisionError
  * IndexError
  * TypeError 등
  * 너무나도 많다.

```python
str = '89'
try:
    score = int(str)
    print(score)
    a = str[5] # 여기 틀림 그래서 저렇게 나옴
except ValueError:
    print('점수의 형식이 잘못되었습니다.')
except IndexError:
    print('첨자 범위를 벗어났습니다.')

print('작업완료')

# 89
# 첨자 범위를 벗어났습니다.
# 작업완료
```

### raise

* 개발자에 의해 임의로 예외를 발생

```python
def calcsum(n):
    if n < 0:
        raise ValueError

    total = 0
    for i in range(n+1):
        total += i
    return total


try:
    print('~10 =', calcsum(10))  # ~10 = 55 <---n이 0보다 커서 가능했다.
    print('~-5 =', calcsum(-5))  # 불가능 except로 넘어감
except ValueError:
    print('입력값이 잘못되었습니다.') # 입력값이 잘못되었습니다.
```

### finally

* 예외 발생 여부와 상관없이 항상 호출
* 작업의 마무리 작업(cleanup) 수행

```python
try:
    print('네트워크 접속')
    a = 2/0   # 분모 0오류 여기가 없다면 ---> # 네트워크 접속
    print('네트워크 통신 수행')              # 네트워크 통신 수행
finally:                                  # 접속 해제
    print('접속 해제')                      # 작업 완료

print('작업 완료')

# 네트워크
# 접속 해제
# Traceback (most recent call last):
  File "c:\Users\wjdgo\iot_workspace\01.python\ch12\ex04_try_finally.py", line 3, in <module>
    a = 2/0
ZeroDivisionError: division by zero
```

```python
def chat():
    try:
        print('네트워크 접속')
        a = 2/0
        return
        print('네트워크 통신 수행')
    except:
        print('네트워크 에러 발생')
    finally:
        print('접속 해제')

    print('=========================')


print('통신을 시작합니다.')
chat()
print('통신이 끝났습니다.')

# try except를 거쳐야 파이널이 실행됨 중요!!!
# 오류없어 except를 안거치면 finally 실행안됨

# 통신을 시작합니다.		    # 통신을 시작합니다.  <--- a= 2/0 없으면
# 네트워크 접속				 # 네트워크 접속
# 네트워크 에러 발생		    # 접속 해제
# 접속 해제                   # 통신이 끝났습니다.       
# =========================
# 통신이 끝났습니다.
```



###  assert(단정문)

*  `assert 조건, 예외메시지`
  * 조건이 True이면 통과,
  * False이면 메시지를 가지는 예외 발생
  * 디폴트 옵션은 프로그램 종료
  * 프로그램 test때 많이 사용

```python
score = 128
assert score <= 100, "점수는 100 이하여야 합니다."
print(score)

# Traceback (most recent call last):
# File, line 2, in <module>
# assert score <= 100, "점수는 100 이하여야 합니다."
# AssertionError: 점수는 100 이하여야 합니다.
```

