
# A.3 자료구조와 순차자료형
## A.3.1 튜플
  - 튜플은 1차원의 고정된 크기를 갖는 변경이 불가능한 순차자료형
  - 튜플을 생성하는 방법은 쉼표로 구분된 값을 대입하는 것
  - 괄호를 사용해 값을 묶우 줌으로써 중첩된 튜플을 정의할 수 있다
  - 모든 순차자료형이나 이터레이터는 튜플메서드를 통해 튜플로 변환할수있다.


```python
set([1,2],[3,4])
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-1-05651d9cf283> in <module>()
    ----> 1 set([1,2],[3,4])
    

    TypeError: set expected at most 1 arguments, got 2



```python
tup = 4, 5, 6
tup
```




    (4, 5, 6)




```python
nested_tup = (4,5,6), (7,8)
nested_tup
```




    ((4, 5, 6), (7, 8))




```python
tuple([2,3,4])
```




    (2, 3, 4)




```python
tup = tuple('string')
tup
```




    ('s', 't', 'r', 'i', 'n', 'g')




```python
tup[0]
```




    's'



  - 튜플에 저장된 개체 자체는 변경이 가능하지만 
  - 한번 생성되면 각 슬롯에 저장된 개체를 변경하는것은 불가능함
  - 하지만 append를 사용하면 추가는 가능함
  - 튜플은 +를 활용해 이어붙일 수 있음


```python
tup =tuple(['foo', [1,2],True])
tup[2] = False
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-8-e0511b8ccab7> in <module>()
          1 tup =tuple(['foo', [1,2],True])
    ----> 2 tup[2] = False
    

    TypeError: 'tuple' object does not support item assignment



```python
tup[1].append(3)
tup
```




    ('foo', [1, 2, 3], True)




```python
(4, None, 'foo')+(6,0)+('bar',)
```




    (4, None, 'foo', 6, 0, 'bar')




```python
('foo','bar')*4
```




    ('foo', 'bar', 'foo', 'bar', 'foo', 'bar', 'foo', 'bar')



#### 튜플에서 값 분리하기


```python
tup = (4,5,6)
a,b,c = tup
b
```




    5




```python
tup = 4, 5, (6, 7)
a, b, (c, d) = tup
d
```




    7



  - 이 기능을 사용하변 변수이름을 바꿀때 다른 언어에서는 다음처럼 처리해 쉽게 해결할수 있다.


```python
tmp = a
a = b
b = tmp
```


```python
b,a = a, b
```


```python
seq = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
for a, b, c in seq:
    pass
```

#### 튜플메서드
  - 튜플은 내용변경이 불가능하므로 인스턴스 메서드도 많지 않다.
  - 유용하게 사용되는 메서드는 count 메서드


```python
a = (1,2,2,3,4,2)
a.count(2)
```




    3



### A.3.2 리스트
  - 튜플과 다르게 크기나 내용수정이 가능함
  - 리스트는 []괄호나 list함수로 생성
  - 1차원 순차자료형으로 많은 함수에서 사용


```python
a_list = [2, 3, 7, None]
```


```python
tup = ['foo', 'bar', 'baz']
```


```python
b_list = list(tup)
b_list
```




    ['foo', 'bar', 'baz']




```python
b_list[1] = 'peekboo'
b_list
```




    ['foo', 'peekboo', 'baz']



#### 원소 추가하고 삭제 
  - append메서드를 사용해 리스트의 끝에 추가
  - insert메서드로 리스트의 특정 위치에 추가
  - pop메서드는 특정위치에서 값을 반한하고 해당값을 리스트에서 삭제
  - remove 메서드를 원소를 삭제(리스트 맨앞에 값부터 삭제됨)


```python
b_list.append('dwarf')
b_list

```




    ['foo', 'peekboo', 'baz', 'dwarf']




```python
b_list.insert(1, 'red')
b_list
```




    ['foo', 'red', 'peekboo', 'baz', 'dwarf']




```python
b_list[2]
b_list
```




    ['foo', 'red', 'peekboo', 'baz', 'dwarf']




```python
b_list.append('foo')
b_list
```




    ['red', 'peekboo', 'baz', 'dwarf', 'foo', 'foo']




```python
b_list.remove('foo')
b_list
```




    ['red', 'peekboo', 'baz', 'dwarf', 'foo']



  - in 함수를 사용해 리스트의 값을 확인할 수 있다.


```python
'dwarf' in b_list
```




    True



  - 리스트 이어붙이기


