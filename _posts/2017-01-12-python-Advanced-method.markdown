---
layout: post
title: "Advanced method, function" 
category: python
---
## re.findall()
re module의 findall() 메서드입니다.  
이 메서드는 입력한 문자열 중에서 사용자가 적용한 규칙에 해당되는 문자열만을 뽑아내어 List화 시켜주는 메서드입니다.  
  
```python
import re
print(re.findall('[0-9]+', '16 2-by-4s in rows of 8'))  
##=> ['16', '2', '4', '8']

print(re.findall('[A-Z]+', 'SEND + MORE == MONEY'))     
##=> ['SEND', 'MORE', 'MONEY']

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
re.findall 메서드는 2개의 인자를 사용합니다.  
첫번째 인자로 정규표현식을 조건으로 받고 두번째 인자로 대상인 문자열을 받습니다.  
  
## set을 이용하여 중복값 걸러내기
List에 존재하는 데이터를 배열내에 중복되는 값이 존재하지 않도록 걸러내고 싶을 때 set을 이용하면 쉽게 가능합니다.  
  
```python
string = 'EAST IS EAST'
print(set(string))
##=> {' ', 'I', 'E', 'S', 'T', 'A'}

string = ['EAST', 'IS', 'EAST']
print(''.join(string))
##=> EASTISEAST

print(set(''.join(string)))
##=> {'I', 'E', 'S', 'T', 'A'}

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
set은 데이터의 순서가 정해져있지 않고 중복을 허용하지 않는다는 특성을 가지고 있기 때문에  
문자열이든 list든 set() 메서드를 통해 set으로 만들 경우 중복값을 걸러낼 수 있습니다.  
''.join() 메서드는 인자로 들어온 문자열을 모두 합쳐서 하나의 문자열로 만들어주는 기능을 합니다.  
set() 메서드와 같이 사용하면 문자열 데이터를 어떻게 뽑아낼지의 폭을 좀 더 넓힐 수 있습니다.  
  
  
## Assert
```python
assert 1+1 == 2
assert 1+1 == 3
##=> Traceback (most recent call last):
#		File "<pyshell#6>", line 1, in <module>
#    	assert 1+1 == 3
#	 AssertionError

assert 1+1 == 3, 'This is False'
##=> Traceback (most recent call last):
#		File "<pyshell#7>", line 1, in <module>
#    	assert 1+1 == 3, 'This is False'
#	 AssertionError: This is False
```
assert는 해당 조건이 True인지 False인지 확인하여  
True일 경우 아무것도 발생시키지 않지만  
False일 경우에는 AssertionError를 발생시키고 뒤에 문자열을 적어주었다면 그 문자열도 같이 출력합니다.  
  
  
## Generator 표현식
```python
unique_characters = {'E', 'D', 'M', 'O', 'N', 'S', 'R', 'Y'}
gen = (ord(c) for c in unique_characters)        
print(gen)                                       
##=> <generator object <genexpr> at 0x00BADC10>

print(next(gen))                                 
##=> 69

print(next(gen))
##=> 68

print(tuple(ord(c) for c in unique_characters))  
##=> (69, 68, 77, 79, 78, 83, 82, 89)

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
generator 표현식은 generator 함수에서 형태만 함수가 아닌 comprehension과 유사한 형태의 표현식으로 바꾸었다고 생각하면 쉽습니다.  
위의 `(ord(c) for c in unique_characters)`처럼 ()괄호를 사용하며  
unique_characters의 데이터를 c라는 변수에 넣고 ord() 메서드를 이용하여 c의 Ascii 코드 번호를 반환하는 코드입니다.  
이렇게 설정한 Generator 표현식을 next() 메서드에 넣으면 순차적으로 값을 반환하며 인자로 사용된 List에 더 이상 남은 값이 없을 경우에는 StopIteration 예외를 발생시킵니다.  
  
결과값을 한 번에 배열로 저장하고 싶다면 list()나 tuple()로 감싸기만 하면 해당 배열로 반환해줍니다.  
  
  
## itertools
1) __itertools.permutations([1, 2, 3], 2)__
itertools module의 permutations() 메서드를 이용하면 입력한 값들의 순열을 구할 수 있습니다.  
위 제목에서 첫번째 인자인 `[1,2,3]`라는 list가 순열을 구할 대상이 되고  
두번째 인자인 2는 몇 개의 값을 가진 순열을 구할 것인지를 지정하는 값입니다.  
여기서는 2이기 때문에 2개의 값을 가진 [1,2,3]의 순열을 구하게 되며 결과는 이하와 같습니다.  
```
(1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)
```
물론 첫번째 인자에는 list만이 아닌 문자열이나 다른 배열도 가능합니다.  
  
2) __itertools.product('ABC', '123')___
product() 메서드는 2개의 값에 대해 곱집합을 구하는 메서드입니다.  
permutations와 마찬가지로 문자열, 배열 모두 가능합니다.  
위의 예시를 실행할 경우의 값은 이하와 같습니다.  
```
('A', '1'), ('A', '2'), ('A', '3'), 
('B', '1'), ('B', '2'), ('B', '3'), 
('C', '1'), ('C', '2'), ('C', '3')
```
  
3) __itertools.combinations([1, 2, 3], 2)__
combinations는 구조는 permutations와 같지만 결과값의 순서를 고려하지 않는다는 차이점이 있습니다.  
permuations에서 (1,2)와 (2,1)은 다른 값이지만  
combinations에서는 같은 값이라는 뜻입니다.  
```
(1,2), (1,3), (2,3)
```
  
4) itertools.groupby(문자열 또는 배열, 조건)
groupby() 메서드는 입력된 값을 특정 조건으로 그룹을 맺어주는 메서드입니다.  
이를 이용하면 이하의 예제와 같은 것이 가능합니다.  
```python
names = ['Alex', 'Anne', 'Dora', 'John', 'Mike', 
'Chris', 'Ethan', 'Sarah', 'Lizzie', 'Wesley']
import itertools

