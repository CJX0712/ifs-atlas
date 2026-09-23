# IFS Atlas · 迭代函数系统分形浏览器

<p align="center">
  <a href="https://github.com/CJX0712/ifs-atlas/actions/workflows/ci.yml"><img src="https://github.com/CJX0712/ifs-atlas/actions/workflows/ci.yml/badge.svg" alt="ci"></a>
  <a href="https://github.com/CJX0712/ifs-atlas/releases"><img src="https://img.shields.io/github/v/release/CJX0712/ifs-atlas?sort=semver" alt="release"></a>
  <a href="https://github.com/CJX0712/ifs-atlas/blob/main/LICENSE"><img src="https://img.shields.io/github/license/CJX0712/ifs-atlas" alt="license"></a>
  <img src="https://img.shields.io/badge/author-%E6%99%A8%E6%98%9F-1f6feb" alt="author">
</p>

一个**单文件、零依赖、纯离线**的网页工具，用混沌游戏（chaos game）算法绘制**仿射迭代函数系统（IFS）**的吸引子。

> 同一个预设 + 同一个随机种子，永远得到**逐像素相同**的图。改种子只是换一种随机走法，形状不变。

## 能做什么

- **6 个经典预设**：Barnsley 蕨叶、Sierpinski 三角、Heighway 龙曲线、Levy C 曲线、分形树、螺旋网。
- **种子可复现**：底部输入种子即可固定随机序列，方便复现/分享某张图。
- **编辑变换矩阵**：每个仿射变换 `x' = a·x + b·y + e`，`y' = c·x + d·y + f`，概率 `p` 自动归一化；可增删变换、实时预览。
- **随机一个（Surprise me）**：用种子化 PRNG 生成 2–4 个随机仿射变换，探索未知吸引子。
- **彩色密度渲染**：按生成该点的变换编号着色，叠加密度做色调映射，导出 PNG。
- **统计面板**：点数、变换数、包围盒尺寸、渲染耗时。

## 一句话原理

给定一组仿射变换 `{T₁…Tₙ}`（各带概率 `pᵢ`），从任意点 `P₀` 出发，每一步按概率随机选一个变换迭代：

```
P_{k+1} = T_i(P_k)
```

丢弃前若干次「预热」迭代后，点的分布会收敛到这组变换的**唯一不变集（吸引子）**——也就是你看到的 fractal。这就是 Barnsley 当年「用 4 个方程画出一整片蕨叶」的魔法。

## 本地运行

直接用浏览器打开 `index.html` 即可，无需联网、无需构建。

## 验证

仓库内附带两个测试脚本（用 Node 运行，仅校验内部数学引擎，不需要浏览器）：

```bash
node _smoke.js   # 27 项断言：PRNG 确定性、chaosGame 逐点可复现、
                 #   fern/sierpinski/dragon 包围盒容差、质心、owner 合法性、
                 #   200 组随机系统有限性+确定性
node _probe.js   # 把小样本渲染成 ASCII 图，肉眼确认形状正确
```

## 许可

MIT —— 见 `LICENSE`。
