#Golang_GDGDevCamp

##Golang Summary
- 파이썬만큼 간단하지만 c,C++만큼 빠른언어이다.
- 정적 타입, 강 타입 언어, 가비지 컬렉션 지원
- 고루틴과 채널을 이요해 간편히 동시성 기능 구현 가능(강점)
- 가상머신 없이 운영체제별 크로스 컴파일 가능
- 간편하고 익숙한 형태로 라이브러리 패키지를 가져오는 것이 가능

##Code Style
- 자료형을 선언 할때는 변수명 뒤에 붙임
- 자료형을 명시 할 수 있지만, 필요에 따라 생략하는 것이 가능 하지만 한번 자료형이 결정되면 변경이 불가능
- 조건문이나 반복문에서 활용되는 ()가 거의 생략됨
- 다중결과값 반환이 가능
- 함수형 언어의 대표적인 기능을 가지고 잇음 -> 익명함수, 클로저, 지연호출 등
- `go fmt`명령어를 이용하여 go언어의 코딩스타일에 맞게 정렬이 가증하다. 포멧이 맞지 않음녀 에러남~!!!
- 사용하지 않는 변수가 있으면, 에러처리

##Golang 문법
```go
import "fmt"
func main)({
	var age = 10
	var name string
	name = "ace"
	id :=131
	
	fmt.Println(age) //10
	fmt.Println(name) // ace
	fmt.Println(id) //131
```

```go
if i:=3; i>2{
	fmt.Println("ok")
	}
```

```go
func main(){
	a := [5]int{31,13,1,31,3}
	for value := range a{
		fmt.Println(value)
	}
}
```

- slice(Dynamic Array)

###function

```go
func sum(a int, b int) (r int){
	r = a+b
	return
}
```

- go언어는 클래스를 자원하지 않고, 구조체를 이용하여 객체지향을 지원함 
- type이라는 키워드로 구조체를 선언 할 수 있으며, 왼쪽과 같이 구조체 인스턴스를 선언하는 방법, 구조체 포인터를 선언하는 방법이 있다.


###Structure Method
```go
type Rect struct{
	w int
	h int
}

func (rect *Rect) area() int {
	return rect.w * rect.h
}
```

###Interface / Duck Typing
- go에서는 구조체가 인터페이스를 다루기 위해 implements 와 같은 키워드를 이용하여 상속을 다루지 않는다.
- 인터페이스를 정의하고 그 인터페이스가 다룰 메소드를 정의 하며 각 구조체나 자료형이 해당 메서드를 구체적으로 구현 하는것으로 본 객체가 해당 인터페이스를 구현한 것으로 간주한다. 

- 별도의 인터페이스 활용을 명시하는 것이 없이 객체의 구현된 행동들을 보고 어떤 인터페이스를 활용하는지를 파악하는 기법을 duck typing 이라고 한다. 


###function literal

```go
func main(){
	s := func(number int) int{
		return number
	}(100)
	
	fmt.Println(s) //100
}
```

###Closure
- 클로저는 함수안에서 함수를 선언하고, 선언된 함수의 바깥에 있는 변수에도 접근 가능한 함수를 가리키는 말
- 장점은 함수가 선언 될 때의 환겨을 계속 유지하는 것이 가능하며, 프로그램의 흐름을 변수에 저장 할 수 있다는 것.


###Goroutines /Channel
고루틴 == 쓰레드
고루틴을 코어 갯수를 정하여 돌릴 수 있다.
여러개의 고루틴을 관라히기 위해 채널을 생성하여, 각각의 데이터를 공유한다. 
채널에서 값을가져오는 것은 해당 채널에 값이 들어왔을 때 가능하는 것~!!

###Go test 
output을 주석으로 만들어도 된다. [joinc.co.kr/w/man/12/TDD](http://www.joinc.co.kr/w/man/12/TDD)

###추천영역
- 웹서비스 백엔드
- 분산처리서버
- Api서버
- 데이터베이스앤진
- 크롤러와 같은 간단한 작업을 진해앟는 애플리케이션

시스템 개발을 비추~!!

웹서비스 - > Revel
Docker가 go언어로 만들어 져있음!!


