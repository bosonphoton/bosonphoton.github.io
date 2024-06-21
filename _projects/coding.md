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
<br>
Random neat trick to flip between 1 and 0 is f(x) = 1 - x. f(1) = 0 and f(0) = 1.

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
<br>

<b>Print the next index:<b>

```python
arr = [0,1,2,3,4]
for i in range(len(arr) - 1):
    print(arr[i], arr[i+1])
```
<br>

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
<b>size of window = right index - left index + 1 </b><br>

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
We have a single "next" pointer, so we need a reference to node at i-1 to refer to previous <br>

Say we want to add a new element X into position i. <br>
1. We need a pointer at i-1
2. The next element (which is at i) will be pushed to i+1
2. Which becomes the next node of X
3. X becomes the next node of pointer 
We need a reference to the node at (i - 1) if we wanted to add or remove at (i)

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

def add_node(prev_node, node_to_add): #prev_node at i-1
    node_to_add.next = prev_node.next #
    prev_node.next = node_to_add #set the next step of the previous node at (i-1) to make it i which becomes equal to the new element 
```
<img src = "/assets/node1.png" width = '300' height = '200'>
<img src = "/assets/node2.png" width = '300' height = '200'>

<br><br>
<b><u>Doubly Linked Lists</u></b><br>
We now have a pointer to previous node as well, so unlike single lists, we only need reference to node at i.<br>
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
<img src = "/assets/node3.png" width = '400' height = "200">

<br><br>
<b><u>Linked Lists w/ Sentinel Nodes</u></b><br>
Head pointer @ start of list and tail pointer @ end of linked lists.<br>
The real head of the linked list is head.next and the real tail is tail.prev. <br>
The sentinel nodes themselves are not part of our linked list.

<br>
<b><u>Fast and slow pointers</u></b><br>

- If we have one pointer moving twice as fast as the other, then by the time it reaches the end, the slow pointer will be halfway through since it is moving at half the speed.

```python
def get_middle(head):
    slow = head
    fast = head
    while fast and fast.next: #fast.next is necessary because if fast is last then fast.next is null and fast.next.next throws an error
        slow = slow.next
        fast = fast.next.next
    
    return slow.val
```

<br>
<b>Ex:</b> Checking if a linked list has a cycle/is closed (imagine a circular track)<br>
- If the fast pointer eventually meets the slow pointer at some point, we can conclude its closed
- Otherwise if the distance between fast and slow just keeps increasing with no end, its non-cyclical

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow = head
        fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True

        return False
```

<b>Ex:</b> Given a linked list and an integer k, return the k'th from the tail end <br>
- Position slow pointer at head and fast pointer k steps from head.
- When fast pointer reaches the end, we know slow must be k'th distance away from tail.

```python
def find_node(head, k):
    slow = head
    fast = head
    for _ in range(k):
        fast = fast.next
    
    while fast:
        slow = slow.next
        fast = fast.next
    
    return slow
```
<b>Ex:</b> Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.
```python
def duplicates(head):
    current = head
    while current and current.next:
        if current == current.next: #if there is a duplicate
          current.next = current.next.next #skip the duplicate (current.next) node
        else:
          current = current.next #increment as normal
    
    return head
```
<br>
<b><u>Reversing Linked Lists</u></b><br>
- At any given node curr, we can set curr.next = prev to switch direction of arrow
- At every step through the list (driven by next_node), we switch the directional arrow  
```python
def reverse_list(head):
    prev = Null #set prev to be before the head
    curr = head
    while curr:
        next_node = curr.next # first, make sure we set the next node one step forward
        curr.next = prev      # reverse the direction of the arrow
        prev = curr           # now prev moves forward to the start curr location
        curr = next_node      # move curr forward
        
    return prev
```

<b>Ex:</b> Swap Nodes in Pairs: <br>
- Given the head of a linked list, swap every pair of nodes. For example, given a linked list 1 -> 2 -> 3 -> 4 -> 5 -> 6, return a linked list 2 -> 1 -> 4 -> 3 -> 6 -> 5.

```python
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        dummy = ListNode(0,head) #initialize dummy variable
        prev, curr = dummy, head #dummy is set to the node before head

        while curr and curr.next: 
          # first define a few pointers
          nextPair = curr.next.next
          secondNode = curr.next
          
          secondNode.next = curr #point the next step of secondNode back to curr
          curr.next = nextPair #point the next step of the first node to the next pair
          
          #now we know first node is in 2nd nodes position
          prev.next = secondNode #swap 2nd node to first position
          
          #update pointers
          prev = curr
          curr = nextPair
        
        return dummy.next #which will always point to head
```

