# LaTeX Beamer + minted Unicode 字体问题修复指南
# LaTeX Beamer + minted Unicode Font Issue Fix Guide

**作者 / Author**: Frankie F.-C. Wang  
**日期 / Date**: 2026-02-01  
**标签 / Tags**: LaTeX, Beamer, minted, XeLaTeX, Unicode, 字体 / font

---

## 📌 问题概述 / Problem Overview

在使用 Beamer + minted 展示 Lean 4 代码时，代码中的 **Unicode 数学符号**（如 `∀`, `∃`, `→`, `↔`, `∈`）无法正常显示，编译时出现以下错误：

```
Missing $ inserted
... 
There is no ∀ in font Imperial Sans Text/OT
There is no ∃ in font Imperial Sans Text/OT
```

**When using Beamer + minted to display Lean 4 code, Unicode math symbols** (like `∀`, `∃`, `→`, `↔`, `∈`) **failed to render**, producing errors:

```
Missing $ inserted
... 
There is no ∀ in font Imperial Sans Text/OT
There is no ∃ in font Imperial Sans Text/OT
```

---

## 🔍 根因分析 / Root Cause Analysis

### 1. 字体不支持 Unicode / Font Doesn't Support Unicode

Imperial College Beamer 主题默认使用 `Imperial Sans Text` 作为等宽字体（用于代码展示），但该字体**不包含 Unicode 数学符号**。

**The Imperial College Beamer theme uses `Imperial Sans Text` as the monospace font by default, but this font does NOT contain Unicode math symbols.**

### 2. 下划线触发数学模式 / Underscore Triggers Math Mode

自定义命令 `\leancode` 在 minted 代码块外使用时，下划线 `_` 被 LaTeX 解释为数学下标，导致 `Missing $ inserted` 错误。

**The custom `\leancode` command, when used outside minted blocks, treats underscores `_` as math subscripts, triggering "Missing $ inserted" errors.**

---

## 🛠️ 修复方案 / Solution

### 方案一：更换支持 Unicode 的等宽字体 / Solution 1: Switch to Unicode-Compatible Monospace Font

在 `main.tex` 导言区添加以下配置：

**Add the following to your preamble in `main.tex`:**

```latex
% Override monospaced font to support Unicode math symbols in code
% (e.g., ∀, ∃, →) that appear in Lean snippets
% Reset fontspec Path so system fonts can be found
\defaultfontfeatures{Ligatures=TeX,Path=}
\IfFontExistsTF{FreeMono}{
  \setmonofont{FreeMono}[Scale=MatchLowercase]
}{
  \setmonofont{Imperial Sans Text}[Scale=MatchLowercase]
}
```

**关键点 / Key Points:**

| 配置项 / Setting | 作用 / Purpose |
|-----------------|---------------|
| `\defaultfontfeatures{Ligatures=TeX,Path=}` | 重置 fontspec 路径，允许使用系统字体 |
| `\setmonofont{FreeMono}` | 使用 FreeMono（系统自带，支持全 Unicode） |
| `\IfFontExistsTF{...}{...}{...}` | 优雅降级：如果 FreeMono 不存在则回退 |

### 方案二：修复 \leancode 下划线问题 / Solution 2: Fix \leancode Underscore Issue

将原有的：

**Change from:**

```latex
\newcommand{\leancode}[1]{\texttt{\small #1}}
```

改为：

**To:**

```latex
\newcommand{\leancode}[1]{\texttt{\small\detokenize{#1}}}
```

