#Codewars #17
##Question
Description:

Create a function that takes a Roman numeral as its argument and returns its value as a numeric decimal integer. You don't need to validate the form of the Roman numeral.

Modern Roman numerals are written by expressing each decimal digit of the number to be encoded separately, starting with the leftmost digit and skipping any 0s. So 1990 is rendered "MCMXC" (1000 = M, 900 = CM, 90 = XC) and 2008 is rendered "MMVIII" (2000 = MM, 8 = VIII). The Roman numeral for 1666, "MDCLXVI", uses each letter in descending order.

Example:

```powershell
solution('XXI') # should return 21
```

[link](https://www.codewars.com/kata/roman-numerals-decoder/python)

#My solution

```python
vals = zip(('M', 'CM', 'D', 'CD', 'C', 'XC', 'L', 'XL', 'X', 'IX', 'V', 'IV', 'I'),
           (1000, 900, 500,  400, 100,   90,  50,   40,  10,    9,   5,    4,   1))

def solution(roman):
    i = result = 0
    for rnum,anum in vals:
        while roman[i:i + len(rnum)] == rnum:
            result += anum
            i += len(rnum)
    return result
```
로마숫자 나온거 계속해서 더해주는 방식

#kurnos solution

```python
values = [('M', 1000), ('CM', -200), ('D', 500), ('CD', -200),
          ('C', 100), ('XC', -20), ('L', 50), ('XL', -20),
          ('X', 10), ('IX', -2), ('V', 5), ('IV', -2),
          ('I', 1)]
def solution(roman):
    return sum(roman.count(s)*v for s,v in values)
```
어쩜 이렇게 간결하게 적을까.. 똑똑하다..

