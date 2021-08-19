
 ## No.1 【bubble sorting】
Bubble sorting is an entry-level algorithm, but there are also some interesting ways to play. Generally speaking, bubble sorting can be written in three ways:
### The basic method  
Compare and swap back in pairs to bubble the maximum / minimum value to the last position.
```python
def basic_bubble(nums):  
	nums_len = len(nums)  
	circle_times = 0  
	exchange_times = 0  
	for i in range(0, nums_len):  
	    for j in range(0, nums_len - 1 - i):  
	        if nums[j] > nums[j + 1]:  
	            nums[j], nums[j + 1] = nums[j + 1], nums[j]  
	            exchange_times = exchange_times + 1  
	            circle_times = circle_times + 1  
	print('in the basic bubble, circle_times is %d' % circle_times)  
	print('in the basic bubble, exchange_times is %d' % exchange_times)
```
Each time the for loop of the outermost layer passes through a round, the maximum value in the remaining numbers will be moved to the last bit of the current round, 
and some adjacent numbers will be exchanged and become orderly in the middle. The total number of comparisons is (n-1) + (n-2) + (n-3) +... + 1 (n − 1) + (n − 2) + (n − 3) +
... + 1.   

### optimization method  
In the basic method, the times of comparisons is (n-1) + (n-2) + (n-3) +... + 1 (n − 1) + (n − 2) + (n − 3) +... + 1. 
Of course, we can optimize it. We use a variable to record in the current circle whether the exchange happens. If the exchange does not happen, 
it mean that the nums has been in order and the sorting does not be needed any more.
```python
def basic_bubble_optimize(nums):  
	nums_len = len(nums)  
	exchange_flag = True  
	circle_times = 0  
	exchange_times = 0  
	for i in range(0, nums_len):  
	    for j in range(0, nums_len - 1 - i):  
	        if nums[j] > nums[j + 1]:  
	            nums[j], nums[j + 1] = nums[j + 1], nums[j]  
	            exchange_times = exchange_times + 1  
			    exchange_flag = True  
			    circle_times = circle_times + 1  
		if not exchange_flag:  
		   break  
		exchange_flag = False  
  
	print('in the optimized bubble, circle_times is %d' % circle_times)  
	print('in the optimized bubble, exchange_times is %d' % exchange_times)
```
So, in one circle ,there exchange does not happen,it means that all the rest numbers have been in order.  

### optimization method again  
In addition to using variables to record whether the current round has been exchanged, another variable is used to record the position of the last exchange. 
When the next round of sorting reaches the position of the last exchange, the comparison will be stopped.
```python
def basic_bubble_optimize_2(nums):  
	nums_len = len(nums)  
	exchange_flag = True  
	last_swap_index = nums_len - 1  
	swap_index = -1  
	circle_times = 0  
	exchange_times = 0  
	for i in range(0, nums_len):  
	    if not exchange_flag:  
	        break  
	    exchange_flag = False  
	    for j in range(0, last_swap_index):  
	        if nums[j] > nums[j + 1]:  
	            nums[j], nums[j + 1] = nums[j + 1], nums[j]  
	            exchange_times = exchange_times + 1  
	            swap_index = j  
	            exchange_flag = True  
	            circle_times = circle_times + 1  
	  last_swap_index = swap_index  
	print('in the optimized_2 bubble, circle_times is %d' % circle_times)  
	print('in the optimized_2 bubble, exchange_times is %d' % exchange_times)
```
We use last_swap_index  to record the last exchange position, then in the next loop, we do not need to circle to nums_len-1-i,
we just need to circle to last_swap_index. Thus, we can reduce the execution times.  

