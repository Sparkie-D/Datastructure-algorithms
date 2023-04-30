# Problem Set 4

### Problem 1

(a)

![](/home/dxh/.deepinwine/Deepin-WeChat/drive_c/Program Files/Tencent/WeChat/0.jpg)

(b)

![](/home/dxh/.deepinwine/Deepin-WeChat/drive_c/Program Files/Tencent/WeChat/1.jpg)

### Problem 2

Description:

1. divide k lists into two groups with equal size.

2. sort the two groups individually.
3.  merge the results into one.

Pseudocode:

```
MySort(A1,A2...,Ak):
  B1=MySort(A1,A2,...,Ak/2)
  B2=MySort(Ak/2+1,...,Ak)
  Merge(B1,B2)
  
Merge(A[1,..a],B[1,...b]):
  int i,j,k=0;
  while(true)
  	if(i==a+1)
  		while(j!=b+1)
  			C[k]=B[j]
  			j++,k++
  		break
  	else if(j==b+1)
  		while(i!=a+1)
  			C[k]=A[i]
  			i++,k++
  		break
  	if(A[i]<=B[j])
  		C[k]=A[i]
  		i++,k++
  	else
  		C[k]=B[j]
  		j++,k++
```

Runtime :

​	the merge part loops no more than n times (for total lenth is n). Each loop takes constant steps.

​	So it costs O(n)

​	$\therefore T(k)=2T(k/2)+O(n)\rightarrow T(k)=O(n\lg k)$

### Problem 3

(a) proof:

​			basis: When input A[1,2], Cruel sorts it by unusual.

​			Induction step:

​				    Assume that Cruel sorts any input array size <=k. When input A[1,..,k+1]:

​					Knowing that size of A[1,...,(k+1)/2]  and A[(k+1)/2+1,...,k+1] are both <k, 

​					From basis we have that Cruel sorts them correctly individually.

​					When doing Unusual(A[1,...,k+1]):

​							$\because A[1,...\frac{k+1}{2}],A[\frac{K+1}{2}+1,...,k+1]\ are\ sorted$

​							Divide them into four parts in place: $p_1,p_2,p_3,p_4$

​							$\therefore \forall x\in p_1,y\in p_2,x<=y;\ \forall m\in p_3,n\in p_4,m<=n$

​							After swapping  $p_2,p_3$, do Unusual($p_1,p_3$) and Unusual($p_2,p_4$) to sort them.

​							Name the new parts $p'_1,p'_2,p'_3,p'_4$ 

​							Knowing that $p'_1,p'_2$ comes from $p_1,p_3$, $p'_3,p'_4$ comes from $p_2,p_4$ 

​							$\therefore p'_1<min(p'_2,p'_3,p'_4);\ p'_4>max(p'_1,p'_2,p'_3) $ and sorted.

​							Then do Unusual($p'_2,p'_3$) result in $p''_2,p''_3$, which $p''_2<=p''_3$

​							$\therefore p'_1<=p''_2<=p''_3<=p'_4$ the input array A[1,...,k+1] is sorted.

(b) proof by counter-example :

When input [4,3,2,1], in the algorithm:

​			Cruel([4,3]) $\rightarrow$ [3,4,2,1]

​			Cruel([2,1]) $\rightarrow$ [3,4,1,2]

​			Unusual([3,4,1,2]):

​					Unusual([3,4]) $\rightarrow$ [3,4,1,2]

​					Unusual([1,2]) $\rightarrow$ [3,4,1,2]

​					Unusual([4,1]) $\rightarrow$ [3,1,4,2]

​			result $\rightarrow$ [3,1,4,2] not sorted !

(c) proof by counter-example:

When input [4,3,2,1], In the algorithm:

​			Cruel([4,3]) $\rightarrow$ [3,4,2,1]

​			Cruel([2,1]) $\rightarrow$ [3,4,1,2]

​			Unusual([3,4,1,2]):

​					swap([4,1]) $\rightarrow$ [3,1,4,2]

​					Unusual([3,1]) $\rightarrow$ [1,3,4,2]

​					Unusual([3,4]) $\rightarrow$ [1,3,4,2]

​					Unusual([4,2]) $\rightarrow$ [1,3,2,4]

​			result $\rightarrow$ [1,3,2,4] not sorted !

(d)

​	Unusual:

​		$T(2)=c_0$

​		$T(n)=c_1n/4+3T(n/2)\rightarrow T(n)=O(3^{\lg n})=O(n^{\lg 3}) $

​	Cruel:

​		$T(2)=c_0$

​		$T(n)=2T(n/2)+n^{\lg 3}=3n^{\lg 3}-n=O(n^{\lg 3})$ 

### Problem 4

(a) proof:

​		(i) For every p=q+1, the algorithm terminates in finite steps (when p >=r).

​		(ii) After each iteration, A[1,...,q] is sorted in place.

​				proof:

​				 	Basis: In 1st loop, after invoking TRQuickSort(A,1,q-1), A[1,...,q-1] is sorted in place. 

​						    And A[q] is pivot, larger than any one before it. So A[1,..,q] is sorted.

​				 	Induction step:  

