#Codewars #15
##Question
Description:

Write an algorithm that will identify valid IPv4 addresses in dot-decimal format. Input to the function is guaranteed to be a single string.

Examples of valid inputs: 1.2.3.4 123.45.67.89

Examples of invalid inputs: 1.2.3 1.2.3.4.5 123.456.78.90 123.045.067.089

[link](https://www.codewars.com/kata/ip-validation/python)

#My solution

```python
def is_valid_IP(strng):
  ip = strng.split('.')
  tbtn = 0
  for sect in ip:
    if sect.isdigit():
      if sect[0] != '0':
        if 0 < int(sect) <= 255:
          tbtn += 1
  return tbtn == 4
```

잘 쪼개면 풀리는 문제다.

#@allonhadaya solution
```python
import socket

def is_valid_IP(addr):
    try:
        socket.inet_pton(socket.AF_INET, addr)
        return True
    except socket.error:
        return False
```
정말 참신하다... socket모듈을 사용하다니..

#@natict solution
```python
def is_valid_IP(s):
    return s.count('.')==3 and all(o.isdigit() and 0<=int(o)<=255 and str(int(o))==o for o in s.split('.'))
```

하.. 이렇게 한줄로 나타내고 싶다..


  