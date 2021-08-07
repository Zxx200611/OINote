给出一个 $n-1$ 次多项式 $F$，求一个多项式 $G$ 满足 $F \times G \equiv 1 \pmod{x^n}$​。

---

由于当 $n=1$，即 $n-1=0$ 时问题非常简单，考虑递归求解。

假设已经求出 $F \times G' \equiv 1 \pmod{x^{n/2}}$，如何求出 $G$ 呢？
$$
G \equiv G' \pmod{x^{n/2}} \\
G - G' \equiv 0 \pmod{x^{n/2}} \\
G^2 - 2GG' + G'^2 \equiv 0 \pmod{x^{n}} \\
G - 2G' + G'^2F \equiv 0 \pmod{x^n} \\
G \equiv 2G' - G'^2F \pmod{x^n}
$$
问题解决。