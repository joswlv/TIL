#Codewars #7
##Question
Description:

How many ways can you make the sum of a number?

From wikipedia: [https://en.wikipedia.org/wiki/Partition_(number_theory)#](https://en.wikipedia.org/wiki/Partition_(number_theory)#)

In number theory and combinatorics, a partition of a positive integer n, also called an integer partition, is a way of writing n as a sum of positive integers. Two sums that differ only in the order of their summands are considered the same partition. If order matters, the sum becomes a composition. For example, 4 can be partitioned in five distinct ways:

```
4
3 + 1
2 + 2
2 + 1 + 1
1 + 1 + 1 + 1
```
Examples

Trivial

```
sum(-1) # 0
sum(1) # 1
```
Basic

```
sum(2) # 2  -> 1+1 , 2
sum(3) # 3 -> 1+1+1, 1+2, 3
sum(4) # 5 -> 1+1+1+1, 1+1+2, 1+3, 2+2, 4
sum(5) # 7 -> 1+1+1+1+1, 1+1+1+2, 1+1+3, 1+2+2, 1+4, 5, 2+3

sum(10) # 42
```
Explosive

```
sum(50) # 204226
sum(80) # 15796476
sum(100) # 190569292
```
[link](https://www.codewars.com/kata/explosive-sum/python)

--
#My Solution

```python
def exp_sum(n):
    dp = [[0 for x in range(n+1)] for x in range(n+1)]
    return e_sum_dp(n, 1, dp)

def e_sum_dp(n, index, dp):
    if n == 0:
        return 1
    if n < 0:
        return 0
    if dp[n][index] != 0:
        return dp[n][index]

    count = 0
    for i in range(index, n+1):
        count += e_sum_dp(n-i, i, dp)

    dp[n][index] = count
    return count
```
2를 구성하는 법은 1+1과 2 총 두가지이다. 그리고 3을 구성하는 법은 2를 구성하는 을 더한 것에 3이라는 숫자 하나를 추가한 것이다. 그리고 4를 구성하는 법은 3을 구성하는 법 2를 구성하는 법을 덧셈한 것이다. 이렇게 동적계획을 설계했다.

--
#@algosage Solution
```python
def exp_sum(n):
  if n < 0:
    return 0
  dp = [1]+[0]*n
  for num in xrange(1,n+1):
    for i in xrange(num,n+1):
      dp[i] += dp[i-num]
  return dp[-1]
```
같은 동적 계획 법인데 좀 더 세련되 보인다~