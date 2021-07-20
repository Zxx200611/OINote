求关于 $x$ 的同余方程组
$$
\begin{cases}
	x \equiv a_1\pmod{m_1} \\
	x \equiv a_2\pmod{m_2} \\
	x \equiv a_3\pmod{m_3} \\
	\qquad \vdots \\
	x \equiv a_n\pmod{m_n} \\
\end{cases}
$$

的解。

---

记前 $i-1$ 组方程的解为 $x$,$M=\operatorname{lcm}_{j=1}^{i-1}m_j$,则其有通解 $x+Mk$。

则需找出一个 $k$ 满足 $x + Mk \equiv a_i \pmod{m_i}$。

将此方程化为 ExGCD 可以求解的形式：$Mk + m_i y = a_i-x$，由于此时 $M$,$m_i$ 不一定互质，还不能简单地使用 ExGCD。

设 $g = \gcd(M,m_i)$，方程两边同除 $g$，得 $\frac{M}{g}k + \frac{m_i}{g} y = \frac{a_i-x}{g}$，由裴蜀定理，若有解，$\frac{a_i-x}{g}$ 必为整数，此时可以用 ExGCD 求解，得到的结果乘 $\frac{a_i-x}{g}$ ，即为 $k$。



```cpp
inline
int excrt(int n)
{
	int M=1,x=0;
	for(int i=1;i<=n;i++)
	{
		int g=gcd(M,m[i]);
		int md=m[i]/g;

		if((a[i]-x)%g!=0)
		{
			return -1;
		}

		int inv,tmp;
		exgcd(M/g,m[i]/g,inv,tmp);
		inv=(inv%md+md)%md;
		int k=(a[i]-x)/g*inv;
		k=(k%m[i]+m[i])%m[i];

		x+=mul(M,k,M/g*m[i]);
		M=m[i]/g*M;
		x=(x%M+M)%M;
	}
	return x;
}
```

