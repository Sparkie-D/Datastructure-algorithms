<center>
    <h1>
        Problem Set 12
    </h1>
    <p1>人工智能学院 201300096 杜兴豪</p1>
</center>
### Problem 1

#### (a)

![](/home/dxh/sophomore/算法/作业/ps12.1.png)

#### (b)

 每个点左边粗线连接的为父节点

![](/home/dxh/sophomore/算法/作业/ps12.2.png)

### Problem 2

#### (a)

![](/home/dxh/sophomore/算法/作业/3.png)

| r=0  | 1        | 2        | 3        | 4        | 5        | 6        |
| ---- | -------- | -------- | -------- | -------- | -------- | -------- |
| 1    | 0        | $\infty$ | $\infty$ | $\infty$ | $\infty$ | $\infty$ |
| 2    | $\infty$ | 0        | $\infty$ | $\infty$ | $\infty$ | $\infty$ |
| 3    | $\infty$ | $\infty$ | 0        | $\infty$ | $\infty$ | $\infty$ |
| 4    | $\infty$ | $\infty$ | $\infty$ | 0        | $\infty$ | $\infty$ |
| 5    | $\infty$ | $\infty$ | $\infty$ | $\infty$ | 0        | $\infty$ |
| 6    | $\infty$ | $\infty$ | $\infty$ | $\infty$ | $\infty$ | 0        |

| r=1  | 1        | 2        | 3        | 4        | 5        | 6        |
| ---- | -------- | -------- | -------- | -------- | -------- | -------- |
| 1    | 0        | $\infty$ | $\infty$ | $\infty$ | -1       | $\infty$ |
| 2    | 1        | 0        | $\infty$ | 2        | $\infty$ | $\infty$ |
| 3    | $\infty$ | 2        | 0        | $\infty$ | $\infty$ | -8       |
| 4    | -3       | $\infty$ | $\infty$ | 0        | 3        | $\infty$ |
| 5    | $\infty$ | 7        | $\infty$ | $\infty$ | 0        | $\infty$ |
| 6    | $\infty$ | 5        | 12       | 7        | $\infty$ | 0        |

![](/home/dxh/sophomore/算法/作业/3.png)

| r=2  | 1    | 2    | 3        | 4        | 5        | 6        |
| ---- | ---- | ---- | -------- | -------- | -------- | -------- |
| 1    | 0    | 6    | $\infty$ | $\infty$ | -1       | $\infty$ |
| 2    | -1   | 0    | $\infty$ | 2        | 5        | $\infty$ |
| 3    | 3    | -3   | 0        | 4        | $\infty$ | -8       |
| 4    | -3   | 10   | $\infty$ | 0        | -4       | $\infty$ |
| 5    | 8    | 7    | $\infty$ | 9        | 0        | $\infty$ |
| 6    | 6    | 5    | 12       | 7        | $\infty$ | 0        |

| r=3  | 1    | 2    | 3        | 4    | 5    | 6        |
| ---- | ---- | ---- | -------- | ---- | ---- | -------- |
| 1    | 0    | 6    | $\infty$ | 8    | -1   | $\infty$ |
| 2    | -1   | 0    | $\infty$ | 2    | -2   | $\infty$ |
| 3    | 1    | -3   | 0        | 4    | 2    | -8       |
| 4    | -3   | 3    | $\infty$ | 0    | -4   | $\infty$ |
| 5    | 6    | 7    | $\infty$ | 9    | 0    | $\infty$ |
| 6    | 4    | 5    | 12       | 7    | 5    | 0        |

![](/home/dxh/sophomore/算法/作业/3.png)

| r=4  | 1    | 2    | 3        | 4    | 5    | 6        |
| ---- | ---- | ---- | -------- | ---- | ---- | -------- |
| 1    | 0    | 6    | $\infty$ | 8    | -1   | $\infty$ |
| 2    | -1   | 0    | $\infty$ | 2    | -2   | $\infty$ |
| 3    | 1    | -3   | 0        | 4    | -3   | -8       |
| 4    | -3   | 3    | $\infty$ | 0    | -4   | $\infty$ |
| 5    | 6    | 7    | $\infty$ | 9    | 0    | $\infty$ |
| 6    | 4    | 5    | 12       | 7    | 5    | 0        |

