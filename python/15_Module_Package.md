# 모듈과 패키지

## 모듈

* 변수와 함수를 모두 한 파일에 정의하면 관리가 힘들어짐

* 비슷한 성격의 변수, 함수들을 파일 별로 나눠 정의

* 이렇게 정의한 파일을 모듈이라고 함

* 파일명이 모듈명이 됨

  

### 모듈의 정의

```python
--------------util.py---------------
INCH = 2.54

def calcsum(n):
    sum = 0
    for num in range(n+1):
        sum += num
    return sum
------------------------------------
```



### 모듈의 사용

```python
import util

print("1inch = ", util.INCH)       # 1inch =  2.54
print("~10 = ", util.calcsum(10))  # ~10 =  55
```

* `from 모듈명 import *`

  * 지정한 모듈의 모든 요소를 임포트함
  * 바로 사용 가능하지만 이름 충돌 발생 가능성이 높아짐 (비권장)

  ```python
  from util import *  # from util import INCH, calcsum   # 권장
  
  print("1inch = ", INCH)  # 1inch =  2.54
  print("~10 = ", calcsum(10))  # ~10 =  55
  ```



### 모듈 테스트

* `__name__` 변수에 모듈명이 저장됨
* 단독으로 실행된 경우 (모듈로 사용된 것이 아님 )
  * `"__main__" `으로 지정됨
* 모듈로 사용된 경우 (`import`에 의해 실행된 경우 )
  * 파일명이 지정됨
* 모듈 개발시 테스트 할 수 있도록 지원

```python
INCH = 2.54

def calcsum(n):
    sum = 0
    for num in range(n+1):
        sum += num
    return sum

if __name__ == "__main__" :  # 단독 실행되었다면 True
    print("1inch = ", INCH)
    print("~10 = ", calcsum(10))

# 전에 만들었던 app도 모듈로 따로 하자
# myapp.py, myappgo.py 참고


#####################################################
# 예제 util.py 만든 상태

print(__name__)

"""
__main__
"""

#  import 는 최초 한번만 실행한다. (두번째부터는 안함)

#####################################################
# 새로운 디렉토리(test)를 만들고 그 안에 test01.py 만든 상태

# test01.py

import util

print(util.INCH)

"""
2.54
"""

# working directory에서 찾는다. (현재 디렉토리 X)

#####################################################
# ■ 모듈 경로
#   ○ sys 모듈의 path 리스트를 먼저 조사
#       ● 현재 워킹 디렉토리가 제일 먼저 조사됨
#   ○ 그 다음 PYTHONPATH 환경 변수의 디렉토리 검색

# test01.py

import sys
for path in sys.path:
    print(path)

"""
C:\workspace\01_python\chapter16\test  # 현재 디렉토리
C:\workspace\01_python\chapter16  # 프로젝트 디렉토리
C:\Users\i\anaconda3\envs\chapter16\python37.zip
C:\Users\i\anaconda3\envs\chapter16\DLLs
C:\Users\i\anaconda3\envs\chapter16\lib
C:\Users\i\anaconda3\envs\chapter16
C:\Users\i\anaconda3\envs\chapter16\lib\site-packages
"""

# myapp.py와 util.py \PYTHON_LIB 로 이동

# 내PC -> 속성 -> 고급 시스템 설정 -> 환경변수 -> 시스템 변수 -> 새로 만들기
# 변수이름 PATHONPATH
# 변수값 C:\PYTHON_LIB

# 다시 실행
# 실행 된다!
```



## 패키지

* 모듈들을 모아 놓은 디렉토리

* 반드시` __init__.py`가 존재해야 함( 패키지용 디렉토리임을 알림)

  * 일반적으로 내용은 없음

    

### `__init__.py`

* `from 패키지 import * `

  * `*`에 의해 임포트될 모듈 목록을 `__all__ `리스트로 지정
  * 지정하지 않으면 모든 모듈이 임포트됨

  ```python
  from mypack.calc import *
  
  add.outadd(1,2)
  multi.outmulti(1,2)
  
  
  ##############################################
  # ■ __init__.py
  
  # 기능은 있지만 사용하지 않음
  
  __all__ = ["add", "multi"]
  print("add module imported")
  ```



## 써드 파티 모듈

### 모듈의 내부

```python
import sys
print(sys.builtin_module_names)

('_abc',
'_ast',
'_codecs',
'_collections',
'_functools',
'_imp',
'_io',
'_locale',
'_operator',
'_signal',
:
)
```

#### `dir()`함수

* 모듈내 함수 목록 출력

```python
import math
dir(math)

['__doc__',
'__file__',
'__loader__',
'__name__',
'__package__',
'__spec__',
'acos',
'acosh',
'asin',
:
]
```

#### `help()`함수

* 함수의 `docstring` 출력

```python
help(math.hypot)


"""Help on built-in function hypot in module math:
hypot(x, y, /)
Return the Euclidean distance, sqrt(x*x + y*y)."""

# ■ 외부 모듈 관리 pip
#   ○ install : 패키지를 설치
#   ○ uninstall : 설치한 패키지를 삭제한다 .
#   ○ freeze : 설치한 패키지의 목록을 보여준다 .
#   ○ show : 패키지의 정보를 보여준다 .
#   ○ search : pyPI에서 패키지를 검색한다 .

# 라이브러리 다운로드

pip install beautifulsoup4  # beautifulsoup4를 다운받겠다. (터미널)

# External Libraries -> site-packages 에서 확인 가능
```

#### 외부 모듈 관리 `pip`

* `install`: 패키지를 설치
* `uninstall`: 설치한 패키지를 삭제한다 .
* `freeze `: 설치한 패키지의 목록을 보여준다 .
* `show`: 패키지의 정보를 보여준다 .
* `search`: `pyPI`에서 패키지를 검색한다 .

```python
# 라이브러리 다운로드

pip install beautifulsoup4  # beautifulsoup4를 다운받겠다. (터미널)

# External Libraries -> site-packages 에서 확인 가능
```

