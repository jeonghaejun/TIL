# 클래스

* 관련 정보와 정보의 조작 함수(메서드)를 묶어서 관리하는것

* `class`키워드로 정의

  * 사용하기 위해서는 인스턴스를 생성한후 사용

  ```python
  # 누구의 계좌인지
  # 출금(withdraw)
  
  # 클래스 설계능력이 중요!!
  
  class Human:
      def __init__(self, name, age):       # <--쓸변수는 다넣어준다. 나중에 정의해줄 변수도
          self.name = name                 # 나중에 정의할 변수에는 None을 넣는다
          self.age = age
          self.gender = None
  
      def intro(self):
          print(f'{self.age}살 {self.name}({self.gender})입니다.')
  
      def change(self, gender):  # <--class 인자 추가가능 하지만 비권장이다.
          self.gender = gender
  
      def __str__(self):  # <-----특수 메소드
          return f'<Human {self.age},{self.name},{self.gender}>'
  
      def __repr__(self):
          return f'<Human {self.name}>'
  
  
  class Account:
      def __init__(self, owner, balance):  # 생성자 함수
          self.owner = owner  # self.owner.name, self.owner.age, self.owner.gender
          self.balance = balance
  
      def deposit(self, money):
          self.balance += money
  
      def inquire(self):
          print('잔액은 %d원 입니다.' % self.balance)
  
      def withdraw(self, money):
          if self.balance < money:
              raise Exception('잔액부족')
  
          self.balance -= money
          return money
  
  
  hong = Human('홍길동', 29)
  account = Account(hong, 8000)   # Account의 인스턴스 생성
  account.deposit(1000)  # <--- ctrl + 클릭시 해당 메소드로 이동 된다.
  account.inquire()
  try:
      account.withdraw(3000)
      account.inquire()
      account.withdraw(10000)
      account.inquire()
  except Exception as e:
      print('예외', e)
  
  # print(account)
  
  ```

## 생성자

* `__init__(self)`

  * 클래스의 인스턴스를 생성할 때 자동으로 호출
  * 멤버 변수 정의 및 초기화 하는 역할

  ```python
  class 이름:
  	def __init__(self, 초기값):
  		
  		멤버 초기화
  	
  	메서드 정의
  
  객체 = 객체명(인수)
  ```

  ```python
  class Human:
      def __init__(self, name, age):       # <--쓸변수는 다넣어준다. 나중에 정의해줄 변수도
          self.name = name                 # 나중에 정의할 변수에는 None을 넣는다
          self.age = age
          self.gender = None
  
      def intro(self):
          print(f'{self.age}살 {self.name}({self.gender})입니다.')
  
      def change(self, gender):  # <--class 인자 추가가능 하지만 비권장이다.
          self.gender = gender
  
      def __str__(self):  # <-----특수 메소드
          return f'<Human {self.age},{self.name},{self.gender}>'
  
      def __repr__(self):
          return f'<Human {self.name}>'
  
  
  kim = Human('김상형', 29)
  print(kim.name)    # 김상형
  kim.name = '홍길동'
  print(kim.name)    # 홍길동
  # kim.gender = '남'
  kim.change('남')
  kim.intro()  # 29살 홍길동(남)입니다.
  
  lee = Human('이승우', 45)
  lee.change('여')
  lee.intro()  # 45살 이승우(여)입니다.
  
  # l1 = list((1, 2, 3))  # 변환 함수, list(), int(), dict()...라고 했는데
  # print(l1)             # class 배우면 리스트 생성자를 만든거다.
  print(kim)            # print(l1)처럼 내부데이터를 보고싶다. 그러면 특수 메소드를 만들어야 한다.
  print(lee)
  
  # <Human 29,홍길동,남>
  # <Human 45,이승우,여>
  
  li = [kim, lee]
  print(li)  # [<Human 홍길동>, <Human 이승우>]
  
  # 식별자(identifier): 변수명, 함수명, 클래스명, 메소드명 등... 주로 개발자가 명명한 이름
  # 특정 메모리 위치에 대한 이름
  # 참조: 실제 데이터가 있는 위치 정보(메모리 주소)를 값으로 가지는 것
  # 파이썬은 상수가 없음.
  # -> 모든 식별자는 자신의 값을 변경할 수 있음
  ```



## 상속

* 기존 클래스 정의를 그대로 자신의 것으로 취하는 방법

  ```python
  class Human:
      def __init__(self, name, age):
          self.name = name
          self.age = age
  
      def intro(self):
          print(str(self.age)+'살'+self.name+'입니다.')
  
  
  class Player:
      def __init__(self, gender):
          self.gender = gender
  
  
  class Student(Human, Player):  # 다중상속
      def __init__(self, name, age, gender, stunum):
          # super().__init__(name, age)  # Human.__init__(name,age) 이렇게하면 에러난다.
          Human.__init__(self,name,age)  # 이렇게하면 된다. 다중상속일때 쓴다.
          Player.__init__(self,gender)
  
          self.stunum = stunum
  
      def intro(self):
          super().intro()
          print('학번: '+str(self.stunum))
  
      def study(self):
          print('하늘천 따지 검을 현 누를 황')
  
  
  kim = Human('김상형', 29)
  kim.intro()
  
  lee = Student('이승우', 45, 117149)
  lee.intro()
  lee.study()
  
  # 29살 김상형입니다.
  # 45살 이승우입니다.
  # 학번: 930011
  # 하늘천 따지 검을 현 누를 황
  ```



