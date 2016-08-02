#Codewars #9
##Question
Description:

Write a function called `validBraces` that takes a string of braces, and determines if the order of the braces is valid. `validBraces` should return true if the string is valid, and false if it's invalid.

This Kata is similar to the Valid Parentheses Kata, but introduces four new characters. Open and closed brackets, and open and closed curly braces. Thanks to @arnedag for the idea!

All input strings will be nonempty, and will only consist of open parentheses '(' , closed parentheses ')', open brackets '[', closed brackets ']', open curly braces '{' and closed curly braces '}'.

What is considered Valid? A string of braces is considered valid if all braces are matched with the correct brace. 
For example:
'(){}[]' and '([{}])' would be considered valid, while '(}', '[(])', and '[({})](]' would be considered invalid.

Examples: 
`validBraces( "(){}[]" )` => returns true 
`validBraces( "(}" )` => returns false 
`validBraces( "[(])" )` => returns false 
`validBraces( "([{}])" )` => returns true 

[link](https://www.codewars.com/kata/valid-braces/python)

--
#My Solution

```python
def validBraces(str):
  stack = []
  pushChars, popChars = "<({[", ">)}]"
  for c in str :
    if c in pushChars :
      stack.append(c)
    elif c in popChars :
      if not len(stack) :
        return False
      else :
        stackTop = stack.pop()
        balancing = pushChars[popChars.index(c)]
        if stackTop != balancing :
          return False
    else :
      return False
  return not len(stack)
```
stack에 넣고 비교를 하였다. 순서를 따지는 비교에는 stack을 사용하면 참 편리한것 같다.

--
#@klintwood Solution

```python
def validBraces(string):    
    while len(string) > 0:        
        if "()" in string:
            string = string.replace("()", "")
        elif "[]" in string:
            string = string.replace("[]", "")
        elif "{}" in string:
            string = string.replace("{}", "")
        else:
            return False
    return True 
```

매우 간단한 방식인것 같다. 따로 저장하지 않고 삭제하는 방식으로...