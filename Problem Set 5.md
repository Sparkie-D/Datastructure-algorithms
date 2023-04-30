# Problem Set 5

### Problem 1













### Problem 2

#### (a)

Let "Two subsets have equal weight" be incident A.
$$
\begin{align}
P(A)&=\frac{\binom{n-2}{\frac{n}{2}}}{\binom{n}{\frac{n}{2}}}=\frac{\frac{(n-2)!}{(\frac{n-4}{2})!(\frac{n-4}{2})!}}{\frac{n!}{(\frac{n}{2})!(\frac{n}{2})!}}=\frac{n-2}{4n-4}
\end{align}
$$

#### (b)

Using an array A[1,...,n] to simulate coins.

```
Balance(A,B)
// if A weighs larger,return -1, B larger 1, equal 0

static enable = false 
RndFind(A[1,...,n]):
//A contains large and small fake coin, return tuple (large,small)
if(enable == false) //recursively stop useless branch
	B1[1,..,n/2]=RandomChoose(A[1,...,n],n/2)
	B2[1,...,n/2]=rest of A
 	if(lenth(A) == 2) return A[1]>A[2] ? (A[1],A[2]) : (A[2],A[1])
	else if(Balance(B1,B2) > 0)
    	enable = true
		return (RndFindLarge(B1),RndFindSmall(B2))
	else if(Balance(B1,B2) < 0) 
		enable = true
		return (RndFindLarge(B2),RndFindSmall(B1))
	else // B1 weighs equal to B2
		res1=RndFind(B1)
		res2=RndFind(B2)
		return res1=NULL? res2:res1
else return NULL
		
RndFindLarge(A[1,...,n]):
// A contains and only contains larger fake coin.
B1[1,..,n/2]=RandomChoose(A[1,...,n],n/2)
B2[1,...,n/2]=rest of A
if(lenth(A) == 2) return A[1]>A[2] ? A[1] : A[2]
else if(Balance(B1,B2) > 0) return RndFindLarge(B1)
else if(Balance(B1,B2) < 0) return RndFindLarge(B2)

RndFindSmall(A[1,...,n]):
// A contains and only contains small fake coin.
B1[1,..,n/2]=RandomChoose(A[1,...,n],n/2)
B2[1,...,n/2]=rest of A
if(lenth(A) == 2) return A[1]>A[2] ? A[2] : A[1]
else if(Balance(B1,B2) < 0) return RndFindSmall(B1)
else if(Balance(B1,B2) > 0) return RndFindSmall(B2)

```

When invoking RndFindSmall and RndFindLarge, the number of times uses the Balance becomes fixed. It varies because of the recursion of invoking RndFind, which is before fake coins can be differentiated. Knowing from (a), probability of fake coins not being differentiated is $\frac{n-2}{4n-4}$, so:

