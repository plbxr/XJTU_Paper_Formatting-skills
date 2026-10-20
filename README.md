# 西安交通大学本科论文排版 Skills

基于随附的《本科论文作业模版+2026.doc》，提供面向 AI 助手的 Word 与 LaTeX 两套排版 Skill，用于创建、整理或核查西安交通大学本科毕业设计（论文）及毕业设计说明书。

项目包含操作指引、格式细则、原始 Word 模板和 LaTeX 正文骨架。具体排版工作由支持 Skill 的 AI 助手结合文档编辑或 TeX 编译工具完成。

## 选择合适的 Skill

| 使用场景 | Skill 名称 | 入口 |
| --- | --- | --- |
| 创建或修改 Word 论文，修复目录、导航、页眉页脚，核查格式与装订材料 | `xjtu-undergraduate-thesis` | [Word Skill](xjtu-undergraduate-thesis/SKILL.md) |
| 编写或迁移 LaTeX 论文，使用 XeLaTeX 排版并生成 PDF | `xjtu-latex-skill` | [LaTeX Skill](xjtu_latex_skill/SKILL.md) |

LaTeX Skill 的目录名为 `xjtu_latex_skill`，其 `SKILL.md` 中声明的名称为 `xjtu-latex-skill`。

## 目录结构

```text
paper-skill/
├── README.md
├── 本科论文作业模版+2026.doc          # 原始模板
├── xjtu-undergraduate-thesis/
│   ├── SKILL.md                    # Word 工作流程与交付要求
│   ├── assets/
│   │   └── 本科论文作业模版+2026.doc
│   └── references/
│       └── 2026-format.md          # Word 格式细则
└── xjtu_latex_skill/
    ├── SKILL.md                    # LaTeX 工作流程与交付要求
    ├── assets/
    │   ├── 本科论文作业模版+2026.doc
    │   └── thesis.tex              # A4 论文内页骨架
    └── references/
        ├── 2026-word-requirements.md
        └── latex-implementation.md # 格式映射、编译与核验说明
```

## 使用方式

将所需 Skill 的整个目录放入所用 AI 工具支持的 Skill 目录，保留 `SKILL.md`、`assets/` 和 `references/` 的相对位置。也可以直接让助手读取本项目中对应的 `SKILL.md`，再按其中指引处理论文。

开始前准备论文稿件或真实研究材料、封面信息、图表、参考文献，以及学院或导师的补充格式要求。明确本次任务是新建、迁移、局部修改还是仅核查。

### Word 示例

```text
请读取 xjtu-undergraduate-thesis/SKILL.md，依据随附的 2026 年模板
检查我的论文。修正标题层级、自动目录、图表编号和页眉页脚，
保留原有学术内容，另存新文件，并列出尚缺的装订材料。
```

在原稿副本上编辑。需要从 `.doc` 转成 `.docx` 时，应使用具备相应能力的文档工具，并在转换后检查分节符、域、图片、公式和表格。交付前更新目录与交叉引用，逐页核对实际渲染效果。

### LaTeX 示例

```text
请读取 xjtu_latex_skill/SKILL.md，以 assets/thesis.tex 为骨架，
将我提供的论文内容整理为 XeLaTeX 项目。保留真实图表和引用关系，
交付源码、本地资源与编译后的 PDF，并说明版式核验结果。
```

也可以直接复制骨架开始编写。在项目根目录执行以下 PowerShell 命令，将源码复制到独立工作目录后编译：

```powershell
New-Item -ItemType Directory -Path .\thesis-work -ErrorAction Stop
Copy-Item -LiteralPath .\xjtu_latex_skill\assets\thesis.tex -Destination .\thesis-work\thesis.tex
Set-Location .\thesis-work
# 编辑 thesis.tex，替换占位内容后编译。
xelatex -interaction=nonstopmode -halt-on-error thesis.tex
xelatex -interaction=nonstopmode -halt-on-error thesis.tex
```

编译环境需提供 XeLaTeX、`ctexbook` 及骨架中引用的宏包。当前骨架使用 `fontset=windows`，并指定宋体 `SimSun` 和 `Times New Roman`；在其他系统使用前需确认字体可用，或调整字体配置并核对版式。

两遍编译用于更新目录和交叉引用；若仍有未解析引用或页码变化，应继续编译至稳定。接入真实文献数据库后，还需按所选方案执行 BibTeX 或 Biber。详细说明见 [LaTeX 实现说明](xjtu_latex_skill/references/latex-implementation.md)。

## 主要格式约束

以下为随附模板的部分要求，完整细则见 [Word 格式细则](xjtu-undergraduate-thesis/references/2026-format.md) 和 [LaTeX 对应要求](xjtu_latex_skill/references/2026-word-requirements.md)。

| 项目 | 要求 |
| --- | --- |
| 题目与字数 | 题目不超过 35 个汉字；正文不少于 15000 字 |
| 摘要与关键词 | 中英文摘要分别成页、内容对应；摘要不少于 400 字，关键词 3～5 个 |
| 正文 | A4；中文宋体，英文和数字 Times New Roman；小四号，约 1.2 倍行距，首行缩进 2 字符 |
| 页边距 | 上 3.0 cm，下 2.5 cm，内外各 2.6 cm，左右对称 |
| 标题编号 | `1`、`1.1`、`1.1.1`；目录一般收录至三级标题 |
| 图表与公式 | 按章编号，如 `图1-3`、`表2-1`、`（3-1）`；图题在下、表题在上，表格采用三线表 |
| 分页与页码 | 目录和正文第一章从奇数页起排；前置内容用罗马数字，正文从阿拉伯数字 1 开始 |
| 页眉页脚 | 奇数页显示对应部分或章名，偶数页显示学校论文名称；页眉下方双横线，页码位于页脚外侧 |

## 使用边界与交付核验

- 模板中的示例研究、示范文献和占位文字需要替换为作者的真实材料；缺项应明确标记，不编造结果、文献、签名或评议结论。
- 学院、专业或导师有适用于当前论文的补充要求时，按用户指定的要求处理冲突，并记录所依据的版本。
- 原模板的示例页序与装订条款对主要符号表的位置存在分歧。新建最终装订稿按“中英文摘要 → 主要符号表（可选）→ 目录”处理；仅修订现稿格式时保留原顺序并说明差异。
- LaTeX 骨架提供 A4 论文内页。正式 A3 封面、任务书和评审等表格需使用学校提供的真实文件，按要求并入最终材料。
- Word 与 LaTeX 的字体度量、行距和分页存在差异。编译成功或样式设置完成后，仍需逐页对照原模板检查目录、页码、图表、公式和附录。
- 交付时说明修改范围、缺失材料及实际完成的核验。LaTeX 项目应包含源码、图表、文献等所需资源与编译说明；未实际编译或查看 PDF 时，应明确标注尚未完成的验证。
