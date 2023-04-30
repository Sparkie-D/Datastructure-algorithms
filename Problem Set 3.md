#  Problem Set 3

### Problem 1

(a)

guess that T(n)=$dn\lg n+d'n\in \Omega(n\lg n)$ 

proof:

​	Induction basis:	$T(1)=c\ge d'$ is satisfiable.

​	Inductive step:	   

​		$T(n)=2T(\frac{n}{2})+n=2d\frac{n}{2}\lg \frac{n}{2}+d'n+n=dn\lg\frac{n}{2}+(d'+1)n$

​											$=dn\lg n+(d'-d+1)n\ge dn\lg n+d'n$ 

​		It is satisfiable only if $d'-d+1\ge d'$ ,that is $d\le 1$. 

(b)

![](/media/dxh/共享文件夹/sophomore/算法/作业/微信图片_20210920183437.jpg)

guess that $T(n)=dn(\frac{3}{2})^\frac{n}{2}-d'n$

proof: 

​		Induction basis:	$T(1)=1<\frac{\sqrt{6}}{2}d-d'$ is satisfiable.

​		Induction step:	

​				$T(n)=T(n-2)+T(\frac{n}{2})+n=d(n-2)(\frac{3}{2})^\frac{n-1}{2}-d'(n-2)+d\frac{n}{2}(\frac{3}{2})^\frac{n}{4}-d'\frac{n}{2}+n$

​			   			$=\frac{2}{3}dn(\frac{3}{2})^\frac{n}{2}-\frac{4}{3}(\frac{3}{2})^\frac{n}{2}-d'n+2d'+\frac{1}{2}dn(\frac{3}{2})^\frac{n}{4}-\frac{1}{2}d'n+n$

 						  $=(\frac{3}{2}dn-\frac{3}{4}+\frac{1}{2}dn(\frac{\sqrt{6}}{3})^\frac{n}{2})(\frac{3}{2})^\frac{n}{2}-(\frac{3}{2}d'-1)n+2d'$

​	   					$\le dn(\frac{3}{2})^\frac{n}{2}-d'n$

Knowing that $2d'$ and $\frac{1}{2}dn(\frac{\sqrt{6}}{3})^\frac{n}{2}$ is small enough for the rest of the formula, to prove the last part, we need :

​		$\frac{2}{3}dn-\frac{3}{4}\le 1$ ->$$

​		$\frac{3}{2}d'-1\ge1$



### Problem 2

(a)

![](/media/dxh/共享文件夹/sophomore/算法/作业//微信图片_20210920195812.jpg)

$\therefore T(n)=(1+\frac{n}{\alpha})cn-c\alpha(1+2+..+\frac{n}{\alpha})=\frac{cn^2}{2\alpha}+\frac{cn}{2}$

(b)



### ![](/media/dxh/共享文件夹/sophomore/算法/作业//微信图片_20210920201136.jpg)

longest path shall be one of the sides.

$\alpha^kcn=1\rightarrow k=\log_\alpha \frac{1}{cn},T(n)=cnk=cn\log_\alpha \frac{1}{cn}, \quad 0.5<\alpha<1$

$(1-\alpha)^k cn=1\rightarrow k=\log_{1-\alpha} \frac{1}{cn},T(n)=cnk=cn\log_{1-\alpha} \frac{1}{cn},\quad 0<\alpha\le 0.5$

### Problem 3

Overview: 

​		Divide the n-digit number N into two $\frac{n}{2}$-digit number a,b,$N=a\times2^\frac{n}{2}+b$. 

​		So $N^2=(a\times2^\frac{n}{2}+b)(a\times2^\frac{n}{2}+b)=a^2\times2^n+ab\times2^{\frac{n}{2}+1}+b^2$ 

​		The part$\times2^i$ can be done by shifting in time $O(1)$, 

​		All works:$T(n)=3T(\frac{n}{2})+f(n)$. $f(n)$ is time cost on combining the three parts.

Pseudocode:

```
multiple(numA,numB): //digit of A and B are same.
if(numA,numB are 1-digit)
	return numA*numB
int dig=numA's digit
int a,b = numA's high/low dig/2 digit.
if(numA==numB)
	return  multiple(a,a)<<2*digb + 2*multiple(a,b)<<digb + multiple(b,b)
else 
	int c,d= numB's high/low dig/2 digit.
	res1=multiple(a,c)
	res2=multiple(a+b,c+d)
	res3=multiple(b,d)
	return res1<<dig + (res2-res1-res2)<<(dig/2) + res2 
```

Runtime:

![](/media/dxh/共享文件夹/sophomore/数据结构与算法/微信图片_20210920212945.jpg)

### Problem 4

```
Search(A,x):
int GREAT_NUM=the largest reachable number
int head=0,tail=GREAT_NUM
int middle=(head+tail)/2
while(true)
	switch
		case(x<A[head])		//x too small
		case(A[head]==A[tail] and head!=tail)	//reach infinity
		case(head==tail and A[head]!=x)		//search fail
			return false
		case(x<=A[tail])			//binary search
			if(x<A[middle])
				tail=middle
			else if(x>A[middle])
				head=middle
			else 
				return middle
			continue
		case(x>A[middle])		//change range
			Search(A[GREAT_NUM:],x)	//copy of A except first GREAT_NUM items 
```

if x exists, the algorithm could locate its position range in time $O(1)$---constant times of comparison. When located the range, search x using binary search takes time $O(\lg n)$, total cost is $T(n)=O(\lg n)$

### Problem 5

Algorithm : 

1. First randomly pick one delegate. 

2. Watch him(her) introduce to all the delegates. 

3.  push those who smiles into stack PARTY, 

   ​	if size of PARTY>n/2, return it. 

   ​	else loop do 1-3 in delegates who is not in the stack until return the major party.

Pseudocode:

```
stack MEETING 		// all delegates
static int n=MEETING.size()
FindMajorParty(MEETING):
picked=MEETING.pop()
stack PARTY,REST
for delegate in MEETING:
	if(delegate smiles at picked)
		PARTY.push(delegate)
	else 
		REST.push(delegate)
if(PARTY.size()>n/2)
	return PARTY
else 
	FindMajorParty(REST)
```

Correctness:

​	(i) the algorithm ends in finite steps: finite number n delegates in the meeting.

​	(ii) Knowing that there exists a major party. Consider the worst case: Using the search method could exclude all minor parties, the left should be the major. So the algorithm will return the major party. 

### Problem 6

Ideas:

​	有点复杂，这里用中文解释。用到的图如下：

![](/media/dxh/共享文件夹/sophomore/数据结构与算法/微信图片_20210922212602.jpg)

当递归分解到左右子数列各只剩下一个元素时，其本身就是左右子数列的最大子数列。在组合为中子数列时，有上述$a_1,a_2,a_3$三种情况。更一般的，如$b_1-b_3$图（并不完整，但足够说明问题）图中画出阴影的为左右部分的最大子数列。我发现，在组合中子数列时，易知图b1所画即为最大中子数列。然而在b2，由中子数列做法知道，左边最大子数列一定会并入中子数列；右边若只并入中间部分，则一定小于再并入右中子数列的部分，以此类推，容易发现：**中子数列的左边界为左最大子数列的左边界，右边界为右最大子数列的右边界**，通过这个发现，可以避免每次求解中子数列遍历整个数组的过程。推广到一般情况（如c图），只要递归求解左右最大子数列，便可以知道中子数列的边界位置。至于求解中子数列的和，我发现它的和可以拆分成两部分——**左子数列的右边界至中线**和**右子数列的左边界到中线**，那么只要递归地得到上次的左右边界以及这几部分加和，便可以在$O(1)$的时间内计算出想要的每一部分和。

$Pseudocode:$

```
FindMaxmumSubarray(A,low,high)
if(high==low)
	return(low,high,A[low],A[low],A[low])
else mid=(low+high)/2
	(left_low,left_high,left_sum,low_to_left_high,left_low_to_mid)=
											     FindMaxmumSubarray(A,low,mid)
	(right_low,right_high,right_sum,mid_to_right_high,right_low_to_high)=
						   					  FindMaxmumSubarray(A,mid+1,high)
	(cross_low,cross_high,cross_sum)=
				(left_low,right_high,left_low_to_mid+mid_to_right_high)
	if(left_sum>=right_sum and left_sum>=cross_sum)
		left_low_to_Ahigh = left_low_to_mid + mid_to_right_high + right_low_to_high - right_sum
		Alow_to_left_high = low_to_left_high
		return (left_low,left_high,left_sum,Alow_to_left_high,left_low_to_Ahigh)
	else if(right_sum>=left_sum and right_sum>=cross_sum)
		Alow_to_right_high = low_to_left_high + left_low_to_mid - left_sum + mid_to_right_high
		right_low_to_Ahigh = right_low_to_high
		return (right_low,right_high,right_sum,Alow_to_right_high,right_low_to_Ahigh)
	else 
		return (cross_low,cross_high,cross_sum,Alow_to_right_high,left_low_to_Ahigh)
```



### Problem 7

(a)

```
FindSecondLargest(A[1,...,n]):
if(n<2)
	return fail
else if(n=2)
	return A[2]
else 
	if(A[2]>A[3])
		return A[2]
    else 
    	return A[3]
```

(b)

Overview:

1. find the max element in the original heap, then use it to build a new max-heap.
2. extract the max element in the new heap, find its children in the original heap and insert them to the new heap.
3. loop do 2. until the new heap pops k elements, the $k^{th}$ popped is the target.  

$Pseudocode:$

```
FindLarge(A[1,...,n],k)
max-heap B.HeapInsert(A[1])
for(int i=0;i<k;i++)
	max=B.HeapExtractMax()
	idx_l=max.idx/2,idx_r=max.idx/2+1
	if(idx_l<=n)
		B.HeapInsert(A[idx_l])
	if(idx_r<=n)
		B.HeapInsert(A[idx_r])
	if(heapsize(B)==0)
		return fail
return max
```

Analyze running time:

Knowing that $HeapInsert()$ takes time $O(\lg heapsize(A))$ and size of max-heap B won't be larger than k,

so in the loop, cost on time won't be larger than $O(k\lg k)$. the first insert operation costs constant time.

Therefore the algorithm costs time $O(k\lg k)$ 
