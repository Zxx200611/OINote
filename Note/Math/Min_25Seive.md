给出一个积性函数 $f$​，满足 $f(p) = \sum_{i=1}^{m} a_i p^i,p \in \mathbb{P}$ 且 $m$ 非常小（即 $f$​ 在质数处的取值为一个低次多项式）。

再给出 $n$​，求​：
$$
S(n) = \sum_{i=1}^{n} f(i) \pmod{10^9+7}
$$
$n\le 10^{11}$。

---

首先将 $f$​ 在质数处的取值多项式 $f(p)$​​ 拆成一堆单项式。这样就只用考虑 $f_k(p) = p^k$​ 的形式，最后再每一项加起来即可。

定义 $\operatorname{lpf}(x)$ 为 $x$ 的最小质因子，将 $x$ 取合数和质数分类讨论，易得：
$$
S(x) = \sum_{p \in \mathbb{P},p\le x} f(p) + \sum_{p \in \mathbb{P},p\le \sqrt x} \sum_{e=1}^{\log_p x} f(p^e) \left( \sum_{i\le n/p^e \& \operatorname{lpf(i)} > p} f(i) + [e \ne 1] \right)
$$
设 $g_k(n,j) = \sum_{i=1}^{n} i^k [i\in \mathbb{P} \operatorname{or} \operatorname{lpf}(i) > p_j]$​​​​​​​，$S_k(n,j) = \sum_{i=1}^{n} f_k(i) [\operatorname{lpf}(i) > p_j]$​​​​​​​​​，$Sp_k(j) = \sum_{i=1}^{j} f_k(p_i)$​。​​其中 $p_j$​​​ 表示从小到大第 $j$​​​​ 个质数。

结合上面的式子，设 $h(n)$ 表示小于等于 $n$ 的质数个数，可以得到 $S_k(n,j)$ 的另外一种和 $g_k(n,j)$ 有关的形式：
$$
\begin{aligned}
S_k(n,j) & = \sum_{p \in \mathbb{P},p\le x} f(p) + \sum_{p \in \mathbb{P},p\le \sqrt x} \sum_{e=1}^{\log_p x} f(p^e) \left( \sum_{i\le n/p^e \& \operatorname{lpf(i)} > p} f(i) + [e \ne 1] \right) \\
         & = g_k(n,h(\sqrt n)) - Sp_k(j) +\sum_{p_d \ge p_j} f(p_d^e) \left( \sum_{i\le n/p_d^e \& \operatorname{lpf(i)} > p_d} f(i) + [e \ne 1] \right) \\
         & = g_k(n,h(\sqrt n)) - Sp_k(j) +\sum_{p_d \ge p_j} f(p_d^e) \left( S_k\left( \left\lfloor \frac{n}{p_d^e} \right\rfloor ,d \right) + [e \ne 1] \right) \\
\end{aligned}
$$
可以递归计算。



那么考虑计算 $g_k$：
$$
g_k(n,j) = \begin{cases}
	g_k(n,j-1) & p_j^2 > n \\
	g_k(n,j-1) - p_j^k (g_k(n/p_j,j-1) - g_k(p_{j-1},j-1)) & p_j^2 \le n
\end{cases}
$$
可以理解为：

+ $p_j^2$ 大于 $n$ 的质数实际上不会有任何用，因为筛不掉任何数。
+ $p_j^2$ 小于 $n$ 的质数会筛掉部分数，将这些数全提出来一个 $p_j^k$ 后就是 $g_k(n/p_j,j-1)$​​，但是还多去掉了小于等于 $p_{j-1}$ 的所有质数，需要再加回来。



那么在一开始先处理出质数处的 $g$ 和 $g(i,0)$ 就可以快速处理 $g$，进而快速得到 $S$​。

有时候给出的 $f$ 是一个函数而不是多项式。此时需要相应地修改求 $g$ 的部分。