groups = itertools.groupby(names, len)

for name_length, name_iter in groups:
	print(f'Names with {name_length:d} letters:')
for name in name_iter:
	print(name)

##=>
#	Names with 4 letters:
#	Alex
#	Anne
#	Dora
#	John
#	Mike
#	Names with 5 letters:
#	Chris
#	Ethan
#	Sarah
#	Names with 6 letters:
#	Lizzie
#	Wesley

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
names라는 list 안에 10개의 문자열 데이터가 들어있습니다.  
이를 groupby() 메서드를 통해 문자열의 길이별로 분류하여 나눈 후 for문을 통해 콘솔창에 띄운 결과물입니다.  
  
5) __itertools.chain(range(0, 3), range(10, 13))__
chain() 메서드는 반복자들을 연결시켜서 하나의 새로운 반복자로 만들어주는 메서드입니다.  
위 예시에서 첫번째 인자인 range(0,3)을 끝까지 반복시킬 경우의 값은 0, 1, 2이고  
두번째 인자의 경우엔 10, 11, 12입니다.  
이 둘을 chain() 메서드에 넣을 경우 첫번째 인자부터 순서대로 0, 1, 2, 10, 11, 12의 값을 반환하는 새로운 반복자가 만들어집니다.  
그 결과 `list(itertools.chain(range(0, 3), range(10, 13)))`와 같이 list를 씌우면  
[1,2,3,10,11,12]라는 새로운 list를 만들 수 있습니다.  
  
chain 메서드에 들어가는 반복자의 갯수는 제한이 없으며 들어간 순서에 따라서 결과값으로 나온 반복자가 반환하는 값의 순서가 결정됩니다.  
  
  
## .strip() 메서드
strip() 메서드는 해당 문자열의 값들의 공백을 제거해주는 역할을 합니다.  
```python
names = ['Dora\n', 'Ethan\n', 'Wesley\n', 'John\n', 'Anne\n',
'Mike\n', 'Chris\n', 'Sarah\n', 'Alex\n', 'Lizzie\n'] 

names = [name.strip() for name in names]                             
print(names)
## ['Dora', 'Ethan', 'Wesley', 'John', 'Anne',
## 'Mike', 'Chris', 'Sarah', 'Alex', 'Lizzie']

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
위와 같이 문자열.strip() 의 형태로 해당 문자열의 공백을 제거할 수 있습니다.  
strip()메서드는 문자열 양쪽의 모든 공백을 제거  
rstrip()메서드는 문자열 오른쪽,  
lstrip()메서드는 문자열 왼쪽의 공백을 제거합니다.  
  
  
## sort()메서드
```python
names = ['Dora', 'Ethan', 'Wesley', 'John', 'Anne', 
'Mike', 'Chris', 'Sarah', 'Alex', 'Lizzie']

names = sorted(names)                                                 
print(names)
##=> ['Alex', 'Anne', 'Chris', 'Dora', 'Ethan',
##=> 'John', 'Lizzie', 'Mike', 'Sarah', 'Wesley']

names = sorted(names, key=len)                                        
print(names)
##=> ['Alex', 'Anne', 'Dora', 'John', 'Mike',
##=> 'Chris', 'Ethan', 'Sarah', 'Lizzie', 'Wesley']

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
sort() 메서드는 인자로 입력된 배열을 정렬하여 List로 반환해주는 메서드입니다.  
조건이 없으면 기본적으로 알파벳 순서대로 정렬하여 반환해주고 인자에 `key=조건`과 같은 방식으로  
조건을 추가해주면 해당 조건에 맞춰서 list를 반환해줍니다.  
  
기능 자체는 `itertools.groupby(값, 조건)`과 같지만  
groupby() 메서드는 결과값을 (조건값, 반복문)의 형태를 가진 데이터의 list로 반환해준다는 점에서 차이가 있습니다.  
  
  
## translate()
translate() 메서드는 `문자열.translate(패턴)`의 형태로 이루어집니다.  
해당 문자열을 살펴보고 패턴에 맞는 문자를 발견했을 경우 패턴에 맞추어서 수정해주는 역할을 합니다.  
때문에 해당 패턴은 Dictionary 타입의 배열입니다.  
단, translate는 byte 타입을 사용하여 수정하기 때문에 패턴을 작성할 때는 byte타입으로 작성해주어야합니다.  
  
```python
translation_table = {ord('A'): ord('O')}    #1
print(translation_table)                    #2
## {65: 79}
print('MARK'.translate(translation_table))  #3
## 'MORK'
```
위와 같이 A와 O의 ascii코드 번호인 65와 79를 key값과 value값으로 가진 사전을 패턴으로 만들고 이를 대입시키면 결과값으로 A를 O로 치환한 문자열이 반환됩니다.  