### About the time complexity and space complexity of bubble sorting   
From the above, whatever basic method or optimized method, the comparsion times should be (n-1) + (n-2) + (n-3) +... + 1 (n − 1) + (n − 2) + (n − 3) +... + 1(although some optimizied algorithm should improve a little). The time compexity if o(n*n). and space complexity is o(1)(we only use two-four variable to finish the algorithm and whatever the n.                                                            

## No.2 【Selection Sort】
Selection Sorting means that double loop traverses the array. After each round of comparison, find the subscript of the smallest element and exchange it to the first place.
### Basic method  
Double loop traverses the array. After each round of comparison, find the subscript of the smallest element and exchange it to the first place.
```python
def selection_basic_sort(nums):  
	nums_len = len(nums)  
	minIndex = 0  
	circle_times = 0  
	exchange_times = 0  
	for i in range(0, nums_len):  
	    minIndex = i  
	    for j in range(i + 1, nums_len):  
	        if nums[j] < nums[minIndex]:  
	            minIndex = j  
	        circle_times = circle_times + 1  
	    nums[i], nums[minIndex] = nums[minIndex], nums[i]  
	    exchange_times = exchange_times + 1  
	print('in the selection_basic_sort, circle_times is %d' % circle_times)  
	print('in the selection_basic_sort, exchange_times is %d' % exchange_times)
```
The code circle from the beginning to the end of the array, if found that some elements are smaller than the current max value,update the minvalue. 
every circle ends, exchange the minIndex value and the beginning of the array. Everytime ,we get the min value of the nums[i+1:end]. After i is from the begining to the end, 
the array is sorted.  

### optimization method  
Because every circle from i+1:end, we get the min value, of course ,we can get the max value,too, we can put the maxvalue to the nums[i],the max value to the 
nums[nums_len-1-i],then, one circle we can deal with two elements.So in the outside circle, we only need to circle the half length(of course ,in the inside circle ,
we have to deal the scope:[i+1:nums_len-i].
```python
def selection_sort_optimize(nums):  
	nums_len = int(len(nums)/2)  
	circle_times = 0  
	exchange_times = 0  
	for i in range(0, nums_len):  
	    minIndex = i  
	    maxIndex = i  
	    for j in range(i + 1, len(nums) - i):  
	        if nums[j] < nums[minIndex]:  
	            minIndex = j  
	        if nums[j] > nums[maxIndex]:  
	            maxIndex = j  
	        circle_times = circle_times + 1  
	   if minIndex == maxIndex:  
	        break  
	   nums[i], nums[minIndex] = nums[minIndex], nums[i]  
	   if maxIndex == i:  
	       maxIndex = minIndex  
	   nums[len(nums) - 1 - i], nums[maxIndex] = nums[maxIndex], nums[len(nums) - 1 - i]  
	   exchange_times = exchange_times + 1  
	print('in the selection_sort_optimize, circle_times is %d' % circle_times)  
	print('in the selection_sort_optimize, exchange_times is %d' % exchange_times)
```
## No.3 【Insert Sort】
In each step, a data to be sorted is inserted into the previously ordered sequence until all elements are inserted.
### basic method  
In the process of inserting new numbers, keep exchanging with the previous numbers until you find your proper position.
```python
def insert_sort(nums):  
	nums_len = len(nums)  
	circle_times = 0  
	exchange_times = 0  
	for i in range(1, nums_len):  
        j = i  
        while j >= 1 and nums[j] < nums[j - 1]:  
            nums[j], nums[j - 1] = nums[j - 1], nums[j]  
            exchange_times = exchange_times + 1  
            j = j - 1  
            circle_times = circle_times + 1   
	print('in the insert_sort, circle_times is %d' % circle_times)  
	print('in the insert_sort, exchange_times is %d' % exchange_times)
```
First, we begin from inde 1(becuase only one number should be sorted) to the end, every time we get the i index, we will from i back to the beginning of the array, 
if we find that the back number is smaller than the previous number, we exchange them, so from the beginning, every time we get the smallest value, second smalles value , 
third smallest value..... At last , the whole array is sorted with ascending order.  

### optimization method  
From the basic exchange model, we can get to know that every time we will exchange the two near value only if the back number is smaller than the previous number, 
actually, many exchanges are waste,becasue in some situation, the back number is maybe smaller than the previous' previous number ,even smaller than the previous'previous'
previous' number, so we only remember the positon and move the front number to the end one by one in this situation .
```python
def insert_sort_optimize(nums):  
	nums_len = len(nums)  
	circle_times = 0  
	exchange_times = 0  
	for i in range(1, nums_len):  
	    current_value = nums[i]  
	    j = i  
	    while j >= 1 and current_value < nums[j - 1]:  
	        nums[j] = nums[j - 1]  
	        j = j - 1  
	        circle_times = circle_times + 1  
        nums[j] = current_value  	  
	print('in the insert_sort, circle_times is %d' % circle_times)  
	print('in the insert_sort_optimize, exchange_times is %d' % exchange_times)
```
## No.4 【The comparsion】
We add the simple counters in function.one is the circle run times, the other is the exchange run times. take the nums=[1,2,5,8,10,3,7,4,6,9].
we run all the function, get the results:
```
in the basic bubble, circle_times is 45
in the basic bubble, exchange_times is 13

in the optimized bubble, circle_times is 35
in the optimized bubble, exchange_times is 13

in the optimized_2 bubble, circle_times is 31
in the optimized_2 bubble, exchange_times is 13

in the selection_basic_sort, circle_times is 45
in the selection_basic_sort, exchange_times is 10

in the selection_sort_optimize, circle_times is 25
in the selection_sort_optimize, exchange_times is 5

in the insert_sort, circle_times is 13
in the insert_sort, exchange_times is 13

in the insert_sort, circle_times is 13
in the insert_sort_optimize, exchange_times is 0
```
Of course, the run times is definitely related with the input array.However,generally speaking, From the output, we can get some useful information about above 
seven algorithm.

## No.5 【The conclusion】 
### Bubble sorting
There are two optimization methods for bubble sorting:
1)Record whether the exchange has occurred in the current round. If no exchange has occurred, it means that the array has been ordered;
2)
Record the position where the last exchange occurred. Only this position will be compared in the next round of sorting.

### Select sort
Selection sorting can evolve into binary selection sorting:
Binary selection sorting: select two values - maximum value and minimum value in one traversal;

### Insert sort
Insert sort can be written in two ways:
1)Exchange method: new numbers find their proper position through continuous exchange;
2)Moving method: the old number keeps moving backward until the new number finds the right position.

### The same points of these algorithms:
All these algorithm, their time complexity is O (n ^ 2) and theire spatial complexity is O (1) and every algorithm Both require a double cycle.

### The differences of these algorithms:
Among the three sorting algorithms, the number of sorting exchange is the least(we can get this conclusion from the output above)
When the array is almost ordered, the time complexity of insertion sorting is close to the linear level
```

