
# ch.3 IPython 소개

## 3.1 IPython 기본
  - 명령어를 입력하여 실행시킬 수 있음


```python
a = 5
a
```




    5




```python
from numpy.random import randn
```


```python
data = {i : randn() for i in range(7)}
data
```




    {0: 0.530991543128973,
     1: 0.6018729297849643,
     2: 0.3647993295723022,
     3: -0.8787495322231684,
     4: 2.5989791500393413,
     5: -0.5930493589857931,
     6: 1.540699459314777}




```python
print data
```

    {0: 0.530991543128973, 1: 0.6018729297849643, 2: 0.3647993295723022, 3: -0.8787495322231684, 4: 2.5989791500393413, 5: -0.5930493589857931, 6: 1.540699459314777}
    

### 3.1.1탭자동 완성
  - 탭을 누르면 네입스페이스에서 그 시점까지 입력한 내용과 맞는 변수를 자동으로 찾아줌


```python
an_apple = 27
an_example = 42
```


```python
an_apple #an<tab>
```




    27



  - 자동완성기능을 활용할 수 있음


```python
b = [1,2,3]
```


```python
b.append  #b.<tab>
```




    <function append>



  - 모듈도 동일하게 작동함
  - 파일경로를 입력하고 탭을 누르면 입력한 문자열에 맞는 파일 경로를 컴퓨터 파일시스템 내에서 찾아줌


```python
import datetime
```


```python
datetime.MAXYEAR  #datetime.<tab>
```




    9999



### 3.1.2 자기관찰
  - 변수 앞이나 뒤에 ?기호를 붙이면 그 개체에 대한 일반정보를 출력한다.
  - 함수에 ??기호를 분이면 함수의 소스코드를 보여준다 add_number??

b = [1,2,3]
?b

## 3.1.3 %run명령어
  - %run 명령어를 사용하면 IPython 세션안에서 파이썬 프로그램 파일을 불러와 실행할 수 있다
  - 실행중인 코드를 중지시키려면 중간에 Ctl+c를 누르면 된다


```python
  %run c:/py_test/test1.py
```

    hello world
    5
    

### 3.1.4 클립보드에 있는 코드 실행하기
  - ctl + shift + v 를 누른다
  - 이방법은 클립보드의 각 줄을 한줄씩 입력하는 방식으로 줄바꿈을 <return>처리한다


```python
x = 5
```


```python
y = 7
```


```python
if x > 5 :
    x += 1
    
```


```python
    y = 8
```

  - 들여쓰기 된 블록안의 빈줄을 블록이 끝난것으로 인식하기 때문에 IndertationError이 발생
  - %paste 혹은 %cpaste 매직함수를 이용해야한다. 
  - %paste함수는 클립보드에 있는 텍스트를 단일블록으로 실행한다.
  - %cpaste함수는 코드를 붙여넣을때 특수한 프롬프트를 제공한다.


```python
%paste
x = 5
y = 7
if x > 5 :
    x += 1
    
    y = 8
```

    ERROR: Line magic function `%paste` not found.
    

### 3.1.5 키보드 단축키

  - ctr + P  위 화살표 : 명령어 히스토리 역순 검색
  - ctr + N 아래 화살표 : 명령어 히스토리 최근순 검색
  - ctr + R  : readline 명령어 형식의 히스토리검색
  - Ctr+shift+V : 클립보드에 텍스트 붙여넣기
  - ctr + C : 실행중인 코드 중단
  - ctr + A : 커서를 줄의 처음으로 이동
  - ctr + E : 커서를 줄의 끝으로 이동
  - ctr + K : 커서가 놓인 곳부터 줄의 끝까지 텍스트 삭제
  - ctr + U : 현재 입력된 모든 텍스트 지우기
  - ctr + F : 커서를 앞으로 한글자씩 이동하기
  - ctr + B : 커서를 뒤로 한글자씩 이동하기
  - ctr + L : 화면 지우기

### 3.1.6 예외와 트레이스백
  - %run 명령어를 사용하면 코드실행중 오류가 발생했을때 전체 스택정보를 각 위치별 문맥정보와 함께 볼수 있음

### 3.1.7 매직명령어
  - 일반적인 작업이나 Ipython시스템 동작을 제어하는 특수명령어
  - 매직명령어 앞에 %를 붙임
  - 행렬곱셈 코드가 실행되는 시간을 측정할때 %timeit 매직함수 사용


```python
from numpy.random import randn
```

a = np.random.randn(100,100)
%time np.dot(a, a)

  - 매직명령어는 추가적인 옵션을 필요로하며 ?를 이용해 옵션을 볼수 있다.
  - %quickref나 %magic 명령을 통해서 사용 가능한 모든 특수명령어를 확인해두는것이 좋다.
  - 매직명령어는 87p 참조

### 3.1.8 Qt기반의 GUI콘솔 (나중에 살표보겠다)
  - 리치텍스트 위젯기능을추가한 GUI콘솔개발, pyQT나 Pyslide가 설치필요함

