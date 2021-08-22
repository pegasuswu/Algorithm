# quick sorting algorithm
The quick sort algorithm realizes sorting through multiple comparisons and exchanges. The sorting process is as follows: 
(1) First, set a boundary value, and divide the array into left and right parts through the boundary value.  
(2) Collect data greater than or equal to the boundary value to the right of the array, and data less than the boundary value to the left of the array. At this time, all elements in the left part are less than or equal to the boundary value, while all elements in the right part are greater than or equal to the boundary value.  
(3) Then, the data on the left and right can be sorted independently. For the array data on the left, you can take another boundary value and divide this part of the data into left and right parts. Similarly, place the smaller value on the left and the larger value on the right. The array data on the right can also be processed similarly.  
(4) By repeating the above process, we can see that this is a recursive definition. After the left part is sorted recursively, the right part is sorted recursively. When the sorting of the data in the left and right parts is completed, the sorting of the whole array is completed.  

## 【Code】
From the analysis above, the code is simple:
```python
1. code - one
def quick_sort(nums):  
    nums_len = len(nums)  
    circle_times = 0  
    if nums_len >= 2:  
        # select the base number random  
        base_index = random.randint(0, nums_len - 1)  
        base_value = nums[base_index]  
        left, right = [], []  
        nums.remove(base_value)  
        for x in nums:  
            if x < base_value:  
                left.append(x)  
            else:  
                right.append(x)  
         circle_times = circle_times + 1  
         return (quick_sort(left)[0] + [base_value] + quick_sort(right)[0], circle_times)  
    else:  
        return (nums, circle_times)

2. code - two 
def quick_sort_get_index(nums, left, right):  
    base_value = nums[left]  
    circle_time = 0  
    exchange_times = 0  
    while left < right:  
        while left < right and nums[right] >= base_value:  
            right -= 1  
            circle_time = circle_time + 1  
  
        nums[left] = nums[right]  
        while left < right and nums[left] <= base_value:  
            left += 1  
            circle_time = circle_time + 1  
  
        nums[right] = nums[left]  
        exchange_times = exchange_times + 2  
        nums[left] = base_value  
    return (left, (circle_time, exchange_times))  
  
def quick_sort_2(nums, left, right):  
    circle_times = 0  
    exchange_times = 0  
    if left < right:  
        return_x = quick_sort_get_index(nums, left, right)  
        index = return_x[0]  
        circle_times = circle_times + return_x[1][0]  
        exchange_times = exchange_times + return_x[1][1]  
        # recurse the left array and right array
        quick_sort_2(nums, left, index - 1)  
        quick_sort_2(nums, index + 1, right)  
    return (circle_times, exchange_times)

nums = [91,60,96,13,35,65,46,65,10,30,20,31,77,81,22]
return_x = quick_sort_2(nums, 0, len(nums) - 1)  
print('in the fast sort_2 algorithm, circle_times is %d' % return_x[0])  
print('in the fast sort_2 algorithm, the exchange times  is %d' % return_x[1])  
print(nums)
```
## 【time complexity and spatial comlexity】
The time complexity of quick sort has been mentioned above. The average time complexity is O (nlogn), and the worst time complexity is O (n ^ 2), the spatial complexity is related to the number of layers of recursion. Each layer of recursion will generate some temporary variables, so the spatial complexity is O (logn) ~ o (n), and the average spatial complexity is O (logn).
