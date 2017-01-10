---
layout: post
title: "정규표현식의 치환" 
category: python
---  
  
  
## 정규표현식의 치환  
  
```Python
import re

def plural(noun):          
    if re.search('[sxz]$', noun):             #1
        return re.sub('$', 'es', noun)        #2
    elif re.search('[^aeioudgkprt]h$', noun):
        return re.sub('$', 'es', noun)       
    elif re.search('[^aeiou]y$', noun):      
        return re.sub('y$', 'ies', noun)     
    else:
        return noun + 's'
```
`[문자열]`은 해당 대괄호 안의 문자 중 정확히 하나와 매치되는 것을 찾는다는 의미합니다.  
`[^문자열]`은 그 반대로 해당 대괄호 안의 문자를 제외한 아무 문자 하나를 찾는다는 뜻입니다.  
  
`re.sub()`는 해당되는 문자열을 치환하는 역할을 합니다.  
위와 같이 re.sub('$', 'es', noun)은 $에 해당되는 문자열의 맨 끝에 'es'를 추가한다는 뜻이 됩니다.($대신 noun을 사용해도 됩니다.)  
re.sub('y$', 'ies', noun)는 문자열 가장 끝에 있는 y를 'ies'로 바꾼다는 뜻입니다.  
  
  
```Python
import re
print(re.search('[abc]', 'Mark'))    
##=> <_sre.SRE_Match object; span=(1, 2), match='a'>
print(re.sub('[abc]', 'o', 'Mark'))  #
##=> 'Mork'
print(re.sub('[abc]', 'o', 'rock'))  #
##=> 'rook'
print(re.sub('[abc]', 'o', 'caps'))  #
##=> 'oops'
```  
`[문자열]`과 위의 `re.sub()`을 합치면 위와같이 해당 문자열에서 원하는 문자들만 치환시킬 수 있습니다.  
`[문자열]`을 통해 찾은 같은 문자의 갯수가 몇 개이든 모두 2번째 인자(위에서는 'o')값으로 치환시킵니다.  
  
  
```Python
import re

print(re.sub('([^aeiou])y$', r'\1ies', 'vacancy'))  
##=> 'vacancies'
```  
위의 코드는 re.search와 re.sub가 각자 하던 역할을 re.sub 하나로 가능하게 만든 코드입니다.  
먼저 `([^aeiou])y$`는 ()를 통해 ()안의 내용에 해당되는 문자열을 찾습니다. 이 경우에는 a,e,i,o,u에 해당되지 않는 다른 문자를 찾고 있습니다.  
이 후 'y$'를 통해 방금 찾은 문자 + 'y'가 문장의 맨 끝에 있는가? 를 체크합니다. 이 모든 것을 만족하면 치환으로 넘어갑니다.  
치환으로 넘어가면 '\1'이라는 문자열이 있습니다. 이는 방금 ()로 묶었던 그룹을 가져와서 여기에 넣겠다는 뜻입니다.  
이전 ([^aeiou])를 통해 찾아낸 값이 'vacancy'의 'c'이기 때문에 이번에는 'c'가 여기에 들어갑니다. 그리고 y를 ies로 치환하여 결과는 'vacancies'가 됩니다.  
  
  