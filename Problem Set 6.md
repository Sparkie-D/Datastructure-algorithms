<center>
    <h1>Problem Set 6</h1>
    <p>人工智能学院&nbsp;&nbsp;&nbsp;201300096&nbsp;&nbsp;&nbsp;杜兴豪</p>
</center>

### Problem 1

#### (a)









#### (b)

#### Description

Learn from properties of $preorder$ and $postorder$ traversals, we can learn that:

1. In $Preorder$ traversal, any given element $a's$ next is its left child.
2. In $Postorder$ traversal, $a$'s previous is its right child.
3. In $Preorder$, if $a.left's$ next is $a.right$ , then $a.left$ is a leaf.
4. In $Postorder$, if $a.right's$ previous is $a.left$, then $a.right$ is a leaf.

Therefore, we can go through the $Preorder$ and $Postorder$ list to build the tree.

#### Pseudocode

```
BuildTree(pre[1,...,n],post[1,...,n]):
leaves={}
for(i=1 to n-2)
	index=binarySearch(post,pre[i])
	if(pre[i+2] == post[index-1])
		leaves.add(pre[i+1])
for(i=n down to 3)
	index=binarySearch(pre,post[i])
	if(post[i-2] == pre[index+1])
		leaves.add(post[i-1])
for(i=1 to n-1)
	if(pre[i] not in leaves)
		pre[i].left=pre[i+1]
for(i=n down to 2)
	if(post[i] not in leaves)
		post[i].right=post[i-1]
```

#### (c)

#### Proof

There might be two different binary tree which have the same $Preorder$ and$Postorder$ list.







### Problem 2

#### Algorithm

​	To transform the given tree into height-balanced binary search tree, we need to do the following steps:

1. Pull the tree into a line using rotations
2. Transform the line into height-balanced shape by rotate all nodes in the same way, which satisfies height balance and search tree property.
3. Finish transform the tree by fix the last part of the tree (In step 2, we have made one stone node not full) 

#### Pseudocode

```
MakeChain(root):
current=root
if(current.right != null)
	left_rotation(current.right)
	root=current.right
	makechain(root)
else if(current.left != null)
	makechain(current.left)
	
BuildBalance(root):
root=MakeChain(root)
tmp=root
i=1
for(;tmp!=null;tmp=tmp.left) 
	tmp.No=i //assign every node an order
	i++
current=root
int cnt=1
int target=n%2==0? n/2:(n+1)/2 //result tree's root number
while(root.No != target)
	current=root
	while(current.left!=null)
		current=current.left
		cnt++
		if(cnt%2==0)
			cnt=0
			right_rotation(current)
current=root
while(current.left!=null) current=current.left
left_rotation(current.right)
```

#### Proof

​		The `Makechain` transform any given search tree into a chain, while the `BulidBalance` transforms chain into height-balanced binary search tree.

​		$\therefore$  They transform any given search tree into height-balanced tree.

​		The following proves their effect and they cost $O(n)$ rotations.

​		The `MakeChain` function works by recursively rotate the given arbitrary search tree into a chain. 

​				Easy to know that after the function ends, all nodes in the given tree should have no right child. 

​				Because all nodes could be the parameter of function once and only once, the function will be invoked at most n times.

​				Rotation complexity  is $O(n)$, which satisfies the rule. 

​		The `BuildBalance` function bend the chain into height-balanced tree by loops.

​				We know that when the function terminates, the center node is the current root.

​				Before it becomes root, all rotations all same before and after it. So when rotate it to be the root, its left and right subtree should appear the same except for the last node, which stays with its parent without loss of generality (different from the right subtree of root on 1 height ).

##### 		Rotation complexity:

​				 After every outer loop the root number get larger: $1,2,4,8,...2^{i-1},...n/2$. And after each outer loop, the rotations in inner loop gets smaller by div 2, which is the array $n/2,n/4,...,1$. So the total rotations in `BulidBalance` will be $R(n)=\sum^{\log n}_{i=1}\frac{n}{2^{i}}=O(n)$   

​				So the **total Rotation Complexity is $O(n)+O(n)=O(n)$**

### Problem 3

#### Algorithm

1. Use the algorithm `MakeChain` used in Problem 2 to transform the given arbitrary tree into a chain (Assume all nodes only have a left child).
2. Compare each node with its parent from leaf node, and use the following steps to swap them if disobey search tree rule (this>this.parent) :









	3. loop do 2 until current node gets root. The result chain is sorted, therefore it is of course a binary search tree.

#### Analysis

1. `MakeChain` takes $O(n)$ rotations proved in Problem 1
2. The Swap step takes 3 rotations and swaps to exchange one node with its parent. In the worst case it takes $3n$ rotations and swaps to make a leaf node travel to the root. So the tree costs rotations and swaps: $R(n)=n\ O(n)=O(n^2)$
3. **The algorithm costs rotations and swaps $O(n)+O(n^2)=O(n^2)$**

