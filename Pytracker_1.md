
# A.1 파이썬 인터프리터
  - 파이썬은 인터프리터 언어로 한번에 하나의 명령을 실행한다
  - 파이썬 프로그램을 실행하는 방법은 첫번째 인자로 .py파일을 넘기는것이다. ex) $python 'hello_world'
  - Ipython에서는 %run 명령어를 사용해 지정 파일의 코드를 실행한다.


```python
a = 5
print a
```

    5
    


```python
print 'hello world'
```

    hello world
    


```python
%run c:/py_test/hello_world.py
```

    hello world
    

# A.2 파이썬 기초
## A.2.1 시멘틱
  - 파이썬은 가독성과 명료성 그리고 명백함을 강조한다(실행 가능한 의사코드라고 표현하기도함)

### 들여쓰기
  - 파이썬은 탭이나 스페이스로 들여쓰기를 하여 코드를 구조화한다
  - 블록이 끝날때 까지 블록안에 있는 코드는 모두 같은 크기 만큼 들여써야한다


```python
for x in array:
    if x < pivot:
        less.append(x)
    else:
        great.append(x)
```

  - 공백이 중요한 이유는 직접 작성하지 않은 코드라도 코드를 읽을 때 인지부조화를 줄일수 있기 때문이다.
  - 공백문자가 의미를 갖지 않은 언어에서는 다음처럼 포맷이 상이한 코드를 읽기 난감할수 있다.
  - 공백이 의미를 갖는것은 파이썬개발자에게는 일상이며, 이로인해 다른 언어보다 가독성이 훨씬 높다


```python
for x in array
    {
      if x < pivot
      {
        less.append(x)
      }
      else
      {
        greater.append(x)
      }
    }  
```

  - 한 줄에 여러 문장이 있을때는 여러문장을 구분하기 위해 세미콜론을 사용한다


```python
a = 5; b = 6; c = 7
```

### 모든것은 객체
  - 모든 숫자, 문자, 자료구조, 함수, 클래스, 모듈 등은 파이썬에서 개체라고 하는 어떤 상자안에 저장된다.
  - 매 객체는 연관된 자료형과 내부데이터를 가지고 있다.
  - 이런 특징은 함수마저도 하나의 개체로 간주함을써 파이썬을 매우유연한 언어로 만든다.

### 주석
  - #_뒤에 오는 글자는 모두 파이썬 인터프리터에서 무시되며 주석을 달 수 있다.
  - 코드를 지우지 않고 실행만 되지 않도록 남겨두고 싶을때도 활용된다.


```python
result = []
for line in file_handle:
#아래코드는 실행되지 않는다
  #if len(line) == 0:
  #_   continue
  result.append(line.replace('foo','bar'))
```

### 함수와 개체 메소드 호출
  - 함수 호출은 괄호와 0개 이상의 인자를 전달해서 이뤄지며, 
  - 선택적으로 반환되는 값을 어떤 변수에 대입할 수 있다.


```python
result = f(x, y, z)
g()
```

  - 모는 객체는 함수를 포함하고 있는데, 이를 메소드라고하며 개체의 내부 데이터에 접근할수 있다.
  - 메소드는 다음 문법으로 호출할 수 있다


```python
object.some_method(x, y, z)
```

  - 함수는 순서별 인자와 키워드 인자를 동시에 받을 수 있다.

result = f(a, b, c, d=5, e='foo')

### 변수와 참조에 의한 전달
  - a리스트를 만들고 b라는 변수에 대입해보자
  - a = b 라고 대입하면 데이터가 복사되고 a에 4를 추가하면 b에도 4가 추가된다.


```python
a = [1, 2, 3]
b = a
a.append(4)
b
```




    [1, 2, 3, 4]



  - 함수에 인자로 개체를 넘기면 개체에 대한 참조만 전달된다
  - 파이썬은 참조에 의한 전달을 한다.


```python
def append_element(some_list, element):
    some_list.append(element)
```


