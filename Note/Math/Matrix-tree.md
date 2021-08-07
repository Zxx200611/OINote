求一张图 $G = V + E$ 的生成树个数。

---

定义度数矩阵 $D$，邻接矩阵 $A$。

则此图的拉普拉斯矩阵（Laplacian Matrix）$L$ 为 $D-A$。

将 $L$ 去掉根所在的行，列后，$\det(L)$ 为此图的生成树个数。 



若 $G$ 为无向图，则：
$$
D_{i,j} = \begin{cases}
\deg(i) & i=j \\
0 & i \neq j
\end{cases}
\qquad
A_{i,j} = \begin{cases}
1 & (i \longleftrightarrow j) \in E \\
0 & (i \longleftrightarrow j) \not\in E
\end{cases}
$$
若 $G$ 为有向图，求内向树棵数，则：
$$
D_{i,j} = \begin{cases}
\deg_{out}(i) & i=j \\
0 & i \neq j
\end{cases}
\qquad
A_{i,j} = \begin{cases}
1 & (i \longrightarrow j) \in E \\
0 & (i \longrightarrow j) \not\in E
\end{cases}
$$
若 $G$ 为有向图，求外向树棵数，则：
$$
D_{i,j} = \begin{cases}
\deg_{in}(i) & i=j \\
0 & i \neq j
\end{cases}
\qquad
A_{i,j} = \begin{cases}
1 & (i \longrightarrow j) \in E \\
0 & (i \longrightarrow j) \not\in E
\end{cases}
$$
加权（有重边），则 $\deg$ 改为 $\operatorname{sum}$ 边权和，$A_{i,j}$ 为 $i$ 到 $j$ 的边权。自环直接删去即可。