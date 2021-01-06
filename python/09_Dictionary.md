# Dictionary



## 사전

* 구조

  ```python
  { 키1:값1
    키2:값2 }
  ```

  ```python
  dic = {
      'boy': '소년',
      'school': '학교',
      'book': '책'
  }
  print(dic)  # {'boy': '소년', 'school': '학교', 'book': '책'}
  
  
  print(dic['boy'])
  print(dic['book'])
  # print(dic['girl']) 없는값 검색하면 오류발생 프로그램 종료됨
  
  # 있으면 리턴해주고 없으면 특정메세지를 리턴해주는 방법
  
  print(dic.get('boy'))
  print(dic.get('girl'))
  print(dic.get('girl', '사전에 없는 단어입니다.'))
  
  for i in dic:
      print(i)  # 사전에 있는 키값을 출력한다!!!
  ```

* 삭제, 추가, 수정

  | 메소드                    | 설명                                                         |
  | ------------------------- | ------------------------------------------------------------ |
  | `사전[키]`                | 키의 값을 리턴, 키가 존재하지 않는 경우 예외 발생            |
  | `사전.get(키 [, 기본값])` | 키의 값을 리턴, 키가 존재하지 않는 경우, None 리턴<br>키가 없을 때 리턴할 값지정 가능 |
  | `.keys()`                 | 키 목록 리턴                                                 |
  | `.values()`               | 값 목록 리턴                                                 |
  | `.itmes()`                | (키,값) 튜플 목록 리턴                                       |
  | `dic1.update(dic2)`       | dic1에 dic2를 추가 중복되는 키 덮어써서 추가한다.            |

  ```python
  dic = {
      'boy': '소년',
      'school': '학교',
      'book': '책'
  }
  dic['boy'] = '남자아이' # 기존값 수정
  dic['girl'] = '소녀'    # 새로운 엔트리 추가
  del dic['book']         # 기존 엔트리 삭제
  print(dic) 
  # {'boy': '남자아이', 'school': '학교', 'girl': '소녀'}
  ```

  ```python
  dic = {'boy': '소년', 'school': '학교', 'book': '책'}
  print(dic.keys())
  print(dic.values())
  print(dic.items())
  # dict_keys(['boy', 'school', 'book'])
  # dict_values(['소년', '학교', '책'])
  # dict_items([('boy', '소년'), ('school', '학교'), ('book', '책')])
  
  # 1번쨰
  keylist = dic.keys()
  for key in dic:
      print(key, dic[key])
  
      # boy 소년
      # school 학교
      # book 책
  
  # 2번째
  for t in dic.items():
      print(t[0], t[1])
  
      # boy 소년
      # school 학교
      # book 책
      
  # 3번째
  for key, value in dic.items():
      print(key, value)
  
      # boy 소년
      # school 학교
      # book 책
  
  # 세개다 결과는 같다. 세번째에 있는 거는 튜플의 특성을 이용한것
  
  li = list(dic.keys())
  print(li)   # ['boy', 'school', 'book']
  
  # 사전을 리스트화 하면 키값이 리스트로 출력된다.
  li = list(dic)
  print(li)   # ['boy', 'school', 'book']
  ```

* 추가

  ```python
  # 사전은 키값이 중복될수있어서 +연산자 사용 불가
  # 그래서 .update 메소드를 사용해서 덮어써서 추가한다.
  
  dic = {'boy': '소년', 'school': '학교', 'book': '책'}
  dic2 = {'student': '학생', 'teacher': '선생님', 'book': '서적'}
  
  dic.update(dic2)
  print(dic)
  
  # {'boy': '소년',
  # 'school': '학교',
  # 'book': '서적',
  # 'student': '학생',
  # 'teacher': '선생님'}
  ```

* 리스트를 사전으로 바꾸기

  ```python
  # 이중리스트만 가능 첫번째 엘리먼트가 키값 두번째 엘리먼트가 벨류값
  
  li = [
      ['boy', '소년'],
      ['school', '학교'],
      ['teacher', '선생님']
  ]
  
  dic = dict(li)
  print(dic)
  ```