```python
data = [1, 2, 3]
append_element(data, 4)
data
```




    [1, 2, 3, 4]



### 동적 참조와 강한 타입
  - 자바나 C++같은 다른 컴파일 언어와 대조적으로 파이썬에서 객체의 참조는 자료형이 정해져 있지 않다.
  - 따라서 다음 코드는 전혀 문제가 되지 않는다

a = 5
type(a)


```python
a = 'foo'
type(a)
```




    str




```python
5+'5'
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-31-7e7d13df5afd> in <module>()
    ----> 1 5+'5'
    

    TypeError: unsupported operand type(s) for +: 'int' and 'str'


  - 비주얼베이직에서는 5가 정수형으로 변환되 10이 나온다
  - 자바스크립트는 5가문자로 변환되 55가 나온다
  - 파이썬의 모든 객체는 특정 자료형을 가직 다음과 같은 명백한 상황에서만 묵시적인 변환을 하는 자료형을 구분하는 언어이다


```python
a = 4.5
b = 2
print 'a is %s, b is %s' %(type(a), type(b))
```

    a is <type 'float'>, b is <type 'int'>
    

  - 객체의 자료형을 알아야함, 그래야 함수활용시 유용함
  - isinstance 함수를 활용하면 객체의 자료형을 알수 있음


```python
a = 5
isinstance(a, int)
```




    True



  - isinstance는 튜플을 넘겨서 객체의 자료형이 주어진 튜플중 하나인지 검사할수 있음


```python
a = 5; b = 4.5
isinstance(a, (int, float))
```




    True




```python
isinstance(b, (int, float))
```




    True



## 속성과 메소드
  - 개체는 일반적으로 그개체 내부에 저장되는 다른 파이썬 개체인 속성과 그개체 내부데이터에 접근할수 있는 함수인 메서드를 갖는다.
  - 속성과 메서드는 obj.attribute_name같은 문법으로 접근할수 있다.
  - getattr함수로 속성과 메소드에 접근할수도 있다.
  - hasattr함수와 setattr함수도 유용하다.


```python
a = 'foo';
```

a.<Tab>


```python
getattr(a,'split')
```




    <function split>



### 덕타이핑
  - 개체가 어떤 매소드나 행동을 지원하는지 알고싶을때
  - 어떤 개체가 이터레이터를 구현해 순회가 가능한 개체지안 알고싶을때 __iter__매직함수를 사용해도되지만 iter함수를 사용해 검사할수도 있다


```python
def isiterable(obj):
    try:
        iter(obj)
        return True
    except TypeError: #not iterable
        return False
```


```python
isiterable('a string')
```




    True




```python
isiterable([1,2,3])
```




    True




```python
isiterable(5)
```




    False



### 모듈 import
  - 파이썬에서 모듈은 다른 .py파일에서 추가해서 사용할 수 있는 함수와 변수 선언을 담고 있는 .py파일이다
  - 다음과 같은 모듈이 있다고 가정해보자


```python
#some_module.py
PI = 3.14159

def f(x):
    return + 2

def g(a, b):
    return a + b
