有一个 $n \times m$​ 的棋盘，用 $c$​ 种颜色染色，每个格子可以染可以不染，满足以下条件：

+ 每行，每列都有格子有颜色。
+ 每种颜色都被使用。

求合法方案数。

---

考虑容斥，枚举至少不染的行，列，颜色数，可得：
$$
\begin{aligned}
Ans & = \sum_{i=0}^{n} \sum_{j=0}^{m} \sum_{k=0}^{c} (-1)^{i+j+k} \binom{n}{i}\binom{m}{j}\binom{c}{k} (c-k+1)^{(n-i)(m-j)} \\
    & = \sum_{i=0}^{n} (-1)^i \binom{n}{i} \sum_{k=0}^{c} \binom{c}{k}(-1)^k \sum_{j=0}^{m} \binom{m}{j} (-1)^j (c-k+1)^{(n-i)(m-j)}
\end{aligned}
$$
将后面的 $\sum_{j=0}^{m} \binom{m}{j} (-1)^j (c-k+1)^{(n-i)(m-j)}$ 使用二项式定理收起来得：
$$
Ans = \sum_{i=0}^{n} (-1)^i \binom{n}{i} \sum_{k=0}^{c} \binom{c}{k}(-1)^k ((c-k+1)^{n-i}-1)^m
$$


直接 $O(nc \log m)$ 计算即可。



经验：

+ 对于一些难以直接算的题，可以考虑容斥。
+ 看到 $\sum_{i=0}^{n} \binom{n}{i} a^i b^{n-i}$​ 的形式可以想到二项式定理。