```python
[1,2, 'kim'] + [7,8,(2,3)]
```




    [1, 2, 'kim', 7, 8, (2, 3)]




```python
x = [4, None, 'foo']
```


```python
x.extend([7,8,(2,3)]) ; x
```




    [4, None, 'foo', 7, 8, (2, 3), 7, 8, (2, 3)]



  - 정렬 : sort함수 사용


```python
a = [7,2,5,1,3]
a.sort()
a
```




    [1, 2, 3, 5, 7]




```python
b = ['aa', 'bbbb', 'zzz', 'c']
b.sort(key=len)
b
```




    ['c', 'aa', 'zzz', 'bbbb']



#### 이진탐색과 정렬된 리스트 유지하기
  - bisect 모듈은 이진탐색과 정렬된 리스트에 값을 추가하는 기능제공
  - bisect.bisect는 값이 추가될 때 리스트가 정렬된 상태를 유지할 수 있는 위치 반환
  - bisect.insort는 실제 정렬된 상태 유지한태 값 추가


```python
import bisect
c = [1, 2, 2, 2, 3, 4, 7]
bisect.bisect(c, 2)
```




    4




```python
bisect.bisect(c, 5)
```




    6




```python
bisect.insort(c, 6)
c
```




    [1, 2, 2, 2, 3, 4, 6, 7]



#### 슬라이싱
  - 리스트와 같은 자료형은 색인 연산자[] 안에 : 기호를 사용해 원하는 만큼 잘라낼수 있다


```python
seq = [1, 2, 3, 4, 5, 6, 7, 8, 9]
seq[0:5]
```




    [1, 2, 3, 4, 5]




```python
seq[3:4] = [0,9]
seq
```




    [1, 2, 3, 0, 9, 9, 5, 6, 7, 8, 9]




```python
seq[:5]
```




    [1, 2, 3, 0, 9]




```python
seq[3:]
```




    [0, 9, 9, 5, 6, 7, 8, 9]




```python
seq[-4:]
```




    [6, 7, 8, 9]




```python
seq[-6:-2]
```




    [9, 5, 6, 7]




```python
seq
```




    [1, 2, 3, 0, 9, 9, 5, 6, 7, 8, 9]




```python
seq[::2]
```




    [1, 3, 9, 5, 7, 9]




```python
seq[::-1]
```




    [9, 8, 7, 6, 5, 9, 9, 0, 3, 2, 1]



### A.3.3 내장 순차 자료형 함수
#### enumerate
  - 순차 자료형에서 현재 아이템의 색인을 함께 처리할때 사용


```python
i = 0
for value in collection
 # value 가지고 무언가 한다
    i + = 1
```

  - 위 코드를 (i, value)튜플을 반환하는 enumerate함수로 작성하면 다음과같다


```python
for i value in enumerate(collection)
 # value가지고 무언가 한다
```

  - 색인을 통해 데이터에 접근할때 enumerate를 사용하는 유용한 패턴은 순차자료형에서 값과 그 위치를 dict에 넘겨주는것


```python
some_list = ['foo', 'bar', 'baz']
```


```python
mapping = dict((v,i) for i, v in enumerate(some_list))
```


```python
mapping
```




    {'bar': 1, 'baz': 2, 'foo': 0}



#### sorted
  - sorted함수는 정렬된 새로운 순차 자료형을 반환한다.


```python
sorted([7,1,2,6,0,3,2])
```




    [0, 1, 2, 2, 3, 6, 7]




```python
sorted('horse race')
```




    [' ', 'a', 'c', 'e', 'e', 'h', 'o', 'r', 'r', 's']




```python
sorted(set('this is'))
```




    [' ', 'h', 'i', 's', 't']



#### zip
  - zip함수는 여러개의 리스트나 튜플 또는 다른 순차자료형을 서로 짝지어서 튜플의 리스트를 생성한다.


```python
seq1 = ['foo', 'bar', 'baz']
seq2 = ['one', 'two', 'three']
zip(seq1, seq2)
```




    [('foo', 'one'), ('bar', 'two'), ('baz', 'three')]




```python
seq3 = [False, True]
zip(seq1, seq2, seq3)
```




    [('foo', 'one', False), ('bar', 'two', True)]



  - enumerate와 함께사용


```python
for i, (a,b) in enumerate(zip(seq1, seq2)):
    print('%d: %s, %s') %(i, a, b)
```

    0: foo, one
    1: bar, two
    2: baz, three
    

