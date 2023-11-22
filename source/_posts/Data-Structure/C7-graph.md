---
title: 数据结构和算法-图
tags:
  - algorithm
categories:
  - Data-Structure
mathjax: true
---
# 7.2 图的定义
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090355732.png)
图( Graph )是由顶点的有穷非空集合和顶点之间边的集合组成,通常表示为: G ( V, E ) ,其中, G 表示一个图，V 是图 G 中顶点的集合，E 是图 G 中边的集会。V standards for vertices (also called nodes or points), E standards for edges (also called links or lines).
重点：
- 线性表中我们把数据元素叫元素,树中将数据元素叫结点 ,在图中数据元素,我们则称之为顶点(Vertex)；
- 顶点集合 V 有穷非空；
- 图中，任意两个顶点之间都可能有关系，顶点之间的逻辑关系用边来表示，边集可以是空的。
## 7.2.1 各种图定义
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090413505.png)
- 无向边：若顶点 $v_i$ 到 $v_j$ 之间的边没有方向,则称这条边为无向边( Edge),用无序偶对 $(v_i,v_j)$ 来表示。如果图中任意两个顶点之间的边都是无向边,则称该图为无向图( Undirected graphs)。图 7-2-2 就是一个无向图,由于是无方向的,连接顶点 A与 D 的边,可以表示成无序对 (A,D), 也可以写成 (D,A).
- 对于图 7-2-2 中的无向图 $G_1$ 来说, $G_1= (V_1,\{E_1\})$, 其中顶点集合 $V_1=\{A,B,C,D\}$；边集合 $E_1=\{ ( A,B ),(B,C) , (C,D),( D,A ) , ( A,C) \}$
- 有向边：若从顶点 $v_i$ 到 $v_j$ 的边有方向,则称这条边为有向边,也称为弧( Arc )。用有序偶 $<v_i,v_j>$ 来表示, $v_i$ 称为弧尾( Tail ) , $v_j$ 称为弧头( Head ) 。 如果图中任意两个顶点之间的边都是有向边,则称该因为有向图( Directed graphs) . 
- 对于图 7-2 -3 中的有向图 $G_2$ 来说, $G_2= ( V_2,\{E_2\} )$,其中顶点集合 $V_2 =\{A,B,C,D\}$ ;弧集合 $E_2=\{<A,D>,<B,A>,<C,A>,<B,C>\}$ 
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090438091.png)
- 简单图：不存在顶点到其自身的边，且同一条边不重复出现的图。图 7-2-4 中的两个图不属于简单图。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090441184.png)
- 无向完全图：任意两个顶点之间都存在边的无向图；含有 n 个顶点的无向完全图 $\frac{n(n-1)}{2}$ 条边。比如图 7-2-5 就是无向完全图
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090443838.png)
- 在有向图中,如果任意两个顶点之间都存在方向互为相反的两条弧,则称该图为有向完全图 。含有 n 个顶点的有向完全图有 n ×( n -1 )条边,如图 7-2-6 所示 。
- 有很少条边或弧的图称为稀疏图 , 反之称为稠密图。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090447222.png)
- 网( Network)：有些图的边或弧具有与它相关的数字,这种与图的边或弧相关的数叫做权(Weight)，网就是带权的图。图 7-2-7 就是一张带权的图,即标识中国四大城市的直线距离的网,此图中的权就是两地的距离。
![image.png](https://illyber-images.oss-cn-chengdu.aliyuncs.com/202307090448949.png)
假设有两个图 $G= (V,\{E\})$和 $G’= (V',\{E’\})$,如果 $V'\subseteq V$ 且 $E'\subseteq E$ ,则称 G'为 G 的子图（subgraph）。例如图 7-2-8 带底纹的图均为左侧无向图与有向图的子图。
## 7.2.2 图的顶点与边间关系
- 对于无向图 $G= (V,\{E\})$ , 如果边 $(v,v')\in E$ , 则称顶点 v 和 v’互为邻接点( Adjacent),即 v 和 v’相邻接。 边 $(v,v')$ 依附 ( incident)于顶点 v 和 v’ ,或者说 $(v,v')$ 与顶点 v 和 v’相关联。 顶点 v 的度 ( Degree )是和 v 相关联的边的数目 ,记为TD(v) 。 $e=\frac{1}{2}\sum_{i=1}^nTD(v_i)$
- 对于有向图 $G= (V,\{E\})$ ,如果弧 $<v,v'>\in E$ ,则称顶点 v 邻接到顶点 v’ , 顶点 v'邻接自顶点 v. 弧 $<v,v'>$ 和顶点 v , v’相关联。以顶点 v 为头的弧的数 目称为 v 的入度( lnDegree) , 记为 ID (v);以 v 为尾的弧的数目称为 v 的出度( OutDegree),记为OD( v ) ;顶点 v 的度为 TD(v) =ID(v) +OD(v) 。$e=\sum_{i=1}^nID(v_i)=\sum_{i=1}^nOD(v_i)$
- 顶点序列：
## 7.2.3 连通图相关术语
## 7.2.4 图的定义与术语总结
# 7.3 图的抽象数据类型
# 7.4 图的存储结构
