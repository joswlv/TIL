#Codewars #18
##Question
Description:

Write a program that will calculate the number of trailing zeros in a factorial of a given number.

N! = 1 * 2 * 3 * 4 ... N

```powershell
zeros(12) = 2 # 1 * 2 * 3 .. 12 = 479001600 
that has 2 trailing zeros 4790016(00)
```
Be careful 1000! has length of 2568 digital numbers.

즉 마지막의 연속된 0의 갯수를 구하는 것이다.

[link](https://www.codewars.com/kata/number-of-trailing-zeros-of-n/python)

#My solution

```python
def zeros(n):
    x = 5
    ans = 0
    while n >= x:
        ans += n / x
        x *= 5
    return ans
```
알고리즘 시간에 배웠던 문제이다. 끝자리가 0이 나올려면, 10의 배수 즉 5로 나누어지면 된다. 2의 갯수는 충분히 나온다는 이론이 있던 것으로 기억한다.

#@Iv.D solution

```python
def zeros(n):
  x = n/5
  return x+zeros(x) if x else 0
```

저렇게 return에 메소드를 적는 연습도 해봐야겠다.