给出一个 $01$ 矩阵，若在相邻的 $1$ 之间连边，此无向图中不存在环（即矩阵中的 $1$ 构成森林）。

每次询问一个子矩阵 $(x_a,y_a)$ 至 $(x_b,y_b)$ 中包含的 $1$ 构成的连通块个数，多组询问。

---

考虑答案的组成：切出一个子矩阵，其中的所有连通块一定还是一些树所构成的森林。

对于森林有一个性质：设森林 $G$ 中包含的树集为 $T_G$，所包含的点集为 $V_G$，所包含的边集为 $E_G$，则有：
$$
|T_G| = |V_G| - |E_G|
$$
非常的显然，但是较难想到。



那么现在需要的就是求：

+ 此子矩阵中含有的 $1$ 的个数。
+ 此子矩阵含有的 $1$ 之间的边数。

第一个很简单，一个二维前缀和即可。

第二个比较麻烦。考虑一个 $1$ 周围，只能有横向边和竖向边，那么可以将这两种边分别做二维前缀和。

至此此题做完。