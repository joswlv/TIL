#Codewars #3
--
##Question
Description:

A Hamming number is a positive integer of the form 2i3j5k, for some non-negative integers i, j, and k.

Write a function that computes the nth smallest Hamming number.

Specifically:

- The first smallest Hamming number is 1 = 203050
- The second smallest Hamming number is 2 = 213050
- The third smallest Hamming number is 3 = 203150
- The fourth smallest Hamming number is 4 = 223050
- The fifth smallest Hamming number is 5 = 203051
- The 20 smallest Hamming numbers are given in example test fixture.

Your code should be able to compute all of the smallest 5,000 (Clojure: 2000) Hamming numbers without timing out.

[link](https://www.codewars.com/kata/hamming-numbers/python)
--
#My Solution
```python
def hamming(n):
    h=[]        
    h.append(1)
    i=j=k=0
    while n:
        while h[i]*2<=h[-1]:
            i+=1
        while h[j]*3<=h[-1]:
            j+=1
        while h[k]*5<=h[-1]:
            k+=1
        h.append(min(h[i]*2,h[j]*3,h[k]*5))
        n-=1
    return h[-2]
```
하나하나 계산해 최소값을 저장하는 방식을 택했다. 

--
#@arthur Solution
```python
import itertools

H = sorted([
  2**i * 3**j * 5**k
  for i, j, k in itertools.product(xrange(50), xrange(50), xrange(50))
])
hamming = lambda n, H=H: H[n-1]
```
모든 경우의 수를 우선 적으로 작성했다 그리고 값만 불려오는 lambda식을 작성하였다.
