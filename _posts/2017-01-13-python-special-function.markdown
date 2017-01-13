---
layout: post
title: "특수 함수(special function)" 
category: python
---

## &#95;&#95;repr&#95;&#95;(self)
'공식적인' 문자열을 반환하는 함수입니다.  
만약 &#95;&#95;str&#95;&#95;함수가 정의되지 않았을 경우 '비공식적인' 문자열의 반환에도 &#95;&#95;repr&#95;&#95;이 사용됩니다.  
(추후 추가)  
  
----------------------------------------------------------------------------------
  
## &#95;&#95;str&#95;&#95;(self)
'비공식적인' 문자열을 반환하는 함수. print(문자열)을 사용할 때 호출됩니다.  
  
----------------------------------------------------------------------------------
  
## &#95;&#95;bytes&#95;&#95;(self)
byte타입의 문자열을 계산할 때 쓰입니다. 반드시 byte타입을 반환합니다.  
  
----------------------------------------------------------------------------------
  
## &#95;&#95;format&#95;&#95;(self, format_spec)
&#95;&#95;format&#95;&#95; 함수는 객체의 형식화 된 문자열을 생성합니다.  
이를 위해 두번째 인자인 format_spec에는 형시화 옵션을 설명하는 문자열을 넣습니다.  
format_spec이 어떤 옵션을 설명할지는 입력하는 값에 따라 달라지며 일반적으로는 내장된 유형 중에서 골라서 서식을 위임하거나 비슷한 형식 지정 옵셥 구문을 사용합니다.  
  
----------------------------------------------------------------------------------
  
## 반복자 특수 함수(iterator spectial function)
  
__&#95;&#95;iter&#95;&#95;__
&#95;&#95;iter&#95;&#95;함수는 새로운 반복자를 만들때마다 호출됩니다.  
반복자를 초기화하는 용도로 사용됩니다.  
  
__&#95;&#95;next&#95;&#95;__
&#95;&#95;next&#95;&#95;함수는 반복자에서 다음 값을 가져올 때 호출하는 함수입니다.  
  
__&#95;&#95;reversed&#95;&#95;__
이 함수는 잘 쓰이지 않지만 이미 존재하는 sequence를 받아 이를 마지막부터 처음까지 역순으로 yield하는 함수입니다.  
  
----------------------------------------------------------------------------------
  
## 계산된 속성(computed attributes)
__&#95;&#95;getattribute&#95;&#95;(값)__
이 메서드가 class 내에 존재한다면 특정 유형이나 메서드 이름이 참조될 때마다 이 메서드를 호출합니다.  
  
__&#95;&#95;getattr&#95;&#95;(값)__
&#95;&#95;getattr&#95;&#95;메서드는 &#95;&#95;getattribute&#95;&#95; 메서드와 같아보이지만 큰 차이가 있습니다.  
해당 이름이 참조될 때마다 무조건 호출되는 getattribute와 달리  
getattr은 우선 해당 이름이 정의된 다른 것이 존재하는지 확인해보고 없을 경우에 호출됩니다.  
  
```python
class Test:
	'''
    	case by use  __getattr__
    '''
	def __getattr__(self, key):
		if key == 'target':
			return 'called getattr'
		else:
			raise AttributeError

test = Test()
print(test.target)
##=> called getattr

test.target = 'called another'
print(test.target)
##=> called another


class Test:
	'''
    	case by use  __getattribute__
    '''
	def __getattribute__(self, key):
		if key == 'target':
			return 'called getattribute'
		else:
			raise AttributeError

test = Test()
print(test.target)
##=> called getattribute

test.target = 'called another'
print(test.target)
##=> called getattribute
```
먼저 getattr부터 살펴보겠습니다.  
Test개체에서 target이라는 이름으로 정의된 속성이 존재하지 않기 때문에 attr이 호출되어 'called getattr'이라는 문자열이 반환되었습니다.  
그리고 바로 다음 Test개체의 target속성은 'called another'이라는 문자열이라고 정의해준 뒤에는  
'called another'이라는 문자열을 반환합니다.  
target속성이 정의되어있기 때문에 getattr 메서드가 호출되지 않은 것이죠.  
  
하지만 getattribute는 다릅니다.  
똑같은 과정을 거쳤음에도 'called getattribute' 문자열이 반환된 이유는  
getattribute 메서드는 test개체 내의 어떠한 것에 접근하던 무조건 호출되기 때문입니다.  
그래서 target 속성을 정의했음에도 getattribute 메서드에 의해 'called getattribute'가 반환된 것입니다.  
  
----------------------------------------------------------------------------------
  
##&#95;&#95;set&#95;&#95;, &#95;&#95;del&#95;&#95;
set메서드와 del메서드는 getattribute메서드를 생각하시면 이해하기 쉽습니다.  
단어 뜻 그대로 set메서드는 속성에 값이 할당될 때마다 호출되며  
del메서드는 속성을 지울 때 마다 호출되는 메서드입니다.  
  
----------------------------------------------------------------------------------
  
## &#95;&#95;dir&#95;&#95;()
추후 수정

  
----------------------------------------------------------------------------------
  