<br><br>
<h2>4. Stacks</h2> <br> 
- LIFO (last in first out) -- like a stack of plates
- Push = append to list 
- Pop = remove from end of list
- Check conditions for stack[-1]
<br>

```python
def isValid(s)
    stack = []
    matching = {"(": ")", "[": "]", "{": "}"}

    for c in s:
        if c in matching: # if c is an opening bracket
            stack.append(c)
        else: # c is either a closing bracket
            if not stack: # or it DNE so return False
                return False
            previous_opening = stack.pop() # check for matching closing bracket
            if matching[previous_opening] != c: #if does not match then return false
                return False

    return not stack # since we are popping/removing elements as we go, return True if empty
```

<br><br>
<h4>Queues</h4> <br> 
- FIFO (first in first out) -- like a fast food line <br>


```python
from collections import deque

class RecentCounter:
    def __init__(self):
        self.queue = deque()

    def ping(self, t: int) -> int:
        while self.queue and self.queue[0] < t - 3000:
            self.queue.popleft()
        
        self.queue.append(t)
        return len(self.queue)


# Your RecentCounter object will be instantiated and called as such:
# obj = RecentCounter()
# param_1 = obj.ping(t)
```
<br>
<h5>Monotonic</h5> <br> 
- For each index, find the number of days it is away from a warmer day

```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        stack = [] #stores indices as long as temp keeps decreasing
        answer = [0] * len(temperatures) # init array
        
        for i in range(len(temperatures)):
            while stack and temperatures[stack[-1]] < temperatures[i]: #make sure stack is monotonic decreasing
                j = stack.pop() 
                answer[j] = i - j #find how many indices away it is from the element
            stack.append(i) 
        
        return answer
```

<br><br>
<h2>5. Binary Trees</h2> <br>

<h4>Depth First Search (DFS): Travel down as deep as possible before wide </h4> 
<br><br>

<h5>Iterative Approach (Using Stacks): Returning DFS Order </h5>
```python
def DFS(root):
    if not root: #base case
      return []
    
    stack = [root] #initialize a stack with root node to keep track of current levels / nodes
    answer = []
    while stack: #while stack contains at least one node
        current = stack.pop() #checks last node of stack (left to right since last element being pushed is left child below)
        answer.append(current.val) #stores current node
        if current.right: #if current node has a right child, then push onto stack
            stack.append(current.right)
        if current.left: #if current node has a left child, then push onto stack
            stack.append(current.left)
```
<br>

<h5>Recursive Approach: Returning DFS Order</h5>
- Preorder: Logic done on current node before moving onto children 
- Inorder: Logic done after reaching node without left child 
- Postorder: Logic done only after reaching leaf nodes

```python
def dfs(node):
    if node == None:
        return

    dfs(node.left) # RECURSIVELY KEEP CALLING LEFT UNTIL NO LEFT NODE EXISTS...THEN CALL RIGHT
    dfs(node.right)
    return
```

<br>

