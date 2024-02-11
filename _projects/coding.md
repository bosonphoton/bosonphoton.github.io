---

layout: page


title: data structures & algos


description: notes from leetcode 


img: 


importance: 4


category: work

---

<h5>Big O & Recursion</h5>
Log time $$O(log$$ $$n)$$: Means that somewhere in algo, input is <b>reduced by a percentage at each step</b> (i.e., binary search where step 1 is n/2 and step 2 is n/4, etc.)
<br><br>
Recursion:
```python
def f(n):
    print(f(n+1))
```
- This function would never stop running
- We need a <b>BASE CASE</b> which specifies when the recursion ends

<b><u>Base cases</u></b> are specified at the start of the function
```python
def fn(i):
    if i > 10:
        return
    print(i)
    fn(i + 1)
```

<br><br>
<h2>1. Array and Strings</h2>
<h5>Two Pointers</h5>
- Start with two pointers left and right
- Iterate these two pointers along an array or string index
- *Usually start code with while left < right

Check if string is palindrome:
```python
def palindrome(n):
    left = 0
    right = len(n) - 1
    
    while left < right:
        if n[left] != n[right]:
            return False
        else:
            left += 1
            right -= 1
    
    return True
```
<br><br>
Check if there exists a target = sum of two numbers, in sorted array:
- Start summing left and right
- Because array is sorted, we can just move right pointer left if sum is too big, and left pointer right if too small

```python
def sorted_twosum(array, target):
    left = 0
    right = len(array) - 1
    
    while left < right: 
        current = array[left] + array[right]
        if current == target:
            return True
        elif current < target:
            left += 1
        elif current > target:
            right -= 1
    
    return False
```
<br><br>
Using two pointers to iterate through two arrays:
- Start both pointers at the first index
- Use while loop until one pointer reaches end
- At each iteration of the loop, move one or both of the pointers forward

Merge two sorted arrays:
```python
def merge(arr1, arr2):
    ans = []
    i = j = 0
    while i < len(arr1) and j < len(arr2):
        if arr1[i] < arr2[j]:
            ans.append(arr1[i])
            i += 1
        else:
            ans.append(arr2[j])
            j += 1
    
    # finish iterating through the remainder array
    # only one of these blocks will be executed 
    while i < len(arr1):
        ans.append(arr1[i])
        i += 1
    
    while j < len(arr2):
        ans.append(arr2[j])
        j += 1
    
    return ans
```
<br><br>
Check if string A is a subsequence of string B:
- Init two pointers for string A and B
- If pointers match, move both pointers to the next letter
- If no match, move pointer for String B to next letter

```python
def subseq(a,b):
    i = j = 0
    while i < len(a) and j < len(b):
        if a[i] == b[j]:
            i += 1 #need to try to match next character of a
        else:
            j += 1 #will move b if no match
            
    return i == len(a) #True only if we iterated all through a

```
<h2>Search</h2>


<h5>Binary Search</h5>

If we are asked to return the index of an element, rather than a for loop with O(n), we can do it in O(log(n)) using binary search. Divides each section in half recursively.


