#Codewars #5

##Question
Description:

Snail Sort

Given an n x n array, return the array elements arranged from outermost elements to the middle element, traveling clockwise.

```
array = [[1,2,3],
         [4,5,6],
         [7,8,9]]
snail(array) #=> [1,2,3,6,9,8,7,4,5]
```
For better understanding, please follow the numbers of the next array consecutively:

```
array = [[1,2,3],
         [8,9,4],
         [7,6,5]]
snail(array) #=> [1,2,3,4,5,6,7,8,9]
```

NOTE: The idea is not sort the elements from the lowest value to the highest; the idea is to traverse the 2-d array in a clockwise snailshell pattern.

NOTE 2: The 0x0 (empty matrix) is represented as [[]]

[link](https://www.codewars.com/kata/snail/python)

--
#My Solution
```python
def snail(array):
    incr = 1
    row =0
    col =-1
    ans = []
    leng = len(array)
    if leng ==1 :
        ans += array[0]
        return ans
    while leng>0:
        for i in range(leng):
            col += incr
            ans.append(array[row][col])
        leng -=1
        if leng==0 :
            break
        for j in range(leng):
            row += incr
            ans.append(array[row][col])
        incr *=-1
    return ans
```
정보처리기사 시험 준비할때 많이 보던 코드다. 순수하게 문제에 충실한 답변이다.

--
#@foxxyz Soultion
```python
def snail(array):
    return list(array[0]) + snail(zip(*array[1:])[::-1]) if array else []
```
'`zip()` 사용을 이렇게 하구나'라는 생각을 하였다.