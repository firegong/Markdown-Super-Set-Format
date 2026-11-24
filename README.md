# Markdown Super Set Format

> **Base standard:** MultiMarkdown 6 (MMD). Syntax not supported by MMD is imported from **Pandoc Markdown → markdown-it → Obsidian** in that order.
> When the same feature exists in multiple standards, use the one that comes first.
>
> **Source attribution:** The Source column lists **every** standard that supports the feature. `(plugin)` means supported only via a markdown-it extension plugin.
> Abbreviations: CM = CommonMark, GFM = GitHub Flavored Markdown, MMD = MultiMarkdown 6, PD = Pandoc Markdown, MI = markdown-it, OB = Obsidian

## 0. Design Principles

1. **MMD first**: If MMD can express it, use only MMD syntax.
2. **Source order**: MMD → Pandoc → markdown-it (GFM family) → Obsidian.
3. **No conflicts**: The same symbol must not have two meanings; follow the "Conflict Resolution" rules below.
4. **Rendering safety**: Imported syntax should leave readable source text even without the tool.
5. **Input convenience**: A single character must not change behavior. Execution/rendering must be explicit via keywords (`run`, `render`).

## 1. Headings

| Feature | Syntax | Source | Notes |
|---|---|---|---|
| ATX heading | `# Title` | CM, GFM, MMD, PD, MI, OB | 1–6 levels |
| Setext heading | `Title` + `===` / `---` | CM, GFM, MMD, PD, MI, OB | |
| Heading ID | `## Title [#id]` | MMD, MI (plugin) | Link target: `[text](#id)` |
| Auto heading ID | (automatic) | GFM, MMD, PD, OB | When no explicit ID |

## 2. Emphasis and Text Formatting

| Feature | Syntax | Source | Notes |
|---|---|---|---|
| Italic | `*a*`, `_a_` | CM, GFM, MMD, PD, MI, OB | |
| Bold | `**a**`, `__a__` | CM, GFM, MMD, PD, MI, OB | |
| Nested emphasis | `***a***` | CM, GFM, MMD, PD, MI, OB | |
| Strikethrough | `~~a~~` | GFM, PD, MI, OB | Not in MMD |
| Subscript | `H~2~O` | MMD, PD, MI (plugin) | No spaces |
| Superscript | `x^2^` | MMD, PD, MI (plugin) | No spaces |
| Underline | `[a]{.underline}` | PD | `<u>a</u>` is the HTML alternative |
| Highlight | `==a==` | OB, MI (plugin) | |

## 3. Lists

| Feature | Syntax | Source | Notes |
|---|---|---|---|
| Unordered list | `-`, `*`, `+` | CM, GFM, MMD, PD, MI, OB | |
| Ordered list | `1.` | CM, GFM, MMD, PD, MI, OB | |
| Start number | `5.` | CM, GFM, MMD, PD, MI, OB | |
| Definition list | `term` then `: definition` | MMD, PD, MI (plugin) | |
| Task list | `- [ ] todo`, `- [x] done` | GFM, PD, MI (plugin), OB | Extended states in section 30 |
| Example list number | `(@)` | PD | For example numbering |

## 4. Code

| Feature | Syntax | Source | Notes |
|---|---|---|---|
| Inline code | `` `code` `` | CM, GFM, MMD, PD, MI, OB | |
| Indented code | 4-space indent | CM, GFM, MMD, PD, MI, OB | |
| Fenced code block | ` ``` ` | CM, GFM, MMD, PD, MI, OB | |
| Language | ` ```python ` | CM, GFM, MMD, PD, MI, OB | Static code |
| Code caption & label | ` ```python caption=example label=lst:name ` | PD (simplified attribute form) | See section 15 |
| Raw format block | ` ```{=latex} ` | PD | Output-specific |

## 5. Quotes, Line Breaks, Horizontal Rules, Pages

