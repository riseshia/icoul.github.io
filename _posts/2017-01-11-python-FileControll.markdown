---
layout: post
title: "파일, 폴더 제어하기" 
category: python
---
## 작업경로
파이썬이 module을 import 할 때 작업경로 내에 해당 module이 존재하지 않을 경우 ImportError를 발생시킵니다.  
이를 해결하기 위해서는 'module을 작업경로로 옮기거나' 혹은 '작업경로를 module이 있는 폴더로 바꾸거나' 등의 과정이 필요합니다.  
  
파이썬은 이러한 작업경로를 항상 메모리에 저장해두고 필요할 때마다 참조합니다.  
그리고 이 작업경로는 os module을 통해서 제어할 수 있습니다.  
  
```python
import os
print(os.getcwd())
##=>C:\python36

os.chdir('C:\pythonProject')
print(os.getcwd())
##=>C:\pythonProject
```
os의 메서드 getcwd()를 통해 현재 작업경로를 확인할 수 있습니다.  
그리고 chdir('주소경로') 메서드를 통해 현재 작업경로를 변경할 수 있습니다.  
  
```python
import os
print(os.path.join('C:\pythonProject', 'example', 'test.py'))
##=> C:\pythonProject\example\test.py

print(os.path.expanduser('~'))
##=> C:\Users\icoul

print(os.path.realpath('test.py'))
##=> C:\pythonProject\test\test.py
```
os.path module의 join 메서드를 이용하면 하나의 파일경로를 만들 수 있습니다.  
expanduser() 메서드에 '~'를 넣음으로써 현재의 작업경로를 출력할 수 있습니다.  
realpath() 메서드를 이용하면 해당 파일의 절대경로를 출력할 수 있습니다.  
  
```python
pathname = 'C:/pythonProject/example/test.py'

print(os.path.split(pathname))
##=> ('C:/pythonProject/example', 'test.py')

(dirname, filename) = os.path.split(pathname)
print(dirname)
##=> C:/pythonProject/example

print(filename)
##=> test.py

(shortname, extension) = os.path.splitext(filename)
print(shortname)
##=> test

print(extension)
##=> .py
```
os.path의 split()메서드를 이용하면 이러한 파일경로를 경로와 파일명으로 나눌 수 있으며  
tuple을 이용해서 결과값을 각각의 변수에 저장할 수도 있습니다.  
splitext()는 파일명을 이름과 확장자로 나누는 역할을 합니다.  
  
  
```python
import glob
print(glob.glob('test/*.py'))
##=> ['test\\alphametics.py', 'test\\filesize.py']

os.chdir('test/')
print(glob.glob('*.py'))
##=> ['alphametics.py', 'filesize.py']
```
glob module을 이용하여 폴더를 조회하여 내용물을 확인할 수 있습니다.  
glob()메서드에 들어가는 값에 따라 폴더명+파일명 혹은 파일명만을 검색하여 List로 반환합니다.  
