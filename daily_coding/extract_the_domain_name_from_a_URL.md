#Codewars #16
##Question

Description:

Write a function that when given a URL as a string, parses out just the domain name and returns it as a string. For example:

```powershell
domain_name("http://github.com/carbonfive/raygun") == "github" 
domain_name("http://www.zombie-bites.com") == "zombie-bites"
domain_name("https://www.cnet.com") == "cnet"
```

[link](https://www.codewars.com/kata/extract-the-domain-name-from-a-url-1/python)

#My Solution
```python
def domain_name(url):
    parts = url.split('//')
    if len(parts)>1:
        domain = parts[1].split('.')
        if domain[0] == "www":
            if len(domain)>1:
                return domain[1]
        else:
            return domain[0]
    else:
        part = url.split('.')
        if part[0]=="www":
            if len(part)>1:
                return part[1]
        else:
            return part[0]
```
if else문 도배..

#@cakko Solution

```python
def domain_name(url):
    return url.split("//")[-1].split("www.")[-1].split(".")[0]
```

정말.. 왜나는 이런 생각을 못할까..
