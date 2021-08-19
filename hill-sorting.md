# hill sorting algorithm
## Introduction
Hill sorting is a sort algorithm proposed by Donald shell in 1959. Hill sort is also an insertion sort. It is a more efficient version of simple insertion sort after improvement, also known as reduced incremental sort. At the same time, this algorithm is one of the first algorithms to break through O (N2). In this paper, the basic idea and code implementation of hill sorting will be introduced in detail.

Simple insertion sorting is very orderly. No matter how the array is distributed, elements are still compared, moved and inserted step by step. For example, in the reverse sequence of [5,4,3,2,1,0], it is very difficult for the 0 at the end of the array to return to the first position. It takes n-1 times to compare and move elements. Hill sort adopts the skip grouping strategy in the array, divides the array elements into several groups through a certain increment, then groups them for insertion sorting, then gradually reduce the increment, and continue to insert sorting by group until the increment is 1. Hill sort uses this strategy to make the whole array basically orderly in the initial stage, with the small one in the front and the large one in the back. Then reduce the increment to 1. In fact, in most cases, it only needs to be fine tuned without too much data movement.

Let's look at the basic steps of hill sorting. Here, we select the increment gap = length / 2, reduce the increment and continue to use gap = gap / 2. This incremental selection can be represented by a sequence, {n / 2, (n / 2) / 2... 1}, which is called the incremental sequence. The selection and proof of the incremental sequence of hill sorting is a mathematical problem. The incremental sequence we choose is commonly used and is also the increment suggested by hill, which is called Hill increment, but in fact, this incremental sequence is not optimal. Here we use hill increment as an example.

## Basic code 
According to the hill sorting algorithm, the code:
```python
def insert_sort_optimize_func(nums, begin, subarray_len, interval):  
	circle_times = 0  
	exchange_times = 0  
	for i in range(0, subarray_len):  
	    current_value = nums[begin + i*interval]  
	    j = begin + i*interval  
	    while j >= interval and current_value < nums[j - interval]:  
	        nums[j] = nums[j - interval]  
	        j = j - interval  
	        exchange_times = exchange_times + 1  
	        nums[j] = current_value  
	    circle_times = circle_times + 1  
	return (circle_times, exchange_times)

def hill_sort(nums):  
	nums_len = len(nums)  
	sequence = []  
	k = int(nums_len / 2)  
	while k >= 1:  
	    sequence.append(k)  
	    k = int(k / 2)  
	k_index = - 1  
	circle_times = 0  
	exchange_times = 0  
	for k_index in range(0, len(sequence)):  
	    sub_array_len = int(nums_len / sequence[k_index])  
	    for i in range(0, sequence[k_index]):  
	        return_times = insert_sort_optimize_func(nums, i, sub_array_len, sequence[k_index])  
	        circle_times = circle_times + return_times[0]  
	        exchange_times = exchange_times + return_times[1]  
	  
	print('in the hill_sort, circle_times is %d' % circle_times)  
	print('in the hill_sort, exchange_times is %d' % exchange_times)
```
In fact, this code can be optimized. Our current processing method is: after processing a group of interval sequences, we come back to process the next group of interval sequences, which is very consistent with human thinking. But for the computer, it prefers to start with the gap element and insert each element forward into its own group in order. Although this process seems to jump in different interval sequences, from the perspective of the computer, it is accessing a continuous array. Here is the Code:
## optimization code
```python
def hill_sort_optimize(nums):  
    nums_len = len(nums)  
    gap = int(len(nums)/2)  
    circle_times = 0  
    exchange_times = 0  
    while gap > 0:  
        for i in range(gap, nums_len):  
            #currentNumber store current value  
            currentNumber = nums[i]    
            preIndex = i - gap  
            while preIndex >= 0 and currentNumber < nums[preIndex]:  
                # move to the back position  
                nums[preIndex + gap] = nums[preIndex]  
                preIndex = preIndex - gap  
                exchange_times = exchange_times + 1  
                # currentNumber find own position
            circle_times = circle_times + 1  
            nums[preIndex + gap] = currentNumber  
        gap = int(gap / 2)  
    print('in the hill_sort_optimize, circle_times is %d' % circle_times)  
	  print('in the hill_sort_optimize, exchange_times is %d' % exchange_times)
```
```
in the hill_sort, circle_times is 30
in the hill_sort, exchange_times is 19

in the hill_sort_optimize, circle_times is 22
in the hill_sort_optimize, exchange_times is 19
```
## time comlexity and space comlexity
The time complexity of Hill sort is very difficult to analyze, and its average complexity ranges from O (n)  to o (n ^ 2). It is generally believed that its best time complexity is O (n ^ {1.3}).
Actually, because we have more fast sorting algorithm, so in the real work, we seldom use the hill sorting method. However, as a sorting algorithm which time complexitiy is from O(n^ 2) to O(nlogn), hill sorting algorithm is very traditional.
