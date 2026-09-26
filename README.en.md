# Academic Translate

[中文](README.md) · [Usage guide in Chinese](docs/usage.md) · [Skill instructions](SKILL.md)

Translate academic PDFs and online documents in full, with English and Chinese paragraphs paired by default. Preserve figures, citations, original attachments, and editable LaTeX. Ordinary translation keeps the source name: local sources produce Markdown, while online sources produce a translation at the corresponding level of the original container.

This repository contains skill instructions and documentation only. It bundles no executable scripts, external code, or program dependencies. Reading, writing, and viewing use capabilities already available and authorized in the host.

## Four independent skills

| Skill | Responsibility |
| --- | --- |
| [academic-rename](https://github.com/kongweiguo/academic-rename) | Bibliographic naming, previews, renames, and restoration; the sole authority for naming rules |
| [academic-translate](https://github.com/kongweiguo/academic-translate) | Complete bilingual translation, figures, formulas, and delivery |
| [academic-read](https://github.com/kongweiguo/academic-read) | Guided close reading, technical explanations, and an experiment reproduction guide |
| [academic-suite](https://github.com/kongweiguo/academic-suite) | Coordinate naming, translation, and close reading, including overall progress |

Translation works independently. Load `academic-rename` only when naming normalization is explicitly requested; do not reconstruct its rules if it is unavailable. Use `academic-suite` for the combined workflow. Each specialist continues to own its instructions.

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

Hosts supporting that invocation syntax can also use `$academic-translate`. Translation does not rename the source or look up CCF grades, bibliographic dates, or title abbreviations solely for naming. Updating an existing translation does not implicitly rename it either.

## Output and location

`N` is the actual source filename without its real extension, or the current title of a native document. If the suite has completed a rename, use the verified current name. Explicit names and existing outputs take precedence.

| Source | Default output |
| --- | --- |
| Local PDF | `N_翻译/N_翻译.md` beside the source, with `images/` and `translation-state.json` |
| Lark / Feishu file or document | `N_翻译` in its actual parent folder; a sibling under the corresponding parent node for wiki sources |
| Notion page | A sibling translation under the page's actual parent |
| Online attachment | `N_翻译` inside the attachment's actual hosting page or container |
| Explicit destination or existing translation | Use the requested target |

A temporary download does not turn an online source into a local-source task. If the target cannot be located or written, report that limitation instead of silently using a workspace root or counting a local draft as online delivery. A matching name alone does not establish ownership of an existing output.

The local PDF stays in its original location with its original bytes. Markdown uses relative links to it and to images. Ordinary translation does not create a rename log. Keep historical `rename-log.json` files and resume existing outputs by their source identity and recorded paths or IDs, without rebuilding them under a newly calculated name.

## Translation requirements

- Pair each `[EN]` paragraph with a following quoted `[ZH]` paragraph; preserve section and list correspondence.
- Cover the requested body, footnotes, acknowledgments, figures, references, and appendices. Summaries or attachments do not replace translation.
- Begin with the translation/source heading, Paper Info card, source-file area, and actual scope statement. Use the full paper title in the content.
- Preserve original figures and their complete original captions, with Chinese captions separately. Prefer editable LaTeX and inspect actual rendering using existing viewing capabilities.
- For online output, insert a real native attachment when an original PDF exists; ordinary links are insufficient. Do not fabricate an original PDF for a text-only source.
- Preserve numbers, conditions, citations, and uncertainty. Flag suspected source errors in translator notes. Extended teaching belongs in the reading skill.

Detailed layout and delivery requirements live in the [translation workflow](references/workflow.md).

## Installation, updates, and portability

Installation means saving the complete skill directory. It does not depend on an agent, LLM, or its private directory. The recommended shared location is `~/.agents/skills/academic-translate/`, or `%USERPROFILE%\.agents\skills\academic-translate\` on Windows. A custom directory is equally valid; adjust the paths below accordingly. Keep `SKILL.md` at the directory root and preserve the relative `references/` structure and other files. Avoid an extra nested copy of the repository folder.

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

This release rebuilds Git history and uses `master` as the default branch. **For the first upgrade from an old clone, preserve local changes, move the old directory outside skill discovery, and clone again using the instructions above.** Review and transfer needed local edits to the new directory; do not copy the old `.git` directory or merge the old history. Papers, translations, and progress belong in task locations and are not replaced when updating skill files.

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

Load the [SKILL acceptance instructions](SKILL.md#通过-skill-验收), then read, inspect, and compare the source and outputs for completeness, figures, formulas, source access, and safe continuation. Review skill changes through the SKILL's document and scenario checks, without validator scripts or added dependencies. Distinguish document review from real platform checks and report anything not actually verified.

See the [usage guide](docs/usage.md) and [contribution guide](CONTRIBUTING.md), or report issues through [GitHub Issues](https://github.com/kongweiguo/academic-translate/issues) without exposing private papers or account data.

The existing [Apache License 2.0](LICENSE) remains in effect. User papers and private translations are not included.
