#Codewars #19
###Question
Description:

Given: an array containing hashes of names

Return: a string formatted as a list of names separated by commas except for the last two names, which should be separated by an ampersand.

Example:

```
namelist([ {'name': 'Bart'}, {'name': 'Lisa'}, {'name': 'Maggie'} ])
# returns 'Bart, Lisa & Maggie'

namelist([ {'name': 'Bart'}, {'name': 'Lisa'} ])
# returns 'Bart & Lisa'

namelist([ {'name': 'Bart'} ])
# returns 'Bart'

namelist([])
# returns ''
```
Note: all the hashes are pre-validated and will only contain A-Z, a-z, '-' and '.'.

[link](https://www.codewars.com/kata/format-a-string-of-names-like-bart-lisa-and-maggie/python)

##My solution

```python
def namelist(names):
    lens=len(names)
    s = []
    if lens == 1:
        return names[0]['name']
    elif lens == 0:
        return ''
    else:
        for n in names:
            s.append(n['name']+", ")
        s[-1]= " & "+s[-1].split(',')[0]
        s[lens-2]=s[lens-2].split(',')[0]
        return "".join(s)
```

문제를 말 그대로 옮겼다..

##@tauchw solution

```python
def namelist(names):
  return ", ".join([name["name"] for name in names])[::-1].replace(",", "& ",1)[::-1]
```
한줄로 만들 수 있다... 

##@marceltschoppch solution

```python
def namelist(names):
    if len(names) > 1:
        return '{} & {}'.format(', '.join(name['name'] for name in names[:-1]), 
                                names[-1]['name'])
    elif names:
        return names[0]['name']
    else:
        return ''
```

`format`을 활용 할 수 있다..