### 액세스

* 파이썬은 기본적으로 정보 은폐 기능을 지원하지 않는다.

* `getter/setter`로 정보(프로퍼티)를 보호

  * `@property`
    * 함수명이 프로퍼티명이 되며 `getter` 함수로 동작
  * `@프로퍼티명.setter`
    * 프로퍼티의 `setter()` 함수 정의

  ```python
  class Date:
      def __init__(self, month):
          self.__month = month
  
      def getmonth(self):
          return self.__month
  
      def setmonth(self, month):
          if 1 <= month <= 12:
              self.month = month
  
  
  today = Date(8)
  today.month = 15
  
  print(today.month)   # 8
  ```



#### 프라이빗 멤버 변수

* 멤버 변수 앞에 `__`을 붙이면 외부에서 바로 접근 불가

  ```python
  class Date:
  	def __init__(self, month):
  		self.__month = month
  		
  	def getmonth(self):
  		return self.__month
  		
  	def setmonth(self, month):
  		if 1 <= month <= 12:
  			self.inner_month = month
  			
  	month = property(getmonth, setmonth)
  
  today = Date(8)
  today.month = 15
  
  print(today.month)   # 8
  print(today.__month) # 예외 발생
  ```

## 클래스 메서드

* 일반적인 메서드는 인스턴스 메서드
  * 반드시 인스턴스를 만든 후 사용 가능
  * 첫 번째 인자는 항상 인스턴스에 대한 참조(`self`)
* 클래스 메서드는 인스턴스와 무관하게 존재
  * 인스턴스 없이도 클래스명을 통해 접근 가능
  * 첫 번째 인자는 클래스에 대한 참조(`cls`)
* `@classmethod`로 정의

### 클래스 멤버 변수

* `class` 안에서 `self`와 무관하게 정의되는 멤버 변수

* 인스턴스와 무관하게 존재하며 모든 인스턴스가 공유하는 정보

  ```python
  class Car:
      
      count = 0
  
      def __init__(self, name):
          self.name = name
          Car.count += 1
  
      @classmethod
      def outcount(cls):
          print(cls.count)
  
  
  pride = Car('프라이드')
  korando = Car('코란도')
  Car.outcount()   # 2
  ```



### 정적 메서드

* 단순히 클래스 내에 정의되는 일반함수

  * 클래스에 대한 어떠한 정보도 제공하지 않음
  * 첫 번째 인자가 정해져 있지 않음

* 비슷한 성격의 함수를 묶어서 관리하는 역할

  ```python
  class Car:
  
      @staticmethod        # 인스턴스와 무관하게 사용할 수 있다.
      def hello():
          print('오늘도 안전 운행 합시다.')
  
      count = 0
  
      def __init__(self, name):
          self.name = name
          Car.count += 1
  
      @classmethod
      def outcount(cls):
          print(cls.count)
   
  Car.hello()      # 오늘도 안전 운행 합시다.
  ```



### 연산자 메서드

* 연산자를 재정의할 수 있는 함수

* 연산자 별로 함수명이 정해져 있음

  | 연산자 | 메서드                        |
  | ------ | ----------------------------- |
  | `==`   | `__eq__`                      |
  | `!=`   | `__ne__`                      |
  | `<`    | `__lt__`                      |
  | `>`    | `__gt__`                      |
  | `<=`   | `__le__`                      |
  | `>=`   | `__ge__`                      |
  | `+`    | `__add__, __radd__`           |
  | `-`    | `__sub__, __rsub__`           |
  | `*`    | `__mul__, __rmul__`           |
  | `/`    | `__div__, __rdiv__`           |
  | `//`   | `__floordiv__, __rfloordiv`__ |
  | `%`    | `__mod__, __rmod__`           |
  | `**`   | `__pow__, __rpow__`           |
  | `<<`   | `__lshift__`                  |
  | `>>`   | `__rshift__`                  |

  ```python
  class Human:
      def __init__(self, name, age):
          self.name = name
          self.age = age
  
      def __eq__(self, other):
          return self.name == other.name and self.age == other.age
  
  
  kim = Human('김상형', 29)
  sang = Human('김상형', 29)
  moon = Human('문종민', 44)
  
  print(kim == sang)  # True
  print(kim == moon)  # False
  ```



### `__str__`

* 객체의 정보를 출력하기위해 객체의 내부 정보를 문자열로 리턴하는 함수

* `print()` 함수에 객체를 지정했을 때 해당 객체의 `__str__()` 호출됨

  ```python
  class Human:
  	def __init__(self, name, age):
  		self.name = name
  		self.age = age
  		
  	def __str__(self):
  		return "이름 %s, 나이 %d" % (self.name, self.age)
  		
  kim = Human("김상형", 29)
  print(kim)   # 이름 김상형, 나이 29
  ```

  