#### reversed
  - 순차 자료를 역순으로 순회


```python
list(reversed(range(10)))
```




    [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]



### A.3.4 사전
  - 유연한 크기를 가지는 키-밸류 쌍으로 키와 값은 모두 객체이다.
  - {}를 사용하여 콜론으로 구분된 키와 값을 넣는다.


```python
empty_dict = {}
d1 = {'a':'some value', 'b':[1,2,3,4]}
```


```python
d1
```




    {'a': 'some value', 'b': [1, 2, 3, 4]}




```python
d1[7] = 'an integer'
d1
```




    {7: 'an integer', 'a': 'some value', 'b': [1, 2, 3, 4]}




```python
d1['b']
```




    [1, 2, 3, 4]




```python
'b' in d1
```




    True



  - del 이나 pop 메서드를 사용해 값을 삭제


```python
d1[5] = 'some value' ; d1
```




    {5: 'some value', 7: 'an integer', 'a': 'some value', 'b': [1, 2, 3, 4]}




```python
d1['dummy'] = 'another value' ;d1
```




    {5: 'some value',
     7: 'an integer',
     'a': 'some value',
     'b': [1, 2, 3, 4],
     'dummy': 'another value'}




```python
del d1[5] ; d1
```




    {7: 'an integer',
     'a': 'some value',
     'b': [1, 2, 3, 4],
     'dummy': 'another value'}




```python
ret = d1.pop('dummy')
ret
```




    'another value'



  - keys 메서드와 values 메서드는 각각 키와 값이 담긴 리스트 반환


```python
d1.keys() 
```




    ['a', 'b', 7]




```python
 d1.values()
```




    ['some value', [1, 2, 3, 4], 'an integer']



  - update 함수로 다른 사전과 합칠수 있다.


```python
d1.update({'b':'foo', 'c':12})
d1
```




    {7: 'an integer', 'a': 'some value', 'b': 'foo', 'c': 12}



#### 순차자료구조에서 사전생성하기
  - 2개의 순차자료의 각 원소를 찍지어 사전으로 만들기


```python
mapping = dict(zip(range(5), reversed(range(5))))
mapping
```




    {0: 4, 1: 3, 2: 2, 3: 1, 4: 0}



#### 세련되게 사전생성


```python
if key in some_dict:
    value = some_dict[key]
else:
    value = defailt_value
```

  - get함수로 위의 코드의 else블록을 다음처럼 간단히 작성할수 있다.


```python
value = somedict.get(key, default_value)
```

  - 단어의 시작글자에 따라 사전에 리스트로 저장


```python
words = ['apple', 'bat', 'bar', 'atom', 'book']
by_letter = {}
```


```python
for word in words:
    letter = word[0]
    if letter not in by_letter:
        by_letter[letter] = [word]
    else:
        by_letter[letter].append(word)
```


