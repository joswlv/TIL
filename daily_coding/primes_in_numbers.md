#Codewars #11
##Question
Description:

Given a positive number n > 0 (Javascript n >= 0) find the prime factor decomposition of n. The result will be a string with the following form :

```python
 "(p1**n1)(p2**n2)...(pk**nk)"
```
with the p(i) in increasing order and n(i) empty if n(i) is 1.

```python
Example: n = 86240 should return "(2**5)(5)(7**2)(11)"
```

[link](https://www.codewars.com/kata/primes-in-numbers/train/python)

#My Solution

```python
import math
def primecheck(n):
    if n == 2 or n == 3:
        return True
    if n % 2 == 0 or n == 1:
        return False
    for i in range(3, int(math.sqrt(n)) + 1, 2):
        if n % i == 0:
            return False
    return True

def primeFactors(n):
    result=[]
    primenumber=[]
    endnum = int(math.sqrt(n))
    if primecheck(n):
        return "("+str(n)+")"
    for i in range(2,endnum):
        if primecheck(i):
            primenumber.append(i)
    for j in primenumber:
        count=0
        while n%j==0:
            count+=1
            n=int(n/j)
        if count==1:
            result.append("("+str(j)+")")
        elif count!=0:
            result.append(("("+str(j)+"**"+str(count)+")"))
        if n==1:
            break
    return "".join(result)
```

0이 될때까지 계속 해서 나누어 count를 증가 시켰다.
문제는 적당히 커지는 숫자에서는 n에 루트한 값보다 큰 소수가 발견되어 에러가 난다.

--
#@student003 Solution

```python
def primeFactors(n):
    ret = ''
    for i in xrange(2, n + 1):
        num = 0
        while(n % i == 0):
            num += 1
            n /= i
        if num > 0:
            ret += '({}{})'.format(i, '**%d' % num if num > 1 else '')
        if n == 1:
            return ret
```

알고리즘은 같은데, 쓸데 없이 리스트에 추가하는 연산등을 하지 않았다. 그래서 잘된거 같다... 결정적인거는 소수를 구할 필요가 없다.. 그냥 값을 구하면 된다....