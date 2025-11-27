# 磁场纪元三部曲 | The Magnetic Era Trilogy

一部关于人类文明进化的硬科幻史诗。

## 📚 作品目录

| 部 | 中文标题 | 英文标题 | 文件 |
|:--:|:-------:|:--------:|:----:|
| I | 胎动 | Fetal Movement | `book1-fetal-movement.tex` |
| II | 幻肢 | Phantom Limb | `book2-phantom-limb.tex` |
| III | 磁骨 | Magnetic Bones | `book3-magnetic-bones.tex` |

---

## 🔧 GitHub 上预览 LaTeX PDF 的方法

GitHub 本身**不直接支持** LaTeX 实时预览，但有以下几种方案：

### 方案一：GitHub Actions 自动编译（推荐）

在仓库中添加 `.github/workflows/latex.yml`，每次 push 自动编译 PDF：

```yaml
name: Build LaTeX documents

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      
      - name: Compile LaTeX documents
        uses: xu-cheng/latex-action@v3
        with:
          root_file: |
            book1-fetal-movement.tex
            book2-phantom-limb.tex
            book3-magnetic-bones.tex
          latexmk_use_xelatex: true
      
      - name: Upload PDFs as artifacts
        uses: actions/upload-artifact@v4
        with:
          name: PDF-documents
          path: "*.pdf"
      
      - name: Release PDFs (on tag)
        if: startsWith(github.ref, 'refs/tags/')
        uses: softprops/action-gh-release@v1
        with:
          files: "*.pdf"
```

**使用方法：**
1. 将上述文件保存到 `.github/workflows/latex.yml`
2. Push 代码后，在 Actions 页面查看编译结果
3. 在 Artifacts 中下载生成的 PDF

### 方案二：Overleaf 在线编辑（最简单）

1. 访问 [Overleaf](https://www.overleaf.com/)
2. 新建项目 → 上传项目 → 选择你的 `.tex` 文件
3. 实时预览 + 在线编辑
4. 可以与 GitHub 同步：Menu → GitHub → Link to GitHub Repository

### 方案三：VS Code + LaTeX Workshop

本地开发最佳方案：

1. 安装 [VS Code](https://code.visualstudio.com/)
2. 安装扩展 **LaTeX Workshop**
3. 安装 TeX 发行版：
   - Windows: [MiKTeX](https://miktex.org/) 或 [TeX Live](https://tug.org/texlive/)
   - macOS: [MacTeX](https://tug.org/mactex/)
   - Linux: `sudo apt install texlive-full texlive-lang-chinese`
4. 打开 `.tex` 文件，按 `Ctrl+Alt+B` 编译，`Ctrl+Alt+V` 预览

### 方案四：GitHub + Overleaf 同步

1. 在 Overleaf 创建项目
2. 菜单 → GitHub → 创建 GitHub 仓库
3. 双向同步：Overleaf 编辑 ↔ GitHub 存储

---

## 📋 编译要求

这些文档使用 **XeLaTeX** 编译，需要以下环境：

### 必需宏包
- `ctex` - 中文支持
- `geometry` - 页面布局
- `fancyhdr` - 页眉页脚
- `xcolor` - 颜色
- `tcolorbox` - 文本框
- `hyperref` - 超链接
- `amsmath`, `amssymb` - 数学符号

### 中文字体
默认使用系统中文字体。如果缺失，可在导言区添加：
```latex
\setCJKmainfont{Noto Serif CJK SC}  % 或其他中文字体
\setCJKsansfont{Noto Sans CJK SC}
```

### 本地编译命令
```bash
xelatex book1-fetal-movement.tex
xelatex book1-fetal-movement.tex  # 运行两次以生成目录

# 或使用 latexmk（推荐）
latexmk -xelatex book1-fetal-movement.tex
```

---

## 📁 项目结构

```
magnetic-era-trilogy/
├── README.md                    # 本文件
├── book1-fetal-movement.tex     # 第一部：胎动
├── book2-phantom-limb.tex       # 第二部：幻肢
├── book3-magnetic-bones.tex     # 第三部：磁骨
└── .github/
    └── workflows/
        └── latex.yml            # GitHub Actions 自动编译
```

---

## 📖 故事简介

**第一部《胎动》**：地球磁场崩溃，人类面临抉择——保留脆弱的肉体，还是化身为光？

**第二部《幻肢》**：三百年后，飞升者们患上"时间潜水病"试图回归，却与留守的碳基人类产生致命冲突。

**第三部《磁骨》**：地球彻底死亡，磁骨人做出最终抉择——拆解母星，化为星舰，驶向深空。

---

## 📝 版式说明

本系列参考经典科幻小说排版，采用以下设计：

- **开本**：A5 (148mm × 210mm)
- **行距**：1.5 倍
- **章节**：中文数字编号（第一章、第二章...）
- **场景标记**：灰色方块 + 时间/地点信息
- **特殊对话框**：
  - 飞升者对话：青色边框
  - 磁骨人通讯：灰色边框
  - 技术档案：黑框文档框

---

## 📜 License

本作品采用 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 许可协议。
