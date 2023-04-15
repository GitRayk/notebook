# Markdown 数学公式

其实是用 LateX 来实现的  
**Markdown 中要使用 LateX 语法，只需要在语法的两端是用一组 “\$” 美元符号表示行内公式，用一组 “\$\$” 表示块级公式**  

**使用 “{}” 大括号表示分组**  

! github居然不支持在 Markdown 中渲染 LaTeX，可恶，只有用 `<img src="http://chart.googleapis.com/chart?cht=tx&chl=Latx语法">` 将公式转换成图片，或者转成其它文件格式的方法了  

$\color{red}{github你坏事做尽！！} $&#128545;  

INDEX：[基础符号](#基础符号) | [逻辑符号](#逻辑符号) | [高数符号](#高数符号) | [数学符号](#数学符号) | [希腊符号](#希腊符号) | [线性代数符号](#线性代数符号)  

------------------

## 基础符号
| 符号 | 代码 | 实际样式 |
| :-: | :-: | :-: |
| 加号 | `+` | + |  
| 减号 | `-` | - |  
| 乘号 | `\times` | $x \times y$ |
| 除号 | `\div` | $x \div y$ |
| 点乘 | `\cdot` | $x \cdot y$ |
| 星乘 | `\ast` | $x \ast y$ |
| 分式 | `\frac{分子}{分母}` | $ \frac x y$|
| 分式2 | `{分子}\over{分母}` | $x \over y$ |
| 绝对值 | `| |` | $\|x\|$ |
| 加减 | `\pm` | $x \pm y$
| 上标 | `^` | $x^2$ |
| 下标 | `_` | $x_2$ |
| 均值 | `\overline` | $\overline x$ |
| 并/交 | `\cup\cap` | $\cup \cap$ |


-----------------

## 逻辑符号
| 符号 | 代码 | 实际样式 |
| :-: | :-: | :-: |
| 等于 | `=` | $x = y$ |
| 小于/大于 | `</>` | $x </> y$ |
| 不等于 | `\neq` | $x \neq y$ |
| 大于等于 | `\geq` | $x \geq y $ |
| 小于等于 | `\leq` | $x \leq y$ |
| 约等于 | `\approx` | $x \approx y$ |  
| 任意的 | `\forall` | $\forall$ |
| 存在 | `\exists` | $\exists$ |
| 属于 | `\in` | $\in$ |

--------------------

## 高数符号
| 符号 | 代码 | 实际样式 |
| :-: | :-: | :-: |
| 求和 | `\sum` | $\sum x$ |
| 求和2 | `\displaystyle \sum` | $\displaystyle\sum _{i=1}^n x$ |
| 连乘 | `\prod` | $\prod _x ^2$ |
| 连乘2 | `\displaystyle \prod` | $\displaystyle \prod _{i=1}^n x$ |
| 极限 | `\lim` | $\lim _{x \to \infty} n$ |
| 极限2 | `\displaystyle \lim` | $\displaystyle\lim _{x \to \infty} n$ |
| 积分 | `\int` | $\int _0^\infty xdx$|
| 微分 | `\partial` | ${\partial x} \over {\partial y}$ |
| 开方 | `\sqrt[开方数]{被开方数}` | $\sqrt[n]{x}$ |
| 对数 | `\log` | $\log _n 2$ |

----------------

## 数学符号
| 符号 | 代码 | 实际样式 |
| :-: | :-: | :-: |
| 趋近 | `\to` | $x\to 0$ |
| 无穷 | `\infty` | $x \to \infty$ |
| 矢量 | `\vec` | $\vec a$ |
| 公式序号(只能在块级用) | `\tag` | (0) |


---------------

## 希腊符号
| 符号 | 代码 | 实际样式 |
| :-: | :-: | :-: |
| pi | `\pi` | $\pi$ |
| rho | `\rho` | $\rho$ |
| alpha | `\alpha` | $\alpha$ |
| beta | `\beta` | $\beta$ |
| theta | `\theta` | $\theta$ |
| mu | `\mu` | $\mu$ |
| delta | `\delta` | $\delta$ |

-----------------

## 线性代数符号
| 符号 | 代码 | 实际样式 |
| :-: | :-: | :-: |
| 矩阵[^矩阵] | `\begin{matrix}矩阵内容\end{matrix}` | $\begin{matrix}2&3&4\\1&2&3\\2&3&5\end{matrix}$ |
| 矩阵2[^矩阵2] | `\left[\begin矩阵内容\end{matrix} \right]` | $\left[\begin{matrix}2&3&4\\1&2&3\\2&3&5\end{matrix} \right]$ |
| 水平省略 | `\cdots` | $\cdots$ |
| 竖直省略 | `\vdots` | $\vdots$ |
| 斜右下省略 | `\ddots` | $\ddots$

[^矩阵]: 矩阵：矩阵内容中可以将 “&” 用作分隔，“\\\\” 用作换行  
[^矩阵2]: `\left` 和 `\right` 实际上是一个范围符号，会将紧跟着的符号变成范围包裹。如果紧跟着 “.”，表示该边不出现符号。“{}” 花括号需转义
