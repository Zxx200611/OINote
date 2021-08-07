给出一个 $n-1$ 次多项式 $F$，求一个多项式 $R$ 满足 $F \equiv R^2 \pmod{x^n}$​。

系数对 $m$ 取模。

---

当 $n = 1$，即 $n-1=0$ 时易得 $R(x) = q$，$q$ 为 $F[1]$ 在 $\bmod m$ 意义下的二次剩余。

考虑递归处理：假设已经求出 $R' \equiv F \pmod{x^{n/2}}$。
$$
R' \equiv R \pmod{x^{n/2}} \\
R - R' \equiv 0 \pmod{x^{n/2}} \\
R^2 - 2RR' + R'^2 \equiv 0 \pmod{x^n} \\
F-2RR'+R'^2\equiv 0 \pmod{x^n} \\
R \equiv \frac{F+R'^2}{2R'} \pmod{x^n}
$$
问题解决。

