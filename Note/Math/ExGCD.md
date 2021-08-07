+ 求解关于 $x$,$y$ 的二元一次不定方程 $ax + by = c$。
+ 求解关于 $x$ 的一元一次同余方程 $ax \equiv b \pmod{m}$。

---

显然，方程 $ax + by = \gcd(a,b)$ 当 $a'=\gcd(a,b)$，$b'=0$ 时有解 $x'=1$，$y'=0$。

考虑如何将此解转化为 $a$，$b$ 原始值时的解。
$$
\because \begin{cases}
	a'= b \\
	b'= a \bmod b = a - \left\lfloor \frac{a}{b} \right\rfloor b 
\end{cases} \\
\therefore bx' + (a - \left\lfloor \frac{a}{b} \right\rfloor b)y' =\gcd(a,b) \\
\therefore a \times y' + b \times (x'-\left\lfloor \frac{a}{b} \right\rfloor y') = \gcd(a,b)
$$
至此，我们找到了转化方法：
$$
\begin{cases}
	x=y' \\
	y=x'- \left\lfloor \frac{a}{b} \right\rfloor y'
\end{cases}
$$
通过此方法，我们可得到 $ax + by = \gcd(a,b)$ 的解；

>**裴蜀定理**
>
>关于 $x$,$y$ 的方程 $ax+by = c$ 的充要条件是 $\gcd(a,b)|c$。

所以若有解， $\frac{c}{\gcd(a,b)}$ 必为整数，将 $x$,$y$ 分别乘 $\frac{c}{gcd(a,b)}$ 即可得原方程的解。

若求的是同余方程 $ax \equiv b \pmod{m}$，将其化为 $ax + my = b$ 即可求解。

我们同时可以得到，若求的是 $a$​ 在 $\bmod m$​ 意义下的逆元，即 $ax \equiv 1 \pmod{m}$​，化为 $ax+my = 1$​，即 $\gcd(a,m) = 1$​，即利用 ExGCD 求逆元必须满足 $a$​，$m$​​ 互质。



```cpp
void exgcd(int a,int b,int &x,int &y)
{
	if(b==0)
	{
		x=1,y=0;
		return;
	}

	exgcd(b,a%b,x,y);
	int t=x-(a/b)*y;
	x=y;
	y=t;
}
```
