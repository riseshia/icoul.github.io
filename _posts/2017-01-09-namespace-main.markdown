---
layout: post
title: __name__ == "__main__":의 의미
category: python
---

## module과 namespace  
파이썬 코드를 보면 가장 마지막에 이러한 if문이 오는 것을 자주 볼 수 있다.  
이 코드를 이해하기 위해서는 우선 파이썬의 module과 namespace에 대해 알아야한다.  

`module` : 파이썬 코드를 담고 있는 파일이다. 해당 파일에는 파이썬의 클래스, 함수, namespace 리스트 등 여러가지가 들어있을 수 있다.  
또한 module은 각각 완벽하게 독립적(isolated)이다. namespace가 다르기 때문이다.  
  
`namespace` : module은 자신만의 유일한 namespace를 갖는다.  
그래서 module에서 동일한 이름을 가지는 클래스나 함수를 정의할 수 없다.  
  
module과 namespace의 관계는 import를 통해 좀 더 쉽게 이해할 수 있다.  
  
__1: import&lt;module_name>__  
아래의 예제에서 sys는 module의 이름이며 path는 module의 namespace에 속해있는 name의 목록을 가져오는 sys에 속한 함수이다.  
해당 module의 name들을 가져와서 mainscript에서 사용하도록 허가해준다는 느낌으로  
name을 사용하기 위해서는 module의 namespace에 접근해야하며 이를 위해 sys를 prefix로 붙여서 사용해야만한다.  
  
```Python
import sys

sys.path

##=> ['', 'C:\\Python34\\Lib\\idlelib', 'C:\\Windows\\system32\\python34.zip',  
     'C:\\Python34\\DLLs', 'C:\\Python34\\lib', 'C:\\Python34']
```
  
  
__2: from&lt;module_name> import&lt;name,>__  
module의 namespace에서 import이하로 지정한 name들을 직접 가져오는 방식이다.  
이를 통해 원하는 name만 가져올 수 있으나 기본 mainscript에 겹치는 name이 있을 경우 import한 name으로 덮어씌워버리는 문제가 있다.  
그러므로 이 방식은 각 module의 name이 겹치지 않을거라는 확신 혹은 겹칠 의도를 가졌을때만 사용하는 것이 좋다.  
  
```Python
from sys import path

path
##=> ['', 'C:\\Python34\\Lib\\idlelib', 'C:\\Windows\\system32\\python34.zip',  
     'C:\\Python34\\DLLs', 'C:\\Python34\\lib', 'C:\\Python34']
```
  
  
__3: from&lt;module_name> import *__  
해당 module의 모든 name을 다 가져와서 기존 mainscript의 name과 뒤섞어버리는 방식이다.  
1번방식이 있기 때문에 기본적으로 쓸 일이 없다.  
  
  
## &#95;&#95;main&#95;&#95; namespace
위와 같은 import가 아닌 해당 파일을 파이썬 인터프리터가 최초로 파일을 읽어서 실행할 경우 코드를 실행하기 전에 특정 변수값을 정의한다.  
이 때 &#95;&#95;name&#95;&#95;을 &#95;&#95;main&#95;&#95;으로 세팅한다.  
즉,  
__python test.py와 같이 직접 쉘에서 실행하는 경우 파이썬 인터프리터가 해당 test.py라는 module을 script라는 namespace가 아닌 &#95;&#95;main&#95;&#95;이라는 namespace로 간주하여 다루게 된다.__  
그러므로  
```
if __name__ == "__main__"
```
의 의미는 __만약 이 파일이 파이썬 인터프리터로 실행되는 경우라면__ 이라는 의미이다.  
import 되었을 때는 실행되고 싶지 않고 직접 실행되었을 경우에만 사용되길 바라는 코드가 있을 경우 사용하는 것이다.  