# 2026.4.6
Jacobi迭代法测试
# My Optimization Journey (我的优化算法学习之路)

> 研0预备役 | 数学优化方向 | 记录从零实现数值线性代数与优化算法

## 📚 学习进度

| 算法 | 状态 | 实现文件 | 学习笔记 |
| :--- | :--- | :--- | :--- |
| Jacobi Iteration (雅可比迭代) | ✅ 已实现 | `jacobi.py` | 理解了对角占优与收敛性 |
| Gauss-Seidel (高斯-赛德尔) | 🚧 进行中 | `gauss_seidel.py` | 相比 Jacobi，利用了最新分量 |
| Gradient Descent (梯度下降) | 📅 计划中 | - | - |

## 🧠 核心理解（示例）

### Jacobi 迭代法
- **思想**：将线性方程组 $Ax=b$ 分解，利用第 $k$ 步的值迭代第 $k+1$ 步。
- **收敛条件**：严格对角占优矩阵必收敛。
- **代码关键点**：注意避免原地更新，需要设置 `x_new` 和 `x_old`。

## 🚀 如何运行代码

## 📝 日志
- **2026.04.06**：初始化仓库，上传 Jacobi 迭代法实现。

- ## 2026.4.7
## Gauss-Seidel迭代法测试

**My Optimization Journey (我的优化算法学习之路)**

研0预备役 | 数学优化方向 | 记录从零实现数值线性代数与优化算法

---

## 📚 学习进度

| 算法 | 状态 | 实现文件 | 学习笔记 |
|:---|:---:|:---|:---|
| Jacobi Iteration (雅可比迭代) | ✅ 已完成 | `jacobi.py` | 理解了对角占优与收敛性 |
| Gauss-Seidel (高斯-赛德尔) | ✅ 已完成 | `gauss_seidel.py` | 理解了利用最新分量的加速技巧 |
| SOR (逐次超松弛迭代) | 📅 计划中 | - | 待学习 |
| Gradient Descent (梯度下降) | 📅 计划中 | - | - |

---

## 🧠 核心理解

### Gauss-Seidel 迭代法

**核心思想**：与 Jacobi 同时使用上一步所有旧值不同，Gauss-Seidel 在计算新分量时，**立即使用已经算出的新分量**（`j < i` 部分），从而加快收敛速度。

**数学表达**：
```math
x_i^{(k+1)} = \frac{b_i - \sum_{j < i} a_{ij} x_j^{(k+1)} - \sum_{j > i} a_{ij} x_j^{(k)}}{a_{ii}}
```

**收敛条件**：
- 严格对角占优矩阵 → 必收敛
- 对称正定矩阵 → 必收敛

**代码关键点**：
- `sum1`：累加左边已更新的分量（`j < i`），用本轮新值 `x[j]`
- `sum2`：累加右边未更新的分量（`j > i`），用上轮旧值 `x_old[j]`
- 收敛判断用**无穷范数** `np.max(np.abs(x - x_old))`，比 L2 范数更快
- 增加 `verbose` 参数控制输出，兼顾调试与安静运行

---

## ⚔️ 性能对比

对比 Jacobi 与 Gauss-Seidel 在相同 20×20 严格对角占优矩阵上的表现：

| 算法 | 迭代次数 | 计算时间 | 收敛精度 |
|:---|:---:|:---:|:---|
| Jacobi | 312 次 | 0.0235 秒 | 9.87e-09 |
| Gauss-Seidel | 156 次 | 0.0082 秒 | 8.45e-09 |

**结论**：Gauss-Seidel 比 Jacobi 快约 **2.85 倍**，迭代次数减少约 **50%**。

---

## 📝 代码结构

```python
gauss_seidel.py
├── gauss_seidel()        # 核心迭代函数
├── test_gauss_seidel()   # 测试用例（对角占优/对称正定/病态矩阵）
├── example_usage()       # 使用示例
└── compare_methods()     # Jacobi vs Gauss-Seidel 性能对比
```

---

## 🐛 今日 Debug 记录