| Feature | Syntax | Source | Notes |
|---|---|---|---|
| Blockquote | `> content` | CM, GFM, MMD, PD, MI, OB | |
| Nested quote | `>> content` | CM, GFM, MMD, PD, MI, OB | |
| Callout | `> [!NOTE] title` | GFM (alerts), OB, MI (plugin) | `+`/`-` for expand/collapse (OB) |
| Horizontal rule | `---`, `***` | CM, GFM, MMD, PD, MI, OB | |
| Hard line break | trailing `\` | CM, GFM, MMD, PD, MI, OB | Two trailing spaces also work |
| Page break | `<!-- pb -->`, `<!-- pagebreak -->` | SuperMarkdown | See section 22 |
| Page break (LaTeX) | ` ```{=latex} \newpage ``` ` | PD | Raw block |

## 6. Links and Images

| Feature | Syntax | Source | Notes |
|---|---|---|---|
| Inline link | `[text](url)` | CM, GFM, MMD, PD, MI, OB | |
| Reference link | `[text][ref]` + `[ref]: url` | CM, GFM, MMD, PD, MI, OB | |
| Autolink | `<url>` | CM, GFM, MMD, PD, MI, OB | |
| Bare URL | `https://...` | GFM, MMD, PD, MI (plugin), OB | Without angle brackets |
| Wikilink | `[[doc]]`, `[[doc\|alias]]` | OB | Note links |
| Image | `![alt](src)` | CM, GFM, MMD, PD, MI, OB | |
| Image size | `![alt](src){width=50%}` | PD | |
| Image embed | `![[img.png\|300]]` | OB | Includes size |
| Figure caption | section 14 `caption=` | MMD, PD | Diagram chunk |
| Figure cross-ref | `[#fig:name]` | MMD | Definition in section 14 `label=fig:name` |

## 7. Tables

| Feature | Syntax | Source | Notes |
|---|---|---|---|
| Pipe table | `\| a \| b \|` | GFM, MMD, PD, MI, OB | |
| Alignment | `:---`, `:---:`, `---:` | GFM, MMD, PD, MI, OB | |
| Table caption & label | `[Table: caption] [#tbl:label]` | MMD, PD | After the table |
| Table cross-ref | `[#tbl:label]` | MMD | |
| Grid table | `+---+---+` | PD | For multi-line cells |
| Multi-line cells | Use grid tables | PD | |

## 8. Math, Footnotes, Citations, Metadata

| Feature | Syntax | Source | Notes |
|---|---|---|---|
| Inline math | `$a^2$` | GFM, MMD, PD, MI (plugin), OB | LaTeX |
| Display math | `$$ ... $$` | GFM, MMD, PD, MI (plugin), OB | LaTeX |
| Footnote | `[^1]` + `[^1]: content` | GFM, MMD, PD, MI (plugin), OB | |
| Citation | `[@key]`, `@key` | PD | Requires bibliography file |
| Cross-reference | `[#label]` | MMD | Headings, figures, tables, math |
| Metadata | `Key: Value` at top | MMD | |
| YAML metadata | `---` block | PD, OB (Properties) | Do not mix with MMD metadata |

## 9. Raw HTML, Comments, Escapes

| Feature | Syntax | Source | Notes |
|---|---|---|---|
| Inline HTML | `<span>` | CM, GFM, MMD, PD, MI, OB | GFM filters some tags |
| HTML block | `<div>...</div>` | CM, GFM, MMD, PD, MI, OB | |
| Comment | `<!-- comment -->` | CM, GFM, MMD, PD, MI, OB | Not rendered |
| Note comment | `%%comment%%` | OB | Use `<!-- -->` for tool compatibility |
| Escape | `\*`, `\#` | CM, GFM, MMD, PD, MI, OB | |

## 10. Note Linking (Obsidian)

| Feature | Syntax | Source | Notes |
|---|---|---|---|
| Tag | `#tag` | OB, MI (plugin) | `# ` (with space) at line start is a heading |
| Block reference | trailing ` ^id` | OB | Only at end of line |
| Block link | `[[doc#^id]]` | OB | |
| Heading link | `[[doc#heading]]` | OB | |

## Conflict Resolution Rules