```

  - 위 함수에 접근하려면 같은 디렉토리에 있는 다른 파일에서 다음 처럼 작성한다


```python
import some_module
result = some_module.f(5)
pi = some_module.PI
```


    ---------------------------------------------------------------------------

    ImportError                               Traceback (most recent call last)

    <ipython-input-66-80deecec23ae> in <module>()
    ----> 1 import some_module
          2 result = some_module.f(5)
          3 pi = some_module.PI
    

    ImportError: No module named some_module


  - 이렇게 불러올수도 있다


```python
from some module import f, g, PI
result = g(5, PI)
```

  - as 예약어를 사용하면 다른이름으로 모듈을 불러올수도 있다. 


```python
import some_module as sm
from some_module import PI as pi, g as gf
r1 = sm.f(pi)
r2 = gf(6, pi)
```

### 이항연산자와 비교문
  - 더하기+, 빼기-, 크거나 같다>= *책 참조 532p
  - 두 참조 변수가 같은 객체를 가리키고 있는지 확인하려면 is 예약어를 사용한다.
  - is not을 사용하면 두 개체가 같지 않은지 검사할 수 있다.


```python
a = [1,2,3]
b = a
c = list(a)
```


```python
a is b
```




    True




```python
a is not c
```




    True




```python
a is None
```




    False



### 뮤터블 이뮤터블 객체
  - 대부분의 객체(리스트 사전 배열 등)는 변경가능하다
  - 변경으로 인한 부작용이 없도록 주석을 잘 남겨둬라


```python
a_list = ['foo', 2, [4, 5]]
a_list[2]
```




    [4, 5]




```python
a_list[2] = (3, 4)
a_list
```




    ['foo', 2, (3, 4)]




```python
a_tuple = (3, 5, (4,5))
```


```python
a_tuple[1] = 'four'
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-77-b7966a9ae0f1> in <module>()
    ----> 1 a_tuple[1] = 'four'
    

    TypeError: 'tuple' object does not support item assignment


## A.2.2 스칼라형
 - 파이썬은 숫자데이터와 문자열, 불리언, 날짜, 시간등을 다루는 자료형을 제공한다
 - None    : 파이썬의 Null값
 - str     : 문자열 자료형
 - unicode : 유니코드 문자열 자료형
 - float   : 배정밀도(64비트) 부동소수점 실수
 - bool    : 참(True)과 거짓(False)
 - int     : 부호가 있는(음수표현이 가능한)정수
 - long    : 무한정밀도의 부호가 있는 정수

### 숫자 자료형 
  - int 와 float 이다.
  - 파이썬은 아주 큰 정수를 무한히 큰 정수를 저장할수 있는 long 자료형으로 변환해준다


```python
ival = 17239871
ival **6
```




    26254519291092456596965462913230729701102721L




```python
fval = 7.243
fval2 = 6.78e-5
```


```python
3/2
```




    1




```python
3/float(2)
```




    1.5



  - 나눈셈의 몫만 돌려주는 // 연산자


```python
3//2
```




    1



  - 복소수의 허수부분은 j로 나타낸다


```python
cval = 1 + 2j
cval*(1-2j)
```




    (5+0j)



### 문자열
  - 파이썬의 강력한 문자열 처리기능!! 작은따옴표나 큰따옴표로 표현
  - 개방문자가 포함된 여러줄에 걸친 문자열은 3개의 작은 따옴표나 큰따옴표사용

  - 문자열은 리스트나 튜플같은 다른 순차적인 자료형rhk 같이 취급


```python
a = 'one way of writing a string'
b = 'another way'
```


```python
c = """
this is longer string that
spans multiple lines
"""
```

  - 문자열은 변경이 불가능(새로만들어야함)


```python
a = 'this is a string'
a[10] = 'f'
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-91-03903a87ead5> in <module>()
          1 a = 'this is a string'
    ----> 2 a[10] = 'f'
    

    TypeError: 'str' object does not support item assignment



```python
b = a.replace('string', 'longer string')
b
```




    'this is a longer string'



- str함수로 객체를 문자열로 바꿀수 있음 숫자5 => 문자5


```python
a = 5.6 ; s = str(a) ;s
```




    '5.6'



 - 문자열은 리스트나 튜플같은 다른 순차적인 자료형과 같이 취급


```python
s = 'python' ; list(s)
```




    ['p', 'y', 't', 'h', 'o', 'n']




```python
s[:3]
```




    'pyt'



  - 역슬래시는 이스케이프 문자로 개행문자나 유니코드 같은 특수한 목적의 글자를 나타내기 위해 사용한다.
  - 역슬래시 자체를 나타내려면 다음처럼 그 자체를 이스케이프 한다
  - 특수문자 없이 역슬래시가 많이 포함된 문자열을 나타내려면 문자열 앞에 r을 써서 문자열을 그자체로만 해석하도록 할 수 있다


```python
s = '12\\34' ; print s
```

    12\34
    


```python
 s = r'this\has\no\special\characters' ; s
