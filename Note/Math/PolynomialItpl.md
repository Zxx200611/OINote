给出 $n$​ 个点 $(x_1,y_1) \dots(x_n,y_n)$​，求一个 $n-1$​ 次多项式 $F$​ 满足 $\forall i \in \{ 1\dots n-1 \}$​，都有 $F(x_i) \equiv y_i$​。

所有的计算对 $998244353$​ 取模。

$1 \le n \le 10^5$。

---

可以使用 Lagrange 插值在 $O(n^2)$​ 复杂度得出结果，但显然无法通过。

观察拉格朗日插值的式子：
$$
\begin{aligned}
F(x) & = \sum_{i=1}^{n} y_i \prod_{j=1,j\ne i}^{n} \frac{x_i-x}{x_i-x_j} \\
     & = \sum_{i=1}^{n} \frac{y_i}{\prod_{j=1,j\ne i}^{n} (x_i-x_j)} \prod_{j=1,j\ne i}^{n}(x-x_j) \\
\end{aligned}
$$
设 $P(x) = \prod_{i=1}^{n} (x-x_i)$​，则 $G(x) = \prod_{j=1,j\ne i}^{n} (x_i-x_j) = \frac{P(x)}{x-x_i}$​​​​。

但是发现当 $x = x_i$ 时 $G(x)$ 无意义，考虑 Lopital 法则：
$$
\lim_{x \rightarrow x_i} G(x) = \lim_{x \rightarrow x_i} \frac{P(x)}{x-x_i} = \lim_{x \rightarrow x_i} \frac{P'(x)}{(x-x_i)'} = \lim_{x \rightarrow x_i} P'(x)
$$
因此，若将 $P$ 求导，得到 $P'$ 后，多点求值即可得到每个 $G(x_i)$​。​

得到 $G(x_i)$​ 之后，考虑分治计算 $F(x)$：设 $F_{l,r}$ 为 $(x_l,y_l) \dots (x_r,y_r)$ 插出的 $F$​。

设 $H_{l,r}(x) = \prod_{j=l}^{r} (x-x_j)$。​

则有：
$$
\begin{aligned}
F_{l,r}(x) & = \sum_{i=l}^{r} \frac{y_i}{G(x_i)} \prod_{j=l,j\ne i}^{r} (x-x_j) \\
           & = F_{l,m}(x) \times \prod_{j=m+1}^{r} (x-x_j) + F_{m+1,r}(x) \times \prod_{j=l}^{m} (x-x_j) \\
           & = F_{l,m}(x) \times H_{m+1,r}(x) + F_{m+1,r}(x) \times H_{l,m}(x)
\end{aligned}
$$
可以递归计算。

边界条件：$l=r$​​​​，$F(x) = \frac{y_l}{G(x)}$​​​​​。​

复杂度 $O(n \log^2 n)$。​