| Conflict | Resolution |
|---|---|
| `^a^` (MMD superscript) vs `^id` (OB block ref) | Block ref only at **end of line**. Superscript in mid-sentence. |
| `~a~` (subscript) vs `~~a~~` (strikethrough) | `~~` is strikethrough, `~` is subscript. No subscript inside strikethrough. |
| `#tag` (OB) vs `# heading` (MMD) | Tag has no space after `#` and is not at line start. |
| `[#id]` (MMD heading ID) vs `[#label]` (MMD cross-ref) | `[#id]` at heading end is ID; `[#label]` in body is reference. |
| `{...}` (Pandoc attrs) vs `{width=...}` | Image/div attributes use Pandoc form; heading ID uses MMD `[#id]`. |
| `[[...]]` (OB wikilink) vs `[...]` (standard link) | `[[` is wikilink, `[` is standard link. |
| `%%` (OB comment) vs `%` (LaTeX) | `%%` is not interpreted as comment inside `$...$` math. |

## Supported Scope Summary

| Source | Imported features |
|---|---|
| MultiMarkdown | Full base syntax, definition lists, sub/superscript, heading IDs, table captions, figure/table cross-refs, math, footnotes, metadata |
| Pandoc Markdown | Strikethrough, underline span, task lists, example lists, code attributes/captions, raw blocks, image size, grid tables, citations, YAML metadata |
| markdown-it | GFM-family features and alert blocks (same syntax as Obsidian). No separate syntax added |
| Obsidian | Wikilinks, embeds, highlights, comments, tags, block refs, callouts, image size embeds |

## Notes

- This document is a **design proposal**. Actual renderers may differ; verify with samples.
- Do not mix Pandoc YAML and MMD metadata.
- Verify against each tool's official spec before final use.

## 11. Per-Format Supported Syntax

Each format's default, plugin-only, and unsupported syntax, regrouped from sections 1–10.

| Format | Basis | Default support | Plugin/extension only | Not supported |
|---|---|---|---|---|
| MultiMarkdown | MMD 6 | Headings (ATX/Setext) with ID `[#id]`, emphasis, sub/superscript, ordered/unordered lists, definition lists, start number, inline/fenced code (with language), indented code, quotes/nested quotes, HR, hard break, inline/reference/autolinks, bare URLs, images, pipe tables/alignment/captions, figure captions, cross-refs `[#label]`, math, footnotes, metadata, raw HTML, comments, escapes | None | Strikethrough, task lists, grid tables, attribute syntax `{...}`, citations `@key`, alert blocks, code attributes/captions, raw format blocks, page breaks |
| Pandoc Markdown | Pandoc 3 | Most MMD features + strikethrough, task lists, example lists `(@)`, underline span, code attributes/captions, raw format blocks, image size `{width=}`, grid tables, multi-line cells, citations `@key`, YAML metadata | None | Alert blocks, wikilinks, embeds, highlights `==a==`, comments `%%a%%`, tags, block refs |
| markdown-it | CommonMark + GFM family | Full CommonMark, strikethrough, pipe tables/alignment, autolinks, HTML options, comments | Task lists, definition lists, sub/superscript, highlights, math, footnotes, heading IDs (attrs), bare URLs (linkify), alert blocks, tags | Grid tables, multi-line cells, table captions, example lists, citations `@key`, block refs, wikilinks, embeds, comments `%%` |
| Obsidian | Obsidian Flavored Markdown | Full CommonMark, strikethrough, tables/alignment, task lists, footnotes, math (LaTeX), bare URLs, image embeds/sizes, callouts, YAML (Properties), wikilinks, embeds, highlights, comments `%%`, tags, block refs, heading links | None | Sub/superscript, definition lists, grid tables, multi-line cells, table captions, heading IDs, citations `@key`, cross-refs `[#label]`, code attributes/captions, raw format blocks, page breaks |

**Notes**
- Standard CommonMark defines only base syntax (headings, emphasis, lists, code, quotes, links, images, HTML, escapes). The rest are GFM or format extensions.
- Plugin items work only when the plugin is installed.
- This table is derived from sections 1–10 and may vary by version.

## 12. SuperMarkdown Table Extension (Cell Merging)

Rows above the separator `|---|---|---|` are **header** rows; rows below are **content cells**. If a cell contains only one of the markers below, it is interpreted as a merge directive. Header and content sections can each have one or more rows.

