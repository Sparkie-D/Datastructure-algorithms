<center>
    <h1>
        Problem Set 7
    </h1>
    <p1>人工智能学院 201300096 杜兴豪</p1>
</center>

### Problem 1

#### 	(a)

$$
\begin{align}
Q_k&=\binom{n}k(1-\frac1n)^{n-k}(\frac1n)^k\\
&<\binom nk (\frac1n)^k\\
&=\frac{n!}{k!(n-k)!}\frac{1}{n^n}\\
&=\frac1{k!}\frac{n!}{(n-k)!n^n}\\
&\le \frac1{k!}\\
&\approx\frac1{\sqrt{2\pi k}}(\frac ek)^k\\
&\le \frac {e^k}{k^k}
\end{align}
$$

#### 		(b)

​		Let $A_i$ be $i_{th}$ slot which contains the most keys and $\le k$
$$
\therefore P_k=P(A_1\bigcup A_2\bigcup ...\bigcup A_n)\le \sum^n_{i=1}P(A_i)\le\sum_{i=1^n}Q_k=nQ_k
$$


#### 	(c)

$$
\begin{align}
&\because k\ge \frac{c\lg n}{\lg\lg n}\\
&\therefore Q_k\le \frac{e^k}{k^k}\le 
\end{align}
$$

### Problem 2

#### 	(a)

​		Proof :

​				Let a string A be: $[a_1,a_2,...,a_n]$ while $a_i$ is the code value of each character. 

​				$\because$ $h(k)=k \mod m$, while $m=2^p-1$ and the code value has radix $2^p$.

​				$\therefore$ Key value of A is : $a_12^{(n-1)p}+a_2 2^{(n-2)p}+...+a_n$

​													$=[a_1(2^p-1)2^{(n-2)p}+a_12^{(n-2)p}]+[a_2(2^p-1)2^{(n-3)p}+a_22^{(n-3)p}]+...+a_n $

​													$=...=c(2^p-1)+a_1+a_2+...+a_n$

​				$\therefore h(k_A)=a_1+a_2+...+a_n$ has nothing to do with its order

​				$\therefore$ if we can derive string x from string y by permuting its characters, then x and y hash to the same value.

#### 		(b)

​		Proof :	

​					Assume $m=c_1d,h_2(k)=c_2d$ and $c_1 ,c_2$ are relatively prime.

​				$\therefore h(k,i)=(h_1(k)+ic_2d)\mod c_1d$

​					When it returns to $h_1(k)$, we have : $ic_2\mod c_1=0\Longrightarrow ic_2=bc_1\Longrightarrow i=c_1$

 				$\because h(k,i)=(h_1(k)+ih_2(k))\mod m\le m$, and each examination takes a distinct place.

​			 	$\therefore$ All searched space are $ c_1/m=1/d$

### Problem 3

#### 	(a)	

​		Let $X_i$ be the $i_{th}$ time insertion when collision happens. (Assume i-1 times before are done successfully)
$$
P(X_i)=\frac{i-1}{m}
$$

$$
\therefore f(m,n)=E(X)=\sum^n_{i=1}P(X_i)=\frac{n^2-n}{2m}
$$

#### 	(b)

​		Let “a random hash function is perfect” be incident A.

​		There are $m^m$ different random hash functions, while only $m!$ are perfect.	
$$
\therefore P(A)=\frac{m!}{m^m}\approx \frac{\sqrt{2\pi m}}{e^m}
$$

#### 	(c)

​		Let X be r.v. of "tests when the first time I find a *perfect* hash function".
$$
P(X=i)=(1-P(A))^{i-1}P(A)\\\\
\therefore X\sim G(P(A))\\\\
\therefore E(X)=\frac1{P(A)}=\frac{e^m}{\sqrt{2\pi m}}
$$

####		(d)

$$
P(X>N)=\sum_{i>N}P(X=i)=1-\int^N_1(1-P(A))^{i-1}P(A)di
$$



### Problem 4

​	Proof :

​		Induction basis : Trivial when i =1

​		Inductive step : 

​				Assume that when $i\le 2^k$ the amortized cost per operation is $O(1)$

​				When $2^k< i<2^{k+1}$, all operations cost 1, $2^k$ in total. After step $i=2^{k+1}$ , the new per operation cost is 
$$
Cost=\frac{2^kO(1)+2^kO(1)+2^{k+1}O(1)}{2^{k+1}}=O(1)
$$
  				The property still holds.

### Problem 5

​	Proof 1 :

​		Firstly, only analyze *Insertion*s.

​		Induction basis : Trivial.

​		Inductive step :	

​			When size of the hash table $\le 4n$, any sequence of insertions have amortized time per operation $O(1)$

​			Consider when size of hash table transform from 4n to 8n. 

​			When allocate a new table, the table is 3/4 full (3n taken) and call *Insertion* operation, which takes $O(1)$ time. And it take $3n\times O(1)$ time to insert everything into it.  Any *Insertion* happened when the table is 3/8 - 3/4 full (3n - 6n taken) takes $O(1)$ time apparently. Therefore the amortized time in the process above becomes:
$$
T_1=\frac{3nO(1)+3nO(1)}{3n}=O(1)
$$
​			So the property still holds.



Proof 2 :

​	Secondly, leave out *Insertions*.

​	Induction basis :  Trivial

​	Inductive step :

​			The same, assume when size of the hash table $\le 4n$,  any sequence of deletions have amortized time per operation $O(1)$	

​			Still consider when size of hash table transform from 8n to 4n.

​			To allocate and free space, the 8n table must be 1/4 full, (2n taken). The next allocation happens when the 4n space is 1/4 full (n taken), means n *Insertions* happen without change of space at the same time. Deletions happen before this all cost $O(1)$. Therefore the amortized time is 		
$$
T_2=\frac{nO(1)+nO(1)}{n}=O(1)
$$
​			The property holds.



Proof 3 ： 

​	Know from Proof 1 and Proof 2, and any sequence of Insertions and Deletions may allocate space more than once.

​	When it first enlarge the space, transforming it from 4n to 8n. There are two ways to go :

1. Resize :

   ​	It takes at least n times of Insertion/Deletions to fulfill the conditions to resize.

$$
T_4=\frac{3nO(1)+(n+i)O(1)}{n+n+i}\le \frac{3nO(1)}{2n}=O(1)
$$

2. Remain the size 8n.

   ​	May occur countless times of insertions and deletions, while none of them make change to the size 8n.

$$
T_3=\frac{3nO(1)+\infty O(1)}{n+\infty}=\lim_{k\to +\infty}\frac{3nO(1)+kO(1)}{n+k}\le \lim_{k\to +\infty}\frac{3nO(1)}{n}=O(1)
$$

$\therefore$ For any sequence of Insertions and Deletions, the amortized time per operation is still $O(1)$

