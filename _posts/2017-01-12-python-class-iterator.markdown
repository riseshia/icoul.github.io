---
layout: post
title: "class와 Iterator(반복자)" 
category: python
---
```python
class Fib:
    '''피보나치 수열을 하나씩 반환하는 반복자'''

    def __init__(self, max):
        self.max = max

    def __iter__(self):
        self.a = 0
        self.b = 1
        return self

    def __next__(self):
        fib = self.a
        if fib > self.max:
            raise StopIteration
        self.a, self.b = self.b, self.a + self.b
        return fib

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```

## class
파이썬의 class는 함수와 큰 차이가 없습니다.  
class 역시 객체이기 때문에 새로운 class를 정의하거나 다른 class를 상속하거나 instance화 시킬 수도 있습니다.  
명시적인 부분에서 함수와 차이점은 선언할 때 class 뒤에 class명과 :만 붙여주면 된다는 것 입니다.  
  
## &#95;&#95;init&#95;&#95; 메서드
JAVA에는 class를 생성할 시 자동으로 만들어지는 생성자 메서드라는 것이 있습니다.  
파이썬의 class에선 자동으로 생성되지 않지만 비슷한 역할을 하는 &#95;&#95;init&#95;&#95;메서드가 있습니다.  
```python
def __init__(self, max):
        self.max = max
```
피보나치 수열 코드에 있는 &#95;&#95;init&#95;&#95;메서드 입니다.  
&#95;&#95;init&#95;&#95;메서드는 class를 초기화시켜주는 역할을 하는 메서드입니다.  
JAVA의 생성자와 마찬가지로 그 외의 일도 할 수는 있지만 기본적으로 초기화라는 업무만하도록 합시다.  
  
&#95;&#95;init&#95;&#95; 메서드의 첫번째 인자인 self는 모든 클래스 메서드에서 해당 메서드를 호출한 객체를 지칭합니다.   
이 경우에는 Fib class를 가리킵니다.  
JAVA의 this와 유사한데 예약어인 this와 달리 self는 관습어이기 때문에 임의의 다른 이름을 붙여도 상관은 없지만 코드의 명시성을 생각하면 self로 통일하는 것이 좋습니다.  
  
## class instance 생성
앞에서 말했듯 파이썬의 class는 함수와 큰 차이가 없습니다.  
함수와 마찬가지로 class명과 인자를 적어주면 됩니다.  
```python
fib = Fib(100)
print(fib)
##=> <__main__.Fib object at 0x0000016B6AC4AEB8>

print(fib.__class__)
##=> <class '__main__.Fib'>

print(fib.__doc__)
##=> 피보나치 수열을 하나씩 반환하는 반복자

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
  
  
## instance 변수
```python
class Fib:
    '''피보나치 수열을 하나씩 반환하는 반복자'''

    def __init__(self, max):
        self.max = max

    def __iter__(self):
        self.a = 0
        self.b = 1
        return self

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
위 코드를 보시면 self.가 붙은 변수가 있는데 이것을 instance 변수라고 부릅니다.  
이러한 instance 변수는 class 내의 다른 메서드에서 자유롭게 사용할 수 있습니다.  
단, 어디까지나 class instance 내에서 정의된 변수이기 때문에 다른 class instance와는 관계없는 변수입니다.  
  
  
## iterator(반복자)
```python
class Fib:
    '''피보나치 수열을 하나씩 반환하는 반복자'''

    def __init__(self, max):
        self.max = max

    def __iter__(self):
        self.a = 0
        self.b = 1
        return self

    def __next__(self):
        fib = self.a
        if fib > self.max:
            raise StopIteration
        self.a, self.b = self.b, self.a + self.b
        return fib

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
iterator를 설명하기 위해 위의 코드를 다시 가져왔습니다.  
iterator는 &#95;&#95;itor&#95;&#95; 메서드를 호출하는 것으로 시작되는데요. 이 과정은 수동으로 할 수도 있지만 보통 for문이 알아서 호출해줍니다.  
&#95;&#95;itor&#95;&#95; 메서드를 호출함으로써 반복과정을 진행하는데 있어서 필요한 a,b 2개의 변수를 초기화해주었습니다.   
그리고 다음 메서드에서 쓰기 위해 self.를 붙여서 instance변수로 지정하고 이 과정을 self로 반환해줍니다.  
이 때 반환해 준 self는 iterator 객체이며 고로 이후 다른 메서드는 iterator 객체를 인자로 받게됩니다.  
  
다음은 &#95;&#95;next&#95;&#95; 메서드를 실행합니다.  
인자로 받은 self로 self.max, self.a, self.b의 변수를 이용해 목적인 피보나치 수열의 값을 구하고 반환해줍니다.  
그리고 루프가 끝날때까지 &#95;&#95;next&#95;&#95; 메서드를 반복적으로 호출해줍니다.  
루프의 끝은 StopIteration 예외를 출력했을 때 입니다.  
StopIteration 예외를 받은 for문은 에러를 발생시키는 것이 아니라 자동으로 여기서 for문을 종료시키게됩니다.  
  
```python
for n in Fib(1000):
    print(n, end=' ')