### 3.1.9 Pylab 모드와 Matplolib 통합
  - Matplolib 및 다양한 라이브러리 사용이 쉽다. IPython은 GUI프레임워크를 이용해 내부에서 멈주칮 않고 작업을 계속할수 있도록 구현되어있다.

## 3.2 명령어 히스토리 사용하기
  - 검색, 자동완성, 최소한의 입력으로 이전 명령어 재실행
  - 세션간의 명령어 히스토리 유지
  - 입,출력 히스토리를 파일에 기록

### 3.2.1 명령어 검색과 재사용
  - ctrl + p / ctrl + N 또는 위 아래 화살표키를 사용 최근 입력한 명령어 검색
  - ctrl + r 을 누르면 유닉스 셸의 readline명령어 처럼 부분 순차검색 

### 3.2.2 입출력 변수
  - IPython은 입력한 내용과 출력된 결과물을 특수한변수에 저장한다.
  - 마지막 2개의 결과를 저장하는 바로 이전 결과는 _변수, 그 이전 결과는 __변수에 저장한다
  - 입력변수는 iX(X는 입력줄번호) 변수에 저장 / 출려변수는 _X변수에 저장된다


```python
2**27
```




    134217728




```python
_
```




    134217728




```python
foo = 'bar'
```


```python
foo
```




    'bar'




```python
_i4
```




    u'foo'




```python
_4
```




    'bar'



### 3.2.3 입출력 기록하기
  - 입출력을 포함한 전체 콘설 세션의 로그를 %logstart를 사용해서 기록할수 있다. 
  - 관련함수로 %logoff, %logon, %logstate, %logstop 있다


```python
%logstart
```

    Activating auto-logging. Current session state plus future input saved.
    Filename       : ipython_log.py
    Mode           : rotate
    Output logging : False
    Raw input log  : False
    Timestamping   : False
    State          : active
    

## 3.3 운영체제와 함께 사용하기
  - 파이썬은  운영체제 셸과 강력하게 통합되어 있다.
  - 윈도우나 유닉스 셀이 일반적인 명령행에서 할수 있는 작업이 가능

  - !cmd   :   시스템셸에서 cmd 명령어 실행
  - output = !cmd args   :   cmd명령어를 실행하고 표준출력 결과를 output에 저장
  - %alias alias_name cmd   :   시스템 명령어에 대한 별칭을 정의한다
  - %bookmark   :   ipython의 디렉터리 북마크 시스템을 활용
  - %cd directory   :   시스템의 작업 디렉토리를 directory로 변경한다
  - %pwd   :   현재 시스템의 작업 디렉토리를 반환한다
  - %pushd directory   :   현재 디렉토리를 스택에 추가하고 새로운 디렉토리로 이동한다
  - %popd   :   스택에 저장된 디렉토리를 꺼내서 그 디렉토리로 이동한다
  - %dirs   :   현재 디렉토리 스택에 저장된 디렉토리 목록을 보여준다
  - %dhist   :   접근했던 디렉토리 히스토리를 출력한다
  - %env   :   시스텝 환견변수를 사전타입으로 출력한다

### 3.3.1 셸 명령어와 별칭 

### 3.3.2 디렉토리 북마크 시스템
  - 자주사용하는 디렉토리에 별칭을 저장해두고 쉽게 이동할수 있다


```python
%bookmark db c:/py_test
```


```python
cd db
```

    (bookmark:db) -> c:/py_test
    c:\py_test
    

## 3.4 소프트웨어 개발도구

### 3.4.1 인터랙티브 디버거

### 3.4.2 코드시간 측정 %time과 %timeit
import time
start = time.time()
for i in range(iterations):
    # some code to run here
elapsed_per = (time.time() - start) / iterations
### 3.4.3 기본적인 프로파일링 : %prun 과 %run -p


```python
import numpy as np
from numpy.linalg import eigvals

def run_experiment(niter=100):
    K = 100
    results = []
    for _ in xrange(niter):
        mat = np.random.randn(K, K)
        max_eigenvalue = np.abs(eigvals(mat)).max()
        results.append(max_eigenvalue)
    return results
some_results = run_experiment()
print 'Lagest one we saw: %s' %np.max(some_results)
```

    Lagest one we saw: 11.7354291978
    


```python
python -m cProfile cprof_example.py
```


      File "<ipython-input-1-9a3aab209a0a>", line 1
        python -m cProfile cprof_example.py
                         ^
    SyntaxError: invalid syntax
    


### 3.4.4 함수 각 줄마다 프로파일링 하기

## 3.5 IPython HTML 노트북
  - 대화형 컴퓨팅 도구이며 연구와 교육을 위해 재사용이 가능한 이상적인 매체

## 3.6 IPython을 사용한 제품개발을 위한 팁

### 3.6.1 모듈 의존성 리로딩하기
 - import some_lib
 - reload(some_lib)

### 3.6.2 코드설계 팀
  - 관련있는 객체와 데이터는 유지
  - 중첩을 피하자
  - 긴파일에 대한 두려움을 버리자

## 3.7 IPython 고급기능


```python

```
