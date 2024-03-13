---

layout: page


title: data structures & algos


description: notes from leetcode 


img: 


importance: 4


category: work

---
<style>
    body {
      font-size: 16px; /* Adjust the font size as needed */
      line-height: 1; /* Adjust the line height as needed */
    }
    p {
      margin-bottom: 8px; /* Adjust the margin bottom for paragraphs as needed */
    }
    .math {
      font-size: 15px; /* Adjust the font size for math expressions as needed */
    }
</style>



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
<h5><b><u>Two Pointers</u></b></h5>
<b>***Algorithm</b>
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
<br>
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
<br>
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
<br>
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
<br>
<h5><b><u>Sliding Window</u></b></h5>
Use sliding windows when the problem:
1. Defines some constraint/attribute to make the subarray "valid" (valid if sum of subarray is < 10)
2. Asks to find subarray in some way (i.e., longest, shortest, largest valid subarray)

Examples of problems include:
- Find the longest subarray with a sum less than or equal to k
- Find the longest substring that has at most one "0"
- Find the number of subarrays that have a product less than k

<b>***Algorithm:</b> Left and right bound of subarray can be defined by two pointers:
- initialize two pointers left = right = 0
- increment right to add new valid elements to subarray
- increment left to remove elements that make subarray invalid
- keep track of constraint using a variable "curr"" and then do "curr += nums[right]" etc. (to maintain O(1))
- use <b>for loop</b> to increment <b>right to </b>add elements 
- use <b>while loop</b> to <b>remove</b> elements until array valid
- update answer after exiting while loop

For an array of length n, there are:<br>
- n subarrays of length 1 <br>
- (n - 1) subarrays of length 2 <br>
- (n - 2) subarrays of length 3...<br>
- So in total there are $$\frac{n(n+1)}{2}$$ subarrays

Return len of longest subarray that sums < k:
```python
def subarr(array,k):
    i = j = 0
    curr = 0 #constraint checker
    ans = 0
    for i in range(len(array)): #keep adding elements til
        curr += array[i] #update current checker
        while curr > k: #keep removing elements until current is <= k
            curr -= array[j]
            j += 1        
        ans = max(ans, right - left + 1)
    
    return ans
```
Return len of longest sequence of 1's in an array of 1s and 0s. You may flip one 0 (notice this is the same as saying longest array that contains at most one 0):
```python
def ones(array): #constraint in this problem is curr <= 1 zeros
    i = j = ans = 0
    curr = 0
    for i in range(len(array)):
        if array[i] == 0: #if right pointer encounters 0
            curr += 1 
        while curr > 1: #remove element if left pointer is 0
            if array[j] == 0:
                curr -= 1
            j += 1   
        ans = max(ans, right - left + 1)

    return ans
```
<br>
<b>Number of Subarrays</b> <br>
- Suppose current window is (left, right). Number of valid subarrays up till right index  = len of window (because left can keep indexing until right).
- Inside while loop, update answer: [Ans += current window length]

Return num of subarrays whose product < k
```python
def subarr(array,k):
    if k <= 1:
        return 0
    
    j = answer = 0
    curr = 1
    for i in range(len(array)):
        curr *= array[i]
        while curr >= k:
            curr /= array[j]
            j += 1
        
        windowlen = i - j + 1 #if you fix the right bound, left bound can take any value up to right 
        ans += windowlen
        
    return answer
```
<br>
<b>Fixed Window Size</b> (problems that require subarrays to be some fixed length k)<br>
- build window: from index 0 to index (k -1)
- add element at index i and keep window size by removing element at index<b> (i - k) </b> <br>

Find sum of the subarray with the largest sum whose length is k:
```python
def subarr(nums,k):
    curr = 0 
    for i in range(k): #build first window 
        curr += nums[i] #sum of first window
    
    ans = curr 
    for i in range(k, len(nums)): #start at element to right of existing window
        curr += nums[i] - nums[i - k] #add right and remove left element
        ans = max(ans, curr)
    
    return an
```
<br>
<h5><b><u>Prefix Sum</u></b></h5>
- Create array prefix where prefix[i] is the sum of all elements up to i
- Sum from i to j = prefix[j] - prefix[i-1] <-- (which is the sum before index i)

Given int array nums, queries where queries[i] = [x, y] and a limit, return bool arr true if the sum from x to y is less than limit: <br>
nums = [1, 6, 3, 2, 7, 2]<br>
queries = [[0, 3], [2, 5], [2, 4]]<br>
limit = 13<br>
the answer is [true, false, true]

```python
def answer_queries(nums, queries, limit):
    #builds the prefix array
    prefix = [nums[0]] #start with first element in nums so [-1] index won't be empty
    for i in range(1, len(nums)): #start adding the last value of prefix with the next value in nums
        prefix.append(nums[i] + prefix[-1])
    
    ans = []
    for x, y in queries:
        curr = prefix[y] - prefix[x] + nums[x] # add nums[x] bc it's included in array 
        ans.append(curr < limit)

    return ans
```








<br><br>
<h2>Search</h2>
<h5>Binary Search</h5>

If we are asked to return the index of an element, rather than a for loop with O(n), we can do it in O(log(n)) using binary search. Divides each section in half recursively.


