<center>
    <h1>
        Problem Set 7.5
    </h1>
<p1>人工智能学院	 201300096	 杜兴豪</p1>
</center>

### Problem 1

证明：

​       有序链表中：

​		$pop$操作仅删除头结点，用时$O(1)$。

​                                            		插入元素$x$所需时间为遍历所有比$x$小的元素花费的时间，加上插入节点所需$O(1)$，共需要$O(n)$。	

​		$\because$ 在$OrderedPush(x)$操作中，遍历所有比$x$小的元素用时不大于查找所有比$x$小的元素，有$T(x)\le\sum\limits_{i<x}T(i)$

​		$\therefore 2T(x) \le\sum\limits_{i\le x}T(i)$  

​		$\therefore$ 若分解每次$OrderedPush$操作，让每次操作花费时间变为之前两倍，即可"提前删除这些元素”，那么此时新$OrderedPush$元素仅花费时间$O(1)$（所有的查找工作已经在之前的$OrderedPush$中做完）

​		又当为空链表时，$OrderedPush(x)$花费为$O(1)$，则让其为$2O(1)=O(1)$，此时每次插入花费时间复杂度均为O(1)。

### Problem 2

证明：

​		易知$Push(x)$和$Pull()$操作所花费时间复杂度均为$O(1)$。

​		假设一段操作序列作用于一长度为$n$的双链表。其中在每一次$Decimate()$操作中将使链表长度减少至少$n/10$，因此做这次$Decimate()操作$之前一定有至少$n/10次Push(x)操作。$此时它们的均摊时间复杂度为
$$
T=\frac{O(n)+\frac{nO(1)}{10}}{1+\frac n{10}}=O(1)
$$
​		在此段序列中，因此任意加入多次$Pull()$操作，均摊复杂度变化为：
$$
T'=\frac{O(n)+\frac{nO(1)}{10}+O(1)O(1)}{1+\frac n{10}+O(1)}\le \frac{O(n)+\frac{nO(1)}{10}}{1+\frac n{10}}=T=O(1)
$$
​		因此任意操作序列下均摊复杂度均为$O(1)$

