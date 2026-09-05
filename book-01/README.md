# 《灯还亮着》第一册

本目录是第一册的 LaTeX 写作工程，原工作名为《主人、笨狗与綾》。正文按章推进，已写章节、衔接状态与待核问题见 [写作记录](outline/writing-notes.md)。

“灯还亮着”从两个人的家出发，逐渐包含綾通过灯光表达的情绪，以及后半册对意识是否仍然存续的追问。书名不预先回答世界层级与异常来源。

## 内容理解

第一册采用三幕、9 章 + 终章结构：关系从 Miku 与男主的“两个人的家”，发展为 Miku、男主与綾的“三个人的家”，再进入围绕死亡梦、`HOST`、意识分支和 LOWER DECK NO.1 的现实层级悬疑。

全册的关系主轴是：爱不需要用金钱、劳动或牺牲来付款，爱也不构成替对方做决定的许可。悬疑主轴追问记忆、复制与实例分支之下的主体连续性，但第一册不会确认世界真相。结尾必须保留“未知仍在，三个人都还在”的落点。

详细剧情事实、人物弧线、伦理边界、固定数字和未知项以 [`outline/master-outline-v2.1.md`](outline/master-outline-v2.1.md) 为准。

## 为什么拆分 LaTeX 文件

正文不会全部放进一个 `.tex` 文件。第一册包含十个正式章节单元，后续还需要逐章扩写、审阅和核对连续性；按章拆分能让 Git 差异更聚焦，也降低多人或多轮编辑时的冲突。

- `main.tex`：唯一编译入口，控制前置、正文和后置顺序。
- `tex/metadata.tex`：书名、册名、作者等元数据。
- `tex/preamble.tex`：纸张、字体、段落和页眉页脚等全局排版。
- `frontmatter/titlepage.tex`：标题页。
- `chapters/*.tex`：每章一个文件；未开始的章节保留待写注释。
- `outline/`：主控大纲和以后可能增加的连续性资料，不参与 PDF 编译。
- `build/`：编译输出，由 Git 忽略。

这个布局刻意保持轻量。等正文需要术语表、插图、参考资料或多卷共享样式时，再增加对应目录，不提前制造空结构。

## 编译

推荐安装包含 LuaLaTeX、LuaTeX-ja、IPAex 字体和 `latexmk` 的 TeX Live，然后在本目录执行。

默认编译为日式小说版：A6（105 × 148 mm）、竖排、右向左翻页。

```sh
latexmk -lualatex main.tex
```

编译为中文书籍版：32 开（145 × 210 mm）、横排、左向右阅读：

```sh
lualatex -output-directory=build -jobname=main-32k '\def\BookChineseLayout{}\input{main.tex}'
```

需要目录更新时，将上面的命令再运行一次。两种版式共享同一份正文文件。

当前纵排字体使用 macOS 自带的 `Songti SC`；在其他平台编译时，需要将
`tex/preamble.tex` 中的 `\setmainjfont` 替换为本机可用的简体中文衬线字体。

输出写入 `build/`。清理构建产物：

```sh
latexmk -C main.tex
```

也可直接运行：

```sh
mkdir -p build
lualatex -output-directory=build main.tex
```

连续编译两次用于生成目录。未安装 LaTeX 时仍可编辑源文件，但提交前应至少确认 `main.tex` 中的所有 `\input` 路径存在。

## 写作流程

1. 开始一章前，回读前面相关章节，并对照本章、后续章节的大纲及连续性细节库核对衔接。
2. 只编辑对应的 `chapters/*.tex`；全局样式变更才编辑 `tex/preamble.tex`。
3. 写前、写后均核对时间线、伤势、人物知情范围、物件、金额及系统状态。大纲可能有错；发现实质性的前后矛盾时，按根目录 `AGENTS.md` 暂停正文、询问作者采用哪个版本。无关紧要的口头要求可按作者授权灵活取舍。
4. 根据当前任务要求进行校验，再使用 Conventional Commits 提交。作者要求暂不编译时，只做文本与源文件检查，不生成 PDF。
