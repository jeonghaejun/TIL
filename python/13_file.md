# 파일



## 파일 쓰기

* `open(파일경로, 모드)`

* 모드1,2 하나씩 결함해서 쓴다. (예. `open("live.txt", "wt", encoding="utf-8")` )

  | 모드1     | 설명                                         |
  | --------- | -------------------------------------------- |
  | `r`       | 읽기, 파일이 없는 경우 예외가 발생한다.      |
  | `w`       | 쓰기, 파일이 없으면 새로 생성                |
  | `a`       | 추가, 기존의 내용 살리고 그 뒤에 내용을 추가 |
  | `x`       | 쓰기용으로 여나 기존 파일이 있는 경우 실패   |
  | **모드2** | **설명**                                     |
  | `t`       | `text`모드로 열기                            |
  | `b`       | `binary`모드로 열기                          |

  ```python
  f = open("live.txt", "wt", encoding="utf-8")
  # CP949(EUC-KR) 운영체제의 문자셋으로 처리됨
  f.write("""삶이 그대를 속일지라도
  믿으라, 기쁨의 날이 오리니""")
  f.write("""추가한 내용입니다.""")
  
  f.write("""또 추가합니다.
  믿으라, 기쁨의 날이 오리니""")
  f.close()
  
  # w는 기존의 것을 버리고 실행
  # a는 기존의 것을 냅두고 실행
  ```

## 파일 읽기

| 메소드          | 설명                                                        |
| --------------- | ----------------------------------------------------------- |
| `f.read()`      | 파일 전체 내용                                              |
| `f.read(n)`     | n개의 내용(모드가 `rt`면 글자수, `rb`면 바이트 수)          |
| `f.readline()`  | 한줄                                                        |
| `f.readlines()` | 전체 라인 리스트(각 라인의 끝에는 개행문자가 포함되어 있음) |

```python
# 파일 읽기

try:
    f = open('live.txt', 'rt', encoding='utf-8')
    text = f.read()
    print(text)
except FileNotFoundError:
    print('파일이 없습니다.')
finally:
    f.close()
    
# 삶이 그대를 속일지라도
# 믿으라, 기쁨의 날이 오리니추가한 내용입니다.또 추가합니다.
# 믿으라, 기쁨의 날이 오리니

# 파일 처리시에는 with를 많이쓴다.
# 반드시 close해야하는 상황일때 with를 쓴다.

try:
    with open('live.txt', 'rt') as f:
        text = f.read()  # 예외 발생시 with 블럭을 벗어날때 close() 자동 호출됨
        print(text)
except Exception as e:
    print('예외발생', e)
```

```python
# read 에서 with과 while 함께쓰기

text=""
line=1
try:
    with open('live.txt', 'rt',encoding='utf-8') as f:
        while True:
            row=f.readline()
            if not row: break
            text+=str(line)+" : "+row
            line+=1
except Exception as e:
    print('예외발생', e)

print(text)

# 결과 같다.

try:
    with open('live.txt', 'rt', encoding='utf-8') as f:
        rows = f.readlines()
        for ix, row in enumerate(rows, 1):
            print(f'{ix}: {row}', end='')

except Exception as e:
    print('예외발생', e)

# 1 : 삶이 그대를 속일지라도
# 2 : 믿으라, 기쁨의 날이 오리니추가한 내용입니다.또 추가합니다.
# 3 : 믿으라, 기쁨의 날이 오리니

f = open('live.txt', 'rt',encoding='utf-8')

for line in f:
    print(line, end='')
f.close()

# 삶이 그대를 속일지라도
# 믿으라, 기쁨의 날이 오리니추가한 내용입니다.또 추가합니다.
# 믿으라, 기쁨의 날이 오리니
```

### pickle 모듈

* python 자료형 그대로 저장하고, 그대로 로드(복원)
* 반드시 `binary`모드로 오픈해야 한다.
* 다른 언어와 호환성이 없다.

```python
-----------------data.csv--------------------
이름,국어,영어,수학,사회
홍길동,80,90,100,40
고길동,40,50,70,90
둘리,60,50,40,60
도우너,30,40,50,60
---------------------------------------------

def load(fpath):
    with open(fpath, 'rt', encoding='utf-8')as f:
        return f.readlines()


def convert(lines):       # 학생이름: key, 성적 리스트: value --> 사전을 리턴
    data = {}
    for line in lines[1:]:  # 헤더는 제외
        items = line.split(',')
        name = items[0]       # 이름
        scores = items[1:]    # 성적 리스트
        data[name] = list(map(int, scores))  # 사전에 추가
        # int를 통해\n삭제->white 문자(공백, 탭, 엔터)
    return data

# 저장하기

import pickle

def save(fpath,data):
    with open(fpath,'wb') as f:
        pickle.dump(data,f)

def main():   # 흐름제어
    try:
        lines = load('data.csv') # 밑에 두개가 대체 
        # fpath = input('파일명: ')  # 파일명 잘못 입력하면 예외 발생
        # lines = load(fpath)
        # print(lines)
        data = convert(lines)
        print(data)
        save('data.dat',data)

    except Exception as e:
        print('예외 발생', e)


main()

# 전역변수 사용 최대한 자제 버그발생 초래 찾기도 힘들다.
# 함수의 단일 책임이 중요

# {'홍길동': [80, 90, 100, 40], 
#  '고길동': [40, 50, 70, 90],
#  '둘리': [60, 50, 40, 60], 
#  '도우너': [30, 40, 50, 60]}
```



```python
# sys.argv를 이용해서 출력


------------------------------------------------data.dat----------------------------------------------------
{'홍길동': [80, 90, 100, 40], '고길동': [40, 50, 70, 90], '둘리': [60, 50, 40, 60], '도우너': [30, 40, 50, 60]}
------------------------------------------------------------------------------------------------------------
import pickle
import sys


def load(fpath):
    with open(fpath, 'rb') as f:
        return pickle.load(f)

# python ex06.py data.dat
# sys.argv


def main():
    if len(sys.argv) != 2:
        print('파일명을 입력하세요.') <-------------- 파일명 잘못입력시 밑의 예외처리 문구 출력
        print('예) python ex06.py filename')
        sys.exit(0)

    fname = sys.argv[1]
    try:
        # data = load('data.dat')
        data = load(fname)
        print(data)
    except Exception as e:
        print('예외 발생', e)


main()

# {'홍길동': [80, 90, 100, 40], 
#  '고길동': [40, 50, 70, 90],
#  '둘리': [60, 50, 40, 60], 
#  '도우너': [30, 40, 50, 60]}

```



