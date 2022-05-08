## Two Sum

#### Approach 1: Brute Force

The brute force approach is simple. Loop through each element x*x* and find if there is another value that equals to target - x

```python
# Approach 1: Brute Force
# Time complexity:O(n^2) Space complexity O(1)
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if(nums[i]+nums[j]==target):
                    return [i,j]
```



#### Approach 2: Two-pass Hash Table

To improve our runtime complexity, we need a more efficient way to check if the complement exists in the array. If the complement exists, we need to get its index.**What is the best way to maintain a mapping of each element in the array to its index? A hash table.**

##### **What is a Hash table or a Hashmap in Python?**

In computer science, a Hash table or a Hashmap is a type of data structure that maps keys to its value pairs (implement abstract array data types). It basically makes use of a function that computes an index value that in turn holds the elements to be searched, inserted, removed, etc. This makes it easy and fast to access data. **In general, hash tables store key-value pairs and the key is generated using a hash function.**

Hash tables or hash maps in Python are implemented through the built-in dictionary data type. The keys of a dictionary in Python are generated by a hashing function. The elements of a dictionary are not ordered and they can be changed.

```python
# Approach 2: Harh Map: reduce loop into search
# Time complexity: O(n)  Space complexity: O(n)
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i in range(len(nums)):
            hashmap[nums[i]] = i
        for i in range(len(nums)):
            complement = target - nums[i]
            if complement in hashmap and i!=hashmap[complement]:
                return [i,hashmap[complement]]
```



#### Approach 3: One-pass Hash Table

It turns out we can do it in one-pass. While we are iterating and inserting elements into the hash table, we also look back to check if current element's complement already exists in the hash table.

```python
# Approach 3: One-pass HarhMap: Search while inserting
# Time complexity: O(n)  Space complexity: O(n)
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i in range(len(nums)):
            complement = target - nums[i]
            if complement in hashmap and i != hashmap[complement]:
                return [i, hashmap[complement]]
            hashmap[nums[i]] = i
```