```python
by_letter
```




    {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book']}



  - setdefault 함수를 쓰면 if-else블록을 아래처럼 간단히작성할수 있다.


```python
by_letter.setdefault(letter, []).append(word)
```


```python
by_letter
```




    {'a': ['apple', 'atom'], 'b': ['bat', 'bar', 'book', 'book']}



  - 내장 collection 모듈은 defaultdict라는 클래스를 갖고있음
  - defaultdict는 자료형 또는 각 사전의 각 슬롯에 담길 기본값을 생성하는 함수를 넘겨 사전을 생성하는거


```python
from collections import defaultdict
by_letter = defaultdict(list)
for word in words:
    by_letter[word[0].append(word)]
```

#### 유효한 사전 키
  - 사전의 키는 스칼라형이나 튜플처럼 값이 바뀌지 않는 객체만 사용가능
  - 키로 사용가능한지는 hash함수로 확인


```python
hash('string')
```




    -1542666171




```python
hash((1,2,(2,3)))
```




    1387206534




```python
hash((1, 2, [2, 3]))
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-87-c7446717475e> in <module>()
    ----> 1 hash((1, 2, [2, 3]))
    

    TypeError: unhashable type: 'list'


  - 리스트를 키로 사용하려면 튜플로 바꿔야함


```python
d = {}
d[tuple([1, 2, 3])] = 5
d
```




    {(1, 2, 3): 5}



### A.3.5 세트
  - 세트는 유일한 원소만 담는 정렬되지 않은 자료형
  - 사전과 유사하지만 값은 없고 키만 가지고 있다
  - set 함수를 사용하거나 중괄호를 사용할수 있다


```python
set([1,2,3,3,4,4,5])
```




    {1, 2, 3, 4, 5}




```python
{2,2,2,2,1,3,3}
```




    {1, 2, 3}




```python
a = {1,2,3,4,5}
b = {3,4,5,6,7,8}
a | b
```




    {1, 2, 3, 4, 5, 6, 7, 8}




```python
a & b
```




    {3, 4, 5}




```python
a - b
```




    {1, 2}




```python
a ^ b #(대칭 차집합)
```




    {1, 2, 6, 7, 8}




```python
a_set = {1, 2, 3, 4, 5}
{1, 2, 3}.issubset(a_set) #부분집합
```




    True




```python
a_set.issuperset({1, 2, 3}) #확대집합
```




    True




```python
{1,2,3} == {1,2,3}
```




    True



### A.3.6 리스트 내포, 사전 내포, 세트 내포
  - 간결한 표현으로 새로운 리스트를 만들수 있다
  - [expr for val in collection if condition]


```python
strings = ['a', 'as', 'bat', 'car', 'dove', 'python']
```


```python
[x.upper() for x in strings if len(x) > 2]
```




    ['BAT', 'CAR', 'DOVE', 'PYTHON']



  - 세트 내포는 대괄호 대신 중괄호 사용
  - 사전 내포는 아래와 같음


```python
{key-expr : value-expr for value in collection if condition}
```


```python
unique_lengths = {len(x) for x in strings}
unique_lengths
```




    {1, 2, 3, 4, 6}




```python
loc_mapping = {val : index for index, val in enumerate(strings)}
loc_mapping
```




    {'a': 0, 'as': 1, 'bat': 2, 'car': 3, 'dove': 4, 'python': 5}




```python
loc_mapping = dict((val, idx) for idx, val in enumerate(strings))
loc_mapping
```




    {'a': 0, 'as': 1, 'bat': 2, 'car': 3, 'dove': 4, 'python': 5}



  - 중첩된 리스트 내포
  - 남녀따로 저장됨, 각 이름에서 e가 2개 이상있는 이름의 리스트 구성


```python
all_data = [['Tom', 'Billy', 'Jefferson', 'Andrew', 'Wesley', 'Steven', 'Joe'],
           ['Susie', 'Casey', 'Jill', 'Ana', 'Eva', 'Jennifer', 'Stephanie']]
```


```python
result = [name for names in all_data for name in names
          if name.count('e') >= 2]
result
```




    ['Jefferson', 'Wesley', 'Steven', 'Jennifer', 'Stephanie']




```python
unique_lengths = {len(x) for x in strings}
unique_lengths
```




    {1, 2, 3, 4, 6}




```python
loc_mapping = {val : index for index, val in enumerate(strings)}
loc_mapping
```




    {'a': 0, 'as': 1, 'bat': 2, 'car': 3, 'dove': 4, 'python': 5}



  - 숫자튜플이 담긴 리스트를 단순리스트로 변환


```python
some_tuple = [(1,2,3), (4,5,6), (7,8,9)]
```


```python
flattend = [x for tup in some_tuple for x in tup]
flattend
```




    [1, 2, 3, 4, 5, 6, 7, 8, 9]



### A.4 함수

  - 함수는 def 예약어로 정의하고 return 예약어를 사용해 값을 반환한다


```python
def my_function(x, y, z=1.5):
    if z > 1:
        return z*(x+y)
    else:
        return z/(x+y)
```


```python
my_function(1,2)
```




    4.5




```python
my_function(1,2,z=0.7)
```




    0.2333333333333333




```python
my_function(3.14, 7, 3.5)
```




    35.49



#### A.4.1 네임스페이스, 스코프, 지역함수
  - 함수는 전역과 지역 수가지 스코프에서 변수를 참조한다.
  - 변수의 스코르를 설명하는 다른용어로 네임스페이스가 있다.
  - 함수 내부에서 선언된 변수는 기본적으로 모두 지역 네임스페이스에 속함
  - 지역네임 스페이스는 함수가 호룻될때 생성되며 함수의 인자를 통해 즉시 생성됨
  - 함수의 실행이 끝나면 네임스페이스는 사라진다.


```python
def func():
    a = []
    for i in range(5):
        a.append(i)
```


```python
a=[]
def func():
    a = []
    for i in range(5):
        a.append(i)
```


```python
a = None
def bind_a_variable():
    global a
    a = []
bind_a_variable()
```

  - 함수는 어디서나 선언할수 있으며 함수가 호출되었을때 지역함수를 선언할수도 있다.
  - 상위함수가 호출되어야 하위함수가 존재하며 상위함수가 끝나면 하위함수도 사라짐


```python
def outer_function(x, y, z):
    def inner_function(a, b, x):
        pass
    pass
```

### A.4.2 여러값 반환하기


```python
def f():
    a = 5
    b = 6
    c = 7
    return a, b, c

a, b, c = f()
```


```python
return_value = f()
```


```python
def f():
    a = 5
    b = 6
    c = 7
    return ('a':a, 'b':b , 'c':c)
```

### A.4.3 함수도 개체다
  - 분석을 위해서는 문자열 정형화해야하는 경우가 있다.


```python
states = ['  Alabama', 'Georgia!', 'Geogia', 'geogia', 'FlOrIda',
         'south carolina##', 'West virginia?']
```


```python
import re

def clean_strings(strings):
    result = []
    for value in strings:
        value = value.strip()
        value = re.sub('[!#?]', '', value) #문장부호제거
        value = value.title()
        result.append(value)
    return result
```


```python
clean_strings(states)
```




    ['Alabama',
     'Georgia',
     'Geogia',
     'Geogia',
     'Florida',
     'South Carolina',
     'West Virginia']



  - 연산의 리스트를 작성하고 문자열에 적용할 수 있다.


```python
def remove_punctuation(value):
    return re.sub('[!#?]', '', value)
```


```python
clean_ops = [str.strip, remove_punctuation, str.title]
```


```python
def clean_strings(strings, ops):
    result = []
    for value in strings:
        for function in ops:
            value = function(value)
        result.append(value)
    return result
```


```python
clean_strings(states, clean_ops)
```




    ['Alabama',
     'Georgia',
     'Geogia',
     'Geogia',
     'Florida',
     'South Carolina',
     'West Virginia']




```python
map(remove_punctuation, states)
```




    ['  Alabama',
     'Georgia',
     'Geogia',
     'geogia',
     'FlOrIda',
     'south carolina',
     'West virginia']



### A4.4 익명함수

  - 파이썬은 익명함수 혹은 람다 함수라고 하는 값을 반환하는 단순한 한문장으로 이뤄진 함수를 지원한다.
  - lamda예약어를 사용해서 정의하며 이는 '익명함수를 선언한다'라는 의미다.


```python
def short_function(x):
    return x*2

equiv_anon = lambda x : x*2
```


```python
def apply_to_list(some_list, f):
    return [f(x) for x in some_list]
```


```python
ints = [4, 0, 1, 5, 6]
apply_to_list(ints, lambda x: x*2)
```




    [8, 0, 2, 10, 12]



  - 문자를 정렬하는 익명함수


```python
strings = ['foo', 'card', 'bar', 'aaaa', 'abab']
strings.sort(key = lambda x: len(set(list(x))))
```


```python
strings
```




    ['aaaa', 'foo', 'abab', 'bar', 'card']



### A4.5 클로저 : 함수를 반환하는 함수
  - 클로저는 함수에 의해 반환되는 동적으로 생성된 함수이다.
  - 핵심은 반한되는 함수는 그 함수가 생성된 시점의 지역 네임스페이스 변수에 접근할 수 있다는 점이다.
  - 먼말인지 모르겠음 pass


```python
def make_closure(a):
    def closure():
        print('I know the secret: %d' %a)
    return closure

closure = make_closure(5)
```

### A4.6 *arg와 *kwargs를 사용해서 호출문법 확장하기
  - 이거도 먼말인지..도저히...pass


```python
func(a, b, c, d = some, e=value)
```

### A.4.7 커링 : 일부 인자만 취하기
  - 함수에서 일부 인자를 고정해 새로운 함수를 만드는 기법


```python
def add_number(x, y):
    return x + y
```

  - 위 함수를 이용해 하나의 변수만 인자로 받아 5를 더하는 새로운 함수생성


```python
add_five = lambda y: add_number(5, y)
```

  - 내장 functools 모듈의 partial함수를 이용하면 더 단순화할 수 있음


```python
from functools import partial
add_five = partial(add_number, 5)
```

### A.4.8 제너레이터
  - 파이썬은 리스트 내의 객체가 파일의 각 행 같은 순차적인 자료를 순회하는 일관적인 방법을 제공한다.
  - 이터레이터 프로토골을 이용해 순회가 가능한 객체를 만들 수 있다.
  - 사전을 순회하면 사전의 키가 반환된다.


```python
some_dict = {'a':1, 'b':2, 'c':3}

for key in some_dict:
    print key,
```

    a c b
    


```python
dict_iterator = iter(some_dict)
dict_iterator
```




    <dictionary-keyiterator at 0x3f06cc8>



  - 제러레이터는 순회가 가능한 개체를 생성하는 간단한 방법이다.
  - 리스트나 리스트와 유사한 개체를 취하는 대부분 메서드는 순회가 가능한 객체도 허용한다.
  - 여기에는 min, max, sum같은 내장메서드와 list, tuple 같은 메서드도 포함된다.


```python
list(dict_iterator)
```




    ['a', 'c', 'b']



  - 제너레이터는 순차적인 값을 매 요청시마다 하나씩 반환한다.
  - 제너레이터를 생성하려면 함수에 return 대신 yield 예약으를 사용한다.


```python
def squares(n=10) :
    for i in xrange(1, n+1):
        print 'Generating squares from 1 to %d' %(n**2)
        yield i**2
```


```python
gen = squares()
gen
```




    <generator object squares at 0x0000000003F03AB0>




```python
for x in gen:
    print x
```

    Generating squares from 1 to 100
    1
    Generating squares from 1 to 100
    4
    Generating squares from 1 to 100
    9
    Generating squares from 1 to 100
    16
    Generating squares from 1 to 100
    25
    Generating squares from 1 to 100
    36
    Generating squares from 1 to 100
    49
    Generating squares from 1 to 100
    64
    Generating squares from 1 to 100
    81
    Generating squares from 1 to 100
    100
    

#### 제너레이터 표현식
  - 리스트, 사전, 세트 내포와 유사한 방식으로 제너레이터 생성
  - 리스트 내포에서 대괗 사용하듯 이 괄호를 사용해서 제너레이터 생성


```python
gen = (x**2 for x in xrange(100))
gen
```




    <generator object <genexpr> at 0x0000000003F03E10>




```python
def _make_gen():
    for x in xrange(100):
        yield x**2
    gen = _make_gen
```


```python
sum(x**2 for x in xrange(100))
```




    328350




```python
dict((i, i**2) for i in xrange(5))
```




    {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}



#### itertools 모듈
  - itertools모듈은 많은 일반 데이터 알고리즘을 위한 제너레이터를 포함하고 있다.
  - 예를들어 groupby는 순차자료구조와 함수를 받아 인자로 받은 함수에서 반환하는 값에 다라 그룹을 지어준다.


```python
import itertoools 
```


    ---------------------------------------------------------------------------

    ImportError                               Traceback (most recent call last)

    <ipython-input-29-323176b31eb1> in <module>()
    ----> 1 import itertoools
    

    ImportError: No module named itertoools



```python
first_letter = lambda x: x[0]
```


```python
names = ['Alan', 'Adam', 'Wes', 'Will', 'Albert', 'Steven']
```

### A.5 파일과 운영체제
  - pandas.read_csv 등을 사용해 파일을 읽어온다.
  - 파일을 읽고 쓰기 위해서는 내장함수인 open을 이용해 파일의 상대경로 혹은 절대 경로를 넘겨줘야함  
  - 파일을 읽고 쓰기 위해서는 내장함수인 open을 이용해 파일의 상대경로 혹은 절대 경로를 넘겨줘야함


```python
path = '‪C:\Users\user\Desktop\data\six_month.csv'
```


```python
f = open(path.r)
```


    ---------------------------------------------------------------------------

    AttributeError                            Traceback (most recent call last)

    <ipython-input-9-e4b5f9a6e95c> in <module>()
    ----> 1 f = open(path.r)
    

    AttributeError: 'str' object has no attribute 'r'


  - f = open(path, 'w') 로 연다면 새로운 파일이 생성되고 파일이 내용이 새로운 내용으로 덮어쓴다.

  - 파이썬 파일 모드
  - r : 읽기 전용 모드
  - w : 쓰기 전용 모드
  - a : 기존파일에 추가한다(파일이 없을땐 새로 생성한다)
  - r+ : 읽기/쓰기 모드
  - b : 이진파일모드, 읽기/쓰기 모드에 추가해서 rb, rw처럼 사용한다.
  - U : 유니버설 개행모드, U만 넘기거나 읽기모드에 추가해서 rU처럼 사용


```python

```