## 함수처럼 동작하는 class. &#95;&#95;call&#95;&#95;()
call 메서드는 class 내에 정의되면 해당 class를 함수처럼 사용할 수 있게 해줍니다.  
```python
class Test:
	def __init__(self, value):
		self.value = value
	def __call__(self, x):
		x = x ** 2
		return x

test = Test('value')
result = list(map(test, range(5)))
print(result)
##=> [0, 1, 4, 9, 16]
```
위의 예제에서 Test class는 init메서드를 통해 초기화하고 call메서드를 통해 함수로 사용되었을 경우  
받은 인자를 제곱하여 반환하는 형태를 가지고 있습니다.  
call메서드가 있기 때문에 첫번째 인자로 함수를 사용하는 map()메서드에 들어가도 아무 문제가 없는 것이지요.  
그 결과 [0,1,2,3,4]라는 list를 받은 test개체는 call메서드를 호출하여 제곱된 값을 반환하고  
이렇게 만들어진 list를 result라는 변수에 정의하였습니다.  
  
----------------------------------------------------------------------------------
  
## set처럼 사용하는 class
```python
import cgi
fs = cgi.FieldStorage()
if 'q' in fs:                                               
  do_search()

class FieldStorage:
#.
#.
#.
    def __contains__(self, key):                            
        if self.list is None:
            raise TypeError('not indexable')
        return any(item.name == key for item in self.list)  

    def __len__(self):                                      
        return len(self.keys())
        
#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
위 예제에서 &#95;&#95;contains&#95;&#95;메서드와 &#95;&#95;len&#95;&#95;메서드가 있습니다.  
우선 &#95;&#95;contatins&#95;&#95;메서드에 대해서 살펴보죠.  
`if 'q' in fs:`를 통해서 fs개체 내에 'q'라는 값이 있는지 확인해보려하면  
FieldStorage class에서 &#95;&#95;contains&#95;&#95; 메서드의 유무를 확인합니다.  
발견하면 호출한 뒤 인자로 'q'를 넣어주고 내용을 실행합니다.  
위 예제의 경우 self.list라는 개체변수가 가진 값 중에 받은 인자값과 같은 값이 존재한다면 그 순간 True를 반환하도록 되어있습니다.  
any()메서드를 통해 True가 반환되는 순간 반복을 정지합니다.  
  
다음으로 &#95;&#95;len&#95;&#95; 메서드는 해당 객체의 길이를 반환합니다.  
  
----------------------------------------------------------------------------------
  
## dictionary처럼 사용하는 class
```python
import cgi
fs = cgi.FieldStorage()
if 'q' in fs:
  do_search(fs['q'])                              #1

class FieldStorage:
#.
#.
#.
    def __getitem__(self, key):                   #2
        if self.list is None:
            raise TypeError('not indexable')
        found = []
        for item in self.list:
            if item.name == key: found.append(item)
        if not found:
            raise KeyError(key)
        if len(found) == 1:
            return found[0]
        else:
            return found

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
이 경우도 위의 set으로 사용하는 경우와 같습니다.  
`fs['q']`라는 명령을 받은 FieldStorage는 &#95;&#95;getitem&#95;&#95; 메서드를 찾습니다.  
그리고 인자로 'q'를 dictionary의 key값으로써 넣어줍니다.  
위의 코드는 이후 key값의 value값이 self.list의 값과 같은지 비교하고 그 결과를 반환해줍니다.  
잘못된 값을 인자로 넘겨주었을 경우 TypeError를  
시퀀스의 index 외부의 값인 경우 IndexError를  
매핑 유형의 키가 누락된 경우 TypeError를 발생시킵니다.  
  
----------------------------------------------------------------------------------
  
## class를 숫자처럼 사용하기
class명(값, 값)과 같은 형태로 class를 숫자처럼 사용할 수 있습니다.  
이를 위해서는 지금까지와 같이 특수함수를 사용해야하는데 그 숫자가 너무 많기 때문에 관련 페이지를 첨부합니다.  
  
[https://docs.python.org/3/reference/datamodel.html?highlight=__add__#emulating-numeric-types](https://docs.python.org/3/reference/datamodel.html?highlight=__add__#emulating-numeric-types "링크")
  
----------------------------------------------------------------------------------
  
## 직렬화 될 수 있는 class
추후 수정  
  
----------------------------------------------------------------------------------
  
## with 블록과 함께 사용할 수 있는 class
일전 파이썬에서 파일을 이용한 작업을 할 때 등장했던 with 블록에서 close() 메서드가 없음에도 에러가 발생하지 않았던 이유에 대해 여기서 설명이 됩니다.  
```python
# excerpt from io.py:
def _checkClosed(self, msg=None):
    '''Internal: raise an ValueError if file is closed
    '''
    if self.closed:
        raise ValueError('I/O operation on closed file.'
                         if msg is None else msg)

def __enter__(self):
    '''Context management protocol.  Returns self.'''
    self._checkClosed()                                #1
    return self                                        #2

def __exit__(self, *args):
    '''Context management protocol.  Calls close()'''
    self.close() 

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
with 블록의 Runtime Context에 진입하면 &#95;&#95;enter&#95;&#95; 메서드를 호출합니다.  
이 때 파일이 닫혀있는지 체크하고 만약 닫혀있다면 ValueError를 발생시킵니다.  
그리고 Runtime Context에서 빠져나올 때 &#95;&#95;exit&#95;&#95;메서드를 호출합니다.  
이 메서드에서 파일을 close()메서드로 닫아주기 때문에 with 블록에서 따로 설정할 필요가 없는 것 입니다.  