| Marker | Meaning | Merge target |
|---|---|---|
| `^` | Merge with cell above | Cell directly above |
| `<` | Merge with cell to the left | Cell directly to the left |
| `>` | Merge with cell to the right | Cell directly to the right |

### Merge Rules

| Rule | Description |
|---|---|
| Header merge | Cells within header rows can be merged with `<`, `>`, `^`. |
| Content merge | Cells within content rows can be merged with `<`, `>`, `^`. |
| No cross-section merge | Cells across the separator cannot be merged. `^` in the first content row cannot refer to a header cell. |
| Consecutive merge | Consecutive same-direction markers extend the merged region. E.g., 3-row vertical merge uses `^` in two consecutive rows. |
| Merged cell content | Content of the merged region is taken from the starting cell (top-left). |
| Escape | Use `\^`, `\<`, `\>` for the literal marker characters. |

### Example

```markdown
| Section | Measurement | < |
|---|---|---|
| Speed | Trial 1 | 10 |
| ^ | Trial 2 | 12 |
```

- Header `Measurement` spans 2 columns (Measurement, Result). The third column's `<` merges with `Measurement` to the left.
- First column `Speed` spans 2 rows. The second row's `^` merges with `Speed` above.

### Conflict Resolution

| Conflict | Resolution |
|---|---|
| Cell content `^`, `<`, `>` (literal text) | Only interpreted as merge marker when the entire cell is a single marker character. Escape with `\^` etc. for literal text. |
| MMD superscript `x^2^` | Only a cell whose entire content is a single `^` is a merge marker. In-sentence superscripts do not conflict. |
| Blockquote `>` | Blockquotes start with `>` at line start; table rows start with `|`, so no conflict. |
| Standard renderers | Standard renderers output markers as literal text. Merge applies only in SuperMarkdown renderers. |

## 13. Code Execution Results (Execution Chunks)

Execution is determined **only** by the `run` keyword. A single character or dot never changes behavior. Results are generated at render time by default, not written to the file.

### 13.1 Syntax Distinction

| Type | Syntax | Behavior |
|---|---|---|
| Static code | ` ```python ` | Highlight only. Not executed. |
| Execution chunk | ` ```{python run} ` | Execute code and display result. |
| Raw block | ` ```{=latex} ` | Insert verbatim into specific output format. (Pandoc) |

- Static code and execution chunks with the same language are distinguished by `{}` and the `run` keyword.
- Omitting `run` means static code; it is not executed. Use `run` only when execution is wanted.

### 13.2 Info String and Chunk Options

Caption and label go in the fence **info string** (section 15). Execution behavior goes in `#|` lines below the chunk's first line as `key: value`.

| Location | Option | Default | Meaning |
|---|---|---|---|
| Info string | `caption` | none | Caption |
| Info string | `label` | none | Label. Used for cross-refs like `[#lst:name]`. |
| `#\|` | `echo` | `true` | Show code |
| `#\|` | `output` | `true` | Show result |
| `#\|` | `cache` | `false` | Reuse stored result |
| `#\|` | `error` | `false` | Continue on error |

````markdown
```{python run label=calc caption=example}
#| echo: true
#| output: true
#| cache: false
print(1 + 2)
```
````

### 13.3 Result Rendering

- Results are displayed as render output immediately below the chunk. They are not written to the file body.
- `output: false` hides the result; `echo: false` hides the code. Both `false` means execute only.
- Results are stored only when `cache: true`. Storage location and format defined in 13.5.

### 13.4 Execution Permission

- Execution chunks run only when document metadata contains `execute: true`.
- If absent or `false`, execution chunks display code only without running.

```markdown
---
execute: true
---
```

### 13.5 Cached Results

- Results of `cache: true` chunks are stored under `.cache/` next to the document, using the chunk's `label` as filename.
- When code changes, the cache is invalidated and re-executed.
- Cache files should be excluded from version control.

### 13.6 Conflict Resolution

| Conflict | Resolution |
|---|---|
| `{python run}` execution chunk vs ` ```python ` static code | Distinguished only by the `run` keyword. No dot notation. |
| `#|` option lines vs regular code comments | Only consecutive `#|` lines immediately below the chunk's first line are options. |
| `label` vs cross-ref `[#label]` | Definition in info string `label=`; reference in body `[#label]`. |
| Execution permission vs security | If `execute` is absent, do not execute. |