| r=5  | 1    | 2    | 3        | 4    | 5    | 6        |
| ---- | ---- | ---- | -------- | ---- | ---- | -------- |
| 1    | 0    | 6    | $\infty$ | 8    | -1   | $\infty$ |
| 2    | -1   | 0    | $\infty$ | 2    | -2   | $\infty$ |
| 3    | 1    | -3   | 0        | 4    | -5   | -8       |
| 4    | -3   | 3    | $\infty$ | 0    | -4   | $\infty$ |
| 5    | 6    | 7    | $\infty$ | 9    | 0    | $\infty$ |
| 6    | 4    | 5    | 12       | 7    | 5    | 0        |

#### (b)

h value is distance to z, $\hat w$ is the number in rectangles.

![](/home/dxh/sophomore/算法/作业/ps12.2.1.png)



final shortest distance:

|      | 1    | 2    | 3        | 4    | 5    | 6        |
| ---- | ---- | ---- | -------- | ---- | ---- | -------- |
| 1    | 0    | 6    | $\infty$ | 8    | -1   | $\infty$ |
| 2    | -1   | 0    | $\infty$ | 2    | -2   | $\infty$ |
| 3    | 1    | -3   | 0        | 4    | -5   | -8       |
| 4    | -3   | 3    | $\infty$ | 0    | -4   | $\infty$ |
| 5    | 6    | 7    | $\infty$ | 9    | 0    | $\infty$ |
| 6    | 4    | 5    | 12       | 7    | 5    | 0        |

### Problem 3

#### (a)

#### 算法描述

跑DFS得到拓扑排序，记录每个点的出度。从s开始按拓扑排序遍历所有点，将出度累乘，记录到cnt里，遍历到t，此时的cnt就是所有路径数

#### 伪代码

```pseudocode
myPathCnt(G,s):
int PathCnt = 1
Run DFS to obtain topological order
for node u in topo order
	int outedge = 0
	if(u == t) 
		break
	for egde (u, v) in G.E
		outedge ++
	PathCnt *= outedge
return PathCnt
```

#### (b)

#### 算法描述

DAGSSSP算法即可

#### 伪代码

```pseudocode
myEarlyStart(G,s):
for node u in G.V
	u.start = INF, u.parent = NIL
s.start = 0
Run DFS to obtain topological order
for node u in topo order
	for edge (u,v) in G.E
		if(v.start > u.start + w(u))
			v.start = u.start + w(u)
			v.parent = u
```

#### (c)

#### 算法描述

即找s到每个点的最长路径，将所有点权取负，权重函数也取负，再次跑DAGSSSP算法计算单源点最短路径，得到每个点权后再将其取负还原即可

#### 伪代码

```
myLateStart(G,s):
for node u in G.V
	u.start = INF, u. parent = NIL
s.start = 0
Run DFS to obtain topological order
for node u in topo order
	for edge (u,v) in G.E
		if(v.start > u.start - w(u))	//权重函数取负
			v.start = u.start - w(u)
			v.parent = u
for node u in topo order 	//还原点权
	u.start *= -1
```

### Problem 4

#### 算法描述

1. 将所有点的距离设置为正无穷
2. 先跑一遍Bellmen-Ford算法，所有未经过环的最短路径都应该被计算出来了，并且属于case 1的点将保持距离为正无穷
3. 再通过找出那些仍然满足`v.dist > u.dist + w(u,v)`的点v（它们属于一个负环），对找出的每一个点单独跑一遍DFS算法，将它能达到的所有点的距离都设置为负无穷（都属于case 2）

#### 正确性证明

​		在步骤二中，通过Bellmen-Ford算法，将所有边都访问n-1次，则和源点s属于同一连通分支的点的距离将一定被设置正确（课上得到证明）。和s不属于同一连通分支的点的距离将保持为`v.dist = max(INF + w(u,v), INF)`，即所有这些点的距离仍然为正无穷。

​		在步骤三中，负环中任意一点的判断正确性显然（课上已证明），对一个负环中得到的任意点，能到达的所有点，都应该属于case 2，它们的距离应该是未良定义的，对它们进行一次访问，设置距离为负无穷，则不会再次被选中（一定不满足`v.dist > u.dist + w(u,v)`），因此这样将最快找出所有未良定义的点。

#### 时间复杂度分析

​		Bellmen-Ford算法用时$O(nm)$，得到的负环中点个数为$O(n)$，对每个点跑一次DFS，用时间复杂度为$O(n)\times O(n+m)=O(n^2+nm)$，因此总时间复杂度为$O(n(n+m))$

### Problem 5

#### (a)

