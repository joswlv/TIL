#Closure


>클로저(Closure)란 자신이 정의된 스코프에 있는 변수를 참조하는 함수 이다.
>
Closure are functions whose inner functions refer to independent (free) variables. In other words, the functions defined in the closure 'remember'the environment in which they were created.

>>클로저가 나온 개념은 자바가 나온지 20년 전부터 나온 개념이라고 한다. 클로저는 글로벌 변수와 객체들을 포함하는 코드 블록이다. 그 안에 있는 변수들은 코드 블록안에 저으이된 채로 숨어 있고, 코드블록을 호출할 때 정의해 놓은 변수와 그것을 정의한 함수를 결합해 새로운 환경제어 영역에 결합함으로써 유연한 결과를 도출하게 해준다.
>



###예) Closure 내부함수의 결과를 저장

```python
'''
Closure 함수속의 함수(내부함수)의 결과를 저장(함수형 언어 : 자바스크립,루비,스칼라)
'''
def Times(a, b ):
    c = a * b
    print(c)  #함수에서 리턴값이 없으면 None을 리턴한다. cf) none 공백, 0 모두 false
    return c
 
print(Times(2, 3))
#print(c)     #error 함수밖에서 지역변수의 값을 찍으면 Error
Kbs = Times 
print(Kbs(2, 3))
print(id(Kbs),id(Times))
del Times #지워버리기
#print(Times(2, 3)) #null point error
print(Kbs(2, 3))
 
Mbc = Kbs
print(Mbc(2, 3))
 
print('\nclosure 구현')
 
def inner():
    count = 0
    def inn():
        nonlocal count #근데 nonlocal로 선언하면 가능하다.
        count += 1 #다른함수에 있는 변수라서 원래는 누적이 안된다. 
        return count
    print(inn())
 
inner() 
inner()
 
print()
def outer():
    count = 0
    def inner():
        nonlocal count   #근데 nonlocal로 선언하면 가능하다.
        count += 1       #다른함수에 있는 변수라서 원래는 누적이 안된다. 
        return count
    return inner          #<== 얘가 클로저 : 내부 함수를 반환하고 있다.
#함수가 가지는 값을 함수가 끝난 후에도 값을 유지하고 싶을때 사용
#사용방법 : 내부함수를 선언해서 내부함수의 이름을 리턴한다. 
 
#클로저로 저장된 값을 이용하는 방법  -> 변수에 저장 후 사용
add1 = outer() #소괄호가 없에 있으면 변수에 실행결과를 저장
print(add1())
print(add1())
print(add1())
 
add2 = outer() #outer type이긴하지만 서로다른 인스턴스이다. 
print(add2())
print(add2())
 
print('\n수량 * 단가 * 세금 결과 출력----')
def outer2(tax) :
    def inner2(su, dan):
        ammount = su * dan * tax
        return ammount 
    return inner2 #<--요게 클로저 함수의 주소를 리턴 (내부함수의 변수를 이용할 수 있다.)
 
r = outer2(0.1)
res = r(5, 50000)
print(res)
 
res = r(3, 25000)
print(res) 
 
r2 = outer2(0.05)
res2 = r2(5, 50000)
print(res2)
res2 = r2( 3, 25000)
print(res2)
```

###Reference
- [EffectivePython](http://www.effectivepython.com)

- [http://forarchitect.tistory.com/53](http://forarchitect.tistory.com/53)

