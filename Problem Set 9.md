<center>
<h1>
    Problem Set 9
    </h1>
    <p1>人工智能学院 201300096 杜兴豪</p1>
</center>
### Problem 1

#### (a)

![](/media/dxh/共享文件夹/sophomore/算法/作业/tree.png)

#### (b)

![](/media/dxh/共享文件夹/sophomore/算法/作业/tree.png)

### Problem 2

#### (a)









#### (b)

|       | WHITE                   | GRAY                    | BLACK                   |
| ----- | ----------------------- | ----------------------- | ----------------------- |
| WHITE | tree/cross/forward/back | cross/back edge         | back edge               |
| GRAY  | tree edge               | tree/cross/back/forward | cross                   |
| BLACK | \                       | \                       | tree/cross/forward/back |

#### (c)









### Problem 3

#### 	方法

​		修改DFS：在深度优先遍历中，为每一个被访问的点赋值，值为DFS传入的参数(`MyDFS(G, s, flag)`其中flag是为每一个点赋的值，即$v.cc = flag$)。

​		识别连通分量方法：对图G中每一个白色节点进行DFS，并为其赋编号值，成功赋值一次之后更新传入的编号值。

#### 	伪代码

```
Identify(G,V):
int flag = 1
for all node in V:
    if(node.color == white)
    	MyDFS(G, node, flag)
    	flag ++
```

易知该方法遍历所有点至多1次，至多遍历每一条边一次，时间复杂度为$O(|V|+|E|)$

### Problem 4

#### (a)

​	证明：

​		归纳奠基：当树只有1或2个顶点时，显然

​		归纳步骤：假设$|V|\le k$时结论成立。当$|V|=k+1$时，取G的一个叶节点$s$，易知仅有一个顶点$v$和其连通，令该边为$e$。断开$e$。原图G变成一个点数为$|V'|=k+1-1=k$的图G'和一个单点树$s$组成的森林。由归纳奠基，G'可以成功分为L和R两个部分。因为$v\sub V'$，所以一定有$v$在L或R中，无妨令其处于L中。则将$s$划归到R中，原性质得以满足。结论成立。

#### (b)

​	证明：

​		由每个环都有偶数个顶点知，所有环可以平均分为上下两部分，所有边均在部分之内（横向），垂直于部分之间、或斜向于部分之间（竖向）。先考虑横向和竖向情况。





​		（1）如图，竖边满足两顶点相对位置一致。则若将横边所处两顶点中的一个和它对应位置处于另一部分的点对换位置（同时带动边移动），则不影响竖边，但此时被交换的点的所有边已经处于斜边状态。按照此方法隔一点交换一次位置，则全部结束后所有边均位于两部分中间，没有横边。则得到均分的两部分。





​		（2）考虑初始时的斜边。因为所有子图均应含有偶数个顶点，那么一条斜边的两个端点之间应含有一个最小的子图，且为偶数顶点的。而其中一点已经在另一部分，则剩余的所有在同一部分的点应剩下奇数个，此时若进行步骤1，则可以保证该斜边两端均不会被翻转，性质保持不变。此外，同部分相邻点若都存在斜边，则容易知道可以通过旋转（将一部分的头放入另一部分，再将另一部分的尾放入这一部分）将这两条斜边转化为一条或0条。因此结论成立。

​		对于该环的两端连点，同样通过这个方法进行分组：和上部分相连的点移入下部分，由（1）知这可以做到。

​		由此方法则将该图分为上下两部分，所有边均在两部分之间。

#### (c)

#### 算法描述

从一个节点开始，把它放入集合A，把所有和其相连的点放入B。之后再遍历这些点，将所有和该点相连，但没有被访问过的点放入和该点不同的集合中，并判断已经被访问过的点是否在该点的同一集合中，若是，返回false，此图不是二部图，否则继续遍历，直到没有未被访问过的点，返回true，结束算法。

#### 伪代码

