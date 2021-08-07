给出一个 $n-1$ 次多项式 $F(x)$，求一个多项式 $G(x)$ 满足：
$$
G(x) \equiv e^{F(x)} \pmod{x^n}
$$
系数对 $998244353$ 取模。

---

两边 $\ln$ 得：$\ln G(x)-F(x) \equiv 0 \pmod{x^n}$​。

所以需找到一个多项式 $G$​ 满足 $H(G(x)) \equiv \ln G(x) - F(x) \equiv 0$ 即可。

根据牛顿迭代公式：
$$
\begin{aligned}
F(G_0(x)) \equiv 0 \pmod{x^{n/2}} \\
\Rightarrow G(x) \equiv G_0(x) - \frac{F(G_0(x))}{F'(G_0(x))} & \pmod{x^n}
\end{aligned}
$$
易得：
$$
\begin{aligned}
G(x) & \equiv G_0(x) - \frac{H(G_0(x))}{H'(G_0(x))} \\
     & \equiv G_0(x) - \frac{\ln G_0(x) - F(x)}{\frac{1}{G_0(x)}-F'(x)} \\
     & \equiv G_0(x) - \frac{G_0(x) \ln G_0(x) - G_0(x)F(x)}{1 - G_0(x)F'(x)} \\
     & \equiv G_0(x) \times \left( 1 - \frac{\ln G_0(x) - F(x)}{1 - G_0(x) F'(x)} \right)
\end{aligned}
$$
