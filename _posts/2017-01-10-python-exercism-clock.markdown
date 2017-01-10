---
layout: post
title: "문제풀이 : 시계 만들기" 
category: python exercism
---
  
## 사양
1. 시와 분을 인자로 받아 '00:00'의 형태로 시간을 표시해주는 시계.
2. 시의 경우 24시간으로 표시하며 24시는 00, 25시는 01과 같은 방식으로 표시한다.
3. 분의 경우 정수라면 입력값에 제한이 없으며 60분을 초과하는 만큼 시로 계산해서 시에 더한다.
4. add함수를 통해 임의의 정수를 분에 더할 수 있다.
  
## 코드
```python
def Clock(hour, minute):
    
    allmin = hour*60 + minute
    if allmin > 1440:
        allmin -= 1440
    
    hour = str(allmin//60)
    minute = str(allmin%60)
    
    if int(hour) < 10:
        hour = ('0'+hour)
    if int(minute) < 10:
        minute = ('0'+minute)

    result = hour + ':' + minute
    
    return result
```
최초로 작성한 코드.  
그러나 시작부터 어마어마한 문제가 있었으니 Test코드의 Clock(인자, 인자)에서 Clock의 첫 글자가 대문자인 것은 이것이 함수가 아닌 클래스라는 것을 의미했던 것.  
기타 내용에도 문제가 많으나 일단 가장 큰 문제인 부분부터 수정을 진행했다.  
  
  
```python
class Clock:
    
    def __init__(self, hour, minute):
        self.hour = hour
        self.minute = minute
        
    def __str__(self):
        allmin = self.hour*60 + self.minute
        if allmin > 1440:
            allmin -= 1440
            
        hour = str(allmin//60)
        minute = str(allmin%60)
        
        if int(hour) < 10:
            hour = ('0'+hour)
        if int(minute) < 10:
            minute = ('0'+minute)
    
        result = hour + ':' + minute
        
        return result
```
기본적인 부분은 고쳤으나 곧 문제에 부딪히게 되는데 `self.assertEqual('04:00', str(Clock(100, 0)))`라는 테스트 코드에서 에러가 발생한 것이다.  
원인은 100시간을 넣었으니 24시간을 여러번 초과했는데 식에서는 1440분을 1번만 빼주었기 때문에 테스트가 실패했던 것.  
  
덧붙여 이걸 고치는 과정에서 너무나 지저분하고 비효율적인 result부분을 interpolation으로 바꾸어보기로 하였다.  
  
```python
class Clock:
    
    def __init__(self, hour, minute):
        self.hour = hour
        self.minute = minute
        
    def __str__(self):
        allmin = (self.hour * 60 + self.minute) % 1440
            
        hour = allmin // 60
        minute = allmin % 60
        
        return '%0.2d:%0.2d' % (hour, minute)
```
훨씬 깔끔해졌다.  
`%0.2d`는 첫 칸에 '0'을 넣고 그 다음 인자로 들어간 정수를 String형태로 넣겠다는 뜻이다.  
그러므로 hour이 8이고 minute가 15라 가정하면 '08:15'라는 의미가 된다.  
  
그러나 `self.assertEqual('10:03', str(Clock(10, 0).add(3)))` 테스트에서 에러가 발생한다.  
이는 처음 사양서에 있던 시계에 add함수를 이용해 분을 더한다는 것을 고려하지 않았기 때문이다.  
  
  
```python
class Clock:
    
    def __init__(self, hour, minute):
        self.hour = hour
        self.minute = minute
       
    def add(self, minute):
        return Clock(self.hour, self.minute + minute)
     
    def __str__(self):
        allmin = (self.hour * 60 + self.minute) % 1440
            
        hour = allmin // 60
        minute = allmin % 60
        
        return '%0.2d:%0.2d' % (hour, minute)
```
add 함수를 추가하여 그 부분을 해결하였다.  
Clock(10,0)이 실행된 시점에서 init 함수가 실행되어 초기화가 진행된 뒤 add 함수를 통해 진행되기 때문에 add에도 str과 같은 과정을 추가해주어야한다.  
그러나 똑같은 과정을 함수가 다르다는 이유로 작성하는 것은 여러모로 좋지 않기 때문에 클래스에 새롭게 더해진 인자를 추가하여 반환하는 것으로 해결하였다.  
  
  
다음으로 실패는 `self.assertEqual(Clock(15, 37), Clock(15, 37))`에서 발생하였다.  
2개의 Clock()으로 비교를 했을 경우 서로 다른 객체값을 반환하며 실패가 발생한 경우이다.  
이를 해결하기 위해 클래스가 작동하는 시점에서 자동으로 작동하는 비교함수 eq()를 사용하였다.  
  
```python
class Clock:
    
    def __init__(self, hour, minute):
        self.hour = hour
        self.minute = minute
       
    def add(self, minute):
        return Clock(self.hour, self.minute + minute)
     
    def __str__(self):
        allmin = (self.hour * 60 + self.minute) % 1440
            
        hour = allmin // 60
        minute = allmin % 60
        
        return '%0.2d:%0.2d' % (hour, minute)
    
    def __eq__(self, other):
        return str(self) == str(other)
```
이로써 모든 테스트를 통과하는데 성공하였다.  
기능적으로는 문제가 없으나 여러가지 면에서 다듬어야 할 부분이 많이 보인다.  
1. str은 오버라이드 메소드로 String으로 정의해주는 역할을 하는데 그 외에 값을 계산하는 등의 기능까지 가지고 있다.  
2. allmin이라는 변수명은 다소 애매한 의미를 준다. 좀 더 명확한 의미를 가지는 변수명으로 교체.  
  
등의 문제를 수정하면 최종적으로 이러한 코드가 된다.  
```python
class Clock:
    
    def __init__(self, hour, minute):
        total = (hour * 60 + minute) % 1440
        self.hour = total // 60
        self.minute = total % 60
       
    def add(self, minute):
        return Clock(self.hour, self.minute + minute)
     
    def __str__(self):
        return '%0.2d:%0.2d' % (self.hour, self.minute)
    
    def __eq__(self, other):
        return str(self) == str(other)
```
이를 통해 init은 각 변수를 정의해주는 역할.  
add는 외부에서 입력된 더하는 값을 인자에 더해주는 역할.  
str은 결과값을 String으로 정의해주는 역할.  
eq는 두 값을 비교해주는 역할.  
로 각자 1개의 역할만을 수행하는 코드가 완성되었다.