证明：假设存在负环$C_0$满足权值之和为负，则

$\sum_{(i,j)\in C}w_{ij}=r\cdot \sum_{(i,j)\in C} c_{ij}-\sum_{(i,j)\in C}p_{j}<0$

$\therefore r<\frac{\sum_{(i,j)\in C_0}p_{j}}{\sum_{(i,j)\in C_0}c_{ij}}\le\max\limits_{C\ in\ graph\ G}\frac{\sum_{(i,j)\in C}p_{j}}{\sum_{(i,j)\in C}c_{ij}}=r^* $

$\therefore r<r^*$

#### (b)

由(a)同理可得

对任意猜想r在环$C_0$中构造边权：

$\sum_{(i,j)\in C}w_{ij}=r\cdot \sum_{(i,j)\in C} c_{ij}-\sum_{(i,j)\in C}p_{j}>0$

$\therefore r>\frac{\sum_{(i,j)\in C_0}p_{j}}{\sum_{(i,j)\in C_0}c_{ij}}\ge\max\limits_{C\ in\ graph\ G}\frac{\sum_{(i,j)\in C}p_{j}}{\sum_{(i,j)\in C}c_{ij}}=r^* $

$\therefore r>r^*$

#### (c)



### Problem 6

#### (a)

#### 算法描述

​		每次找从当前加油站最远能跑到的站去加油，直到找到终点

#### 伪代码

```pseudocode
FindPathGreedy(D[1,...,n]):
queue nexts = NIL 	//需要经停的加油站编号
nexts.push(1)
current = 1
while(current != n)
	for(i = current + 1; i < n; i ++)
		if(i == n) 
			current = n
			break
		else if(D[i]-D[current] >= 100)  //这里假设至少有一站和本站相隔不到100公里
			current = i - 1
            break
	nexts.push(current)
return nexts
```

#### 时间复杂度分析

本算法将遍历一次所有加油站点，最多会在else if语句中将某些加油站遍历第二次，总时间复杂度为$O(n)$

#### (b)

如图:

![](/home/dxh/sophomore/算法/作业/greedy.png)

#### (c)

#### 算法描述

​		计算每个站点的平均电池开销$P_i=\frac{C[i]}{D[i]}$，再基于贪心算法从距离100公里之内的所有站点中选出平均电池开销最低的站点作为下次的站点，直到找到终点。

#### 伪代码

```pseudocode
FindPathAvg(D[1,...,n],C[1,...,n]):
queue nexts = NIL 	//需要经停的加油站编号
nexts.push(1)
current = 1
while(current != n)
	next = current + 1
	candidate = next
	priceAvg = C[next]/D[next]
	while(D[next]-D[current] <= 100)
		priceAvgNext = C[next]/D[next]
		if(next == )
		else if(priceAvgNext < priceAvg)
			candidate = next
			priceAvg = priceAvgNext
	current = candidate		//100公里之内性价比最高的站点
	nexts.push(current)
return nexts
```

#### 时间复杂度分析

在最坏情况下，只有倒数第二个点距离终点100公里之内，并且倒数第二个点性价比最低，这种情况下若从起点开始每次都遍历到倒数第二个点，总共遍历n-1次它以及它之前的点，终点遍历一次，每次遍历中操作为常数时间，总时间复杂度为$O(n^2)$

### Problem 7

#### 算法描述

1. 假设输入为$A[a,...,b]$
2. 从左向右逐字检查$IsWord(A[a,...,i])$
3. 如果2中返回true，对$A[i+1,...,b]$递归调用本算法
4. 直到$i=b$，返回此时已经得到的所有划分数

#### 伪代码

```pseudocode
WordPartition(A[a,...,b]):
int cnt = 0
if(a == b) 
	cnt += IsWord(A[a])? 1:0
	return cnt
if(IsWord(A[a,...,b])) cnt += 1
for(int i = a; i < b; i ++)
	if(IsWord(A[a,...,i]))
		cnt += WordPartition(A[i+1,...,b])
return cnt
```

#### 时间复杂度分析

当输入字符串长度为1时调用$IsWord$方法1次，长度为2时调用3次（总串一次，两个字母分别各一次）

容易得出递归式$T(n)=n+\sum\limits^n_{i=1}T(n-i),T(0)=0$

$\therefore T(n)=n+(n-1)+2(n-2)+3(n-3)+\cdots+(n-1)(n-(n-1))=\frac{(n-1)n(n+1)}6+n=O(n^3)$

