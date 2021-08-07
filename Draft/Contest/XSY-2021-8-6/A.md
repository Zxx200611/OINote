给出三个正整数 $b$，$d$，$n$。求：
$$
\left\lfloor \left( \frac{b + \sqrt{d}}{2} \right)^n \right\rfloor \bmod 999999999999999989
$$
的值。

$n \le 10^8$​​，$b \bmod 2 = 1$​​，$d \bmod 4 = 1$​​，$b^2 \le d < (b+1)^2$​。

---

观察到 $(b+\sqrt{d})^n$ 的形式，可以配上一个 $(b-\sqrt d)^n$​ 构造对称基底。

设出 $f(n)$：
$$
\begin{aligned}
f(n) & = \left( \frac{b + \sqrt{d}}{2} \right)^n + \left( \frac{b - \sqrt{d}}{2} \right)^n \\
\end{aligned}
$$
根据对称基底知识 $a^n + b^n = (a^{n-1} + b^{n-1})(a + b) - ab(a^{n-2} + b^{n-2})$​​ 有：
$$
f(n) = f(n-1)\times b - f(n-2) \times \frac{b^2 - d}{4}
$$
得到了 $f$​​ 的递推式。由于 $b \bmod 2 = 1$​​，$d \bmod 4 = 1$​​​，$\frac{b^2-d}{4}$​​ 一定是整数。又因 $f(0)$，$f(1)$ 为整数，根据数归易证 $f$​ 一定是整数。

那么就可以使用矩阵快速幂算出 $f$。

得到 $f$​​ 后，答案就是 $\left\lfloor f(n) - g(n) \right\rfloor$，其中 $g(n) = \left( \frac{b - \sqrt{d}}{2} \right)^n$。

由于 $b^2 \le d < (b+1)^2$​​，即 $g(n)$​​ 为 $0$​​ 或某个绝对值小于 $1$​​​ 的值。可以分类讨论：
$$
g(n) = \begin{cases}
0 & b^2=d \operatorname{or} (b^2 \ne d \operatorname{and} n \bmod 2 = 0) \\
1 & \operatorname{otherwise}
\end{cases}
$$


