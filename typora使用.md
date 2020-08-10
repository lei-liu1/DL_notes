[toc]

### 方法：动态规划 :smile:

### 代码块 (```)

```python
# 新21点
class Solution:
    def new21Game(self, N: int, K: int, W: int) -> float:
        dp=[None]*(K+W)
        s=0
        for i in range(K,K+W):          # 填蓝色的格子
            dp[i] = 1 if i <= N else 0
            s += dp[i]
        for i in range(K-1,-1,-1):      # 填橘黄色格子
            dp[i] = s/W
            s = s - dp[i+W] + dp[i]
        return dp[0]
```

### 公式($$)

$$
\sigma \cdot y^3
$$

行内公式  $a^2\cdot b_1$

```python
y = 1
```

love :wilted_flower: H~2~O $H_2O$ :potable_water: :horse: 

### 引用

> 我爱发奥利弗金额欧锦



### 我的表格(ctrl + T)

| name | age  | school | major | grade |
| :--: | :--: | :----: | :---: | :---: |
|      |      |        |       |       |
|      |      |        |       |       |

### 列表

- 1
  - 1.1
    - 1.1.1
  - 1.2
    - 1.2.1

* 2

### 任务列表（- [ ] )

### 分割线 （--- ）

---

- [x] Andrew Ng

- [ ] 李宏毅

---

### 流程图

（```+ Enter 打开代码块，选择语言flow或者mermaid）

```flow

```

$b = a^2 + c^2$
$$
\begin{align}
z &= y\cdot u\\
y &= x^2
\end{align}
$$

![递龟](https://i.loli.net/2020/08/10/Zx9OtFpd3NrLi1l.png)

### 矩阵

$$
a = \left[
\matrix{
  \alpha_1 & 100\\
  \alpha_2 & 200\\
  \alpha_3 & 300 
}
\right]
$$



