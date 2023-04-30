# Problem Set 1

### Problem 1

a.(i)the outside loop ends in n-1 times(n is finite), while all the inside loops ends in at most n-1 times (from n to i+1>=2), this means the algorithm terminates in finite steps.

(ii) to prove (1), using mathematical induction:

 proof:

​		basis: By the end of the 1st iteration, A'[1] is in sorted order.

​		Inductive step:

​			Assume by the end of the jth iteration, we have A'[1]<=A'[2]<=...A'[j];

​			In the (j+1)th iteration, the A'[j+1] is the smallest among the remaining numbers.

​			Without loss of generality, let A[k]=A'[j+1].

​			When j=k,A[k]<=A[k-1], they will be swapped, A'[j+1] becomes A[k-1], then, j=k-1 ...

​			when the (j+1)th iteration ends,  

​			A'[j+1] appears to be in the front of the unsorted list, 

​			which means we have A'[1]<=A'[2]<=...A'[j]<=A'[j+1] now.



b. in the **for** loop in lines 2-4, a loop invariant is that after each loop ends, the first number in the loop is the smallest one.

proof: 

​			without loss of generality, we make the subarray A0 for the 2-4 loop, and the smallest number S=A0[a].			

​			When j=a,A[a]<=A[a-1], they will be swapped, A[a] becomes A[a-1],

​			then, j=a-1 ,A[a] then becomes A[a-2]....

​			when the iteration ends, S becomes the first number in the subarray.  



c. for the **for **loop in line 1-4, a loop invariant is that by the end of **i**th iteration, the subarray A[1,2......i] is sorted in order.

(i)proof:

​		basis: by the end of the 1st iteration, A[1] is sorted in order.			

​		inductive step:

​				assume by the end of jth iteration, A[1,2...j] is sorted.

​				after the (j+1)th iteration, as proved in b. , the result of the 2-4 loop makes the A[j+1] 				in appropriate place, A[1,2....j.j+1] is sorted in order.

  (ii)proof:

​				Know that by the end of ith iteration, the subarray A[1,2...i] is sorted in order.

​				therefore, after the (n-1)th iteration, the subarray A[1,2.....n-1] i sorted, and the last 	one is the biggest.

​				therefore, the array is sorted in order,

​				therefore, we have : A'[1]<=A'[2]<=...A'[n]

### Problem 2

$$
(a)\ T=c_1+c_2n=\Theta(n)
$$

(b) loop invariant: by the end of ith iteration, we have 
$$
P_i(x)=c_{n-i+1}+x(c_{n-i+2}+...+x(c_{n-1}+xc_n)),(c_k,k<=n)
$$
proof:

​		basis: by the end of 1st iteration, we have 
$$
P_1(x)=c_n
$$
​		inductive step:

​				assume by the end of jth iteration, we have
$$
y=P_j(x)=c_{n-j+1}+x(c_{n-j+2}+...+x(c_{n-1}+xc_n))
$$
 				in the (j+1)th iteration, do y=ci+x*y, we have:
$$
y'=c_{n-j}+x(c_{n-j+1}+x(c_{n-j+2}+...+x(c_{n-1}+xc_n)))=P_{j+1}(x)
$$
correctness of **PolyEval**:

proof:

(i) the loop ends in n times(n is finite).

(ii)proved in (b), we have :

​	when the algorithm ends, y becomes:
$$
y=c_{0}+x(c_{1}+...+x(c_{n-1}+xc_n))
$$
which shows the correctness of PolyEval.

### Problem 3


$$
f\in\ O(g):b,c,k,l,m,
$$

$$
f\in\Omega(g):e,g,h,i,j,k,o,p
$$

$$
f\in\Theta(g):a,d,f,n
$$

### Problem 4

$$
1\ll n^{1/\lg n}\ll \lg(\lg^*n)=\lg^*(\lg n) \ll \lg^*n\ll \ln\ln n\ll  \lg^2n\ll \sqrt{\lg n}\ll \ln n\ll n
\\\ll n\lg n=\lg(n!)\ll
n^2\ll n^3\ll 2^{\lg^*n}\ll 2^{\sqrt{2\lg n}}\ll (\sqrt2)^{\lg n}\ll 2^{\lg n}\ll  (3/2)^n\ll 2^n\ll n*2^n\ll e^n
\\\ll 4^{\lg n} \ll (\lg n)!\ll n!\ll (n+1)!\ll \lg n^{\lg n}\ll n^{\lg\lg n}\ll 2^{2^n}=2^{2^{n+1}}
$$



### Problem 5

Use a circular array (Arr) to implement two stacks:  

Stack A moves the head to push and pop, while stack B moves the tail.

Pseudocode:

```
when (head==tail+1)or(head==1 and tail==8) 
can only pop,if push, each of the stacks will overflow 

PushA(x):
	if(head==1)then head=n+1     #Arr[1,2...,n]
	head-=1
	Arr[head]=x
PopA():
	head=(head==n)?1:(head+1)

PushB(x):
	tail=(tail==n)?1:(tail+1)
	Arr[tail]=x
PopB():
	if(tail==1)then tail=n+1
	tail-=1
	

```

### Problem 6

We call FIFO queue 1 F1, FIFO queue 2 F2.  When pushing, add x to the end of F1 (F2 remains empty). When popping, add all but x (the last in F1 queue) to F2 one by one. After that, pop the remaining one out of F1. Then add the ones in F2 back one by one.

Pseudocode:

```
Push(x):
	set F1[i+1]=F1[i] for n>i>=1  # n is the lenth of F1(F2)
	set F1[0]=x
Pop():
	set F2[i-1]=F1[i] for n>=i>1
	set F1[i]=F2[i] for n>i>=1
```

analyse:

Push:
$$
set\ F1[i+1]=F1[i]\ for\ n> i\ge 1:\quad \Theta(1)\ to\ \Theta(n)
\\set\ F1[0]=x:\quad\quad\quad\quad\quad\quad\ \ \ \Theta(1)
$$
Pop:
$$
set\ F2[i-1]=F1[i]\ for\ n\ge i>1:\quad\Theta(1)\ to\ \Theta(n)
\\set\ F1[i]=F2[i]\ for\ n>i\ge 1:\quad\quad\ \ \ \Theta(1)\ to\ \Theta(n)
$$
