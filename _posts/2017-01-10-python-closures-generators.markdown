---
layout: post
title: "클로저와 제너레이터" 
category: python
---
## 함수의 리스트
```Python
import re

def match_sxz(noun):
    return re.search('[sxz]$', noun)

def apply_sxz(noun):
    return re.sub('$', 'es', noun)

def match_h(noun):
    return re.search('[^aeioudgkprt]h$', noun)

def apply_h(noun):
    return re.sub('$', 'es', noun)

def match_y(noun):                             
    return re.search('[^aeiou]y$', noun)

def apply_y(noun):                             
    return re.sub('y$', 'ies', noun)

def match_default(noun):
    return True

def apply_default(noun):
    return noun + 's'

rules = ((match_sxz, apply_sxz),               
         (match_h, apply_h),
         (match_y, apply_y),
         (match_default, apply_default)
         )

def plural(noun):           
    for matches_rule, apply_rule in rules:       
        if matches_rule(noun):
            return apply_rule(noun)
```
위의 코드는 3가지로 나뉘어서 볼 수 있습니다.
1. re.search와 re.sub를 각각 기능별로 나누어 함수를 만들었습니다. 
이로써 문자를 찾는 re.search가 match_*함수, 문자를 치환하는 re.sub가 apply_*함수가 됩니다.  
  
2. rules라는 tuple에 이 함수들을 각각 짝지어서 넣었습니다.  
이는 파이썬에서 함수가 객체이기 때문에 가능한 것 입니다. 객체이니 tuple의 값으로 정렬시키는 것이 아무 문제가 없죠.  
  
3. plural함수를 통해서 이 rules라는 tuple의 값을 이용해 원하는 값을 얻어낼 수 있습니다.  
for문을 통해 match_sxz는 matches_rule이 되고 apply_sxz는 apply_rule이 될 것 입니다.  
그리고 for문이 돌아가면서 각 값들은 tuple내부의 다음 index번호에 저장된 값으로 넘어갑니다.  
이렇게 최종적으로 맞는 값이 없어서 match_default로 넘어갈 경우 여기서 무조건 True를 반환해줍니다.  
따라서 `if matches_rule(noun):`는 최소한 마지막에는 무조건 참이기 때문에 `apply_rule(noun)`를 반환해줍니다.  
  
## 패턴의 리스트
  
위와 같은 함수의 리스트는 잘 살펴보면 결국 rules에 의해 배열되고 간접적으로 호출되어 사용되어질 뿐 그 자신이 직접적으로 하는 일은 없습니다.  
그러므로 패턴에 해당하는 rules의 단계에서 이 모든 것이 이루어지게 만든다면 우리는 굳이 여러개의 함수를 정의하는 번거로움을 덜어낼 수 있을 것 입니다.  
  
```Python
import re

def build_match_and_apply_functions(pattern, search, replace):
    def matches_rule(word):                                     
        return re.search(pattern, word)
    def apply_rule(word):                                       
        return re.sub(search, replace, word)
    return (matches_rule, apply_rule)                           
```
build_match_and_apply_functions라는 함수가 정의되고 3개의 인자를 사용합니다.  
그리고 내부에서 matches_rule와 apply_rule라는 2개의 함수를 정의하고 인자로 word를 사용합니다.  
이 2개가 실질적으로 사용되는 적용함수입니다. 이들은 인자로 사용된 word를 내부의 re.search, re.sub에 전달합니다.  
그와 동시에 build_match_and_apply_functions의 인자인 pattern, search, replace 역시 같이 전달합니다.  
  
이처럼 적용함수가 직접 전달받은 것이 아닌 외부함수의 인자를 가져와서 내부에서 사용하는 것을 `클로저(closure)`라고 부릅니다.  
build_match_and_apply_functions는 2개의 함수를 정의한 후 return을 통해 이 2개의 함수를 tuple에 저장하는데요.  
이렇게 return하고 build_match_and_apply_functions가 종료되더라도 각 적용함수에 남아있던 build_match_and_apply_functions의 인자들은 적용함수 내에서 그대로 살아있게 됩니다.  
  
  
```Python
patterns = \                                                        
  (
    ('[sxz]$',           '$',  'es'),
    ('[^aeioudgkprt]h$', '$',  'es'),
    ('(qu|[^aeiou])y$',  'y$', 'ies'),
    ('$',                '$',  's')                                 
  )
rules = [build_match_and_apply_functions(pattern, search, replace)  
         for (pattern, search, replace) in patterns]
```
이렇게 만들어진 build_match_and_apply_functions함수는 위와 같이 patterns라는 tuple을 이용하여 사용하면 for문을 거쳐서 rules라는 list를 생성하게 됩니다.  
이는 함수의 리스트에서 보았던 rules와 기능적으로 완벽하게 일치합니다.  
  
