#Coderwars #8
##Question
Description:

Construct a function that, when given a string containing an expression in infix notation, will return an identical expression in postfix notation.

The operators used will be +, -, *, /, and ^ with standard precedence rules and left-associativity of all operators but ^.

The operands will be single-digit integers between 0 and 9, inclusive.

Parentheses may be included in the input, and are guaranteed to be in correct pairs.

```python
to_postfix("2+7*5") # Should return "275*+"
to_postfix("3*3/(7+1)") # Should return "33*71+/"
to_postfix("5+(6-2)*9+3^(7-1)") # Should return "562-9*+371-^+"
```
[link](https://www.codewars.com/kata/infix-to-postfix-converter/python)
#My Solution

```python
class Stack:
     def __init__(self):
         self.items = []

     def isEmpty(self):
         return self.items == []

     def push(self, item):
         self.items.append(item)

     def pop(self):
         return self.items.pop()

     def peek(self):
         return self.items[len(self.items)-1]

def to_postfix(infix):
    s=Stack()
    outlst=[]
    prec={}
    prec['^']=4
    prec['/']=3
    prec['*']=3
    prec['+']=2
    prec['-']=2
    prec['(']=1
    infix = ' '.join(infix)
    tokenlst=infix.split()
    for token in tokenlst:
        if token in '0123456789':
            outlst.append(token)
        elif token == '(':
            s.push(token)
        elif token == ')':
            topToken=s.pop()
            while topToken != '(':
                outlst.append(topToken)
                topToken=s.pop()
        else:
            while (not s.isEmpty()) and (prec[s.peek()] >= prec[token]):
                outlst.append(s.pop())
            s.push(token)

    while not s.isEmpty():
        opToken=s.pop()
        outlst.append(opToken)

    return "".join(outlst)
```

stack에 연산기호를 넣었기 때문에 postfix로 변경이 가능했다. 만약 Queue에 연산기호를 넣고 똑같이 하면 prefix로 변경이 가능할 것이다.