X' is number of time uses balance before invoking RndFindLarge/Small.
$$
\begin{align}
&P(X'=2^{i-1})=P(A)^{i-1}(1-P(A))=\frac{(n-2)^{i-1}(3n-2)}{4^i(n-1)^i}\\
\end{align}
$$
When invoking RndFindLarge/Small, it uses Balance $\log n$ times of input size n. We have:
$$
E(X)=\sum^\infty_{i=1}2^{i-1}\frac{(n-2)^{i-1}(3n-2)}{4^i(n-1)^i}\log{\frac{n}{2^i}}
$$

### Problem 3

#### (a)

#### Describe 

1. QuickSort the value set while using another list to record their number, and change W at the same time. 
2. Look through the changed W, compute the sum of the weights before and after the current element until find one fits the rule.
3. return the number of the target.

#### Analyze

Part 1 takes time complexity $O(n\log n)$, Part 2 takes $O(n)$ So **the total time complexity is $O(n\log n)$**

#### (b)

#### Describe 

Use BST.

1. Create tree nodes with members: (1) number (2) value (3) weight (4) left subtree weight (5) right subtree weight
2. Insert elements by their value into the BST :
          1. Add them into the tree.
             2. Recount every parent node's left and right subtree weight.
3. Count $w(S)$ and save.
4. Traverse the BST until find one both are smaller than $w(S)/2$ and return its number. 

#### Analyze

Part 1 takes time complexity $O(n)$, Part 2 takes $O(n)$ , Part 3 takes $\Theta(1)$, Part 4 takes $O(n)$. So **the total time complexity is $O(n)$** 

### Problem 4

#### (a)

#### Algorithm

1. Prepare two empty arraies A , B of size n.
2. Compare every element in the sequence $a_i$ with the first item $a_1$,  judge the first compare:

   1. $a_i>a_1$ : Add $a_1$ to A, $a_i$ to B       																			(confirm $a_1=0$)

   2. $a_i=a_1$ : Add $a_1,a_i$ to A, watch next comparison:

      1. $a_{i+1}>a_1$: Add $a_{i+1}$ to B, break           															(confirm $a_1=0$)
      2. $a_{i+1}=a_1$: Add $a_{i+1}$ to A

      3. $a_{i+1}<a_1$: Swap the name of A and B, add $a_{i+1}$ to current A, break		(confirm $a_1=1$)

   3. $a_i<a_1$ : Add $a_1$ to A																				                 (confirm $a_1=1$)
3. Knowing value of $a_1$, then add every 0 to A, and every 1 to B
4. Combine A and B

#### Analyze

For every item in the input array, it is compared to $a_1$ once and only once. (And it's not $a_1$). So the **total comparison times are n-1**.

#### (b) 

#### Algorithm

1. Compare and sort **stably** the strings from the last character. (if the string's length is small, use '\0' as its character.)
2. for i = n **down to** 1, **stably **sort the strings' $i_{th}$ character using the way in 1.

#### Analyze

​	In each sort using comparison, the characters will be swapped constant times,which takes time cmoplexity $\Theta(1)$. The total loops will be no more than n times (depending on the longest string). So **the total time complexity will be $T(n)=n\times\Theta(1)=O(n)$**  

### Problem 5

#### (a)

Prove by induction:

​	Basis:  

​			When n=1, the root is a central vertex.

​	Hypothethisis: 

​			When $n\le k$ , every tree has a central vertex.

​	Inductive step:

​			When $n=k+1$, assume that before the last node was added, the tree has a central vertex $c_0$ , dividing the tree into three parts, largest of which is size $k/2$. Easy to know, the rest two parts won't get larger than $k/2$ even having added the $(k+1)_{th}$ node. Analyze the largest part:

1. If it is $c_0$'s subtree, choose $c_0$'s child node of its side as the new central vertex $c_1$. Since this part has $k/2$ nodes, the rest two parts have $k/2-1$ in total (apart from $c_0$) . So when choosing $c_1$ as the central, the rest two parts combine into one, size=$k/2-1+1(c_0)=k/2<(k+1)/2$, while the largest part would be divided into at most two parts, of total nodes $k/2-1+1=k/2$, both of which is smaller than $(k+1)/2$.
2. If it is $c_0$'s parent tree, choose its parent node as the new center vertex, the analysis is similar to 1.

#### (b)



### Problem 6

#### (b)

Suppose that the tree given uses **Left-child, right sibling representation**.

For all nodes in this tree, has member: (1) parent (2) firstChild (3) nextSibling (4) visited (boolean)

Initialize all node unvisited.

#### Algorithm

Traverse the tree with the following rules:

1. If currrent node has an unvisited child, visit it.
2. If current node has a next sibling, visit it.
3. If both not obey, go back to visit its parent node.
4. loop 1-3 until it travels back to root. 

```
Traverse(Node *root):
Node *current=root
do
	if(current.firstChild != NULL && current.firstChild.visited == false)
		current = current.firstChild
	else if(current.nextSibling != NULL)
		current = current.nextSibling
	else 
		current = current.parent
	current.visited=true
while(current != root)
```

#### Analyze

##### Space complexity

The algorithm only takes $O(1)$ space to store the node *current*, So the total space complexity is $O(1)$

##### Time complexity

The whole path will traverse all node at least once, costs $ O(n)$ time.Since there are average $n/2$ leaves, There will be at most $n/2 $ parent nodes to return to, so the return time takes at most $O(n)$. Therefore, **the total time complexity will be $O(n)+O(n/2)=O(n)$**  