## 패턴 파일
패턴의 리스트를 통해 함수를 정의하여 rules를 생성하는데 성공하였습니다.  
그러나 이 경우 코드 내부에 pattern이라는 이름의 변수로 데이터를 저장해둬야한다는 문제가 발생합니다.  
데이터와 코드를 따로 분리시켜서 관리할 수 있다면 가장 좋겠죠.  
이를 위해 pattern의 내용을 따로 빼내어 pattern.txt 파일을 만들었고 이를 사용하기 위한 코드를 짰습니다.  
```Python
rules = []
with open('pattern.txt', encoding='utf-8') as pattern_file:  
    for line in pattern_file:                                      
        pattern, search, replace = line.split(None, 3)             
        rules.append(build_match_and_apply_functions(              
                pattern, search, replace))
```
  
rules라는 이름의 list를 생성하면서 with를 통해서 open()함수를 같이 실행시켰습니다.  
open함수는 pattern_file이라는 alias를 가진 pattern.txt 파일을 이용해 for문을 돌립니다.  
for문의 line을 통해 해당 파일의 내용을 for문 한 번에 한 줄씩만 사용하도록 하였습니다.  
그리고 split을 통해 한 줄의 문자열인 데이터를 쪼개어 각각 pattern, search, replace변수에 담습니다.  
이 후에는 build_match_and_apply_functions함수를 실행시켜서 적용함수가 담긴 tuple을 생성하고 append()함수를 통하여 rules라는 list에 차례대로 집어넣으면 끝납니다.  
  
이를 통해 데이터와 코드를 따로 관리할 수 있게 되었습니다.  
  
  
## 제너레이터
```Python
def fib(max):
    a, b = 0, 1          
    while a < max:
        yield a          
        a, b = b, a + b  
```
제너레이터은 일반적인 함수와는 다르게 반복문과 특정 규칙을 1번씩 돌릴 수 있도록 만든 것 입니다.  
함수 내에 존재하는 yield 키워드를 이용하여 함수가 일시정지하고 반환할 시점을 지정한 뒤 원할 때 사용할 수 있도록 한 것입니다.  
이를 위해 제너레이터는 제너레이터 객체를 생성하여 시작을 알릴 필요가 있는데요. 이는 간단하게 해당 함수를 실행하기만 하면 됩니다.  
  
```Python
>>> f = fib(10)
>>> f
<generator object fib at 0x000001B2A25C8C50>
>>> next(f)
##=> 0
>>> next(f)
##=> 1
>>> next(f)
##=> 1
>>> next(f)
##=> 2
>>> next(f)
##=> 3
>>> next(f)
##=> 5
>>> next(f)
##=> 8
>>> next(f)
##=> Traceback (most recent call last):
  File "<pyshell#34>", line 1, in <module>
    next(f)
StopIteration
```
위와 같이 인자가 포함된 함수를 f라는 변수에 넣고 실행시키면 `<generator object fib at 0x000001B2A25C8C50>`라는 객체를 반환합니다.  
이 후 next()함수를 통해 실행하면 첫번째 yield키워드가 있는 장소에서 멈추고 a변수의 값을 반한합니다.  
다시 next()함수를 실행하면 yield키워드의 자리부터 시작하여 a,b = b,a+b라는 식을 실행하고 while문의 처음으로 돌아옵니다.  
while문의 조건이 True임을 확인하고 다시 yield에서 멈추고 a변수의 값을 반환합니다. 이번에는 1입니다.  
이런식으로 while문이 False일때까지 반복합니다.  
  
```Python
for n in fib(1000):          
    print(n, end=' ')        
## 0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
print('\n')
print(list(fib(1000)))       
## [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610, 987]
```
for문과 list를 통하여 이런 식으로 사용할 수 있습니다.  
  
  
  
제너레이터의 장점 : yield를 사용하지 않았을 경우 파일에 있는 모든 패턴을 다 읽어와서 데이터로 만들어둡니다. 하지만 제너레이터를 사용하면 꼭 필요한 만큼만 우선 사용하고 추후 필요하면 나머지를 만드는 등의 융통성 있는 작업이 가능합니다.
이를 통해 시작 초기의 속도가 향상되는 효과를 볼 수 있습니다. 
  
제너레이터의 단점 : 제너레이터가 포함된 함수가 호출될 때마다 매번 처음부터 일을 새로 시작해야합니다.  
한 번 호출하면 결과값을 List나 tuple에 저장해두는 것이 아니라 그 때 그 때마다 결과값을 반환하기 때문이죠.  
그래서 전체적인 성능은 떨어집니다.  