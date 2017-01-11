---
layout: post
title: "파이썬의 컴프리헨션" 
category: python
---
## Comprehension
파이썬은 List, 집합, 사전에 대해서 comprehension이라는 기능을 지원하고 있습니다.  
(Tuple은 내부의 값을 수정할 수 없기 때문에 지원하지 않습니다.)  
이는 간편하게 배열 내의 __원하는 데이터__를 __원하는 방식으로__ 변형하여 새로운 배열을 만들거나 기존 배열을 수정할 수 있도록 하는 기능입니다.
  
```python
a_list = [1,2,3]
print(a_list)
##=> [1, 2, 3]

b_list = [value * 2 for value in a_list if value > 1]
print(b_list)
##=> [4, 6]
```
정수 1,2,3을 값으로 가진 'a_list'라는 이름의 List를 만들어서  
[value * 2 for value in a_list if value > 1] 라는 식에 넣었습니다.  
이는  
  
1. in a_list : a_list라는 이름을 가진 List를 대상으로  
2. for value : index 순서대로 하나씩 값을 출력하여 이를 변수 value에 넣겠다.  
3. if value > 1 : 단, 1보다 큰 숫자일때만 넣겠다.  
4. [value \* 2 ...] : 조건에 맞는 숫자는 *2를 한 다음 새로운 List에 index 순서대로 삽입하겠다.  
  
라는 의미입니다.  
이렇게 만들어진 List는 b_list라는 이름을 가지게 됩니다.  
만약 기존 List를 수정하고자 하는 의도라면 b_list 대신 a_list를 입력하면 됩니다.  
  
이 외에 집합과 사전의 comprehension도 똑같은 구조로 이루어집니다.  
차이가 있다면  
사전 : 항상 key값, value값을 모두 받아야하며 in에 들어가는 사전은 .items()메서드를 사용해야한다.  
집합 : 실행되는 값의 순서가 없다.  
사전과 집합은 모두 comprehension을 쓸 때 {}를 사용한다.  
  
이러한 comprehension을 사용하면 사전의 key값과 value값을 서로 뒤바꾸는 것이 가능합니다.  
  
```python
a_dic = {'a' : '1', 'b' : '2', 'c' : '3'}
a_dic
##=> {'a : 1', 'c : 3', 'b : 2'}

b_dic = {value : key for key, value in a_dic.items()}
b_dic
##=> {'1': 'a', '2': 'b', '3': 'c'}
```