```




    'this\\has\\no\\special\\characters'



  - 두 문자열을 더하면 이어붙여준다


```python
a = 'you are so' ; b = 'beautiful' ; a + b
```




    'you are sobeautiful'



  - %뒤에 하나이상의 포맷문자가 붙어있는 문자열은 값을 문자열로 대체할수 있다.
  - %.2f 소수점 둘째자리까지 나타낸숫자 %s 문자열  $%d 일반정수 포맷


```python
template = '%.2f %s are worth $%d'
```


```python
template % (4.5560, 'Argentine Pesos', 1)
```




    '4.56 Argentine Pesos are worth $1'




```python
### 불리언
  - True 와 False 비교 및 기타 조건식으로 불리언으로 해석된다
  - and 와 or 예약어로 조합할수 있다
```


```python
True and True
```




    True




```python
False or True 
```




    True




```python
False and False
```




    False



  - 대부분 파이썬 개체는 참 혹은 거짓개념을 갖고 있음
  - 예를 들어 비어있는 리스트, 튜블, 사전은 False로 간주한다


```python
bool([]), bool([1, 2, 3])
```




    (False, True)




```python
bool('hello world'), bool('')
```




    (True, False)



### 형변환
 - str, bool, float 자료형은 형 변환을 위한 함수로 사용된다.


```python
s = '3.14159'
fval = float(s)
type(fval)
```




    float




```python
int(fval)
```




    3




```python
bool(fval)
```




    True




```python
bool(0)
```




    False



### 날짜와 시간
  - 파이썬 내장 datetime모듈은 datetime, date 그리고 time형을 지원한다.
  - datetime형은 이름에서 알 수 있듯이 date와 time정보를 함께 저장한다


```python
from datetime import datetime, date, time
dt = datetime(2011, 10, 29, 20, 30, 21)
```

  - 데이트 메서드와 타임메서드로 날짜와 시간을 추출할수 있다


```python
dt.day
```




    29




```python
dt.minute
```




    30




```python
dt.date()
```




    datetime.date(2011, 10, 29)




```python
dt.time()
```




    datetime.time(20, 30, 21)



  - strftime 함수는 datetime을 문자로 만들어준다.


```python
dt.strftime('%m/%d/%Y %H:%M')
```




    '10/29/2011 20:30'



  - strptime은 문자열을 해석하여 datetime 객체로 만들어준다


```python
datetime.strptime('20091031', '%Y%m%d')
```




    datetime.datetime(2009, 10, 31, 0, 0)



  - 두 객체의 시간차는 datetime.timedelta객체를 반환한다.
  - timedelta 객체를 datetime 객체에 더하면 그만큼 시간이 지연된 datetime 객체를 얻을 수 있다.


```python
dt2 = datetime(2011, 11, 15, 22, 30)
delta = dt2 - dt
delta
```




    datetime.timedelta(17, 7179)




```python
type(delta)
```




    datetime.timedelta




```python
dt
```




    datetime.datetime(2011, 10, 29, 20, 30, 21)




```python
dt + delta
```




    datetime.datetime(2011, 11, 15, 22, 30)



## A.2.3 흐름제어
  ### if, elif, else
  - if문은 조건을 검사하여 조건이 참인경우 블록내의 코드를 수행함
  - if문은 부가적으로 하나 이상의 elif 블록과 다른 모든 조건이 False인 경우 수행될 else블록을 가질수 있다.

if x < 0:
    print 'Its negative'
elif x == 0:
    print 'Equal to zero'
elif 0 < x < 5:
    print 'Positive but  smaller than 5'
else:
    print 'positive and larger than or equal to 5'

  - 만약 이중 어떤 조건이라도 참이면 다른 elif나 else블록은 검사하지 않는다.
  - and나 or와 함께 사용하면 이조건은 왼쪽에서부터 오른쪽 순으로 검사하며 
  - 앞선 조건이 참인경우 다음 조건은 검사하지 않는다.


```python
a = 5; b = 7
```


```python
c = 8; d = 4
```


```python
if a < b or c > d:
    print 'Made it'
