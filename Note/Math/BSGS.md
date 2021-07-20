求解关于 $x$ 的高次同余方程组 $a ^ x \equiv b \pmod{m}$。

保证 $m \in \operatorname{Prime}$，$a \perp m$。

---

先设定一个值 $q$。

设 $x = pq-r$，$r \in \{1, \dots, q \}$。

则有：
$$
a^{pq-r} \equiv b \pmod{m} \\
a^{pq} \equiv b \times a^r \pmod m \\
$$
因此，将 $b \times a^r$，$r \in \{ 1, \dots, q \}$ 插入 Map 或 HashTable，再枚举 $p \in \{ 1, \dots, \left\lfloor \frac{m}{q} \right\rfloor \}$，在其中查询 $a^{pq}$ 即可。

若寻找到 $a^{qp} \equiv b \times a^r$，则 $x = qp-r$。

易知复杂度为 $O(\max(q,\left\lfloor \frac{m}{q} \right\rfloor))$，所以 $q$ 取 $\left\lceil \sqrt{m} \right\rceil$ 最合适。



```cpp
inline
int bsgs(int a,int b)
{
	if(a%p==0&&b)
	{
		return -1;
	}
	
	int m=ceil(sqrt(p));
	map<int,int> mp;
	mp.clear();

	int s=b;
	for(int i=1;i<=m;i++)
	{
		s=(s*a)%p;
		mp[s]=i;
	}

	int w=quickPow(a,m);
	s=w;
	for(int i=1;i<=m;i++)
	{
		if(mp[s])
		{
			return (i*m-mp[s])%p;
		}
		s=(s*w)%p;
	}

	return -1;
}
```