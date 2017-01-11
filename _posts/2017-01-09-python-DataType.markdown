---
layout: post
title: "파이썬의 자료형" 
category: python
---

## 자료형의 종류  
  
1.__boolean__ : True, False의 값을 가지는 자료형입니다.  
2.__Number__ : 정수, 실수, 분수 혹은 복소수의 값을 가질 수 있는 자료형입니다.  
3.__String__ : 유니코드 문자의 연속. 문자열을 가지는 자료형입니다.  
4.__Byte__ : 0~255사이 코드의 열이다. 문자열과의 연산은 불가능하다.  
5.__List__ : 여러개의 값을 순서대로 가지고 있는 배열이다.  
6.__Tuple__ : 여러개의 값을 순서대로 가지고 있다는 점에서 List와 같지만 Tople은 값의 수정이 불가능하다.  
7.__set__ : 집합은 순서가 정해져있지 않은 값들의 집합이다.  
8.__Dictionary__ : 정렬되지 않은 key값:value값 들의 집합이다.  
  
  
## Boolean
Boolean타입은 True, False 중 하나의 값을 가집니다.  
이를 통해 반드시 True 혹은 False가 결정되어야만하는 조건식에서 사용되며 이러한 상황을 `boolean context`라고합니다.  
  
Boolean 타입은 숫자처럼 활용할 수도 있는데요. True는 1, False는 0을 의미합니다.  
```python
print(True + True)
##=> 2
print(True - False)
##=> 1
print(True * False)
##=> 0

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
  
## Number
Number는 정수, 실수, 분수 등의 다양한 종류의 수를 가지는 데이터타입입니다.  
각 타입은 `type(값)`을 통해서 어떤 타입인지 확인할 수 있으며 `isinstance(값, 타입명)`을 통해서 직접 비교하여 True 혹은 False를 반환시킬 수도 있습니다.  
  
정수와 실수간의 연산도 가능하며 이 경우 결과값은 실수형으로 반환됩니다.  
실수형으로 반환된 값에 int를 붙이면 정수형으로 변환되며 소수점 값이 버려집니다.  
반대로 정수형에 float을 붙이면 소수점 첫째자리에 0이 붙습니다.  
  
파이썬에서는 이하와 같이 나눗셈, 곱셈의 연산이 가능합니다.  
```python
print(11 / 2)      #1
##=> 5.5