**`\detokenize` 阻止 LaTeX 解释特殊字符（如 `_`, `*`, `\`），避免进入数学模式。**

**`\detokenize` prevents LaTeX from interpreting special characters (like `_`, `*`, `\`), avoiding math mode.**

---

## 🔧 推荐构建命令 / Recommended Build Command

使用 `latexmk` 配合 XeLaTeX：

**Use `latexmk` with XeLaTeX:**

```bash
latexmk -xelatex -shell-escape -interaction=nonstopmode main.tex
```

**参数说明 / Parameters:**

| 参数 / Flag | 作用 / Purpose |
|------------|---------------|
| `-xelatex` | 使用 XeLaTeX 引擎（支持系统字体） |
| `-shell-escape` | 允许 minted 调用 Pygments 高亮 |
| `-interaction=nonstopmode` | 遇错不暂停，继续编译 |
| `-halt-on-error` | 遇严重错误立即停止（推荐用于调试） |

---

## 📊 对比表格 / Comparison Table

| 字体 / Font | Unicode 支持 / Unicode Support | 适用场景 / Use Case |
|-------------|-------------------------------|-------------------|
| **FreeMono** | ✅ 完整 Unicode | 代码展示、数学符号 |
| **DejaVu Sans Mono** | ✅ 完整 Unicode | 备选方案 |
| **Menlo** (macOS) | ✅ 完整 Unicode | macOS 专用 |
| **Imperial Sans Text** | ❌ 仅 ASCII | 不适合代码展示 |
| **Computer Modern Typewriter** | ⚠️ 部分 | 传统 LaTeX，但符号有限 |

---

## 📁 相关文件 / Related Files

| 文件 / File | 路径 / Path | 说明 / Description |
|-------------|-------------|-------------------|
| `main.tex` | `/Slides/main.tex` | Beamer 演示文稿主文件 |
| `beamerthemeImperial.sty` | `/Slides/beamerthemeImperial.sty` | Imperial 主题 |
| `doc/font-fix-guide.md` | `/Slides/doc/font-fix-guide.md` | 本文档 |

---

## ✅ 验证步骤 / Verification Steps

1. **运行编译 / Run compilation:**
   ```bash
   cd Slides
   latexmk -xelatex -shell-escape main.tex
   ```

2. **检查输出 / Check output:**
   ```
   Output written on main.pdf (XX pages).
   ```

3. **确认无字体错误 / Confirm no font errors:**
   ```bash
   grep -i "There is no.*font" main.log  # 应无输出 / should return nothing
   ```

---

## 💡 经验总结 / Lessons Learned

1. **系统字体 vs TeX 字体 / System Fonts vs TeX Fonts**
   - XeLaTeX 可以使用系统字体（OTF/TTF），无需依赖 TeX 发行版自带字体
   - **XeLaTeX can use system fonts (OTF/TTF), no need to rely on TeX distribution fonts**

2. **fontspec 路径问题 / fontspec Path Issues**
   - 主题可能预设 `fontspec` 路径导致系统字体不可见
   - 使用 `\defaultfontfeatures{Path=}` 重置
   - **Themes may preset fontspec path, hiding system fonts**
   - **Use `\defaultfontfeatures{Path=}` to reset**

3. **优雅降级 / Graceful Degradation**
   - 使用 `\IfFontExistsTF` 确保在无 FreeMono 的机器上仍能编译
   - **Use `\IfFontExistsTF` to ensure compilation works on machines without FreeMono**

4. **minted vs listings / minted vs listings**
   - minted 配合 Pygments 提供更好的语法高亮
   - listings 更轻量但 Unicode 支持有限
   - **minted with Pygments provides better syntax highlighting**
   - **listings is lighter but has limited Unicode support**

---

## 🔗 参考资源 / References

- [fontspec 文档 / fontspec documentation](https://ctan.org/pkg/fontspec)
- [minted 文档 / minted documentation](https://ctan.org/pkg/minted)
- [LaTeX3 unicode-math / LaTeX3 unicode-math](https://ctan.org/pkg/unicode-math)
- [FreeMono 字体 / FreeMono font](https://www.fonts.com/font/gnu/freefont/freemono)

---

## 📝 修订历史 / Changelog

| 日期 / Date | 版本 / Version | 变更 / Change |
|-------------|---------------|---------------|
| 2026-02-01 | 1.0 | 初始版本 / Initial version |

---

**Happy TeXing! 🎉**
