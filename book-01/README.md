# 《主人、笨狗与綾》第一册

本目录是第一册的 LaTeX 写作工程。目前只完成项目初始化与章节骨架，尚未开始正文扩写。

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
- `chapters/*.tex`：每章一个文件；目前只有标题与待写标记。
- `outline/`：主控大纲和以后可能增加的连续性资料，不参与 PDF 编译。
- `build/`：编译输出，由 Git 忽略。

这个布局刻意保持轻量。等正文需要术语表、插图、参考资料或多卷共享样式时，再增加对应目录，不提前制造空结构。

## 编译

推荐安装包含 XeLaTeX、`ctex` 和 `latexmk` 的 TeX Live，然后在本目录执行：

```sh
latexmk -xelatex main.tex
```

输出写入 `build/`。清理构建产物：

```sh
latexmk -C main.tex
```

也可直接运行：

```sh
mkdir -p build
xelatex -output-directory=build main.tex
xelatex -output-directory=build main.tex
```

连续编译两次用于生成目录。未安装 LaTeX 时仍可编辑源文件，但提交前应至少确认 `main.tex` 中的所有 `\input` 路径存在。

## 写作流程

1. 开始一章前，阅读主控大纲的全局人物/伦理规则、该章场景组以及连续性细节库。
2. 只编辑对应的 `chapters/*.tex`；全局样式变更才编辑 `tex/preamble.tex`。
3. 完成后核对固定数字、系统字符串、角色已知信息与“已确认 / 角色判断 / 仍未知”边界。
4. 编译并检查 PDF，再使用 Conventional Commits 提交。