<b>Ex: Return Maximum Depth of Tree</b>
```python
def maxDepth(self, root):
    if not root:
        return 0
    
    left = self.maxDepth(root.left)
    right = self.maxDepth(root.right)
    return max(left, right) + 1
```
<br>
<h4>Breadth First Search (BFS):</h4> Traverse as <b>wide</b> as possible at given level first before deep <br>
- init a queue
- while queue:
- init variable tracking length of queue (# of current nodes we need to iterate left/right for)
- iterate over that many of times (to find left/right child of current nodes)
- pop the queue so it clears for the next step
- append the children (so queue only storing next nodes)


```python
from collections import deque

def print_all_nodes(root):
    queue = deque([root])  #stores all nodes at NEXT level from left to right
    while queue:
        nodes_in_current_level = len(queue) #we must iterate over this # of times to find left/right child for each

        for _ in range(nodes_in_current_level): #iterate over each level
            node = queue.popleft() #removes all nodes at CURRENT level
    
            print(node.val)
            
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
```
<br>
<b>Ex: Return all right values</b>

```python
def rightSideView(self, root):
    if not root:
        return []
    
    ans = []
    queue = deque([root])
    
    while queue:
        current_length = len(queue)
        ans.append(queue[-1].val) # this is the rightmost node for the current level
        
        for _ in range(current_length):
            node = queue.popleft()
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
    
    return ans
```
<br>

<h5>Binary Search Trees:</h5> 
- All left children are less than the parent, all right values are greater than the parent <br>
<br>

<b>Ex: Give a range [low,high], return sum of all tree values within that range </b>
```python
  def rangeSumBST(self, root, low, high):
      if not root:
          return 0

      ans = 0
      if low <= root.val <= high: 
          ans += root.val
      if low < root.val:
          ans += self.rangeSumBST(root.left, low, high)
      if root.val < high:
          ans += self.rangeSumBST(root.right, low, high)

      return ans
```
<b>Ex: Check if its a valid binary search tree </b>
```python
  def isValidBST(self, root: Optional[TreeNode]) -> bool:
      def dfs(node, small, large):
          if not node:
              return True
          
          if not (small < node.val < large):
              return False

          left = dfs(node.left, small, node.val) #update the upper bound cuz left has to be smaller
          right = dfs(node.right, node.val, large) #update the lower bound cuz right has to be greater

          # tree is a BST if left and right subtrees are also BSTs
          return left and right

      return dfs(root, float("-inf"), float("inf"))
```
<br>

<h2>6. Graphs</h2> <br>
- Undirected (Bidirectional) vs Directed (Unidirectional)
- Usually represented by a dictionary where each key is node, values are its outgoing connections from each node
- Use a set "seen" to make sure node is only visited once (to prevent infinite loops in cyclical cases)

<center>
<img src = "/assets/graphs.png" width = '300' height = '200'>
</center><br>

<b>Input Type 1: Array of Edges</b> (pairs of edges)
- edges = [[0, 1], [1, 2], [2, 0], [2, 3]]
- each pair element in array represents an outgoing edge connection

```python
def build_graph(edges):
    graph = {}
    for x, y in edges:
        graph[x].append(y)
        # graph[y].append(x)
        # uncomment the above line if the graph is undirected
    
    return graph
```
<br>

<b>Input Type 2: Adjacency List</b> (index based)
- graph = [[1], [2], [0, 3], []]
- graph[i] = outgoing connections from node i
- 
<br><br>

<b>Input Type 3: Adjacency Matrix</b> (matrix form of array of edges)
- graph[i][j] = 1 if there is an outgoing connection from node i to node j
- i.e., if graph[node][i] = 1 then i is a neighbor to node 
- essentially the same as putting a 1 in the position of "array of edges" representation


<center>$$
\begin{bmatrix}
0 & 1 & 0 & 0 \\
0 & 0 & 1 & 0 \\
1 & 0 & 0 & 1 \\
0 & 0 & 0 & 0
\end{bmatrix}
$$</center>
<br><br>

<h5><b>DFS Graphs</b></h5> 
- Exploring each node's neighbors recursively one by one

<b>Return the total number of closed cycle loops</b>
- Init a set "seen" to prevent from revisiting nodes
- Internal logic: If node[i]'s neighbor has not seen yet, then mark as seen and recursively check the neighbors on all of its neighbors (this will handle all connections in a cycle as "seen")
- Iterate over all nodes and if something hasn't been seen yet, we know that's a new cycle

```python
def findCircleNum(self, isConnected: List[List[int]]) -> int:
    
  #internal logic: marks all neighbors in a province as seen
  def dfs(node): 
        for neighbor in graph[node]:
            if neighbor not in seen:
                seen.add(neighbor)
                dfs(neighbor)
    
    def dfs(start): #iteratively instead of recursively
        stack = [start]
        while stack:
            node = stack.pop()
            for neighbor in graph[node]:
                if neighbor not in seen:
                    seen.add(neighbor)
                    stack.append(neighbor)     
                  
                   
    # build the graph
    n = len(isConnected)
    graph = defaultdict(list)
    for i in range(n):
        for j in range(i + 1, n): 
        # instead of for j in i because if 1s are in the diagonal, 
        # that would just indicate a node connection to itself 
            if isConnected[i][j]:
                graph[i].append(j)
                graph[j].append(i)
    
    seen = set()
    ans = 0
    
    for i in range(n): #checks for new provinces
        if i not in seen:
            # add all nodes of a connected component to the set
            ans += 1
            seen.add(i)
            dfs(i)
    
    return ans
```
<br>

<b>Ex: Return the minimum number of swaps needed for a directed graph to make them all lead into one node</b><br>
- Indentify all edges pointing away from 0
- Start DFS starting from node 0 (meaning we will always be moving away from 0)
- Record the direction, if the original direction matches the DFS, then we need +1 swap (indicate moving towards)


```python
def minReorder(self, n: int, connections: List[List[int]]) -> int:
    roads = set()
    graph = defaultdict(list)
    for x, y in connections:
        graph[x].append(y)
        graph[y].append(x)
        roads.add((x, y))

    def dfs(node):
        ans = 0
        for neighbor in graph[node]:
            if neighbor not in seen:
                if (node, neighbor) in roads:
                    ans += 1
                seen.add(neighbor)
                ans += dfs(neighbor)
        
        return ans

    seen = {0}
    return dfs(0)

    #iterative version 
    ans = 0
    stack = [0]
    seen = {0}
    while stack:
        node = stack.pop()
        for neighbor in graph[node]:
            if neighbor not in seen:
                if (node, neighbor) in roads:
                    ans += 1
                seen.add(neighbor)
                stack.append(neighbor)
    
    return ans
```
<br>
<b>Ex: rooms[i] is all keys to other rooms that can be found in that room. Return true if one can visit all rooms</b>

```python
def canVisitAll(rooms):
  def dfs(node):
    for neighbor in rooms[node]:
      if neighbor not in seen:
        seen.add(neighbor)
        dfs(neighbor)

  seen = set()
  dfs(0)
  return len(seen) == len(rooms)

```
<br>
<b>Ex: Find islands</b><br>
<img src = "/assets/island.png" width = '300' height = '200'>

```python
def numIslands(self, grid: List[List[str]]) -> int:
    def valid(row, col):
        return 0 <= row < m and 0 <= col < n and grid[row][col] == "1"
    
    def dfs(row, col):
        for dx, dy in directions:
            next_row, next_col = row + dy, col + dx
            if valid(next_row, next_col) and (next_row, next_col) not in seen:
                seen.add((next_row, next_col))
                dfs(next_row, next_col)
    
    directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]
    seen = set()
    ans = 0
    m = len(grid)
    n = len(grid[0])
    for row in range(m):
        for col in range(n):
            if grid[row][col] == "1" and (row, col) not in seen:
                ans += 1
                seen.add((row, col))
                dfs(row, col)
    
    return ans
```
<br><br>

<h5><b>BFS Graphs</b></h5> (think of water ripples from a stone in pond) <br>
- Explores all possible neighbors from starting node (level 0)
- Better for finding <b>shortest path</b>
- With BFS, every time we visit a node, we must have arrived in the fewest possible steps
- Each "level" is the direct connection from the chosen node

<b>Ex: Find shortest path of 0's from (0,0) to (n,n)<//b>
```python
def shortestPathBinaryMatrix(self, grid):
    if grid[0][0] == 1:
        return -1
    
    def valid(row, col):
        return 0 <= row < n and 0 <= col < n and grid[row][col] == 0
    
    n = len(grid)
    seen = {(0, 0)}
    queue = deque([(0, 0, 1)]) # row, col, steps
    directions = [(0, 1), (1, 0), (1, 1), (-1, -1), (-1, 1), (1, -1), (0, -1), (-1, 0)]
    
    while queue:
        row, col, steps = queue.popleft()
        if (row, col) == (n - 1, n - 1): #shortest path is a diagonal
            return steps
        
        for dx, dy in directions:
            next_row, next_col = row + dy, col + dx
            if valid(next_row, next_col) and (next_row, next_col) not in seen:
                seen.add((next_row, next_col))
                queue.append((next_row, next_col, steps + 1))
    
    return -1
```
<br><br>

<b>Ex: Given the root of binary tree, target node, and integer k, return all nodes that are k distance from target</b>
from collections import deque

```python
def distanceK(self, root, target):
  # converts tree to undirected graph
    def dfs(node, parent): 
        if not node:
            return
        
        node.parent = parent
        dfs(node.left, node)
        dfs(node.right, node)
    
    dfs(root, None)
    queue = deque([target]) #stores node at each level
    seen = {target}
    distance = 0 #ensures queue is at the kth level
    
    while queue and distance < k:
        current_length = len(queue)
        for _ in range(current_length): #iterate over all nodes at current level
            node = queue.popleft()
            for neighbor in [node.left, node.right, node.parent]: #all neighbors of tree
                if neighbor and neighbor not in seen:
                    seen.add(neighbor)
                    queue.append(neighbor)
        
        distance += 1
    
    return [node.val for node in queue]
```
<br><br>

<b>Ex: Find distance from 0 for each cell (i.e., Return matrix of values where each cell is k distances away from 0<b>
- Start at all 0 nodes
- Set all direct neighbors = 1, neighbors of neighbors = 2, and so on

```python
def updateMatrix(self, mat):
    def valid(row, col): #check if in bounds and valid
        return 0 <= row < m and 0 <= col < n and mat[row][col] == 1
    
    m = len(mat)
    n = len(mat[0])
    queue = deque()
    seen = set()
    
    for row in range(m):
        for col in range(n):
            if mat[row][col] == 0:
                queue.append((row, col, 1))
                seen.add((row, col))
    
    directions = [(0, 1), (1, 0), (0, -1), (-1, 0)]

    while queue:
        row, col, steps = queue.popleft()
        
        for dx, dy in directions:
            next_row, next_col = row + dy, col + dx
            if (next_row, next_col) not in seen and valid(next_row, next_col):
                seen.add((next_row, next_col))
                queue.append((next_row, next_col, steps + 1))
                mat[next_row][next_col] = steps
    
    return mat
```
<br>

<h2>7. Heaps</h2> <br>
- Used for repeatedly finding max or min element
- Complete binary tree structure (all levels must be full except last) 

Min Heapify: <br>
1. Starts at the last nonleaf node
2. Take min of (child 1, child 2, parent)
3. Swap places with the min as the parent
4. Keep doing this until we reach the root node which should then contain the min value
<br>

<b>Ex: Stones[i] is the weight of i'th stone. Choose heaviest two stones x and y. If x == y, both stones removed. If x < y, put back a stone with weight y - x.  Return weight of the last remaining stone.
```python
import heapq #min to max, heapop pops the min

def lastStoneWeight(stones):
        stones = [-stone for stone in stones] #bc heapq only does min heaps, take the negative for the max heap
        heapq.heapify(stones) # turns an array into a heap in linear time
        while len(stones) > 1:
            first = abs(heapq.heappop(stones)) #pop heaviest stone
            second = abs(heapq.heappop(stones)) #pop second heaviest stone
            if first != second:
                heapq.heappush(stones, -abs(first - second)) #push back the difference

        return -stones[0] if stones else 0
```
<br>
<h5><b>Two Heaps</b></h5> <br>

- Good for finding the median <br>

<b>Ex: Find median </b>
- Max heap with lower half of data
- Min heap with upper half of data
- If even: Heappop average of both will return the median 
- If odd: Heappop element of larger array is the median
<br>
1. Push num onto the max heap (as mentioned above we arbitrarily chose the max heap).
2. Pop from the max heap, and push that element onto the min heap.
3. After step 2, if the min heap has more elements than the max heap, pop from the min heap and push the result onto the max heap.


```python
def __init__(self):
    self.min_heap = []
    self.max_heap = []

def addNum(self, num):
    heapq.heappush(self.max_heap, -num) #add num to max heap
    heapq.heappush(self.min_heap, -heapq.heappop(self.max_heap)) #pop from max heap and push to min heap
    if len(self.min_heap) > len(self.max_heap): #if odd
        heapq.heappush(self.max_heap, -heapq.heappop(self.min_heap)) #balances out

def findMedian(self):
    if len(self.max_heap) > len(self.min_heap): #the popped element of larger array is the median, otherwise it's the average
        return -self.max_heap[0]
    return (self.min_heap[0] - self.max_heap[0]) / 2
```
<br>

<h5><b>Top K</b></h5> <br>
- We want to find the "best" k elements of a collection
- Use heap to keep popping off the "worst" elements to keep the top K elements in answer array


```python
def topKFrequent(nums,k):
    counts = {}
    heap = []
    
    for key, val in counts.items():
        heapq.heappush(heap, (val, key))
        if len(heap) > k: #keep popping off worse elements
            heapq.heappop(heap)
    
    return [pair[1] for pair in heap]
```












<br><br>
<h2>Search</h2>
<h5>Binary Search</h5>





If we are asked to return the index of an element, rather than a for loop with O(n), we can do it in O(log(n)) using binary search. Divides each section in half recursively.


