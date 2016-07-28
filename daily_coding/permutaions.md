#Codewars #4
--
##Question
Description:

In this kata you have to create all permutations of an input string and remove duplicates, if present. This means, you have to shuffle all letters from the input in all possible orders.

Examples:

```
permutations('a'); # ['a']
permutations('ab'); # ['ab', 'ba']
permutations('aabb'); # ['aabb', 'abab', 'abba', 'baab', 'baba', 'bbaa']
```
The order of the permutations doesn't matter.

[link](https://www.codewars.com/kata/permutations/python)
--
#My Solution
```python
def permutations(string):
    ans = set([string])
    if len(string) ==2 :
        ans.add(string[1]+string[0])
    elif len(string)>2:
        for i, c in enumerate(string):
            for s in permuations(string[:i]+string[i+1]):
                ans.add(c+s)
    return list(ans)
```
글자 하나하나 반복문으로 재배열하는 노동을 하였다.
--
#@tmikkelsen Solution
```python
import itertools

def permutations(string):
    return list("".join(p) for p in set(itertools.permutations(string)))
```
`itertools`가 이번 문제와 같은 기능을 하는 함수였다. 이런 모듈이 있었다니~!!! 

