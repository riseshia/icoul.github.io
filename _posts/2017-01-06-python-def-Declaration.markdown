---
layout: post
title: "파이썬의 함수선언" 
category: python
---

{% highlight python %}
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
{% endhighlight %}
  
  
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
  
추후 수정