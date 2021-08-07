给出一个有向无环图 $G = V + E$，保证从点 $1$ 出发可以到达所有点。再给出一条边 $s \rightarrow t$。

问原图 $G$​ 加上这条边后的生成树形图棵数。

注意加上 $s \rightarrow t$ 后图可能有环。

---

考虑一个有向无环图的生成树棵数，由矩阵树定理显然是：
$$
Sp=\prod_{i=2}^{n} \operatorname{ind} (i)
$$
其中 $\operatorname{ind}(i)$​​ 表示编号为 $i$​ 的节点的入度。其实也可以理解成是每一个点选择一个父亲。



那么若成环，会有什么影响？就是算多了一些形如 一个环+一个树状图 的东西，且这个环一定为 $t$​ 至 $s$​ 的一条路径加上 $s \rightarrow t$​。将它们从答案中减掉即可。

那么设 $f[i] = \sum_{R} \prod_{j \not\in R} \operatorname{ind}(j) = \sum_{R} \frac{Sp}{\prod_{j\in R} \operatorname{ind}(j)}$​​​​​​​​​ 为此点若和 $s$​ 成环对答案的负贡献，其中 $R$​​​​​​​​ 为 $i$​​​​​​​​ 至 $s$​​​​​​​​ 的所有路径构成的集合。可以理解为将这个路径加上 $s \to i$​​​​​​ 构成那个环，那么它们的入边就只能选环上的那一条边，相当于将此路径上所有点的入度置为 $1$​​​​​ 后计算答案。

答案就是 $Sp - f[t]$​​​。



考虑计算 $f$​：由于原图是一个 DAG，可以在原图上从 $x$​ 开始 DP。有转移方程：
$$
f[u] = \sum_{R} \frac{1}{\prod_{j \in R} \operatorname{ind}(j)} = \begin{cases}
	\dfrac{\sum_{u \to v \in E} f[v]}{\operatorname{ind}(u)} & u\ne x \\
	\dfrac{Sp}{\operatorname{ind}(u)} & u = x
\end{cases}
$$
那么方法就明确了，从 $x$​​​ 开始按拓扑序倒序 DP（因为若要计算 $f_u$​​ 要先算出 $u$​​ 的所有出边指向的点的 $f$​​）计算 $f$​​，得到答案。

