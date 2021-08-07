有 $n$ 家烧烤店编号从 $1$ 到 $n$。第 $i$ 家与第 $i+1$ 家距离 $d_i$。走 $1$ 单位的路愉悦度会减少 $1$。

还有 $m$ 张餐票。在第 $i$ 家烧烤店使用第 $j$​ 张餐票 可以获得 $A_{i,j}$​ 的愉悦度。

求从任意一家烧烤店开始可以获得的愉悦度最大值。

---

易得最优方案一定是单向地走完一个区间 $[l,r]$ 且在此区间第 $j$​​ 张餐票价值最高的店消费这张餐票。

可以得到一个 $O(n^2m)$ 的做法：枚举区间和每一张票，所有票的价值最大值取 $\max$ 后加起来。显然不能过。



不妨设是从左到右走。观察得到若设 $B_i$ 为在第 $i$ 家店结束的最优开始点，则 $B_i$ 随 $i$ 的增大而增大。换句话说，就是满足决策单调性。（其实不一定叫这个，但是差不多。

那么对于一家店 $i$，假设我们已经求出了 $B_i$。那对于所有 $j < i$，有 $B_j \le B_i$。对于所有 $j > i$，有 $B_j \ge B_i$。

于是可以使用类似于整体二分的方法：若现在正在求店 $l \dots r$ 的最优开始点且知道答案在 $a\dots b$ 中，可以先求出 $m = \lfloor\frac{l+r}{2}\rfloor$ 的最优开始点 $k$。这样一来，店 $l \dots m-1$ 的最优开始点一定小于等于 $k$。右边同理。可以递归地计算。

最后若 $l=r$，就把 $a \dots b$​ 扫一遍求 $\max$。

于是复杂度就是 $O(nm \log n)$，可以通过。

需要使用 St 表来 $O(1)$​ 得到区间最大值。



经验：

+ 代价与距离相关的，可以往决策单调性方面想。

+ 可以使用类似整体二分的方法解决决策有单调性的问题。