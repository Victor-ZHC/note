# 图
## 完全图
* 无向图，顶点n，边<=n*(n-1)/2，若取等，则为无向完全图
* 有向图，顶点n，边<=n*(n-1)，若取等，则为有向完全图

## 图的度
* 与顶点关联的边的条数
* 入度：顶点v为终点，ID(v)，即：指向v的边数
* 出度：顶点v为起点，OD(v)
* 顶点度=入度+出度

## 强连通图
* 存在vi->vj, vj->vi的路径，则为强连通图
* 非强连通图的极大连通子图是强连通分量

## 网络
* 带权的连通图

## 图的存储表示
1. 邻接矩阵 Adjacency Matrix
    * 是对称矩阵
2. 邻接表 Linked-adjacency Lists
3. 邻接多重表 Adjacency multilist

## 图的遍历与连通性
* 遍历树
    * 深度优先遍历（先根、后根）
    * 广度优先遍历
* 遍历森林
    * 深度优先遍历（先根、中根、后根）
    * 广度优先遍历
* 遍历图
    * 深度优先遍历DFS（Depth First Search）
    ```
    void dfs( Vertex v ) {
        v.visited = true;
        for each w adjacent to v
            if( !w.visited )
                dfs(w);
    }
    ```
    * 广度优先遍历BFS（Breadth First Search）

## 最小生成树算法
* 都采用逐步求解的策略，n个顶点
    * Prim
        * 从任意边长为1的起点开始，依次选择权值最小的边，且不和已有边构成回路
    * Kruskal
        * 边排序，选择代价最小的边并且不和已有边构成回路，直至加满n-1条边
        * 取最小边利用：最小堆，判断是否构成回路，利用：并查集

## 最短路径（shortest path）
* Dijkstra算法
    * 按最短路径长度递增的次序产生最短路径
    * 首先，在从源点出发的直线中找最短直线相应的顶点，然后去掉该点，从剩余点中选择最短path

## 活动网络（Activity Network）
* 用顶点表示活动的网络（AOV网络 Activity On Vertex network）
    * 用顶点表示活动，用弧表示活动间的优先关系的有向图
    * 拓扑排序（Topological Sort）
        * 有向图G=(V,E)，V里结点的线性序列(Vi1,Vi2,...,Vin)若满足：在G中从结点Vi到Vj有一条路径，则序列中结点Vi必先于结点Vj，称这样的线性序列为：拓扑序列
        * 算法：依次删点和出边
* 用边表示活动的网络（AOE网络）
    * 用边表示活动的网络
        * 入边表示活动已完成，出表表示活动可以开始

[返回目录](../CONTENTS.md)