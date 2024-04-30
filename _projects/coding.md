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
<h5><b><u>Rows & Columns</u></b></h5>
Transpose matrix
- Iterate through number of row
  - Iterate through number of columns
  - switch rows and columns so matrix[columns][rows]

```python
numRows = len(matrix)
numCols = len(matrix[0])
transposed = []
for row in range(numRows):
    newCol = []
    for col in range(numCols):
        newCol.append(matrix[col][row])
    transposed.append(newCol)
```

<h5><b><u>Two Pointers</u></b></h5>
<b>***Algorithm</b>
- Start with two pointers left and right
- Iterate these two pointers along an array or string index
- *Usually start code with while left < right

<b>Ex:</b> Check if string is palindrome:
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
<b>Ex:</b> Check if there exists a target = sum of two numbers, in sorted array:
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

<b>Ex:</b> Merge two sorted arrays:
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
<b>Ex:</b> Check if string A is a subsequence of string B:
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

<b>Ex:</b> Return len of longest subarray that sums < k:
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

<b>Ex:</b>Return len of longest sequence of 1's in an array of 1s and 0s. You may flip one 0 (notice this is the same as saying longest array that contains at most one 0):
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

<b>Ex:</b> Return num of subarrays whose product < k
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

<b>Ex:</b> Find sum of the subarray with the largest sum whose length is k:
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

Given int array nums, queries (pertaining to index of nums) where queries[i] = [x, y] and a limit, return bool arr true if the sum from x to y is less than limit: <br>
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
<br>

<b>Ex: Running Sum of 1d Array</b>: Given an array of integers nums, you start with an initial positive value startValue. In each iteration, you calculate the step by step sum of startValue plus elements in nums (from left to right).
Return the minimum positive value of startValue such that the step by step sum is never less than 1. <br><br>
Input: nums = [-3,2,-3,4,2] <br>
Output: 5<br>
Explanation: If you choose startValue = 4, in the third iteration your step by step sum is less than 1.<br>
- Make prefix sum array
- Find minimum of prefix array (pref_min)
- Find X such that sum(X,pref_min) is 1
- If X is less than 1, return 1

```python
def minStartValue(self, nums):
        prefix = [nums[0]]
        for i in range(1,len(nums)):
            prefix.append(prefix[-1]+nums[i])

        if 1 - min(prefix) < 1:
            return 1
        return 1 - min(prefix)
```

<br><br>
<h2>2. Hashing</h2>
A hash function is a function that takes any input and converts to an integer (that is less than some determined value).<br>

<b>PROS</b>
- Hashmaps (dictionaries) are all O(1) for the following: adding key value pairs, delete element if exists, check existence.<br>

<b>CONS</b>
- slower for smaller input sizes
- collisions (when different keys convert to same integer)
- take up more space (arrays are more flexible with resizing)

<h5><b><u>Checking for Existence</u></b></h5>
<b>Ex:</b> Given an array of integers nums and an integer target, return indices of two numbers such that they add up to target. You cannot use the same index twice.<br>
- Store each (key, value) as (element, and it's index)
- Iterate through the array, checking if  already exists in the dictionary
- If not, initialize new entry
- Else, return array[target - array[i]] (which is the index of the "target - array[i]" element)

<b><u>Missing Number</u></b>
<b>Ex:</b> Given an array nums containing n distinct numbers in the range [0, n], return the only number in the range that is missing from the array. <br>
- Approach 1: Sort and compare (return the index that is out of place compared to array element when sorted ascending)
- Approach 2: Hashset (see which number missing from range [0,n] after creating a dictionary)
- Approach 3 (clever trick): Sum Cancellation (sum of expected minus sum of array) 

<h5><b><u>Counting</u></b></h5>
- General tip: Use hashmaps for anything counting related

<b>Ex:</b> You are given a string s and an integer k. Find the length of the longest substring that contains at most k distinct characters.
For example, given s = "eceba" and k = 2, return 3. The longest substring with at most 2 distinct characters is "ece".
- Sliding windows + hashmap: Iterate through the string with sliding windows technique and update the hashmap (deleting elements from left and adding elements such that it satisfies the constraint of len(dict) <= 2) 


```python
def find_longest_substring(s, k):
    counts = {}
    left = ans = 0
    for right in range(len(s)):
        counts[s[right]] += 1 #add the letter (key) to dictionary
        while len(counts) > k: #while constraint is violated, keep removing count (value) of letter (key)
            counts[s[left]] -= 1
            if counts[s[left]] == 0: #also remove letter (key) if value is 0
                del counts[s[left]]
            left += 1 
        
        ans = max(ans, right - left + 1)
    
    return ans
```
<br>
<b><u>Anagrams</u></b>
- Sorting the strings in alphabetical order, if they are anagrams they will be equal

<b>Ex:</b> Given an array of strings strs, group the anagrams together. For example, given strs = ["eat","tea","tan","ate","nat","bat"], return [["bat"],["nat","tan"],["ate","eat","tea"]]. <br>
```python
def groupAnagrams(self, strs):
    groups = defaultdict(list)
    for s in strs:
        key = "".join(sorted(s))
        groups[key].append(s)
    
    return groups.values()
```
<br>

<b>Ex: Minimum Consecutive Cards to Pick Up:</b> Given an integer array cards, find the length of the shortest subarray that contains at least one duplicate. If the array has no duplicates, return -1.
- Initialize a dictionary storing all the indexes of the elements as values
- The shortest array will have the same element in its first and last index
- Check the distance between all adjacent pairs of values and find the minimum

<br><br>
<h2>3. Linked Lists</h2><br>
Even though head changes, ptr still refers to same node
```python
ptr = head
head = head.next
head = None
```
<br>

<b><u>Single Linked Lists</u></b><br>
Say we want to add a new element at position i. <br>
We need a reference to the node at (i - 1) if we wanted to add or remove at (i)

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

def add_node(prev_node, node_to_add):
    node_to_add.next = prev_node.next #next step for new element is to position itself at the next step of previous node (at i-1)
    prev_node.next = node_to_add #set the next step of the previous node at (i-1) to make it i which becomes equal to the new element 
```
<br>
<b><u>Doubly Linked Lists</u></b><br>
Each node also contains pointer to previous node.

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
        self.prev = None

# Let node be the node at position i
def add_node(node, node_to_add):
    prev_node = node.prev
    node_to_add.next = node
    node_to_add.prev = prev_node
    prev_node.next = node_to_add
    node.prev = node_to_add

# Let node be the node at position i
def delete_node(node):
    prev_node = node.prev
    next_node = node.next
    prev_node.next = next_node
    next_node.prev = prev_node
```

<b><u>Fast and slow pointers</u></b><br>
If we have one pointer moving twice as fast as the other, then by the time it reaches the end, the slow pointer will be halfway through since it is moving at half the speed.
```python
def get_middle(head):
    slow = head
    fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    
    return slow.val
```

<br><br>
<h2>Search</h2>
<h5>Binary Search</h5>

If we are asked to return the index of an element, rather than a for loop with O(n), we can do it in O(log(n)) using binary search. Divides each section in half recursively.