## 0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
이 과정을 거치면 위와 같은 수열이 완성됩니다.  

## 복수 규칙 반복자
```python
class LazyRules:
    rules_filename = 'plural6-rules.txt'

    def __init__(self):
        self.pattern_file = open(self.rules_filename, encoding='utf-8')
        self.cache = []

    def __iter__(self):
        self.cache_index = 0
        return self

    def __next__(self):
        self.cache_index += 1
        if len(self.cache) >= self.cache_index:
            return self.cache[self.cache_index - 1]

        if self.pattern_file.closed:
            raise StopIteration

        line = self.pattern_file.readline()
        if not line:
            self.pattern_file.close()
            raise StopIteration

        pattern, search, replace = line.split(None, 3)
        funcs = build_match_and_apply_functions(
            pattern, search, replace)
        self.cache.append(funcs)
        return funcs

rules = LazyRules()

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
위 코드에서 주목해야 할 부분은 2가지입니다.  
__첫째, rules_filename = 'plural6-rules.txt'입니다.__  
이 코드에서는 데이터를 가공할 조건을 담은 패턴 데이터가 존재하는데 이를 class 내에서 관리하는 것이 아닌 외부의 txt 파일에 저장하여 이를 불러와서 사용하는 형태를 취하고 있습니다.  
이를 통해 코드와 데이터가 서로 섞이는 일을 방지할 수 있습니다.  
  
txt 파일 내의 데이터를 제어하는 것은 open()메서드, close()메서드, readline() 메서드입니다.  
처음 &#95;&#95;init&#95;&#95; 메서드가 실행되었을 때 open() 메서드를 통해 패턴이 담긴 txt파일을 가져와서 변수에 담습니다.  
이 후, readLine() 메서드를 이용해 txt 파일의 데이터를 한 줄씩 가져와서 사용합니다.  
`if not line:` 을 통해 더 이상 남은 데이터가 없음을 확인하면 close()메서드를 통해 가져왔던 txt파일을 닫아서 더 이상 사용하지 않겠다고 선언하고 StopIteration을 통해 iterator를 종료시킵니다.  
  
여기서 close() 메서드를 통해 닫는 과정은 앞으로 설명할 부분을 위해 반드시 필요한 작업입니다.  
  
__둘째,__  

```python
self.cache_index += 1
        if len(self.cache) >= self.cache_index:
            return self.cache[self.cache_index - 1]

        if self.pattern_file.closed:
            raise StopIteration
```
__&#95;&#95;next&#95;&#95; 메서드의 이 부분입니다.__  
기본적으로 &#95;&#95;next&#95;&#95;메서드는 일전에 살펴보았던 피보나치 수열 class와 똑같은 구조이지만 이 부분만이 다릅니다.  
이는 생성된 LazyRule instance가 재차 호출되었을 때 다시 처음부터 작업을 반복하는 것이 아닌,  
이미 가져온 부분은 cache에 저장된 데이터를 반환해주고 만약 저번에 미처 가져오지 못 한 데이터가 있었다면 마저 가져오는 작업을 진행하도록 되어있습니다.  
또한, 이전 호출 때 모든 데이터를 가져와서 close() 메서드를 통해 닫았을 경우,  
closed 명령어를 통해 파일이 닫혀있는지 유무를 판단하여 추가적인 작업이 없이 그대로 종료시키는 용도입니다.  
  
즉, 불필요한 작업을 2번 이상 하지 않도록 만들어 둔 제어장치와 같습니다.  
