#Codewars #2
--
##Question
Description:

Problem Context

The Fibonacci sequence is traditionally used to explain tree recursion.

```python
def fibonacci(n):
    if n in [0, 1]:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```
This algorithm serves welll its educative purpose but it's tremendously inefficient, not only because of recursion, but because we invoke the fibonacci function twice, and the right branch of recursion (i.e. fibonacci(n-2)) recalculates all the Fibonacci numbers already calculated by the left branch (i.e. fibonacci(n-1)).

This algorithm is so inefficient that the time to calculate any Fibonacci number over 50 is simply too much. You may go for a cup of coffee or go take a nap while you wait for the answer. But if you try it here in Code Wars you will most likely get a code timeout before any answers.

For this particular Kata we want to implement the memoization solution. This will be cool because it will let us keep using the tree recursion algorithm while still keeping it sufficiently optimized to get an answer very rapidly.

The trick of the memoized version is that we will keep a cache data structure (most likely an associative array) where we will store the Fibonacci numbers as we calculate them. When a Fibonacci number is calculated, we first look it up in the cache, if it's not there, we calculate it and put it in the cache, otherwise we returned the cached number.

Refactor the function into a recursive Fibonacci function that using a memoized data structure avoids the deficiencies of tree recursion Can you make it so the memoization cache is private to this function?

[link](https://www.codewars.com/kata/memoized-fibonacci/python)

##My Solution
```python
def fibonacci(n):
    sw = True
    f1 = 1
    f2 = 1
    while n>2:
        if sw:
            f1 = f1+f2
        else:
            f2 = f1+f2
        sw = not sw
        n -=1
    if sw:
        return f2
    else:
        return f1
```
변수 두개만 사용하여 저장하여 구현 하였다.

##@edalorzo Solution
```python
def fibonacci(n):
  fib = [0,1]
  for i in xrange(2,n+1):
    fib.append(fib[i-1] + fib[i-2])
  return fib[n]
```
교과서에서 배운 배열에 저장하는 방법을 사용하였다.