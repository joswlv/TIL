#Codeewars #14
##Question
Description:

Create a function taking a positive integer as its parameter and returning a string containing the Roman Numeral representation of that integer.

Modern Roman numerals are written by expressing each digit separately starting with the left most digit and skipping any digit with a value of zero. In Roman numerals 1990 is rendered: 1000=M, 900=CM, 90=XC; resulting in MCMXC. 2008 is written as 2000=MM, 8=VIII; or MMVIII. 1666 uses each Roman symbol in descending order: MDCLXVI.

Example:

```
solution(1000) # should return 'M'
```
Help:

```
Symbol    Value
I          1
V          5
X          10
L          50
C          100
D          500
M          1,000
```
Remember that there can't be more than 3 identical symbols in a row.

[link](http://www.codewars.com/kata/roman-numerals-encoder/python)

##My solution

```python
def solution(x):
    anums = [1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1]
    rnums = "M CM D CD C XC L XL X IX V IV I".split()
    ret = []
    for a,r in zip(anums, rnums):
        n,x = divmod(x,a)
        ret.append(r*n)
    return ''.join(ret)
```

앞선 문제랑 비슷하다. 

맥북프로에서 돌렸을때, 9자리부터 컴퓨터가 힘들어 한다...

##@kurnos solution

```python
vals = zip(('M', 'CM', 'D', 'CD', 'C', 'XC', 'L', 'XL', 'X', 'IX', 'V', 'IV', 'I'),
           (1000, 900, 500,  400, 100,   90,  50,   40,  10,    9,   5,    4,   1))

def solution(n):
    if n == 0: return ""
    return next(c + solution(n-v) for c,v in vals if v <= n)
```
`next()`를 사용하였다. 나누기 대신에 뺄셈으로 정답을 구해간다.

사칙연산중에 나머지연산이 가장느리다고 하니.. 뺄셈으로 하는게 더 나을 지도..