* 예제

  ```python
  # find index는 함수 자체내에서 루프를 돌기 때문에 시간이 오래걸린다
  # 하지만 사전은 키값을 해쉬값 즉 숫자로 가지고있어서 키값만 안다면
  # 찾는시간을 극소화 시킬수있다.
  song = """by the rivers of babylon, there we sat down
  yeah we wept, when we remember zion.
  when the wicked carried us away in captivity
  required from us a song
  now how shall we sing the lord's song in a strange land"""
  
  alphabet = dict()
  for c in song:
      if c.isalpha() == False:  # 부호, 개행문자는 제외하는 조건.
          continue
      c = c.lower()
      if c not in alphabet:  # 처음 등장한 경우.
          alphabet[c] = 1
      else:
          alphabet[c] += 1
  
  print(alphabet)
  
  # 알파벳 순서대로
  key = list(alphabet.keys())
  key.sort()
  for c in key:
      num = alphabet[c]
      print(f'{c} : {num}')
  
  # 벨류 높은 순
  # 벨류가 높은 순서대로는 힘들다 벨류로 키를 찾을수가 없어서
  # sort메소드 말고 items로 찾는다
  
  def get_value(a):
      print(a)      # a[0] - key, a[1] - value / ('b', 4)
      return a[1]   # value
  
  items = list(alphabet.items())
  print(items)
  items.sort(reverse=True, key=get_value) 
  # items.sort(reverse=True, key=lambda a: a[1]) 이거 쓰면
  # 함수정의 안하고 바로 할 수 있다. a[0] 이면 키 a[1]이면 벨류정렬
  
  for k, v in items:
      print(f'{k} : {v}')
  
  # 단어 횟수로 찾기
  
  word_dict = {}  # dict()
  # for line in song.splitlines: # 라인 단위 분리
  lines = song.splitlines()
  
  for line in lines:
      words = line.split()
      for word in words:     # 한 라인에서 단어 분리
          word = word.lower()
          if word not in word_dict:
              word_dict[word] = 1
          else:
              word_dict[word] += 1
  
  print(word_dict)
  print(song.splitlines())
  ```

* 람다함수

  ```python
  def get_value(a):
      return a[0]
  
  f=lambda a:a[0]
  
  item=('a',10)
  print(f(item))
  ```



## 집합

* 구조

  ```python
  { 값1, 값2, ... }
  ```

* 값의 중복을 허용하지 않음

  | **함수**         | **설명**                                                     |
  | ---------------- | ------------------------------------------------------------ |
  | set(다른 시퀀스) | 집합 변환 함수                                               |
  | **메소드**       | **설명**                                                     |
  | .add(값)         | 집합에 값 추가, 이미 값이 있으면 추가하지 않음<br>회원들의 명단에서 사는곳이 추릴때 루프돌려서 <br />계속집합에 추가하면 중복은 사라지고 값만 남음 |
  | .remove(값)      | 집합에서 값을 제거, 값이 없는 경우 예외 발생                 |

  ```python
  asia = {'korea', 'china', 'japan', 'korea'}
  print(asia) # {'china', 'japan', 'korea'}
  
  print(set('aaabbbccc'))
  print(set([12, 34, 56, 78]))
  print(set(('홍길동', '고길동','둘리')))
  print(set({'boy': '소년', 'school': '학교', 'book': '책'})) # 사전의 키 목록을 집합으로 변환
  print(set())
  
  # {'a', 'c', 'b'}
  # {56, 34, 12, 78}
  # {'홍길동', '둘리', '고길동'}
  # {'book', 'boy', 'school'}
  # set()
  
  asia = {'korea', 'china', 'japan'}
  asia.add('vietnam')
  asia.add('korea')
  asia.remove('japan')
  print(asia)           #{'vietnam', 'china', 'korea'}
  ```

* 집합연산

  | 연산          | 기호 | 메소드               | 설명                                          |
  | ------------- | ---- | -------------------- | --------------------------------------------- |
  | 합집합        | \|   | union                | 두 집합의 모든 원소                           |
  | 교집합        | &    | intersection         | 두 집합 모두에 있는 원소                      |
  | 차집합        | -    | difference           | 왼쪽 집합의 원소 중 오른쪽 집합의 원소를 뺀것 |
  | 배타적 차집합 | ^    | symmetric_difference | 한쪽 집합에만 있는 원소의 합                  |

  ```python
  twox = {2, 4, 6, 8, 10, 12}
  threex = {3, 6, 9, 12, 15}
  
  print('교집합', twox & threex)        # 교집합 {12, 6}
  print('합집합', twox | threex)        # 합집합 {2, 3, 4, 6, 8, 9, 10, 12, 15}
  print('차집합', twox-threex)          # 차집합 {8, 2, 10, 4}
  print('차집합', threex-twox)          # 차집합 {9, 3, 15}
  print('배타적 차집합', twox ^ threex)  # 배타적 차집합 {2, 3, 4, 8, 9, 10, 15}
  ```

## 인수의 형식

```python
# 일반변수, 가변변수,키워드 가변변수 순서로 배치해야한다!!!!
# calcstep('김한슬',99,98,95,89,avg=False)
# calcstep(name, *score,**option)

def calcstep(name, *score, **option):
    print(name)
    total = 0
    for s in score:
        total += s

    print('총점 :', total)
    if(option['avg'] == True):   # 여기서 avg를 꼭 써야 해서 없으면 오류
        print('평균 :', total/len(score))


calcstep('홍길동', 88, 99, 77, avg=True)
calcstep('고길동', 99, 88, 95, 85, avg=False)
# calcstep('둘리', 99, 85, 20, 40, 80) 에러 난다.
```



## 

