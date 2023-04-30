# Problem Set 2

## Problem 1

(a) the procedure is given in the form of the pseudocode as follows:

```
Reverse(head):
	x=head
	y=x.next
	while(y!=NULL):
		temp=y.next
		y.next=x
		x=y
		y=temp
```

(b)

(i) 

Information needed to access the head of the list: 

​			the address of the head of the list.

Implement: 

​			using the address to access *x.np* of the head, knowing that *x.prev*=NULL, use NULL (0) to XOR *x.np*, we have *x.next* (i.e. the address of the second node, y). Using *y.np* XOR *y.prev* (the address of x given), we then have *y.next* ...... the whole doubly linked list can be implemented.

pseudocode:

```
Insert(x,i):
	nod=new node
	nod.value=x
	prev=&head        	# the address of prev
    next=head.np XOR 0 		# the address of the next
    if(i==1)
    	nod.np=0 XOR prev
    	prev.np=&nod XOR next
    else if(i==2)
    	nod.np=prev XOR next
    	prev.np=0 XOR &nod
    	next.np=&nod XOR (next.np XOR prev)
    else
        num=2
          	while(num<i): 	# stop when next point at the ith node
                temp=next
                next=next.np XOR prev
                prev=temp
                num++          
        nod.np=prev XOR next
        pprev=prev.np XOR next
        prev.np=pprev XOR &nod		#update the np of the prev
        if(i!=list.lenth)
        	nnext=next.np XOR prev
        	next.np=&nod XOR nnext 		#update the np of the next

```



```
Delete(i):
	prev=&head        	# the address of prev
    next=head.np XOR 0 		# the address of the next 	
    if(i==1)
    	next.np=0 XOR (next.np XOR prev)
    else
    	num=2
		while(num<i): 	# stop when next point at the ith node
			temp=next
			next=next.np XOR prev
			prev=temp
			num++ 
		nnext=prev XOR next.np
    	head.np=0 XOR nnext
    	if(i!=list.lenth)
    		nnext.np=prev XOR (next XOR nnext.np)
```



## Problem 2

overview: the MAXSTACK consists of two stacks, s stores data and smax stores the max ones. When push x in s, if x is larger than smax[top] , also push x in smax, which ensures the top of smax stays the max. Also, when popping, if the popped one in s is also at the top of smax, pop it at the same time. When invoke max(), return the top of smax.   

```
stack s,smax

Push(x):
	s.push(x)
	if(size(smax)==0 or smax[smax.top]<=x)
		smax.push(x)
Pop():
	num=s.pop()
	if(num==smax[smax.top])
		smax.pop()
	
Max():
	return smax[smax.top]
```

Space complexity: assume s costs O(n), we know that size(smax)<=s, the total cost won't be more than double of s costs. So the total space complexity is O(n). 



## Problem 3

Overview: if scanner get an operand or a'!', push it into string immediately. If scanner get an else operator, when it is a 'x' , scan the following operator, when it is a '!', push it before the 'x', else, push the 'x'. When scanner get a '+', loop to find a next '+', anything before the following '+' are pushed in the rule. See the block before the following '+' as an operand, push it after the previous operand, then push the '+'    

```
str s=""
part_Convert(str,s):		# when token!='+'				#	O(1) to O(n)
	while((token=NextToken(str))!=NULL or '+')
		if(token is an operand or token=='!')
        	s+=token
        else 	#	token=='x'
        	s+=NextToken(str)
        	if((token1=NextToken(str.copy()))=='!') # token1 won't always affect main loop
        		s=s+NextToken(str)+token  # same as s=s+token1+token
        	else 
        		s+=token
    return s
Convert(str):												#	O(n)
	while((token=NextToken(str))!=NULL)
			s=part_Convert(str,s)
			if(token=NextToken(str)==NULL)
				break
			else
				s=s+part_Convert(str,s)+'+'
	return s
        	
```

though there are loop-in-loop, but all the loops use the same string position, which means after the invoke, the string has only been gone through once. So the total time complexity won't beyond O(n)



## Problem 4

Algorithm A :

![](/home/dxh/sophomore/数据结构与算法/微信图片_20210915180248.jpg)

Algorithm B:

![](/home/dxh/sophomore/数据结构与算法/微信图片_20210915181041.jpg)

Algorithm C:

![](/home/dxh/sophomore/数据结构与算法/微信图片_20210915181636.jpg)

Choice: I will choose Algorithm A, because it has the smallest time complexity :
$$
n^{\lg5}<n^{\lg8}=n^3<2^n
$$
while it has middle space complexity (better than Algorithm C, worse than B).

## Problem 5

Overview:

 First, merge sort the array(in time *O(n log n)* ). Then,divide the array into subarrays which contains only the same number( in time *O(n)*). Pop the redundant numbers in each array (in time *O(n)*). Finally, combine them into one array(in time *O(n)*).

Pseudocode:

```
RemoveDuplicates(A[1,...n]):
MergeSort(A)
new list B[n]
int k=0
for i 0->n:
	divide(A[i...j]) into B[k]
	k++
for i 0->sizeof(B):
	combine(B[i][0])

```

Correctness:

(i) all loops in the algorithm will terminate in at most n times (n is finite)

(ii) Merge sort is correct without my argument. Given that all arrays are cut out from sorted list A, items in them are different. So the result can be guaranteed. 

Running time:
$$
T(n)=O(n\lg n)+O(n)+O(n)+O(n)=O(n\lg n)
$$

## Problem 6

(a) 

​	(8,6), (8,1), (6,1)

(b)

The larger the number of inversions (N), the more running time of insertion sort.

Proof is a little beyond me...

(c) Pseudocode of the algorithm:

```
CountInversions(A[1,...,n]):
if(n==1)
	counter=0
else
	solLeft=CountInversions(A[1,...,n/2])
	solRight=CountInversions(A[n/2+1,...,n])
	counter+=compare(solLeft,solRight)   #in merge, if item in left is smaller, counter++
	sol=merge(solLeft,solR)
return counter
```

