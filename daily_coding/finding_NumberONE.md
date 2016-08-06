#Google Problem #13
##Question
정수 1에서 n 까지 숫자를 f(n)에 n이하의 수에1이 들어가는 갯수를 k라 할때, f(n)=k

- ex) f(13)=6 => 1,10,11,12,13 (총 1이 6개)
<!> n=k 이 되는 최초의 n은 1일때가 된다. 

`두번째로 n=k가 되는 n을 구하라`

#My Solution

```python
count =0
def finding(n):
    global count
    num = int(n/10)
    if n%10 ==1 :
        count +=1
    if num >0 :
        finding(num)
    return

def findOne():
    n =1
    while 1:
        finding(n)
        if n ==count and n!=1:
            break
        n+=1
    return n
```

`count`를 전역변수로 사용하여 카운팅을 한다. 

답 -> `199981`가 나온다.
[Finished in 0.343s]