### Problem 4

#### (a)













#### (b)













### Problem 5

#### (a)

#### proof

$\because$ $AVL\ tree$ holds that for each node, heights of left and right subtree differ by at most 1

$\therefore$ An $AVL\ tree$ of height $h$ have at least: (1) A root (2) a height $h-1$ $AVL\ subtree$ and a height $h-2$ $AVL\ subtree$

Let $AVL(h)$ stands for all nodes of a least $AVL\ tree$ of height $h$

$\therefore$ $AVL(h)=1+AVL(h-1)+AVL(h-2)\to AVL(h-1)+AVL(h-2)$

$\because AVL(1)=1+AVL(0)+AVL(-1)=1\to F_1,AVL(2)=1+AVL(1)+AVL(0)=2\to F_2$ 

$\therefore $ An $AVL\ tree$ of height $h$ has at least $F_{h-1}+F_{h-2}=F_h$ nodes 	(Asymptotically)

$\because F_n=\frac{1}{\sqrt5}((\frac{1+\sqrt5}{2})^n-(\frac{1-\sqrt5}{2})^n)$

$\therefore \frac{F_n}{2^n}=\frac{\frac{1}{\sqrt5}((\frac{1+\sqrt5}{2})^n-(\frac{1-\sqrt5}{2})^n)}{2^n}=\frac1{\sqrt5}((\frac{1+\sqrt5}{4})^n-(\frac{1-\sqrt5}{4})^n)\to 0$

$\therefore AVL(h)<2^h$

$\therefore$  An $AVL\ tree$  with $n$ nodes has height $O(\log n)$

#### (b)

#### Description

​		My algorithm rotate the higher subtree's root to the other, causing the larger one's height-1, smaller one's height+1. To make sure they will only cause height change on 1, my algorithm makes the subtree added to $x.smaller$ when rotation is the smaller part of the larger tree's subtrees, which satisfies the moved subtree of $x.larger $ has height equal to $x.smaller$.  The following describes in detail.

Compare $x$'s left and right subtrees, and do corresponding steps as follows:

#### Pseudocode

```
Balance(x):
if( x != null)
	if(|x.left.h-x.right.h| <= 1 )
		Balance(x.left) 
		Balance(x.right) 
	if((x.left.h==2 && x.right==null) ||x.left.h-x.right.h == 2 ) 
    	if(x.left.left.h < x.left.right.h)	
    		left_rotation(x.left.right)  
    		//here x.left has been changed into x.left.right
  		right_rotation(x.left)
	else if((x.right.h==2 && x.left==null)||x.left.h-x.right.h == -2) 		
		//x.left.h-x.right.h == -2
    	if(x.right.left.h > x.right.right.h)
    		right_rotation(x.right.left) 
    		//here x.right has been changed into x.right.left
   		left_rotation(x.right)
   	Balance(x.left)
   	Balance(x.right)
```

#### (c)

#### Description

1. Insert the new node into $AVL\ tree$, taking it as an $BST$
2. From the inserted node, maintain every node's height
3. Balance the tree

#### Pseudocode

```
AVLInsert(x):
BSTInsert(x)
current=x
while(current!=null)	//maintain height value
	if(current.parent have only one child)
		current.parent.h+=1
	else if(current.parent.h == current.h+1)	//current is highest subtree
		current.parent.h+=1
	current=current.parent
Balance(root)
```

#### (d)

#### Time Complexity

1. `BSTInsert(x)` takes time $O(h)=O(\log n)$ in $AVL\ tree$
2. maintain height value takes time $O(h)=O(\log n)$. Because in the worst case x is in the end of the longest path from root to leaf, the path visits h nodes.
3. `Balance(root)` also takes time $O(h)=O(\log n)$. Because it visits all nodes through paths from root to leaves, longest of which is h.

Therefore **total Time Complexity is $O(h)+O(h)+O(h) =O(h) =O(\log n)$** 

#### Rotations 

The algorithm only use rotations in part `Balance(root)`

Claim: `Balance(root)` only operate once.

​	Proof: 

​	$\because$ It was an $AVL\ tree$ before insertion

​	$\therefore$ The only way to cause not balance is that x is added to the higher subtree's higher branch. Rest of the tree should be balanced.

​	$\therefore$ Assume the subtree to add x has height h. Its sibling should has height $\in[h-1,h]$. After insertion, it became $h+1$

​	$\therefore$ After Balance first operates on it, its sibling's height become $\in[h,h+1]$, while its height becomes $h$, which satisfies the rule 

​	$\because$ x is added to higher subtree

​	$\therefore$ the subtree's height -=1 won't have influence on other parts 

Therefore, Balance operates only once, using rotations only $O(1)$ times.

### Problem 6



