---
layout: post
title: "파이썬의 문자열 다루기" 
category: python
---
## 문자열 치환필드
```python
username = 'mark'
password = 'PapayaWhip'                                    
print("{0}'s password is {1}".format(username, password))  
##=> "mark's password is PapayaWhip"

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
"문자열".format(값)  
위와 같은 형태로 문자열에 원하는 형태의 문자열을 삽입할 수 있습니다.  
물론 이러한 형식을 거치지 않고 일일히 작업을 진행하고 입력하는 것도 가능하지만  
같은 작업을 여러번 반복하기보다는 하나의 틀을 만들고 필요할 때마다 쓰는 쪽이 더 효율적입니다.  
  
위 코드에서 {0}과 {1}은 format()메서드의 인자의 index번호입니다.  
그래서 {0}에는 첫번째 인자인 username이 {1}에는 두번째 인자인 password가 들어갑니다.  
이러한 치환필드에는 문자열만이 아닌 List도 이용 가능합니다.  
  
```python
a_list = ['mark','papayawhip']
print("{0[0]}'s password is {0[1]}".format(a_list))
##=> mark's password is papayawhip
```
위와 같이 List를 넣고 {}안에 인자의 index번호를 넣고 []에 원하는 데이터의 index번호를 입력함으로써  
원하는 문자열을 완성시킬 수 있습니다.  
물론 List만이 아닌 Tuple, 사전도 가능합니다. 단, 집합은 순서를 알 수 없기 때문에 불가능합니다.  
  
  
```python
print('{0:.1f} {1}'.format(698.24, 'GB'))
##=> '698.2 GB'

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
이와 같이 단순히 문자열을 입력하는 것만이 아닌 가공도 가능합니다.  
위는 698.24라는 실수를 받아서 .1f를 통해 소숫점 둘째자리에서 반올림시킨 코드입니다.  
  
## 문자열 메서드
```python
s = '''Finished files are the re-
sult of years of scientif-
ic study combined with the
experience of years.'''

print(s.splitlines())                     
##=> ['Finished files are the re-',
##=>  'sult of years of scientif-',
##=>  'ic study combined with the',
##=>  'experience of years.']

print(s.lower())                          
##=> finished files are the re-
##=> sult of years of scientif-
##=> ic study combined with the
##=> experience of years.

print(s.lower().count('f'))               
##=> 6

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
splitlines() 메서드는 해당 문자열이 줄바꿈이 될 때마다 문자열을 잘라서 List화 시켜줍니다.  
이 때, 줄바꿈은 List에 들어가는 문자열에 포함되지 않습니다.  
  
lower() 메서드는 해당 문자열을 모두 소문자로 바꿔줍니다. upper()는 대문자로 바꿉니다.  
  
count(문자열) 메서드는 인자로 받은 문자열이 해당 문자열에서 몇 개 존재하는지 확인하고 정수로 반환해주는 메서드입니다.  
  
```python
query = 'user=pilgrim&database=master&password=PapayaWhip'

a_list = query.split('&')                                        
print(a_list)
##=> ['user=pilgrim', 'database=master', 'password=PapayaWhip']

a_list_of_lists = [v.split('=', 1) for v in a_list if '=' in v]  
print(a_list_of_lists)
##=> [['user', 'pilgrim'], ['database', 'master'], ['password', 'PapayaWhip']]

a_dict = dict(a_list_of_lists)                                   
print(a_dict)
##=> {'password': 'PapayaWhip', 'user': 'pilgrim', 'database': 'master'}

#코드 출처 : CodeOnWeb 파이썬3에 뛰어들기
```
위의 query와 같이 일정한 규칙으로 나뉘어져 key, value값을 구분할 수 있는 문자열은 split 메서드를 이용하여  
사전으로 만들 수 있습니다.  
  
  