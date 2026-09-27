# Academic Translate · 学术文献翻译

[English](README.en.md) · [使用指南](docs/usage.md) · [技能入口](SKILL.md)

完整翻译学术 PDF 和在线文档，默认提供英文原文与中文译文逐段对照，保留图表、引用和原始附件。全文数学表达式强制使用可编辑 LaTeX，包括段落内的变量和短公式。普通翻译保留源名称，新成果使用共享编号与类型标签，并关联已核实的原文和精读；本地输出 Markdown，在线在原文对应层级创建译文。

本仓库只分发技能指令和文档，不附带执行脚本、外部代码或程序依赖。实际读取、写入和查看使用宿主已经提供并授权的能力。

## 四个独立技能

| 技能 | 用途 |
| --- | --- |
| [academic-rename](https://github.com/kongweiguo/academic-rename) | 共享编号与目录取号、统一书目命名、改名预览、执行和恢复；编号和命名规则的唯一来源 |
| [academic-translate](https://github.com/kongweiguo/academic-translate) | 完整对照翻译、图表公式及译文交付 |
| [academic-read](https://github.com/kongweiguo/academic-read) | 原理教学、论文精读与实验复现指南 |
| [academic-suite](https://github.com/kongweiguo/academic-suite) | 一次编排命名、翻译和精读，管理整体进度和论文索引 |

本技能可以独立完成翻译。普通翻译读取 `academic-rename` 的共享编号、目录取号及类型规则，现场取号或核实复用同源同版本资源的已有编号，不触发 CCF、书目规范化或源改名。缺少规则或无法完整列出当前目录时不猜新号，可继续已有成果、完成内容并标明命名待处理，或使用用户指定名称。完整处理三项工作可调用 `academic-suite`；单独翻译不自动创建精读或论文索引。

## 快速开始

先按[安装说明](#安装更新与跨宿主使用)保存完整技能目录。宿主已加载本技能时，直接用自然语言提出任务：

```text
使用 academic-translate，完整翻译 /path/to/paper.pdf，生成本地中英对照 Markdown。
```

```text
使用 academic-translate，翻译这篇飞书或 Notion 文献，在原文对应层级创建译文：〈源链接〉。
```

```text
使用 academic-translate，继续〈已有译文路径或链接〉，保留已有编辑，只补完剩余部分。
```

```text
使用 academic-translate，全文公式（包括段落内公式）都用 LaTeX。核实同篇已有精读并复用编号，在译文和精读开头补齐关联导航，保留我的编辑。
```

在支持该语法的宿主中也可使用 `$academic-translate`。单独翻译不改源名，不为命名查询 CCF、日期或标题缩写；指定已有译文时也不顺带修改其名称。

## 成果与位置

`B` 为不含已核实共享编号、类型标记和真实扩展名的基本名，可为六段书目名或普通源基本名，与实际源名分别记录。编号及名称组合遵循 [academic-rename 的“共享编号与目录取号”](https://github.com/kongweiguo/academic-rename/blob/master/references/naming.md#共享编号与目录取号)和[“类型前缀与基本名”](https://github.com/kongweiguo/academic-rename/blob/master/references/naming.md#类型前缀与基本名)，执行时读取实际安装版本。以下 `P001` 仅示意现场取得或从同源同版本资源复用的编号；指定名称和已有成果优先。

按 rename 规则完整列出当前源父目录或在线父容器的直接子项，不递归全库；新号取当前最大可识别前置编号加一，没有则用 `P001`。原文、译文或精读已有同源同版本编号时先核实后复用，不自动重编。指定输出位置时按命名规则确认实际范围。同批同篇共享内存交接编号，写入前重读目录；结果未知先读真实资源，不立刻另取号。不新增编号账本、计数器或占号文件；原有翻译进度和改名恢复日志继续保留，但不作为发号依据。

名称相似或同哈希不自动合并，新版本不关联旧成果，必要时另取新号。编号不承诺跨目录全局唯一或删除后永不复用；跨目录同号以实际范围路径/容器 ID 和真实资源 ID 区分。论文索引只展示实际成果，不参与取号。

| 来源 | 默认成果 |
| --- | --- |
| 本地 PDF | 原文件旁的 `[P001][翻译]B/[P001][翻译]B.md`，配套 `images/` 和 `translation-state.json` |
| 飞书/Lark 文件或正文 | 实际父目录内的 `[P001][翻译]B`；知识库在对应节点父级创建同级成果 |
| Notion 页面 | 原页面实际父级下的同级译文 |
| 在线附件 | 在实际承载页面或容器内创建 `[P001][翻译]B` |
| 指定目的位置或已有译文 | 按指定目标执行 |

在线来源的临时下载不改变输出归属。无法定位或写入目标时明确说明，不擅自换到根目录或把本地草稿当作在线交付。同名成果先核验来源；无关文件和用户修改不会被覆盖。

例如当前目录无可识别编号时，`paper.pdf` 的新译文使用 `[P001][翻译]paper/[P001][翻译]paper.md`，源仍叫 `paper.pdf`。若真实源或已有精读含 `P001`，核实同源同版本后复用；目录已有其他论文的最大编号 `P012` 时，新论文取 `P013`。源链接始终指向实际名称。`[原文]paper.pdf` 等旧类型名由 rename 规则解释，不叠加编号或类型；题名中的相似文字不凭词形删去。

本地原 PDF 保留原位置和字节，译文通过相对链接访问原件和 `images/`。普通翻译不生成改名日志；旧成果中的 `rename-log.json` 继续保留。已有 `_翻译` 或 `[翻译]B` 成果按记录路径或 ID 原位续作，不因编号或类型规则更新迁移或重建。只有用户明确要求改成果名称时才交由 rename 规划，本技能修复可验证的引用、导航和进度并保留用户修改。名称长度和冲突统一按 rename 规则检查，包含编号、类型、扩展名及完整目标路径。

译文开头提供“原文｜翻译｜精读”导航，保留原有源链接与附件。精读必须实际读取并确认同源同版本才关联；缺失阶段标“未生成”“未找到”或“待核实”，不生成候选 URL。任务授权范围内同步已有精读的导航，用户修改或不可写处记为待同步；不批量改原文。改名后核验本地相对路径和在线稳定 URL，链接及同步状态交 suite 维护论文索引。

## 翻译要求

- 默认按段落输出 `[EN]` 原文，再输出引用块中的 `[ZH]` 中文，章节与列表保持对应。
- 覆盖用户范围内正文、脚注、致谢、图表、参考文献及附录，不以摘要或附件代替翻译。
- 开头依次为“翻译说明和源文件”、文档导航、论文信息卡、源文件区和实际范围说明。正文使用完整题名。
- 图表保留原始图像和完整原始题注，中文题注另置；图中公式另附 LaTeX 转写。全文所有数学表达式必须使用可编辑 LaTeX，包括中英段落、表格、题注、脚注及附录中的行内公式和变量；不能用纯文本、反引号或截图替代。
- 本地行内公式用 `$...$`、独立公式用 `$$...$$`；在线使用 LaTeX 数学节点。逐段核对转写和实际渲染，无法完成时保留待处理/未验证状态。真实代码、命令和配置项保持原有语法。
- 在线有原始 PDF 时插入真实原生附件，普通链接不能替代；来源只有在线正文时不虚构原始 PDF。
- 保留数字、条件、引用和不确定性；疑似原文错误用译者注说明。深入教学和扩展分析交给精读技能。

详细内容、排版与交付规则只在 [翻译工作流](references/workflow.md) 维护。

## 安装、更新与跨宿主使用

安装只是保存完整的技能目录，不绑定 agent、LLM 或其私有目录。推荐通用位置 `~/.agents/skills/academic-translate/`；Windows 对应 `%USERPROFILE%\.agents\skills\academic-translate\`。也可自选目录，并相应替换以下路径。目录根部须包含 `SKILL.md`，保留 `references/` 等原有相对结构；不要把整份仓库嵌套在另一个同名目录中。

默认共享编号输出需能读取 `academic-rename` 的目录取号规则或接收同批已核实交接，写入前仍回读目录；单独安装本技能仍可按用户指定名称工作，不自动安装其他技能或自造编号规则。

### 使用 Git 安装

本方式使用本机已有的 Git。首次安装时目标目录应不存在；已有旧版用户先阅读下方“更新与旧版升级”。

macOS / Linux：

```bash
mkdir -p "$HOME/.agents/skills"
git clone --branch master https://github.com/kongweiguo/academic-translate.git "$HOME/.agents/skills/academic-translate"
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.agents\skills" | Out-Null
git clone --branch master https://github.com/kongweiguo/academic-translate.git "$env:USERPROFILE\.agents\skills\academic-translate"
```

### 使用 ZIP 安装

下载 [master 分支 ZIP](https://github.com/kongweiguo/academic-translate/archive/refs/heads/master.zip)，使用系统解压功能解压。将得到的 `academic-translate-master` 文件夹改名为 `academic-translate`，放入上述通用目录或自选位置。确认最终路径为 `<技能目录>/academic-translate/SKILL.md`。ZIP 安装无需 Git。

### 加载技能

通用存放目录不保证被所有宿主自动发现。宿主支持自定义技能路径时，将该位置加入其配置并按说明刷新；没有自动发现时，使用普通自然语言明确读取实际路径：

```text
请读取 ~/.agents/skills/academic-translate/SKILL.md，按其中引用读取所需参考文件，
然后完整翻译 /path/to/paper.pdf，生成本地中英对照 Markdown。
```

Windows 可将技能路径替换为 `C:\Users\<用户名>\.agents\skills\academic-translate\SKILL.md`；自选安装位置使用对应实际路径。需要支持本地文件读取的宿主；纯聊天环境可提供 `SKILL.md` 和它引用的所需文档，再提供论文内容，实际文件或在线交付仍取决于该环境的能力和授权。

`$academic-translate` 仅是部分宿主支持的可选调用语法。`agents/openai.yaml` 是可选界面元数据，不是通用运行依赖。每个执行环境分别准备技能和平台授权，技能不会自动同步账号或成果；同一发现范围只保留一份同名技能。

### 更新与旧版升级

仓库此前已重建 Git 历史，默认分支为 `master`，本次功能更新以普通提交发布，已使用新历史的克隆直接按下方快进更新。**只有仍使用历史重建前的旧克隆时，才先保存本地修改，将旧目录移到技能发现范围之外，再重新克隆。** 需要的本地修改经核对后迁入新目录；不要复制旧 `.git`，也不要合并旧历史。论文、译文及进度应保存在任务位置，不随技能目录更新。

新克隆后常规更新先保存本地修改，再使用快进更新：

macOS / Linux：

```bash
git -C "$HOME/.agents/skills/academic-translate" pull --ff-only origin master
```

Windows PowerShell：

```powershell
git -C "$env:USERPROFILE\.agents\skills\academic-translate" pull --ff-only origin master
```

无法快进时先检查本地修改和历史差异，不强行覆盖。ZIP 安装则重新下载 ZIP，保存本地修改后用新目录替换旧目录，并按需迁回修改，不使用 `git pull`。

从原先的合并工作流升级后仍保留独立 `academic-rename`，不要按旧说明将它归档或删除。旧译文和日志继续可用；命名预览、执行和恢复改由 rename 处理，普通翻译默认不再改名。

## 验收与贡献

按 [SKILL 中的验收要求](SKILL.md#通过-skill-验收) 阅读、回读和对照原文，检查现场目录取号或已有编号复用、编号与类型顺序、内容完整性、图表公式、源访问、导航及续作行为。数学验收逐段覆盖中英两侧的行内表达式，不能只查编号公式；纯文本或截图替代公式不能通过。技能维护也通过加载 SKILL 做文档及场景评审，不运行校验脚本、不新增校验依赖；未实际查看的平台显示或附件须列为未验证。

常见问题和操作示例见 [使用指南](docs/usage.md)，修改方式见 [贡献说明](CONTRIBUTING.md)。可通过 [Issues](https://github.com/kongweiguo/academic-translate/issues) 反馈问题，避免公开私人论文和账户信息。

本项目沿用 [Apache License 2.0](LICENSE)，不包含用户论文和私人译文。