| 错误 | 原因 | 解决方案 |
|:---|:---|:---|
| 迭代不收敛 | 收敛判断误放在 `for i` 循环内部 | 移到所有分量更新完成之后 |
| `b` 定义错误 | 写成了 2×2 矩阵 | 改为一维数组 `[11, 13]` |
| 缩进错误 | 测试用例2、3 多缩进 | 减少4个空格，与 `print` 对齐 |

---

## 💡 今日收获

1. **Gauss-Seidel 的本质**：不是"原地更新"的 Jacobi，而是"用最新信息加速"的策略
2. **收敛判断的位置很重要**：必须等本轮所有分量都更新完再判断
3. **`verbose` 参数设计**：默认 `False`（安静运行），需要时手动打开，适合调试
4. **无穷范数**：`np.max(np.abs(x - x_old))` 比 L2 范数计算更快，适合迭代法

---

## 🚀 如何运行代码

```bash
python gauss_seidel.py
```

---

## 📋 明日计划

- [ ] 实现 SOR（逐次超松弛迭代）并对比收敛速度
- [ ] 可视化三种迭代法的误差下降曲线
- [ ] 开始梯度下降方法的学习

---

## 📎 更新日志

| 日期 | 内容 |
|:---|:---|
| 2026.04.06 | 初始化仓库，上传 Jacobi 迭代法实现 |
| 2026.04.07 | 完成 Gauss-Seidel 迭代法实现，添加性能对比模块，修复多个 bug |

---

## 📖 参考资料

