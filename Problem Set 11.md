<center>
    <h1>
        Problem Set 11
    </h1>
    <p1>人工智能学院 201300096 杜兴豪</p1>
</center>

### Problem 1

#### (a)

![](/media/dxh/共享文件夹/sophomore/算法/作业/ps11.1.png)

![](/media/dxh/共享文件夹/sophomore/算法/作业/ps11.1.png)

#### (b)









#### (c)











### Problem 2

#### 算法描述

使用Dijkstra算法，每条边权为其置信度的倒数（非负且大于1），这条路径上所有边权重之积为当前点值。最后得到的具有最小权值的路径即为最高置信度的路径。

#### 伪代码

```
MaxReliable(G,s,t):
build priority queue Nodes based on dist
for u in V
	if(u != s)
		u.real = INF
	else u.real = 1 	// s
	u.parent = NULL
	Nodes.push(u)
s.real = 1
R = NULL //routine set
while( !Nodes.empty() )
	u = Nodes.ExtractMin()
	for (u,v) in G.E
		if(v.real > u.real*r(u,v))
			v.real = u.real * r(u.v)
			v.parent = u
			Q.DecreaseKey(v)
```

#### 时间复杂度分析

给每个点设定置信值和父节点用$O(n)$，while循环中，遍历所有点的ExtractMin共用时间$O(n\log n)$，遍历所有边的DecreaseKey用时间$O(m\log n)$，总用时间$O((n+m)\log n)$

### Problem 3



### Problem 4

#### (a)

incorrect strategy. 

conterexample :

![](/media/dxh/共享文件夹/sophomore/算法/作业/4a.png)

#### (b)

incorrect strategy.

conterexample :

![](/media/dxh/共享文件夹/sophomore/算法/作业/4b.png)

#### (c)

correct strategy.

#### (d)

incorrect strategy.

conterexample :

![](/media/dxh/共享文件夹/sophomore/算法/作业/4d.png)

#### (e)

correct strategy.

#### (f)

incorrect strategy.

conterexample :

![](/media/dxh/共享文件夹/sophomore/算法/作业/4d.png)

#### (g)

incorrect strategy.

conterexample :

![](/media/dxh/共享文件夹/sophomore/算法/作业/4g.png)

有1/3的概率第一次删除中间小间隔，导致得到错误结果。

#### (h)

correct strategy.

### Problem 5

#### 算法描述

按从小到大顺序快速排序L[1,...,n]，同时改变R中顺序与之对应。创建最小覆盖集合S，将最左端的间隔放入S。再重复以下操作：

* 获取S中最后一个元素m
* 继续遍历L集合（若第一次遍历则从头），记录所有左端点大于m的左端点，并且小于m的右端点的元素，将其中右端点最大的元素放入S
* 重复第二步直到遍历完L

#### 伪代码

```
MinCover(L[1,...,n],R[1,...,n]):
RndQuickSort X in L order 
stack S
S.push(1) //将间隔的标号放入栈中，方便访问其左右端点
while(R[S.top()]!=R[n])
	index = S.top()+1	//不可能溢出，否则满足while跳出条件
	target = index
	while(L[index]<R[S.top()])
		if(R[index]>R[target])
			target = index
		index ++
	S.push(target)
return S
```

#### 正确性证明

证明：

​		因为每次选取的点的左端点一定大于上次选点的右端点，所有由这个算法跑出来的一定是对X的一个覆盖。下证最小覆盖。

​		设这样得到的最小覆盖为S。

  		1. S中的第一个元素a显然一定属于最小覆盖，否则不能覆盖住X的最左端。
  		2. 假设去掉第一个元素后，原集合变为X'，S变为S'，则S'的第一个元素一定属于X'的最小覆盖。因为S'中第一个元素b的右端点为覆盖住a的元素中右端点最靠右的。所以X'的任何一种最小覆盖中，第一个元素都可以用b来替换，使之属于一个最小覆盖。
  		3. 由1.2.容易知道，S中的每一个元素都属于一个最小覆盖，假设最小覆盖的基数为$|M|,则一定有|S|=|M|$，因此S也为一种最小覆盖。

#### 时间复杂度分析

while循环中循环最多执行n次，遍历完L就终止，因此while循环的时间复杂度为$O(n)$，在不影响时间复杂度的情况下，排序L数组的时间复杂度为$O(n\log n)$。总时间复杂度为$O(n\log n)$

### Problem 6

#### (a)

面额：50 20 1 某次找零：60

按给定的贪心算法，需找1张50和10张1，共1张，可是3张20就够解决问题。

#### (b)

证明：

只需证任何一个数m都可以唯一表示为$m=\sum_{i=0}c_ib^i,c_i<b,b^i\le m$，则贪心算法可以从高位到低位做到最优。

因为$b^k=b\times b^{k-1}\ge c_{k-1}b^{k-1}+b^{k-1}\ge c_{k-1}b^{k-1}+c_{k-2}b^{k-2}+b^{k-2}\ge\cdots $

所以$b^k>\sum^{k-1}_{i=0}c_ib^i$

因此当得到确定的找零方案后，任意一张高面额货币数量都不能通过均摊到较小面额的方式减少，也不能通过减少小面额货币的方式增加高面额货币的数量。

因此以b进制的这种表示法唯一且为最优。

所以按照贪心算法的做法一定能找到最优解。

 