print(11 // 2)     #2
##=> 5

print(-11 // 2)    #3
##=> −6

print(11.0 // 2)   #4
##=> 5.0

print(11 ** 2)     #5
##=> 121

print(11 % 2)      #6
##=> 1

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```  

  
분수의 경우 fractions module을 import해야합니다.  
```Python
x = fractions.Fraction(1, 3)         #2
print(x)
##=> 1/3

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
이를 통해 생성된 값은 분수 타입을 가지며 연산을 통해 1, 0등의 정수형처럼 외형이 변하여도 타입은 여전히 분수타입입니다.  
  
  
boolean context 상태에서 __숫자 0은 False를 의미하며 그 이외의 값은 모두 True입니다.__  
  
  
## List
List는 `리스트명 = [값1, 값2, 값3]` 등의 방법으로 생성이 가능합니다.  
  
```python
a_list = ['a', 'b', 'mpilgrim', 'z', 'example']
print(a_list)
##=> ['a', 'b', 'mpilgrim', 'z', 'example']

print(a_list[1:3])            #: index 1번부터 3번 바로 전까지의 값
##=> ['b', 'mpilgrim']

print(a_list[1:-1])           #: index 1번부터 뒤에서 첫번째 바로 전 까지의 값
##=> ['b', 'mpilgrim', 'z']

print(a_list[0:3])            #: index 0번부터 3번 바로 전까지의 값
##=> ['a', 'b', 'mpilgrim']

print(a_list[:3])             #: 처음번부터 3번 바로 전까지의 값
##=> ['a', 'b', 'mpilgrim'

print(a_list[3:])             #: index 3번부터 끝까지의 값
##=> ['z', 'example']

print(a_list[:])              #: 리스트 내의 모든 값
##=> ['a', 'b', 'mpilgrim', 'z', 'example']

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
위와 같이 List 중 일부만을 확인하거나 사용할 수 있으며 이렇게 생성된 값을 다른 List로 정의하는 것으로 새로운 List를 만들 수 있는데 이를 리스트 쪼개기(slicing the list)라고 합니다.  
  
  
__List에는 append(), extend(), insert() 등을 통하여 값을 추가할 수 있습니다.__  
1. append(값)  
append의 경우 List의 맨 뒷 순번에 해당되는 값을 추가하는 메서드입니다.  
append로 List타입의 값을 추가할 경우 List 내부의 값이 각각 추가되는 것이 아니라 List 자체가 하나의 값으로 추가됩니다.  
  
2. extend(리스트)  
extend는 List의 맨 뒷 순번에 인자에 해당되는 List의 값들을 차례대로 추가합니다.  
  
3. insert(번호, 값)  
insert는 번호를 지정하여 원하는 장소에 원하는 값을 집어넣을 수 있습니다. 번호가 0이면 가장 앞에 위치합니다.  
  
  
__List를 검색하는 것은 count(), in, index() 등의 방법이 있습니다.__  
1. List명.count(값)  
count 메서드에 들어간 인자값이 해당 List에 몇 개 존재하는지 확인하여 그 갯수를 반환해주는 메서드입니다.  
  
2. List명 in 값  
해당 List안에 해당 값이 존재하는지 여부를 확인하여 그 결과를 True, False로 반환합니다.  
  
3. List명.index(값)  
List 내에서 해당 값이 index 상으로 몇 번째에 위치하는지 확인하고 그 index 값을 반환해주는 메서드.  
이러한 index메서드는 List 내에서 해당 인자값과 일치하는 값을 발견하지 못했을 경우 예외를 발생시킵니다.  
  
  
__List를 삭제할 때는 del, remove(), pop()등의 방법이 있다.__  
1. del List명[index 번호]  
해당 index 번호에 존재하는 List의 값을 삭제합니다  
  
2. List명.remove(값)
해당 List 내에서 해당 인자값과 같은 값을 찾아내어 삭제합니다. 같은 값이 없을 경우 예외를 발생시킵니다.  
  
3. pop()
해당 List 내에서 가장 뒷번호에 위치한 값을 삭제합니다. ()안에 index 번호를 넣으면 지정하여 삭제할 수 있습니다.  


## Tuple

```python
a_tuple = ("a", "b", "mpilgrim", "z", "example")  
print(a_tuple)
##=> ('a', 'b', 'mpilgrim', 'z', 'example')

print(a_tuple[0])                                 
##=> 'a'

print(a_tuple[-1])                                
##=> 'example'

print(a_tuple[1:3])                               
##=> ('b', 'mpilgrim')

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
  
Tuple은 기본적으로 List와 같이 데이터를 순서대로 저장하는 배열입니다.  
대신, __저장된 데이터의 내용을 수정할 수 없다__라는 점이 가장 큰 차이점이지요.  
  
때문에 이미 생성된 Tuple을 자르는 것은 가능하지만 내용의 추가, 삭제, 수정은 불가능합니다.  
  
* 데이터 추가 : 불가능
* 데이터 삭제 : 불가능
* 데이터 수정 : 불가능
* 데이터 자르기(slice) : 가능
* 데이터의 검색 : 가능

```python
v = ('a', 2, True)
(x, y, z) = v       
print(x)
## 'a'
print(y)
## 2
print(z)
## True

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
위와 같이 Tuple을 이용하면 내용물을 여러개의 변수에 한 번에 정의하는 것이 가능합니다.  
이러한 성질을 이용하여 함수에ㅔ서 2개 이상의 값을 반환하는 것도 가능합니다.  
  
Tuple의 장점
1. 빠르다 : Tuple은 List에 비해 빠르기 때문에 검색에만 사용할 용도의 배열이 필요할 때 적당합니다.  
2. Key값의 저장소로 유용 : Tuple은 값을 변경할 수 없기 때문에 Dictionary의 Key값을 담아두기에 유용합니다.  
3. 실수를 방지 : 프로그램을 구성하다보면 만들어진 배열 내의 내용이 개발자의 의지와 별개로 바뀌는 경우가 종종 있습니다. Tuple은 이러한 문제를 미연에 방지해줍니다.  
  
  
## Sets(집합)
집합은 순서가 정해져있지 않은 유일한 데이터들의 모임이라고 볼 수 있습니다.  
즉, List나 Tuple과 달리 값들의 순서가 없으며 집합 내에서는 중복되는 값이 존재하지 않습니다.  
1을 3개 넣으면 집합에는 1이 1개만 존재한다는 뜻이죠.  
그리고 교집합, 합집합과 같은 집합연산이 가능하다는 점이 특징입니다.  
  
```python
a_set = {1, 2}        # 집합의 생성
print(a_set)
##=> {1, 2}

print(type(a_set))    # 집합 타입의 확인
##=> <class 'set'>

a_set = set()		  # 빈 집합의 생성, set이 없이 그냥 {}의 경우 사전을 생성합니다.

#List를 집합으로 바꾸는 과정
a_list = ['a', 'b', 'mpilgrim', True, False, 42]
a_set = set(a_list)                           
print(a_set)                                  
##=> {'a', False, 'b', True, 'mpilgrim', 42}

print(a_list)                                 
##=> ['a', 'b', 'mpilgrim', True, False, 42]

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
위와 같이 집합을 생성할 때는 {}를 사용합니다.  
빈 집합만 생성하거나 다른 배열을 집합으로 만들고 싶을때는 set() 메서드를 이용합니다.  
  
__집합에는 add(), update() 등을 통하여 값을 추가할 수 있습니다.__  
1. add(값)  
add메소드의 경우 하나의 인자만을 받습니다. 이 인자는 어떠한 데이터 타입이든 상관없으나 하나의 값이어야만 합니다.  
즉, List나 Tuple, 집합 같은 배열을 받을 수 없습니다.  
  
2. update(배열)  
update는 List, Tuple, 집합등의 배열을 받아서 해당 데이터들을 집합에 넣어줍니다.  
update에선 단일값을 추가할 수 없으며 배열이라면 여러개를 한꺼번에 인자에 추가하여도 상관없습니다.  
  
  
__집합을 삭제할 때는 discard, remove(), pop(), clear()등의 방법이 있다.__  
1. discard(값)  
집합 내에서 받은 인자와 동일한 값을 찾아서 해당 값을 삭제한다.  
만약 동일한 값이 존재하지 않을 경우 아무런 일도 일어나지 않습니다.  
  
2. remove(값)
집합 내에서 받은 인자와 동일한 값을 찾아서 해당 값을 삭제한다.  
만약 동일한 값이 존재하지 않을 경우 KeyError를 발생시킵니다.  
  
3. pop()
해당 집합 내에서 임의의 값 1개를 삭제합니다.  
  
4. clear()
해당 집합 내의 모든 값을 삭제합니다.  
  
  
__집합연산__  
1. A.union(B)
A집합과 B집합의 __합집합__을 새로운 집합으로 반환합니다.  
  
2. A.intersection(B)
A집합과 B집합의 __교집합__을 새로운 집합으로 반환합니다.  
  
3. A.difference(B)
A에는 존재하지만 B에는 존재하지 않는 결과만을 새로운 집합으로 반환합니다.  
집합연산 중 유일하게 비대칭적인 연산입니다.  
  
4. A.symmetric_difference(B)
두 집합의 합집합에서 교집합에 해당되는 부분을 제외한 결과만을 새로운 집합으로 반환합니다.  
  
  
## Dictionaries(사전)
사전은 Key값, Value값의 한 쌍을 하나의 값으로 가지고 있는 배열입니다.  
  
```python
a_dict = {'server': 'db.exit.org', 'database': 'mysql'}  
print(a_dict)
##=> {'server': 'db.exit.org', 'database': 'mysql'}

print(a_dict['server'])                                             
##=> 'db.exit.org'

print(a_dict['database'])                                           
##=> 'mysql'

print(a_dict['db.exit.org'])                             
##=> KeyError: 'db.exit.org'

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
위와 같이 사전을 생성할 때는 `Key값 : Value값`을 적어야합니다.  
이 경우 Value값에 들어갈 수 있는 것은 문자열 뿐만이 아니라 배열도 들어갈 수 있습니다.  
  
```python
a_dict = {'server': 'db.exit.org', 'database': 'mysql'}
print(a_dict)
##=> {'server': 'db.exit.org', 'database': 'mysql'}

a_dict['database'] = 'blog'  
print(a_dict)
##=> {'server': 'db.exit.org', 'database': 'blog'}

a_dict['user'] = 'mark'      
print(a_dict)                
##=> {'server': 'db.exit.org', 'user': 'mark', 'database': 'blog'}

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
사전의 value값을 수정하거나 새로운 아이템을 추가하고 싶을 때는 위와 같이 `사전명[KEy값]`을 입력하면 됩니다.  
그러면 파이썬이 자동으로 사전내부를 검색하여 동일한 Key값이 있으면 수정, 없으면 추가를 합니다.  
당연하지만 이 Key값은 대소문자를 구분합니다.  
  
  
## 배열로 참, 거짓 판별하기
지금까지 살펴본 List, Tuple, 집합, 사전은 내부에 내용물이 있는지 없는지에 따라 판별을 요구시 반환하는 값이 다릅니다.  
  
배열내에 값이 1개라도 존재할 경우 : True  
배열이 텅 비어있을 경우 : False  
  
  
## 배열 생성 정리
List = [ ]  
Tuple = ( )  
집합 = {값}  
빈 집합 = set()  
사전 = {Key값 : Value값}  
빈 사전 = {}  