```

    Made it
    

  - for문은 리스트나 튜플 같은 걸렉션이나 이터레이터를 순회한다.
  - for문은 continue예약어를 사용해서 남은 블럭을 건너뛰고 다음 순회로 넘어갈 수 있다.
  - None값은 건너뛰고 리스트에 있는 정수를 모두 더하는 코드를 살표보자


```python
sequence = [1, 2, None, 4, None, 5]
total = 0
for value in sequence:
    if value is None:
        continue
    total += value
```

  - for문은 예약어를 사용해서 빠져나갈수 있다. 
  - 다음 코드는 5를 만날때까지 모든 원소를 더한다.


```python
sequence = [1, 2, 0, 4, 6, 5, 2, 1]
```


```python
total_until_5 = 0
for value in sequence:
    if value == 5:
        break
    total_until_5 += value
```

  - while 반복문은 조건을 명시하고 해당 조건이 False가 되거나 break문을 사용해 명시적으로 반복을 끝낼때까지 블록안의 코드를 수행한다.


```python
x = 256
total = 0
while x > 0:
    if total > 500:
        break
    total += x
    x = x//2
```

  - pass는 파이썬의 아무것도 하지 않음 을 나타낸다. 
  - pass문은 블록안에서 어떤 작업도 실행하지 않을 때 사용됨
  - 이는 파이썬이 블록을 구분하는데 공백문자를 사용하기 때문


```python
if x < 0:
    print 'nagative!'
elif x == 0:
    # todo : 나중에 뭔가 추가해야함
    pass
else:
    print'positive!'
```

    positive!
    

  - 예외처리 : 데이터분석 애플리캐이션에서 많은 함수가 특정 종류의 입력만 처리힘
  - 적절치 않은 입력은 입력을 그대로 반환하는 예외적인 함수를 작성할때, try/except블록을 사용할수 있다


```python
def attempt_float(x):
    try:
        return float(x)
    except:
        return x
```


```python
attempt_float('1.2345')
```




    1.2345




```python
attempt_float('something')
```




    'something'



  - 예외를 무시하지 않고 코드수행가 상관 없이 실행 시키고 싶은 코드는 finally 블록을 사용한다.


```python
f = open(path, 'w')

try:
    write_to_file(f)
finally:
    f.close()
```

  - range와 xrange
  - range함수는 연속된 정수의 리스트를 생성한다
  - start, end, step값을 넘겨서 시작과 끝 간격을 지정할수 있다


```python
range(10)
```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]




```python
range(0, 20, 2)
```




    [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]



  - 아주 큰범위의 값을 사용할때는 xrange를 사용하는 것이 좋다
  - xrange는 range와 같은 인자를 받지만 이터레이터를 반환하여 한 번에 전체 리스트를 생성하는 것이 아니라 필요할때 마다 값을 하나씩 생성한다. 
  - 아래 코드는 0~9999까지의 숫자 중에서 3이나 5배수인 값만 모두 더 한다.


```python
sum = 0
for i in xrange(10000):
    # % is the modulo operator
    if x % 3 ==0 or x % 5 == 0:
        sum += i
```

  - 삼단표현 : 파이썬에서 삼단표현은 if-else블록을 한줄로 표현할수 있도록한다


```python
value = true-expr if condition else 
false-expr
```


```python
if condition:
    value = true=extr
else:
    value = false-expr
```

  - 하나의 표현식만 평가됨, 코드를 줄일때 사용할수 있지만 평가해야하는 표현식이 복잡한경우 가독성을 떨어뜨림


```python
x = 5 
'Non-negative' if x >= 0 else 'Negative'
```




    'Non-negative'


