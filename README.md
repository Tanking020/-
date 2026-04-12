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

## 2026.04.12
## 线性方程组迭代法求解：Jacobi、Gauss-Seidel 与 SOR 的完整实现

**My Optimization Journey (我的优化算法学习之路)**

研0预备役 | 数学优化方向 | 记录从零实现数值线性代数与优化算法

---

## 📚 学习进度

| 算法 | 状态 | 核心收获 |
|:---|:---:|:---|
| Jacobi 迭代 | ✅ | 理解对角占优与收敛性 |
| Gauss-Seidel 迭代 | ✅ | 利用最新分量加速收敛 |
| SOR 超松弛迭代 | ✅ | 松弛因子 ω 的加权平均思想 |
| 可视化对比 | ✅ | 收敛曲线 + 性能对比图表 |

---

## 📊 重点：图像与图表生成

### 1. 收敛曲线图（两张）

运行代码自动生成两张对比图，清晰展示三种方法的收敛速度差异。

| 图片文件 | 坐标类型 | 特点 |
|:---|:---|:---|
| `convergence_linear.png` | 线性坐标 | 直观看到误差下降趋势 |
| `convergence_log.png` | 半对数坐标 | Y轴对数刻度，指数收敛一目了然 |

**生成效果**：
```
半对数坐标图（关键）：
误差
  │
10⁰ ┤    ⚪───⚪ (Jacobi)
  │   ⚪
10⁻² ┤  ⚪
  │  □───□ (Gauss-Seidel)
10⁻⁴ ┤ □
  │ △
10⁻⁶ ┤△───△ (SOR)
  │
  └───────────────── 迭代次数
      0    10    20    30    40
```

**核心代码**：
```python
plt.semilogy(errors_jacobi, 'o-', label='Jacobi')
plt.semilogy(errors_gs, 's-', label='Gauss-Seidel')
plt.semilogy(errors_sor, '^-', label='SOR (w=1.2)')
plt.xlabel('迭代次数')
plt.ylabel('误差（对数坐标）')
plt.legend()
plt.savefig('convergence_log.png', dpi=150)
```

### 2. 性能对比表格（控制台输出）

```
============================================================
详细性能对比
============================================================

总耗时对比（秒）：
----------------------------------------
Jacobi         : 0.006228秒
Gauss-Seidel   : 0.000782秒
SOR(w=1.2)     : 0.001171秒

========================================
最快的是：Gauss-Seidel迭代法
========================================

迭代次数对比：
Jacobi: 41 次
Gauss-Seidel: 14 次
SOR(w=1.2): 19 次
```

**表格对齐技巧**：
```python
print(f"{'Jacobi':15} : {time_j:.6f}秒")
# 'Jacobi' 占15字符，左对齐
```

---

## 🧠 重点：较难问题解析

### 难点1：SOR 的加权平均公式为什么这样写？

```python
x_gs = (b[i] - sum1 - sum2) / A[i, i]  # Gauss-Seidel 值
x[i] = w * x_gs + (1 - w) * x_old[i]   # 加权平均
```

**理解**：
- `x_old[i]`：旧解（上一步的值）
- `x_gs`：Gauss-Seidel 算出的新解
- `w`：松弛因子，控制"跨步"大小
  - `w = 1`：`x[i] = x_gs`（就是 GS）
  - `w = 1.2`：`x[i] = 1.2*x_gs - 0.2*x_old[i]`（超松弛，跨过 GS 值）

### 难点2：为什么 SOR 不一定比 GS 快？

SOR 的收敛速度高度依赖 **ω 的选择**：

```
收敛速度
    │
    │        ╱╲
    │       ╱  ╲
    │      ╱    ╲
    │     ╱      ╲
    │    ╱        ╲
    └──┴────┴────┴────┴──→ ω
       1.0   1.2   1.5
       GS    你选  发散
```

- ω 太小：欠松弛，收敛慢
- ω 太大：过冲，可能发散
- 最优 ω 通常在 1.0~1.5 之间，需要针对具体矩阵估算

### 难点3：为什么用迭代增量（x_new - x_old）判断收敛？

**原因**：真解 `x*` 不知道，无法计算真误差。

| 可计算 | 不可计算 |
|:---|:---|
| `x_new - x_old`（迭代增量） | `x - x*`（真误差） |
| `Ax - b`（残差） | - |