## 14. Diagram Rendering Chunks

Languages that produce images from text (PlantUML, Mermaid, etc.) use the same execution-chunk mechanism, but the result is an **image** rather than a value. Rendering is controlled by the `render` keyword.

### 14.1 Syntax Distinction

| Type | Syntax | Behavior |
|---|---|---|
| Static code | ` ```plantuml `, ` ```mermaid ` | Rendered to image in body (backward compat). |
| Raw block | ` ```{=plantuml} `, ` ```{=mermaid} ` | Displayed as text only. |
| Rendering chunk | ` ```{plantuml render} `, ` ```{mermaid render} ` | Rendered to image in body. |

The `render` keyword follows the same rules as `run` in section 13.

### 14.2 Info String and Chunk Options

| Location | Option | Default | Meaning |
|---|---|---|---|
| Info string | `caption` | none | Figure caption |
| Info string | `label` | none | Figure label. Used for cross-refs `[#fig:name]`. |
| `#\|` | `format` | `svg` | Output format (`svg`, `png`) |
| `#\|` | `width` | none | Figure width (e.g., `60%`) |
| `#\|` | `echo` | `false` | Show code block alongside the image |
| `#\|` | `output` | `true` | Show image. `false` means do not render. |
| `#\|` | `cache` | `false` | Store rendered result for reuse |

### 14.3 Code and Image Display

| Purpose | Method | Result |
|---|---|---|
| Image only | `echo: false` (default) | Image only |
| Code and image | `echo: true` | Code block followed by image |
| Code only (no image) | `echo: true`, `output: false` | Code block only, not rendered |
| Code example only (no render) | ` ```plantuml ` static block | Text only |

````markdown
```{plantuml render caption="Login flow" label=fig:flow}
#| echo: true
#| format: svg
@startuml
Alice -> Bob: request
Bob --> Alice: response
@enduml
```
````

### 14.4 Execution Permission and Cache

- External renderers (Java, Kroki, etc.) are invoked, so rendering only happens when document metadata contains `execute: true`. Otherwise displayed as static code.
- When `cache: true`, rendered images are stored under `.cache/` with the `label` as filename. Same rules as 13.5.

### 14.5 Environment-Specific Behavior

- GitHub and Obsidian render ` ```mermaid ` by default, so static blocks show images there.
- Rendering chunks `{plantuml render}`, `{mermaid render}` work only in SuperMarkdown renderers. Other renderers display them as static code.

### 14.6 Conflict Resolution

| Conflict | Resolution |
|---|---|
| Rendering chunk vs static code | Distinguished only by the `render` keyword. |
| `echo` default difference | Execution chunks (section 13) default `echo: true`; diagram chunks (section 14) default `echo: false`. Image is the main content, so code is hidden by default. |
| Figure caption vs table caption | Figure uses info string `caption`; table uses `[Table: caption]`. |

## 15. Code Block Caption and Label

Caption and label go **only** in the fence info string. They are never written as `#|` options. Same rule applies to section 13 and 14 chunks.

### 15.1 Syntax

````markdown
```python caption="example code" label=lst:hello
print("hello")
```
````

