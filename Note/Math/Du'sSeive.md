给出 $n$ 和一个积性函数 $f$，在亚线性复杂度内求出：
$$
\sum_{i=1}^{n}f(i)
$$
---

找到一个积性函数 $g$，满足 $f * g = h$，则有：
$$
\begin{aligned}
\sum_{i=1}^{n} h(i) & = \sum_{i=1}^{n} \sum_{d|n} f(d) g\left( \frac{n}{d} \right) \\
	 & = \sum_{d=1}^{n}  g(d) \sum_{i=1}^{n/d} f(i) \\
	 & = \sum_{i=1}^{n} g(i) S\left( \left\lfloor \frac{n}{i} \right\rfloor \right)
\end{aligned}
$$
考虑要求的 $S(n)$，式子中只有 $i=1$​ 时右式中有它，将它拿出来：
$$
g(1) S(n) = \sum_{i=1}^{n}h(i) - \sum_{i=2}^{n} g(i) S\left( \left\lfloor \frac{n}{i} \right\rfloor \right)
$$
可以对 $\left\lfloor \frac{n}{i} \right\rfloor$​ 整除分块，此时若可以快速计算 $\sum_{i=1}^{n} g(i)$，$\sum_{i=1}^{n} h(i)$​，则可以递归计算 $S$。

因为递归后计算的是 $\left\lfloor \frac{n}{ij} \right\rfloor$ 的​形式，已经被算过了，所以可以记忆化搜索。

