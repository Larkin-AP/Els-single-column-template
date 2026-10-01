# MMT 单栏 LaTeX 投稿起始模板

## 从这里开始

主文件是 `main.tex`，编译器使用 **pdfLaTeX**，参考文献使用 **BibTeX**。
当前作者、正文、声明、关键词、Highlights 和一条示例引用都是占位内容，须替换后再投稿。

```sh
latexmk -pdf main.tex
```

`latexmk` 会自动运行 BibTeX 和必要的多轮 LaTeX，使引用、作者信息与页码稳定。
若没有 `latexmk`，依次运行：

```sh
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

在 Overleaf 中选择 `main.tex` 为主文件、pdfLaTeX 为编译器。
当前 Codex 内置 LaTeX 预览只编译单个源文件，暂不支持读取本项目的外部章节和文献库；
分章节版本请用上述本地命令或 Overleaf 编译。内置预览提示章节文件缺失时，不代表文件实际丢失。
清理编译中间文件、保留 PDF：`latexmk -c main.tex`。
本地已有的 `main.pdf` 可直接预览；PDF 和编译中间文件不纳入 Git，从仓库恢复后需重新编译。

## 文件用途

- `main.tex`：排版配置、作者信息和章节入口，通过 `\input{...}` 引入各章节。
- `00-abstract.tex`：摘要。
- `01-introduction.tex`、`02-methods.tex`、`03-results-discussion.tex`、`04-conclusions.tex`：正文各章。
- `05-credit.tex`、`06-competing-interest.tex`、`07-funding.tex`、`08-data-availability.tex`、`09-acknowledgements.tex`：各项声明与致谢。
- `ref.bib`：默认 BibTeX 文献库；目前只有一条真实的 Elsevier 官方说明示例。
- `cas-sc.cls`、`cas-common.sty`：原版 CAS 2.4 单栏类及公共依赖，内容未修改。
- `elsarticle-num.bst`：Elsevier 数字编号文献样式，按引用出现顺序排列。
- `highlights.txt`：单独提交的 Highlights 起始文件，填写 3–5 条真实成果。
- `.latexmkrc`：编译与清理配置。
- `.gitignore`：过滤主稿 PDF、编译中间文件与系统临时文件；保留 PDF 格式原始插图的版本管理。
- `manifest.txt`：原版 CAS 包清单及版权/许可说明；用于保留上游出处，并非本精简目录的文件清单。
- `main.pdf`：当前模板的编译预览。
- `main.bbl`：已生成的参考文献，可随源文件提交；修改文献后重新编译更新。

双栏模板、两种布局的演示论文、演示图片、模板手册及未使用的作者社交图标已移除。
邮箱和 URL 使用文字标签，因此不依赖 `thumbnails/`。
后续论文图片与 `.tex` 放在同一层级，便于 Editorial Manager 处理。
提交源文件时包含 `main.tex`、全部章节 `.tex` 文件、`ref.bib`、两个 CAS 文件、数字文献样式以及实际使用的图片；
如提交系统要求 `.bbl`，使用编译生成的 `main.bbl`。说明文件与本地编译配置无需上传。

## 分章节写作与文献引用

直接编辑对应章节文件，始终编译 `main.tex`。章节文件与主文件放在同一层，
`\input` 不会强制每章换页；各章节首行的 TeX root 注释指向主文件。
新增章节时创建 `.tex` 文件，再在 `main.tex` 中按顺序添加 `\input{文件名}`。

将文献条目加入 `ref.bib`，正文使用 `\cite{引用键}`，例如 `\cite{elsevierLatex}`。
主文件使用 `\bibliographystyle{elsarticle-num}` 和 `\bibliography{ref}`，
由 BibTeX 生成按引用顺序排列的数字编号文献；不要手动编辑生成的 `main.bbl`。

## 本地 Git

本目录使用本地 Git 管理源文件。日常使用：

```sh
git status
git diff
git add .
git commit -m "Update manuscript"
```

`main.pdf`、`main.bbl`、日志等生成文件不会纳入提交，但会保留在本地。
`.gitignore` 仅忽略主稿的输出 PDF，原始 PDF 插图仍可正常加入版本管理。
若将主文件改名，应同步修改 `.latexmkrc` 和 `.gitignore` 中的主文件设置。

## MMT 格式依据

核对日期：2026-10-01。

- Word 稿件要求单栏；LaTeX 稿件也允许双栏。因此本目录采用单栏是作者的选择，并非 LaTeX 投稿的唯一允许格式。
- 使用 `cas-sc` 的原始单栏正文和首页布局；首页摘要与关键词并排是该模板的正常设计。
- 单盲评审：保留作者姓名、单位及通讯作者信息。
- 摘要最多 **180 词**；关键词 **1–6 个**。
- Highlights 必须作为单独的可编辑文件提交；**3–5 条，每条最多 85 个字符（含空格）**。这里的 TXT 可编辑，如系统要求其他扩展名可转换为 DOCX。
- 文内引用使用方括号数字，按出现顺序编号；投稿阶段文献细节格式允许保持一致的其他样式。
- 填写真实的 CRediT、利益冲突、资助及数据可用性信息；如适用，在参考文献前加入生成式 AI 使用声明。
- `review` 选项可用于正文双倍行距；目前没有强行启用。首页信息过长时可添加 `longmktitle`。

官方来源：

- [MMT Guide for authors](https://www.sciencedirect.com/journal/mechanism-and-machine-theory/publish/guide-for-authors)
- [Elsevier LaTeX instructions](https://www.elsevier.com/researcher/author/policies-and-guidelines/latex-instructions)
- [CAS 模板上游](https://ctan.org/pkg/els-cas-templates)

## 编译修复与验证

`main.tex` 中的局部修复不修改上游类文件，也不屏蔽日志：

1. 关闭脚注超链接，避免 CAS 首页手动脚注生成空链接目标；正文引用与链接仍保留。
2. 将关键词的零宽盒改成正式的重叠盒，修复 CAS 2.4 的横向溢出报告，保留原版布局。
3. 没有 ORCID 时不生成空 ORCID 脚注；填写 ORCID 后仍会正常显示。
4. 使用 `xurl` 允许长网址换行。

最终模板以 TeX Live 2025 的 pdfLaTeX + BibTeX + latexmk 验证；最终稳定轮次的 LaTeX 日志
与 BibTeX 日志无警告，无 Overfull/Underfull box。首次编译中间轮次的暂时引用提示由 latexmk 自动解决。
更换论文内容后需重新检查，不保证任意新增图表或文本也无警告。

## 上游许可

CAS 文件来自 Elsevier CAS Bundle 2.4（2024-05-04），Copyright 2019–2024 Elsevier Ltd，
按 LPPL 1.3c 或更新版本许可。原始文件头与 `manifest.txt` 保留。
`elsarticle-num.bst` 来自本机 TeX Live 2025 的 Elsevier Elsarticle Bundle，版本 2.1，
Copyright 2007–2025 Elsevier Ltd；其原始文件头含 LPPL 1.3 或更新版本许可说明。
完整原版 CAS 包可通过上面的 CTAN 链接获取。
