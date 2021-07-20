有 $n$ 堆石子，第 $i$ 堆有 $A_i$ 个。

两个人 A，B 轮流取石子，每次可以选不多于 $k$ 堆，在每堆中取走任意个数的石子，没得取的输。

问先手 A 必胜还是必败。

---

设 $S_j = \sum_{i=0} A_i \land 2^j$，即把所有 $A_i$ 二进制第 $j$ 位加起来。

则结束状态的 $S$ 总和为 $0$。



我们希望将其使用类似 $Nim$ 游戏的方式解决，则必须满足：

+ 称先手必败态为 $P$ 态，必胜态为 $N$ 态。
+ $P$ 态的后继必全为 $N$ 态。
+ $N$ 态的后继中一定有 $P$ 态。



因为每次最多改变 $k$ 堆石子，对于第 $j$ 位，$S_j$ 每次改变值小于等于 $k$。

所以我们考虑 $S_j \bmod (k+1)$，他刚好满足上面的条件：

+ 若 $\forall j \in \mathbb{Z}$，$ S_j \bmod (k+1) = 0$，必不存在一种方法保持其全为 $0$。
+ 若 $\exist j \in \mathbb{Z}$，$S_j \bmod (k+1) \ne 0$，则总存在一种方法将其变为全为 $0$。



所以我们得到结论，若对于初始状态，$\forall j \in \mathbb{Z}$，$S_j = 0$，则先手必败，否则先手必胜。