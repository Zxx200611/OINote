给出两个 $n-1$​ 次多项式 $F$​ 和 $G$​，求 $F \times G$​。

---

暴力计算复杂度为 $O(n^2)$，无法通过。

考虑多项式的点值表示，通过 $F$ 和 $G$ 的点值表示求 $F \times G$ 的点值表示复杂度仅为 $O(n)$，所以要是能找到低于 $O(n^2)$ 的复杂度将系数表示转化为点值表示，问题并迎刃而解。

考虑将 $n$ 次单位根 $\omega_n$ 代入 $F$，$F(x)=\sum_{i=0}^{n-1} F[i]x^i$。首先将 $F$​ 拆成两个部分：奇次 $Fl$ 和偶次 $Fr$。
$$
Fl(x)= \sum_{i=0}^{n/2-1} F[2i]x^2 \qquad Fr(x)=\sum_{i=0}^{n/2-1} F[2i+1]x^2 \\
\Rightarrow F(x) = \sum_{i=0}^{n/2-1} F[2i]x^2 + x\sum_{i=0}^{n/2-1} F[2i+1]x^2 = Fl(x)+xFr(x)
$$
若我们现在有 $Fl$​​ 和 $Fr$​​ 在 $\omega_{n/2}^{k}, 0 \le k \le \frac{n}{2}-1$​​​​ 处的点值，好像是可以比较快地求出 $F$ 在 $\omega_{n}^{k}, 0 \le k \le n-1$ 处的点值。

具体怎么做呢？

1. 小于 $n/2$ 处的点值，$0 \le k \le n/2$。
    $$
    \begin{aligned}
    F(\omega_{n}^{k}) & = Fl((\omega_{n}^{k})^2) + \omega_n^k Fr((\omega_{n}^{k})^2) \\
                      & = Fl(\omega_{n/2}^{k}) + \omega_n^k Fr(\omega_{n/2}^{k}) \\
    \end{aligned}
    $$


2. 大于等于 $n/2$​ 处的点值，$0 \le k \le n/2$。
    $$
    \begin{aligned}
    F(\omega_{n}^{k+n/2}) & = Fl((\omega_{n}^{k+n/2})^2)+\omega_{n}^{k+n/2}Fr((\omega_{n}^{k+n/2})^2) \\
                          & = Fl(\omega_{n/2}^{k}) - \omega_{n}^{k} Fr(\omega_{n/2}^{k})
    \end{aligned}
    $$

综上，我们得到了 $F$ 在 $\omega_{n}^{k}, 0 \le k \le n-1$ 处的点值：
$$
F(\omega_{n}^{k}) = \begin{cases}
Fl(\omega_{n/2}^{k}) + \omega_n^k Fr(\omega_{n/2}^{k}) & k < n/2 \\
Fl(\omega_{n/2}^{k}) - \omega_{n}^{k} Fr(\omega_{n/2}^{k}) & k \ge n/2
\end{cases}
$$
那么，只需每次将 $F$ 分为 $Fl$，$Fr$，递归地计算后合并即可，递归边界是 $n=1$，此时直接返回。

