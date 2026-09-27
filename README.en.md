# Academic Translate

[中文](README.md) · [Usage guide in Chinese](docs/usage.md) · [Skill instructions](SKILL.md)

Translate academic PDFs and online documents in full, with English and Chinese paragraphs paired by default. Preserve figures, citations, and original attachments. All mathematical expressions must use editable LaTeX, including variables and short formulas within paragraphs. Ordinary translation keeps the source name. New outputs use a shared paper identifier and type marker, with navigation to verified source and reading resources. Local sources produce Markdown; online sources produce a translation at the corresponding level of the original container.

This repository contains skill instructions and documentation only. It bundles no executable scripts, external code, or program dependencies. Reading, writing, and viewing use capabilities already available and authorized in the host.

## Four independent skills

| Skill | Responsibility |
| --- | --- |
| [academic-rename](https://github.com/kongweiguo/academic-rename) | Shared numbers from current directory contents, bibliographic naming, previews, renames, and restoration; the sole authority for numbering and naming |
| [academic-translate](https://github.com/kongweiguo/academic-translate) | Complete bilingual translation, figures, formulas, and delivery |
| [academic-read](https://github.com/kongweiguo/academic-read) | Guided close reading, technical explanations, and an experiment reproduction guide |
| [academic-suite](https://github.com/kongweiguo/academic-suite) | Coordinate naming, translation, and close reading, including overall progress and the paper index |

Translation works independently. Read the directory numbering and type rules in `academic-rename` to choose a number from current contents or verify and reuse one from the same source version, without starting CCF checks, bibliographic normalization, or source renaming. If the rules or a complete directory listing are unavailable, do not guess a new number: resume existing outputs, continue content with naming pending, or use an explicit user-supplied name. Use `academic-suite` for the combined workflow. Translation alone does not create reading documents or a paper index.

## Quick start

Save the complete skill directory using the [installation instructions](#installation-updates-and-portability). Once the host has loaded the skill, describe the task in ordinary language:

```text
Use academic-translate to translate /path/to/paper.pdf in full into local English–Chinese Markdown.
```

```text
Use academic-translate to translate this Lark or Notion paper at the corresponding level of its original container: <source link>.
```

```text
Use academic-translate to resume <existing translation path or link>, preserving my edits and completing only the remaining content.
```

```text
Use academic-translate with LaTeX for all math, including inline formulas. Verify the existing reading document for the same paper, reuse its number, and add navigation to both outputs while preserving my edits.
```

Hosts supporting that invocation syntax can also use `$academic-translate`. Translation does not rename the source or look up CCF grades, bibliographic dates, or title abbreviations solely for naming. Updating an existing translation does not implicitly rename it either.

## Output and location

`B` is the base name without verified shared numbers, type markers, or the real extension, recorded separately from the actual source name. It may be a six-field bibliographic name or an ordinary source base name. Numbering and composed names follow [academic-rename's directory numbering section](https://github.com/kongweiguo/academic-rename/blob/master/references/naming.md#共享编号与目录取号) and [type-prefix and base-name section](https://github.com/kongweiguo/academic-rename/blob/master/references/naming.md#类型前缀与基本名); execution uses the installed version. Below, `P001` illustrates a number chosen from current directory contents or reused from a verified resource for the same source version. Explicit names and existing outputs take precedence.

Follow rename's rules to list all direct children of the current source parent directory or online container, without recursively scanning the library. A new number is the largest recognizable leading number plus one, starting at `P001` when none exists. First verify and reuse a number already present on a source, translation, or reading resource for the same source version; do not renumber existing outputs. Resolve the actual numbering scope through the naming rules when a different destination is specified. Share one number in memory for the same paper within a batch and reread the directory before writing. If a write result is unknown, inspect actual resources before choosing another number. Do not add numbering ledgers, counters, or reservation files. Preserve existing translation progress and rename recovery logs, without using them to issue numbers.

Similar names or matching hashes do not automatically merge resources. New versions must not link to older outputs and may need a new number. Numbers are not globally unique across directories and are not guaranteed to remain unused after deletion. Distinguish identical numbers across directories by actual scope paths or container IDs together with real resource IDs. The paper index displays outputs; it is not a numbering source.

| Source | Default output |
| --- | --- |
| Local PDF | `[P001][翻译]B/[P001][翻译]B.md` beside the source, with `images/` and `translation-state.json` |
| Lark / Feishu file or document | `[P001][翻译]B` in its actual parent folder; a sibling under the corresponding parent node for wiki sources |
| Notion page | A sibling translation under the page's actual parent |
| Online attachment | `[P001][翻译]B` inside the attachment's actual hosting page or container |
| Explicit destination or existing translation | Use the requested target |

A temporary download does not turn an online source into a local-source task. If the target cannot be located or written, report that limitation instead of silently using a workspace root or counting a local draft as online delivery. A matching name alone does not establish ownership of an existing output.

For example, when the current directory has no recognizable numbers, a new translation of `paper.pdf` uses `[P001][翻译]paper/[P001][翻译]paper.md`; the source remains `paper.pdf`. Reuse `P001` from an existing source or reading output after verifying the same source version. If other papers have a maximum number of `P012`, a new paper uses `P013`. Always link to the actual source name. Interpret older names such as `[原文]paper.pdf` through the rename rules without duplicating numbers or markers, or stripping similar title text by appearance.

The local PDF stays in its original location with its original bytes. Markdown uses relative links to it and to images. Ordinary translation does not create a rename log. Keep historical `rename-log.json` files and resume existing `_翻译` or `[翻译]B` outputs by their recorded paths or IDs without migrating or rebuilding them. Only an explicit request to rename existing outputs invokes rename planning; translation then repairs verifiable references, navigation, and progress while preserving user edits. Follow rename's length and collision rules, including the identifier, type marker, extension, and full destination path.

The opening navigation lists “原文｜翻译｜精读” (source, translation, reading), alongside the existing source link and attachments. Link a reading resource only after reading it and confirming the same source and version. Mark missing stages as not generated, not found, or awaiting verification, without candidate URLs. Within the task's authorization, synchronize navigation in an existing reading document; preserve user edits and record pending synchronization when it cannot be written. Do not bulk-edit sources. Verify relative paths and stable online URLs after renaming, and pass actual links and synchronization status to the suite for its paper index.

## Translation requirements

- Pair each `[EN]` paragraph with a following quoted `[ZH]` paragraph; preserve section and list correspondence.
- Cover the requested body, footnotes, acknowledgments, figures, references, and appendices. Summaries or attachments do not replace translation.
- Begin with the translation/source heading, document navigation, Paper Info card, source-file area, and actual scope statement. Use the full paper title in the content.
- Preserve original figures and their complete original captions, with Chinese captions separately; also provide LaTeX transcriptions of formulas in figures. Editable LaTeX is mandatory for all mathematics in English and Chinese paragraphs, tables, captions, footnotes, and appendices, including inline variables. Plain text, backticks, and screenshots cannot substitute for formulas.
- Use `$...$` for inline and `$$...$$` for display math in local Markdown; use native LaTeX math nodes online. Review every paragraph and inspect actual rendering, recording unfinished or unverified items instead of claiming completion. Keep actual code, commands, and configuration syntax intact.
- For online output, insert a real native attachment when an original PDF exists; ordinary links are insufficient. Do not fabricate an original PDF for a text-only source.
- Preserve numbers, conditions, citations, and uncertainty. Flag suspected source errors in translator notes. Extended teaching belongs in the reading skill.

Detailed layout and delivery requirements live in the [translation workflow](references/workflow.md).

## Installation, updates, and portability

Installation means saving the complete skill directory. It does not depend on an agent, LLM, or its private directory. The recommended shared location is `~/.agents/skills/academic-translate/`, or `%USERPROFILE%\.agents\skills\academic-translate\` on Windows. A custom directory is equally valid; adjust the paths below accordingly. Keep `SKILL.md` at the directory root and preserve the relative `references/` structure and other files. Avoid an extra nested copy of the repository folder.

Default shared-number output requires readable `academic-rename` directory rules or a verified handoff within the current batch, followed by a fresh directory read before writing. This skill alone can still use an explicit user-supplied name; it does not install other skills or invent numbering rules.

### Install with Git

This option uses Git already available on your machine. The destination must not exist for a fresh clone. Existing users should first read “Updates and migration from old versions” below.

macOS / Linux:

```bash
mkdir -p "$HOME/.agents/skills"
git clone --branch master https://github.com/kongweiguo/academic-translate.git "$HOME/.agents/skills/academic-translate"
```

Windows PowerShell:

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.agents\skills" | Out-Null
git clone --branch master https://github.com/kongweiguo/academic-translate.git "$env:USERPROFILE\.agents\skills\academic-translate"
```

### Install from ZIP

Download the [master branch ZIP](https://github.com/kongweiguo/academic-translate/archive/refs/heads/master.zip) and extract it with your operating system's archive tools. Rename the extracted `academic-translate-master` folder to `academic-translate`, then place it in the shared directory above or a custom location. The final path must be `<skill directory>/academic-translate/SKILL.md`. ZIP installation does not require Git.

### Load the skill

A shared storage directory does not guarantee automatic discovery by every host. If your host supports custom skill paths, add the location in its settings and refresh discovery as documented. Otherwise, explicitly request the actual file in ordinary language:

```text
Read ~/.agents/skills/academic-translate/SKILL.md and the reference files it requires for this task.
Then translate /path/to/paper.pdf in full into local English–Chinese Markdown.
```

On Windows, replace the skill path with `C:\Users\<username>\.agents\skills\academic-translate\SKILL.md`; for a custom installation, use its actual path. The host needs local file access to load a local directory. In a chat-only environment, provide `SKILL.md`, the relevant referenced documents, and the paper content; actual file or online delivery still depends on that environment's capabilities and authorization.

`$academic-translate` is optional syntax supported by some hosts. `agents/openai.yaml` is optional interface metadata, not a universal runtime dependency. Each environment needs its own skill files and authorized platform access; skills do not automatically synchronize accounts or outputs. Keep only one installation of the same skill within a discovery scope.

### Updates and migration from old versions

Git history was rebuilt previously, with `master` as the default branch. This feature update uses normal commits; clones already based on the new history can use the fast-forward commands below. **Only clones from before the history rebuild need to be replaced: preserve local changes, move the old directory outside skill discovery, and clone again.** Review and transfer needed local edits to the new directory; do not copy the old `.git` directory or merge the old history. Papers, translations, and progress belong in task locations and are not replaced when updating skill files.

After a fresh clone, preserve local changes before routine fast-forward updates:

macOS / Linux:

```bash
git -C "$HOME/.agents/skills/academic-translate" pull --ff-only origin master
```

Windows PowerShell:

```powershell
git -C "$env:USERPROFILE\.agents\skills\academic-translate" pull --ff-only origin master
```

If a fast-forward is unavailable, inspect local changes and history differences instead of forcing an overwrite. For ZIP installations, download the latest ZIP, preserve local edits, replace the old directory with the new one, and transfer needed edits after review; `git pull` does not apply.

When upgrading from the former combined workflow, retain the independent `academic-rename` skill rather than archiving it. Existing translations and logs remain usable. Naming previews, changes, and restoration now belong to rename; ordinary translation no longer renames sources by default.

## Review and contribution

Load the [SKILL acceptance instructions](SKILL.md#通过-skill-验收), then read, inspect, and compare the source and outputs for numbering from current directory contents or verified reuse, number-before-type naming, completeness, figures, formulas, source access, navigation, and safe continuation. Review skill changes through the SKILL's document and scenario checks, without validator scripts or added dependencies. Distinguish document review from real platform checks and report anything not actually verified.

See the [usage guide](docs/usage.md) and [contribution guide](CONTRIBUTING.md), or report issues through [GitHub Issues](https://github.com/kongweiguo/academic-translate/issues) without exposing private papers or account data.

The existing [Apache License 2.0](LICENSE) remains in effect. User papers and private translations are not included.
