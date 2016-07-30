#Codewars #6
##Question
Description:

Write a function that counts how many different ways you can make change for an amount of money, given an array of coin denominations. For example, there are 3 ways to give change for 4 if you have coins with denomination 1 and 2:

```
1+1+1+1, 1+1+2, 2+2.
```
The order of coins does not matter:

```
1+1+2 == 2+1+1
```
Also, assume that you have an infinite ammount of coins.

Your function should take an amount to change and an array of unique denominations for the coins:

```
  count_change(4, [1,2]) # => 3
  count_change(10, [5,2,3]) # => 4
  count_change(11, [5,7]) # => 0
```
[link](https://www.codewars.com/kata/counting-change-combinations/python)

--
#My Solution
```python
def count_change(money, coins):
    if money == 0:
        return 1
    elif money < 0 or not coins:
        return 0
    else:
        coin = coins[-1]
        return sum(
            count_change(a, coins[:-1])
            for a in range(money, -1, -coin)
        )
```

총액에서 각각의 코인을 빼서 0이 되면 count를 증가 시키는 방법 이다. Top-Down방식~~

#@rincewind Solution
```python
def count_change(money, coins):
    dp = [1]+[0]*money
    for coin in coins:
        for x in xrange(coin,money+1):
            dp[x] += dp[x-coin]
    return dp[money]
```
DP를 이용한 풀이 방법이다.