- [数值线性代数 - 迭代法](https://en.wikipedia.org/wiki/Iterative_method)
- [Gauss-Seidel Method - Wikipedia](https://en.wikipedia.org/wiki/Gauss%E2%80%93Seidel_method)
- [NumPy 官方文档](https://numpy.org/doc/stable/)

---

## 2026.4.8
## SOR超松弛迭代法实现与性能分析

**My Optimization Journey (我的优化算法学习之路)**

研0预备役 | 数学优化方向 | 记录从零实现数值线性代数与优化算法

---

## 📚 学习进度

| 算法 | 状态 | 实现文件 | 学习笔记 |
|:---|:---:|:---|:---|
| Jacobi Iteration (雅可比迭代) | ✅ 已完成 | `jacobi.py` | 理解了对角占优与收敛性 |
| Gauss-Seidel (高斯-赛德尔) | ✅ 已完成 | `gauss_seidel.py` | 理解了利用最新分量的加速技巧 |
| **SOR (逐次超松弛迭代)** | ✅ **已完成** | `SOR.py` | **理解了松弛因子的加权平均思想** |
| Gradient Descent (梯度下降) | 📅 计划中 | - | 待学习 |

---

## 🧠 核心理解

### SOR (Successive Over-Relaxation) 迭代法

**核心思想**：在 Gauss-Seidel 的基础上引入**松弛因子 ω**，对旧解与 Gauss-Seidel 新解进行**加权平均**，通过选择合适的 ω 来加速收敛。

**数学表达**：
$$x_i^{(k+1)} = (1 - \omega) \cdot x_i^{(k)} + \omega \cdot x_i^{(GS)}$$

其中 $x_i^{(GS)}$ 是 Gauss-Seidel 计算出的值：
$$x_i^{(GS)} = \frac{b_i - \sum_{j < i} a_{ij}x_j^{(k+1)} - \sum_{j > i} a_{ij}x_j^{(k)}}{a_{ii}}$$

**合并后的完整公式**：
$$x_i^{(k+1)} = (1-\omega)x_i^{(k)} + \frac{\omega}{a_{ii}}\left(b_i - \sum_{j < i} a_{ij}x_j^{(k+1)} - \sum_{j > i} a_{ij}x_j^{(k)}\right)$$

---

### 松弛因子 ω 的选择

| ω 范围 | 名称 | 效果 |
|:---|:---|:---|
| `0 < ω < 1` | 欠松弛 (Under-Relaxation) | 收敛慢但更稳定，适合病态矩阵 |
| `ω = 1` | Gauss-Seidel | 标准情况 |
| `1 < ω < 2` | 超松弛 (Over-Relaxation) | 收敛更快，需满足条件 |
| `ω ≥ 2` 或 `ω ≤ 0` | 发散 | 不收敛 |

**收敛充分条件**：`0 < ω < 2` **且** 矩阵严格对角占优（或对称正定）

---

### 代码关键点

```python
def SOR(A, b, x0=None, w=None, tol=1.0e-6, verbose=False, max_iter=1000):
    # 1. 初始化
    if x0 is None:
        x0 = np.zeros(n)
    if w is None:
        w = 1.0
    
    # 2. 对角占优检查
    is_diag_dominant = True
    for i in range(n):
        diag_val = abs(A[i, i])
        row_sum = sum(abs(A[i, j]) for j in range(n) if j != i)
        if diag_val <= row_sum:
            is_diag_dominant = False
            break
    
    # 3. SOR 迭代主循环
    for k in range(max_iter):
        x_old = x.copy()
        
        for i in range(n):
            # 左边和（j < i）：用本轮已更新的新值
            sum1 = sum(A[i, j] * x[j] for j in range(i))
            
            # 右边和（j > i）：用上一轮的旧值
            sum2 = sum(A[i, j] * x_old[j] for j in range(i+1, n))
            
            # Gauss-Seidel 步
            x_gs = (b[i] - sum1 - sum2) / A[i, i]
            
            # SOR 步：加权平均
            x[i] = w * x_gs + (1 - w) * x_old[i]
        
        # 收敛判断（无穷范数）
        error = np.max(np.abs(x - x_old))
        
        if error < tol:
            return x, k+1, True
    
    return x, max_iter, False
```

---

## ⚔️ 三种迭代法对比

| 算法 | 更新公式 | 特点 | 收敛速度 |
|:---|:---|:---|:---|
| **Jacobi** | 全部用旧值 | 可并行计算 | 慢 |
| **Gauss-Seidel** | 左边用新值，右边用旧值 | 串行更新 | 中 |
| **SOR** | GS值 + 旧值 加权平均 | 可调参数 ω | 快（ω选得好时） |

---

## 🐛 今日 Debug 记录

| 错误 | 原因 | 解决方案 |
|:---|:---|:---|
| 迭代不收敛 | `break` 放在循环外 | 将 `break` 移到 `if` 内部 |
| 残差计算错误 | `np.dot(A, b) - b` | 改为 `np.dot(A, x) - b` |
| 松弛因子未生效 | 调用时写死 `w=1.0` | 改为 `w=w` 或直接传值 |
| 打印信息显示错误 | 用 `k` 而非 `k+1` | 收敛时显示 `k+1` |

---

## 💡 今日收获

1. **SOR 的本质**：不是简单的"加速版 GS"，而是对 GS 结果和旧解进行加权平均
2. **ω 的选择很重要**：`1 < ω < 2` 可加速，`ω=1` 退化为 GS，`ω>2` 发散
3. **加权平均公式**：`(1-ω)×旧解 + ω×GS解`，注意权重分配
4. **`x_old` 的作用**：必须保存本轮开始时的值，用于计算右边和与加权平均
5. **参数传递**：调用函数时用 `verbose=verbose` 才能把变量值传进去

---

## 📝 代码结构

```
SOR.py
├── SOR()               # 核心迭代函数（支持自定义 ω）
├── test_SOR()          # 测试用例（严格对角占优矩阵）
└── if __name__ == "__main__"
```

---

## 🚀 如何运行代码

```bash
python SOR.py
```

---

## 📋 明日计划

- [ ] 实现 SOR 的最优 ω 估算
- [ ] 可视化三种迭代法的误差下降曲线
- [ ] 开始梯度下降方法的学习

---

## 📎 更新日志

| 日期 | 内容 |
|:---|:---|
| 2026.04.06 | 初始化仓库，上传 Jacobi 迭代法实现 |
| 2026.04.07 | 完成 Gauss-Seidel 迭代法实现，添加性能对比 |
| 2026.04.08 | 完成 SOR 超松弛迭代法实现，理解松弛因子 ω 的作用 |

---

## 📖 参考资料

- [SOR Method - Wikipedia](https://en.wikipedia.org/wiki/Successive_over-relaxation)
- [数值线性代数 - 迭代法](https://en.wikipedia.org/wiki/Iterative_method)
- [NumPy 官方文档](https://numpy.org/doc/stable/)

---

*持续更新中...*
