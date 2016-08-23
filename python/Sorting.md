#Sorting

##MergeSort
```python
def mergeSort(x):
    if len(x)<=1:
        return x
    m = len(x)//2
    L = mergeSort(x[:m])
    R = mergeSort(x[m:])
    result = []
    i=0
    j=0
    while i<len(L) and j<len(R):
        if L[i]<R[j]:
            result.append(L[i])
            i+=1
        else:
            result.append(R[j])
            j+=1
    result +=L[i:]
    result +=R[j:]
    return result
```

##QuickSort
```python
def quickSort(x):
    if len(x)<=1:
        return x
    pivot = x[len(x)//2]
    less = []
    more = []
    equal = []
    for a in x:
        if a<pivot:
            less.append(a)
        elif a>pivot:
            more.append(a)
        else :
            equal.append(a)
    return quickSort(less)+equal+quickSort(more)
```

##BubbleSort
```python
def bubbleSort(x):
    length = len(x)-1
    for i in range(length):
        for j in range(length-i):
            if x[j]>x[j+1]:
                x[j], x[j+1]=x[j+1], x[j]
    return x
```

##SelectionSort
```python
def selectionSort(x):
    length = len(x)
    for i in range(length-1):
        for j in range(i+1,length):
            if x[i]>x[j]:
                x[i],x[j]=x[j],x[i]
    return x
```

##InsertSort
```python
def insertSort(x):
    for i in range(1,len(x)):
        j = i-1
        key = x[i]
        while x[j]>key and j>=0:
            x[j+1] = x[j]
            j=j-1
        x[j+1]=key
    return x
```

##BinarySearch
```python
def binarySearch(arr, val):
    arr = quickSort(arr)
    low =0
    high = len(arr)-1
    while(low<=high):
        mid= (low+high)//2
        if arr[mid]>val:
            high = mid-1
        elif arr[mid]<val:
            low = mid+1
        else:
            return True
    return False
```