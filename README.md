
+ 一简单概率游走问题
	- 初始时你在数轴的位置0处。每单位时间你能向左或者向右走一格。
	- 问第一次走到1的期望步数。
	- 解法一：
		+ 设 $f_i$ 表示正好向右走了 $i$ 步的期望。得 $f_i=\frac{1}{2}(f_{i-1}+f_{i+1})+1$ 且 $f_0=0$，联立化简后得 $f_i = 2f_{i-1}-f_{i-2}-2(i \geq 2)$。继续化简得 $f_i=(3i-4)f_1-(i-1)i$。
		+ 我们要求的是 $f_1$。假设 $f_1=x$，则 $f_n=(3n-4)x-(n-1)n$，当 $n \rightarrow +\infty$ 时 $f_n \rightarrow -\infty$，显然矛盾。所以 $f_1=+\infty$
	- 上述做法太麻烦了。解法二：
		+ 设 $f_1$ 表示正好向右走了一步的期望。注意期望是有可加性的，所以$f_1=\frac{1}{2}(0+2f_1)+1$，化简得 $f_1=f_1+1$。显然 $f_1=+\infty$。

+ 一个概率构造问题
	- 一个函数 $f()$ 会以 $p$ 的概率返回 $1$，以 $1-p$ 的概率返回0。
	- 要构造一个函数 $g()$，以正好 $0.5$ 的概率返回 $0$ 和 $1$。
	- 注意：$p$ 是一个固定但是未知的概率。
	- 解法一：
		- 连续调用两次 $f()$，显然返回 $01$ 和 $10$ 的概率相同，我们可以根据这个来决定 $g()$ 的返回，如果返回值相同，就继续这么操作。显然，当 $p \rightarrow 0/1$ 时，这个的期望步数趋于无穷大。
	- 解法二（改进）：
		- 我们可以设计算法使期望步数进一步下降。
		- 对于询问序列的一个前缀长度 $n$，一旦 $C_n^m$ 是偶数（$m$ 是返回的 $1$ 的个数），其实我们就能立即结束并得到返回值（总能分成两半）。
		- 如何决定返回什么呢？每次看当前01序列和它的回文哪个字典序小，一样就递归一半，复杂度是 $O(N)$ 的。
    	-  [知乎](https://www.zhihu.com/question/304075115) 上有更详细讨论。

+ 一个概率构造和计算问题
	- 有 $100$ 个人被编号为 $1 \sim 100$，对应他们编号的 $100$ 个号码牌被打乱顺序放在了$100$ 个抽屉里。每个人可以打开至多半数的抽屉，并从中找出对应自己编号的号码牌。只有所有人都找到了自己的号码牌，任务才算成功（所有人会依次独立地操作，彼此不能交流，操作完后所有抽屉都会复原）。**假设抽屉的各种放置状态出现的概率均等**，设计一种固定的策略，所有人都成功的概率尽可能的大。
	- 成功的概率比直觉上要高很多。
	- 策略：**首先打开自己号码的抽屉，如果没中，继续打开抽屉里号码牌对应的抽屉……重复50次。**。
	- 分析：
		+ 显然，所有人都能找到自己，当且仅当所有圆环的长度不超过 $50$。
		+ 下面就是要计算，对于一个随机排列，置换环长度全都不超过 $50$ 的概率是多少。
		+ 容斥。从 $100$ 个数中选出 $m(> 50)$ 个数构成大环（剩下的随便排）的方案数是：$C_{100}^m \cdot (m-1)! \cdot (100-m)!$
		+ 所以最终答案为 $P=1-\sum \limits_{m=51}^100 \frac{1}{m}$。且当 $n \rightarrow \infty$ 时，$P \rightarrow 1-\ln{2}$