​							when A[1,..,q] is sorted, p=q+1, q'=Partition(A,q+1,n), which means A[q+1,q'-1]<=A[q'], 

​							then invoke TRQuickSort(A,q+1,q'-1), makes A[q+1,q'-1] sorted in place. 

​							Therefore A[q+1,q'] is sorted. 

​							Knowing that any element in A[q+1,q'-1] is larger than one in A[1,q], So A[1,...q'] is sorted.

​			Therefore, when q=r, A[1,...r] (r=n) is sorted, the array A is sorted in place. 

(b) Scenario: The input array A is sorted in place already.

(c)

```
MyTRQuickSort(A[1,...,n],p,r)
while(p<r)do
	SetMid(A);
	q=Partition(A,p,r)
	TRQuickSort(A,p,q-1)
	p=q+1
	
SetMid(A[1,...,n]):
mid=1,val=A[1],total=0;
for(i=0;i<n;i++)
	if(A[i]<val)
		if(total<n/2)
			total+=1
		else
			mid=i,val=A[i]
```



### Problem 5

(a)

Pseudocode:

```
MySort(A[1,...,n]):
sorted=0;
while(sorted<n)
	i=1
	while(i<=n)
		SqrtSort(i)
		i+=sqrt(n)-1
	sorted++
```

proof:

​	claim: After ith outer iteration, the last i items of current size are sorted in place.

​				 proof:

​						claim: After each SqrtSort(i), the last item of the subarray A[k+a,...,k+a+sqrt(n)] is the largest of A[1,...,k+a+sqrt(n)].

​								proof:

​										basis: After SqrtSort(1), A[1+sqrt(n)] is largest in A[1,...,1+sqrt(n)]

​										Inductive step: 

​												Assume that After SqrtSort(k), A[m] (the last item) is largest in A[1,...,m]. Then in SqrtSort(k+sqrt(size)-1), we know that the first 												item of current subarray is A[m], after sorting, the last item A[p] must >=A[m], while A[m] is lagest in the former subarray. 												Therefore A[p] is largest in A[1,...,p]. 

​						Therefore: When the inner while loop quits, the last item is largest in the current array.

​	basis: After first outer loop, A[n] is inplace.

​	Inductive step:

​		Assuming that After kth loop, A[n-k+1,...,n]  is inplace. In the (k+1)th loop, size of the array is n-k,. Knowing from claim that after this iteration, A[n-k] 		is largest in A[1,...,n-k]. while A[n-k+1,..,n] are larger than any in A[1,...,n-k], A[n-k] is sorted in place.

​	Therefore: After n outer loops, when size=0, A is sorted in place.

  (b)Knowing that each time invoke Mysort, it invoke SqrtSort $n\sqrt{n}$ times. Let A(n), B(n) be running time of Mysort and SqrtSort, we have:

​	$A(n)=n\sqrt{n}B(n),B(n)=A(\sqrt{n})\rightarrow A(n)=n\sqrt{n}A(\sqrt n)$

​	From 4.3, we know: let $m=\lg n$, then $n=2^m,A(n)=n\sqrt{n}A(\sqrt n)\rightarrow A(2^m)=2^{3m/2}A(2^{m/2})$ 

​	let $C(m)=A(2^m)$, we have$C(m)=2^{3m/2}A(m/2)=2^{3m/2+3m/4+...+0}=2^{3m}$

​	$\therefore A(n)=n^3,B(n)=n^(3/2)$  

### Problem 6

(a) proof:

​			Let OneInThree returns 1 be incident A, FairCoin returns 0 be B.

​			$P(B)=P(\overline B)=\frac{1}{2}$

​			$P(A)=P(\overline B)P(\overline A)=P(\overline B)(1-P(A))=\frac{1}{2}(1-P(A))$

​			$\therefore P(A)=\frac{1}{3}$

(b) proof: 	

​			Let times this algorithm calls FairCoin be X, then $P(X=i)=\frac{1}{2^i}$

​			Basis: $P(X = 1)=P(B)=\frac{1}{2}$

​			Induction step: Let $P(X=k)=\frac{1}{2^k}$, then

​			$P(X=k+1)=\frac{P(X=k)}{P(B)}P(\overline B)P(B)=P(X=k)P(B)=\frac{1}{2^k}\times\frac{1}{2}=\frac{1}{2^{k+1}}$

​			$\therefore$$E[x]=1\times\frac{1}{2}+2\times\frac{1}{4}+..+n\times\frac{1}{2^n}+...$

​			$E[x]=\lim_{n\rightarrow+\infty}2\frac{1-\frac{1}{2}}{1-\frac{1}{2^n}}=1$

(c)



### Problem 7

Pseudcode:

```
FindNumber(head,tail,target):
mid=(head+tail)/2
if(head<tail or head=tail!=target) return false
else if(head=tail) return head
else if(target=mid) return mid                                    //ask 1
else if(target<mid) return FindNumber(head,mid-1,target)          //ask 2
else if(target>=mid) return FindNumber(mid,tail,target)           //from ask 2
```

FindNumber(1,100000,integer);

upper bound: $2\lg 100000$ times, which is equal to binary search.

lower bound:  

### Problem 8