| Type | Syntax | Notes |
|---|---|---|
| Static code | ` ```python caption=example label=lst:hello ` | Quotes optional if no spaces |
| Execution chunk | ` ```{python run caption=example label=lst:hello} ` | Same attributes as section 13 |
| Rendering chunk | ` ```{plantuml render caption="login flow" label=fig:flow} ` | Same attributes as section 14 |

### 15.2 Rules

- Values with spaces must be quoted. Values without spaces may omit quotes.
- Caption is displayed above the code block.
- `label` uses a prefix to indicate type: `lst:` (code), `fig:` (figure). Cross-references use `[#lst:name]`, `[#fig:name]`.
- If no caption or label, no caption area is created.

### 15.3 Conflict Resolution

| Conflict | Resolution |
|---|---|
| Info string `caption` vs `#|` option | Caption and label go only in info string. No `#| caption:` option is defined. |
| Info string `key=value` vs language name | Only `key=value` after the language name and a space is treated as an attribute. |
| Code caption vs figure caption | Both use `caption`. Type is distinguished by `label` prefix (`lst:`, `fig:`). |

## 16. Fenced Div (Section Blocks)

Pandoc-style fenced divs for grouping callouts, conditional blocks, tabs, etc. All attributes are optional.

### 16.1 Syntax

```markdown
:::{.warning title=caution}
Content is normal markdown.
:::
```

| Element | Meaning |
|---|---|
| `:::` (3+ colons) | Section start and end. Closing `:::` must have at least as many colons. |
| `.class` | Optional. CSS class. Used for styling and conditional output. |
| `#id` | Optional. Identifier. Only when cross-reference is needed. |
| `key=value` | Optional. E.g., `title`. Quote values with spaces. |

### 16.2 Nesting

Outer sections use more colons. Nesting is determined by colon count.

```markdown
::::{.tabset}
:::{.tab title=Python}
content
:::
::::
```

### 16.3 Conflict Resolution

| Conflict | Resolution |
|---|---|
| `:::` vs colons in body | Only `:::` alone at line start is a section. |
| Fenced div vs code block | `:::` inside code blocks is not a section. |

## 17. Callouts (Obsidian Syntax Unified)

Callouts use Obsidian syntax only. Fenced admonitions are not used.

### 17.1 Syntax

```markdown
> [!NOTE] Title
> Content is normal markdown.
```

| Element | Meaning |
|---|---|
| `> [!type]` | Callout start. Type inside brackets. |
| `title` | Rest of the line. If omitted, type name is used as title. |
| Lines after `> ` | Callout body. Starts with `>`. |

### 17.2 Types

Default types: `note`, `tip`, `warning`, `important`, `caution`, `danger`, `info`, `question`, `quote`, `example`, `abstract`, `success`, `failure`, `bug`, `todo`. Case-insensitive.

### 17.3 Collapse

| Notation | Behavior |
|---|---|
| `> [!NOTE]+ title` | Starts expanded |
| `> [!NOTE]- title` | Starts collapsed |
| `> [!NOTE] title` | No collapse |

### 17.4 Nesting

Callouts can nest. Increase quote depth by one.

```markdown
> [!NOTE] Outer
> > [!TIP] Inner
> > content
```

### 17.5 Conflict Resolution

| Conflict | Resolution |
|---|---|
| Callout vs regular quote | Only `[!type]` makes it a callout. Regular quotes use `>` only. |
| Callout type vs wikilink `[[...]]` | Callout starts with `[!`, distinguishing from wikilink. |
| Collapse `+`/`-` vs math/list symbols | Collapse symbol only immediately after `]`. |

## 18. Table Cell Checkbox

Task status inside table cells. Uses the same state characters as section 30.

```markdown
| Task | Status |
|---|---|
| Design | [x] |
| Implement | [ ] |
```

| Rule | Description |
|---|---|
| Allowed formats | `[ ]`, `[x]`, `[/]`, `[-]` (see section 30) |
| Rendering | Displayed as checkbox symbols. |
| Conflict with merge markers | Merge markers (section 12) are only interpreted when the entire cell is `^`, `<`, or `>`. No conflict. |

## 19. Table of Contents

```markdown
[TOC]
```

| Option | Default | Meaning |
|---|---|---|
| Depth | Headings 1–3 | Change with `[TOC depth=2]` |
| Position | Top of document | Place on its own line to set position. |

- `[TOC]` only on its own line. `[TOC]` in body text is not a TOC.
- TOC entries use heading IDs (section 1) as link targets.

## 20. Math Numbering and Reference

Math labels go after the closing `$$` line as `[#eq:label]`. Definitions and references both use `[#...]` format.

```markdown
$$
E = mc^2
$$ [#eq:energy]

Equation [#eq:energy] states ...
```

| Rule | Description |
|---|---|
| Numbering | Appending `[#eq:label]` after the closing `$$` line auto-numbers the equation. |
| Reference | Reference the number with `[#eq:label]`. |
| Conflict | Label only after closing `$$`. Distinguished from `{}` (LaTeX groups) inside math. |

## 21. Cross-Reference Auto-Numbering

Labels attached to headings, figures, tables, math, and code are referenced by number. All definitions use `[#type:name]` or info string `label=type:name`.

| Target | Label definition | Reference | Output example |
|---|---|---|---|
| Heading | `## Intro [#sec:intro]` | `[#sec:intro]` | Section 3.2 |
| Figure | Section 14 info string `label=fig:name` | `[#fig:name]` | Figure 2 |
| Table | `[Table: caption] [#tbl:label]` | `[#tbl:label]` | Table 1 |
| Math | Section 20 `$$ ... $$ [#eq:label]` | `[#eq:label]` | Equation (3) |
| Code | Section 15 info string `label=lst:name` | `[#lst:name]` | Listing 1 |

- Numbers are computed at render time. Do not write numbers in the file.
- Defining the same label twice is an error.

## 22. Page Breaks

Two formats are allowed; they mean the same thing.

```markdown
<!-- pb -->
<!-- pagebreak -->
```

| Output | Behavior |
|---|---|
| PDF, DOCX | Converted to page break |
| HTML, preview | Ignored |

- Only exactly `pb` or `pagebreak` triggers a page break. Other comments are regular comments (section 9).
- Existing raw LaTeX `\newpage` (section 5) is kept for LaTeX-only output.

## 23. Footnote Definition Blocks

Long footnotes use indentation for multiple lines and paragraphs.

```markdown
Body sentence[^long].

[^long]: First paragraph.

    Second paragraph uses 4-space indent.
```

| Rule | Description |
|---|---|
| Indentation | 4 spaces or 1 tab continues the footnote. |
| Reference | Connects to `[^label]` in body. |

## 24. Conditional Blocks

Content is included/excluded by output format. Uses fenced divs (section 16).

```markdown
:::{.only-html}
Visible only in HTML
:::

:::{.only-latex}
Visible only in PDF
:::
```

| Class | Target |
|---|---|
| `only-html` | HTML output |
| `only-latex` | LaTeX/PDF output |
| `only-docx` | DOCX output |

- Content is removed for non-target formats.

## 25. Variable Substitution

Insert document metadata values into body text.

```markdown
---
title: Design Doc
version: 1.2
---

{{title}} v{{version}}
```

| Rule | Description |
|---|---|
| Format | `{{key}}`. `{{ key }}` (with spaces) means the same. Key must exist in metadata. |
| Missing key | Show error and leave original text. |
| Execution | Variable substitution is not an execution chunk; works regardless of `execute` value. |
| Conflict | `{{ }}` inside code blocks is not substituted. |

## 26. Tab Blocks

Fenced div (section 16) with `tabset` class.

```markdown
::::{.tabset}
:::{.tab title=Python}
print("hi")
:::
:::{.tab title=R}
print("hi")
:::
::::
```

| Rule | Description |
|---|---|
| Outer section | `.tabset` class. 4+ colons. |
| Each tab | `.tab title=...` |
| Output | Formats without tab support expand tab titles as subheadings. |

## 27. File Inclusion

Split long documents and combine into one.

```markdown
@include chapters/intro.md
```

| Rule | Description |
|---|---|
| Format | `@include path`. Quote paths with spaces. |
| Path | Relative to current document. |
| Nesting | Included files can also use include syntax. Circular includes are errors. |
| Metadata | Included file metadata is overridden by top-level document. |
| Conflict | Only `@include ` at line start is an include. `@include` inside code blocks is not included. |

## 28. Post-Addition Conflict Summary

| Added syntax | Possible conflict with existing | Resolution |
|---|---|---|
| `:::` fenced div | Colons in body | Only `:::` alone at line start is a section. |
| `[TOC]` | Link `[TOC]` | Only on its own line. |
| `$$ ... $$ [#eq:label]` | Reference `[#label]` | Label only after closing `$$`. |
| `<!-- pb -->`, `<!-- pagebreak -->` | Regular comments | Only exactly `pb` or `pagebreak`. |
| `{{key}}` | LaTeX, templates | Outside code blocks, only if key exists in metadata. |
| `@include path` | Citation `@key` | Only `@include ` at line start. |
| `caption=`, `label=` | Language name | Only `key=value` after language name and space. |
| `run`, `render` keywords | Language name | Only keywords after language name and space. |

## 29. Keyboard Keys

Display keyboard keys. Base syntax uses bracket notation; `<kbd>` is the alternative for environments where brackets are hard to type.

### 29.1 Syntax

| Method | Syntax | Notes |
|---|---|---|
| Bracket key | `[Ctrl]+[S]` | Base syntax |
| HTML key | `<kbd>Ctrl</kbd>+<kbd>S</kbd>` | Alternative |

```markdown
Press [Ctrl]+[S] to save, [Esc] to cancel.
```

### 29.2 Rules

| Rule | Description |
|---|---|
| Key name | Key name inside brackets. E.g., `[Ctrl]`, `[Shift]`, `[Enter]`, `[F5]`. |
| Combination | Keys joined with `+`. Spaces allowed but default is no spaces. |
| Distinction from links | `[Ctrl]` followed immediately by `(url)` or `[ref]` is a link. For a key, put a space or other character after `[Ctrl]`. |
| Code blocks | Key notation is not interpreted inside code blocks or inline code. |
| Rendering | Displayed as rounded key caps. Unsupported renderers leave bracket text. |

### 29.3 Conflict Resolution

| Conflict | Resolution |
|---|---|
| `[text]` vs link `[text](url)`, `[text][ref]` | Immediately followed by `(` or `[` means link. |
| `[[...]]` wikilink | Double brackets are wikilink, not key notation. |
| Footnote `[^1]` | Starting with `^` means footnote. |
| Checkbox `[ ]`, `[x]` | Only after list marker or entire table cell. |

## 30. Extended Checklist States

Extends task list (section 3) and table cell checkbox (section 18) states from the standard two to four.

### 30.1 State Characters

| Char | Meaning | Display | Source |
|---|---|---|---|
| `[ ]` | Incomplete | Empty box | GFM, Obsidian |
| `[x]` | Complete (`[X]` also allowed) | Checked | GFM, Obsidian |
| `[/]` | In progress | Half-filled box | Obsidian extension |
| `[-]` | Cancelled | Box with horizontal line | Obsidian extension |

```markdown
- [ ] Design review
- [/] Implementing
- [x] Requirements defined
- [-] Deprecated approach
```

### 30.2 Rules

| Rule | Description |
|---|---|
| Case | `x` and `X` are the same complete state. |
| Standard compatibility | `[ ]` and `[x]` work in GFM and Obsidian. `[/]`, `[-]` display only in SuperMarkdown renderers and Obsidian extensions; elsewhere they remain as text. |
| Table cells | Table cell checkboxes (section 18) use the same state characters. |
| Aggregation | State counting is not part of the syntax. Use variables or tool features if needed. |

### 30.3 Conflict Resolution

| Conflict | Resolution |
|---|---|
| `[-]` vs list marker `-` | Only a state when `[-]` follows a list marker and space. |
| `[/]` vs path notation | Only a state at the start of a list item. `[/]` mid-sentence is literal text. |
| `[x]` vs callout `> [!type]` | Callouts start with `>`, distinguishing from list item checkboxes. |

---

## Supported Scope Summary

| Source | Imported features |
|---|---|
| MultiMarkdown | Full base syntax, definition lists, sub/superscript, heading IDs, table captions, figure/table cross-refs, math, footnotes, metadata |
| Pandoc Markdown | Strikethrough, underline span, task lists, example lists, code attributes/captions, raw blocks, image size, grid tables, citations, YAML metadata |
| markdown-it | GFM-family features and alert blocks (same syntax as Obsidian, integrated). No separate syntax added |
| Obsidian | Wikilinks, embeds, highlights, comments, tags, block refs, callouts, image size embeds |

## Notes

- This document is a **design proposal**. Actual renderers may differ; verify with samples.
- Do not mix Pandoc YAML and MMD metadata.
- Verify against each tool's official spec before final use.

## License

MIT License. See the SuperMark project for full license details.