```
//一些预处理工作
	node s //randomly given
	s.visited = true
	set[2]// set of sets,set[0] = L, set[1] = R
	set[1].push(s)
	s.flag = 1// number of the set contains s

//主函数
Bipartite(G, s)
	new stack n
	for (s, v) in E
		if(v.visited == false)		//将该点添加到s点的异侧
			n.push(v)//to be visited
			v.visited = true
			v.flag = (s.flag + 1) % 2
			set[v.flag].push(v)
		else 
			if(v.flag == s.flag)	//该点已经被添加到了s点的同侧
				return false
	while(n.size() > 0)
		v = n.top() 
		n.pop()
    	Bipartite(G, v)
    return true
	
```

算法在遍历过程中，遇到不符合条件的就会立即返回退出。并且在遍历时，仅仅会将所有点遍历至多一次，所有边至多2次，所以时间复杂度为$O(|V|+|E|)$

### Problem 5

#### 	伪代码

```
FindFlag(x, y):
	return maze(x,y)
	
BuildNode(pos):
	node child
	child.pos = pos
	child.flag = FindFlag(pos)
	child.visit = 0 //important
	return child
	
FindChild(node, visitedlist):
	//	node.pos=(x,y),node.flag
	avapos = [(node.flag,0),(-node.flag,0)(0,node.flag),(0,-node.flag)]		//available choices
	for( position in avapos)
		newpos = node.pos + position
		if((newpos in maze) and (newpos not in visitedlist))
			newnode = BuildNode(newpos)
			node.children.add(newnode)

BuildGraph(maze):
	nodemap = null	//key:pos val:node
		for(pos in maze)
			if(pos not in nodemap.key())
				nodemap[pos] = BuildNode(pos)
				FindChild(nodemap[pos])
				for(child in nodemap[pos].children)
					nodemap.insert(child,child.pos)
	return nodemap
```

```
FindWay(maze,oripos,tarpos):
nodemap = BuildGraph(maze)
for i = 1 to n * n
	record = 0	//current shortest path
	DFS(nodemap, nodemap[oripos])	//do nothing to the nodes
	node = nodemap[tarpos]
    while(node != null)		//oripos has null parent
    	node.visit ++
    	node = node.parent
    	cnt ++
    	if(cnt > n*n) break //没有从起点到终点的路径
    cnt = cnt > n*n ? 0 : cnt
    if(cnt != 0) record = record <= cnt ? record : cnt // 按照成功的遍历更新record
```

注：在进行DFS时，尽量选择被访问次数最少的节点，并且在一次成功的遍历之后，会将路径上所有点的访问次数+1

每次DFS将生成一条不重复的树，至多n平方次后一定能找出所有的生成树，挑选出最小值返回。

#### 分析时间复杂度

建图用时为$O(n)$，每次DFS将至多遍历所有节点一次，为$O(n)$的，循环至多进行n平方次，则总时间复杂度为$O(n^3)$



### Problem 6

```
Findnext(G, u):
	nextlist = null
	for all (u,v) in E
		switch(u.color)
		case red: 
			if(v.color == white) 
				nextlist.add(v)
                continue
        case white:
            if(v.color == blue)
            	nextlist.add(v)
            	continue
        case blue:
        	if(v.color == red)
        		nextlist.add(n)
        		continue
     return nextlist
     
BuildGraph(G，u):
while(true)
	node = u
	for all (u, v) in V:
		node = v
		u.nexts = Findnext(G, node)
	if(u == node) break
	else u = node
```

```
FindFrench(G, v):
	BuildGraph(G, v)
	if (v.next == null) return v // 叶节点
	french = null // list to hold vertices
	french.push(v)
	node = v.nexts.pop()//delete node from v.next
	french.push(node)
	while(v.nexts.size() != 0)
		if(node.nexts == null)	//新节点
			node.nexts = Findnext(G,node)
            continue
		else if (node.nexts.size() == 0)
			= node.parent
		else
			node = node.nexts.pop()
			if(node in french)
				node = node.parent//重新弹出一个孩子
			else 
				french.push(node)
	return french
```

算法和DFS类似，会生成以v为根的子树，也即遍历从v出发的所有边，找到french flag walk节点。因为有查重复的操作，所以每个节点至多被遍历一次（被加入french后将不再遍历它），所以时间复杂度为$O(|V|+|E|)$