**逻辑**：当迭代增量足够小时 → 解已稳定 → 可以认为接近真解。

### 难点4：元组 + lambda 找出最快方法

```python
results = [("Jacobi", 0.006228), ("Gauss-Seidel", 0.000782), ("SOR", 0.001171)]
fastest = min(results, key=lambda x: x[1])
# key=lambda x: x[1] 表示：比较每个元组的第2项（耗时）
# 返回：("Gauss-Seidel", 0.000782)
```

**为什么用元组？** 把名字和时间**绑定**在一起，排序后仍能知道哪个名字对应哪个时间。

---

## 📈 测试结果分析

### 测试矩阵（严格对角占优）
```
A = [[5, 1, 2],
     [1, 4, 1],
     [2, 1, 6]]
b = [10, 8, 16]
精确解：x = [1, 1, 2]
```

### 关键发现
| 方法 | 迭代次数 | 耗时 | 结论 |
|:---|:---:|:---:|:---|
| Jacobi | 41 | 最慢 | 需要全部旧值，收敛最慢 |
| Gauss-Seidel | 14 | **最快** | 利用最新信息，加速明显 |
| SOR(1.2) | 19 | 中等 | ω=1.2 不是最优值 |

**对于此矩阵，Gauss-Seidel 已经是最优选择。**

---

## 🐛 重点 Debug 记录

| 错误 | 原因 | 解决方案 |
|:---|:---|:---|
| 迭代次数显示1000 | 返回了 `max_iter` 而非 `k+1` | `return x_new, k+1, True, errors` |
| SOR 和 GS 曲线重合 | 绘图时未传入 `w=1.2` | `SOR_with_history(A, b, w=1.2)` |
| 字体警告 | matplotlib 默认字体无中文 | 设置中文字体 + `axes.unicode_minus=False` |
| 性能对比重复输出 | 单独调用 + 绘图函数都运行 | 主程序只保留绘图函数 |

---

## 🚀 核心代码片段

### 统一接口（三个函数返回值一致）
```python
def Jacobi_with_history(...):
    return x, iterations, converged, errors

def Gauss_Seidel_with_history(...):
    return x, iterations, converged, errors

def SOR_with_history(...):
    return x, iterations, converged, errors
```

### 绘图函数核心
```python
def plot_convergence_comparison(A, b):
    _, _, _, err_j = Jacobi_with_history(A, b, verbose=False)
    _, _, _, err_gs = Gauss_Seidel_with_history(A, b, verbose=False)
    _, _, _, err_sor = SOR_with_history(A, b, w=1.2, verbose=False)
    
    # 线性坐标
    plt.plot(err_j, 'o-', label='Jacobi')
    plt.plot(err_gs, 's-', label='Gauss-Seidel')
    plt.plot(err_sor, '^-', label='SOR')
    
    # 半对数坐标
    plt.semilogy(err_j, 'o-', label='Jacobi')
    plt.semilogy(err_gs, 's-', label='Gauss-Seidel')
    plt.semilogy(err_sor, '^-', label='SOR')
```

### 性能对比核心
```python
def compare_time_J_G_S(A, b, w=1.2):
    results = []
    
    start = time.time()
    _, iter_j, _, _ = Jacobi_with_history(A, b, verbose=False)
    results.append(("Jacobi", time.time() - start))
    
    # ... GS 和 SOR 同理
    
    fastest = min(results, key=lambda x: x[1])
    print(f"最快的是：{fastest[0]}迭代法")
```

---

## 📁 生成的文件

| 文件 | 内容 |
|:---|:---|
| `convergence_linear.png` | 线性坐标收敛曲线 |
| `convergence_log.png` | 半对数坐标收敛曲线 |
| 控制台输出 | 性能对比表格 + 迭代次数 |

---

## 💡 核心收获

1. **可视化是关键**：一张半对数图胜过千行文字
2. **统一接口设计**：三个函数返回值一致，便于对比
3. **元组 + lambda**：优雅地找出最快方法
4. **SOR 的 ω 需调优**：不是 ω>1 就一定快
5. **迭代增量 vs 残差**：前者判断收敛，后者验证正确性

---

## 📋 后续计划

- [ ] 实现共轭梯度法
- [ ] SOR 最优 ω 自动估算
- [ ] 大规模矩阵测试（100×100+）

---

*持续更新中...* 🚀
