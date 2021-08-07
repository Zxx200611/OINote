求解关于 $x$ 的线性同余方程组：
$$
\begin{cases}
x \equiv a_1 \pmod{m_1} \\
x \equiv a_2 \pmod{m_2} \\
\qquad \vdots \\
x \equiv a_3 \pmod{m_3} \\
\end{cases}
$$
保证 $\forall i,j \in \{ 1\dots n \}$，$m_i \perp m_j$。

---

设 $M = \operatorname{lcm}_{i=1}^{n} m_i$，$M_i = \frac{M}{m_i}$。

对于第 $i$ 条方程，我们构造出一个解 $t_i$，满足 $M_i t_i \equiv 1 \pmod{m_i}$。

则有：
$$
\begin{cases}
a_i M_i t_i \equiv a_i \pmod{m_j} & j=i \\
a_i M_i t_i \equiv 0 \pmod{m_j} & \operatorname{otherwise}
\end{cases}
$$
则 $x = \sum_{i=1}^{n} a_i M_i t_i$ 为此方程组的一个解。通解为 $x+Mk$，$k$ 属于整数。



```cpp
struct Equation		//x=a (mod m)
{
	int a;
	int m;
};
inline
int crt(vector<Equation> eqs)
{
	int M=1;
	for(int i=0;i<eqs.size();i++)
	{
		M=M/gcd(M,eqs[i].m)*eqs[i].m;
	}

	int ans=0;
	for(int i=0;i<eqs.size();i++)
	{
		int Mi=M/eqs[i].m;
		int ti=inv(Mi,eqs[i].m);
		ans+=(((eqs[i].a*Mi)%M)*ti)%M;
		ans%=M;
	}

	return ans;
}
```

