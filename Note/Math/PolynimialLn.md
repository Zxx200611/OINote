给出一个 $n-1$​ 次多项式 $F(x)$​，求一个多项式 $G(x)$​ 满足：
$$
G(x) \equiv \ln F(x) \pmod{x^n}
$$
对 $998244353$ 取模。

---

两边同时求导，有：
$$
G(x) \equiv \ln F(x) \pmod{x^n} \\
G'(x) \equiv (\ln'F(x))\times F'(x) \pmod{x^ n} \\
G'(x) \equiv \frac{F'(x)}{F(x)} \pmod{x^n}
$$
两边再同时积分：
$$
G(x) \equiv \int \frac{F'(x)}{F(x)} \pmod{x^n}
$$
那么就只用求逆 + 乘法 + 求导 + 积分即可算出 $G$。

复杂度为求逆的 $O(n \log^2 n)$​。​