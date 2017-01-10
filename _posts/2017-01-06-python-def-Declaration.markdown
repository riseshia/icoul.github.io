---
layout: post
title: "파이썬의 함수선언" 
category: python
---

```Python
SUFFIXES = {1000: ['KB', 'MB', 'GB', 'TB', 'PB', 'EB', 'ZB', 'YB'],
			1024: ['KiB', 'MiB', 'GiB', 'TiB', 'PiB', 'EiB', 'ZiB', 'YiB']}

def approximate_size(size, a_kilobyte_is_1024_bytes=True):
    if size < 0:
        raise ValueError('number must be non-negative')
    
    multiple = 1024 if a_kilobyte_is_1024_bytes else 1000
    for suffix in SUFFIXES[multiple]:
        size /= multiple
        if size < multiple:
            return '{0:.1f} {1}'.format(size, suffix)
        
    raise ValueError('number too large')

if __name__ == '__main__':
    print(approximate_size(1000000000000, False))
    print(approximate_size(1000000000000))
```
  
  
## 파이썬에서의 함수선언

def라는 키워드로 함수를 선언하고 함수명, 괄호로 묶인 인자가 된다. 인자는 ,로 구분한다.  
`def 함수명(인자1, 인자2)`  
  
### 변수선언
이 때 함수의 인자에 자료형을 표시하지 않았는데  
파이썬에서는 **변수에 자료형을 선언하지 않는다.**  
파이썬이 내부적으로 자료형을 알아내어서 지정하기 때문이다.  
  
### 인자의 기본값 정의
함수의 인자를 선언할 때 `='value'`를 통해서 호출되지 않았을 경우에는 자동으로 기본값을 사용할 수 있다.  
위 코드에서 `a_kilobyte_is_1024_bytes=True`는 `True`를 기본값으로 가지고 있다는 뜻이다.  
  
### return
파이썬에서는 별도로 return을 정해주지 않아도 문제없이 작동한다.  
단, 이 경우 항상 None(java로 치면 null)값을 반환한다.  
  
## 객체  
파이썬에서는 모든 것이 객체입니다.  
함수, 클래스, 변수 등 모든 것은 객체로써 할당될 수도 있고 함수의 인자로 넘길 수도 있습니다.  
또한, import한 module의 이름을 prefix로 붙이는 것으로 다른 mainscript에서 사용할 수도 있습니다.  
당연히 import된 당사자인 module 역시 객체입니다.  
  
## 코드 들여쓰기  
파이썬에서는 코드 들여쓰기를 통해 함수의 끝을 알립니다.  
우선 함수나 for문, if문 등의 제어문이 시작할 때 `:`를 붙여서 시작을 알리고 이 후에는 들여쓰기를 몇 칸 했는지에 따라 함수의 진행과 끝을 결정합니다.  
그러므로 파이썬에서는 __들여쓰기가 실수할 경우 에러가 발생합니다.__  
  
## 예외처리
파이썬에선 어떤 예외를 처리할 지 따로 지정하지 않습니다.  
대신 이하의 기능을 통해 예외처리를 진행합니다.  
try....except : 예외 처리 블록 (JAVA의 try..catch)  
raise : 예외를 발생시키는 문구 (JAVA의 throw)  
  
## import 예외처리하기
파이썬에서 module을 import 할 시 경로에서 해당 module을 찾지 못 했을 시 에러가 발생합니다.  
이 오류를 처리하기 위해 `ImportError`라는 예외 클래스를 사용하며 단순히 예외처리만이 아닌 다양한 용도로 사용할 수 있습니다.  
```Python
try:
  import chardet
except ImportError:
  chardet = None
```  
if문을 통한 module의 존재여부확인  
  
  
```Python
try:
    from lxml import etree
except ImportError:
    import xml.etree.ElementTree as etree
```  
예외처리를 통해 import되는 module의 우선순위를 정할 수도 있습니다.  
lxml은 성능이 좋지만 존재하지 않는 환경일 가능성이 있고  
ElementTree는 성능은 다소 떨어지지만 기본으로 내장되어있는 module입니다.  
이 경우 위와같이 설정해두면 우선 lxml을 import시키고 만약 lxml이 없으면 그 때 ElementTree를 import하여 좀 더 유연하게 대응할 수 있게 합니다.  
  
  
## Unbound 변수
선언하지 않고 값을 할당한 변수입니다.  
단, 할당된 값이 없는 변수를 참조하는 것은 허용되지 않으며 이 경우 NameError에러가 발생합니다.  
  
  