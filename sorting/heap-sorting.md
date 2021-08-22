# heap sorting algorithm
Heap sort is a sort algorithm designed by using the data structure of heap. Heap is a structure similar to a complete binary tree and satisfies the nature of heap: that is, the key value or index of a child node is always less than (or greater than) its parent node.
In order to sort from small to large, it is necessary to establish a large top heap, that is, the parent node is larger than the child node.
There are some dynamic diagram online to illustrate the whole process of heap sorting.

## No.1 【algorithm】
The algorithm process includes:
1. Firstly, create a large top heap according to the array.
Attention: a large top heap is a complete binary tree which every node's value is bigger than its left son and right son. From the reciprocal to the root, in every node, we search its child node and if the value of child node is bigger than current node's value ,than exchange it. Through the penultimate  floor to the root, the construction of the large top heap is finished. 
From the algorithm above, we can draw a conclusion: after the operation above is finished,the whole complete binary tree is a large top heap: every node's value is bigger than its children.  
2. Now, as soon as the large top heap is finished, the biggest value of the arry node is the root node, then, exchange the root node with the last index element.----Now, We get the biggest value of the array.
Now ,because we have exchanged the root and the last index of the array, so , the rest of the array is not a large top heap anymore, thus ,we should make the rest of data a large top heap again.  
3. Because we only change the root node, so we begin to check whether root node's value is bigger than its child,if small, then exchange, so we need to deal with the child'child if after exchanging ...., at last, the rest of data structure becomes a large top heap again, so exchange the root value and the last index element again....
 
## No.2 【Dynamic diagram】
From someone's website, the dynamic diagram is:

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190613001742222.gif)

## No.3 【Code】
```python
def initial_heap(nums, length):  
    i = length // 2 - 1  
    return_times = 0  
    circle_times = 0  
    exchange_times = 0  
    while i >= 0:
        # from the reciprocal to the root, be careful ,the process should be downhill to uphill, otherwise, 
        # after the processing ,the data structure may not be a large top heap.
        return_times = heap_deal_root(nums, i, length)  
        circle_times = circle_times + return_times[0]  
        exchange_times = exchange_times + return_times[1]  
        i = i - 1  
    return (circle_times,exchange_times)

def heap_deal_root(nums, index, length):  
	circle_times = 0  
	exchange_times = 0  
	parent = index  
	child = 2 * parent + 1 
	# From child to the last one , exchange value if needed. 
	while child < length:  
	    if child + 1 < length and nums[child] < nums[child + 1]:  
	        child = child + 1  
	    if nums[parent] < nums[child]:  
	        nums[parent], nums[child] = nums[child], nums[parent]  
	        exchange_times = exchange_times + 1  
	        parent = child  
	        child = 2 * child + 1  
        circle_times = circle_times + 1  
    return (circle_times, exchange_times)

def heap_sort(nums):  
    nums_len = len(nums)  
    circle_times = 0  
    exchange_times = 0  
    # initial big heap  
    return_times = initial_heap(nums, nums_len)  
    circle_times = return_times[0]  
    exchange_times = return_times[1]
    length = nums_len - 1  
    while length > 0:  
        # the root number is exchanged with the last number  
        nums[0], nums[length] = nums[length], nums[0] 
        # From the last index to the front index one by one. 
        return_times = heap_deal_root(nums, 0, length)  
        length = length - 1  
        circle_times = circle_times + return_times[0]  
        exchange_times = exchange_times + return_times[1]    
    print('in the heap_sort, circle_times is %d' % circle_times)  
    print('in the heap_sort, exchange_times is %d' % exchange_times)
```
## No.4 【Performance Analysis】
nums = [91,60,96,13,35,65,46,65,10,30,20,31,77,81,22]  
in the basic bubble, circle_times is 105(~~n*n/2)  
in the basic bubble, exchange_times is 60  

in the optimized bubble, circle_times is 102(~~n*n/2)  
in the optimized bubble, exchange_times is 60  

in the optimized_2 bubble, circle_times is 102(~~n*n/2)  
in the optimized_2 bubble, exchange_times is 60  

in the selection_basic_sort, circle_times is 105(~~n*n/2)  
in the selection_basic_sort, exchange_times is 15  

in the selection_sort_optimize, circle_times is 56(~~n*n/2/2)  
in the selection_sort_optimize, exchange_times is 14  

in the insert_sort, circle_times is 74  
in the insert_sort, exchange_times is 60  

in the insert_sort, circle_times is 74  
in the insert_sort_optimize, exchange_times is 60  

in the hill_sort, circle_times is 77  
in the hill_sort, exchange_times is 33  

in the hill_sort_optimize, circle_times is 57  
in the hill_sort_optimize, exchange_times is 23  

in the heap_sort, circle_times is 28  
in the heap_sort, exchange_times is 25  

in the heap_sort_2, circle_times is 98  
in the heap_sort_2, exchange_times is 45  

From the result above ,we can see the efficiency of the heap sort algorithm.

## No.4 【time complexity and space complexity】
Heap sorting is divided into two stages: initial heap (buildmaxheap) and rebuild heap (maxheap). Therefore, the time complexity should be analyzed from these two aspects.
According to the mathematical operation, it can be deduced that the time complexity of initialization heap building is O(n), and the time complexity of reconstruction heap is O(nlogn), so the total time complexity of heap sorting is O(nlogn). The derivation process is complex, so the proof process is no longer given.    
The spatial complexity of heap sorting is O (1), and only constant level temporary variables are required
