---
name: kcs-markdown-formatting
description: Reference for the Red Hat Knowledgebase (KCS) / Customer Portal Markdown dialect (marked.js, CommonMark + GitHub Flavored Markdown) as documented at access.redhat.com/articles/7056942, plus this repo's faq.txt formatting conventions. Use when writing, editing, or reviewing faq.txt, adding new FAQ entries, or when the user asks about KCS/Customer Portal markdown formatting rules.
---

# KCS Markdown Formatting

`faq.txt` in this repo is written in the same Markdown dialect used by the Red Hat
Customer Portal / Knowledgebase (KCS) editing form. The portal renders Markdown, not
HTML — raw HTML tags will NOT render and should be avoided. The engine is `marked.js`,
which supports CommonMark plus GitHub Flavored Markdown (GFM) extensions (tables,
strikethrough, autolinks).

Sources: [Markdown Help](https://access.redhat.com/articles/7056942) (KCS editing form
help) and [Case Comment Formatting (Markdown)](https://access.redhat.com/articles/4729621)
(documents the same marked.js engine used portal-wide).

## Syntax reference

| Element | Syntax | Notes |
|---|---|---|
| Headers | `# H1`, `## H2`, `### H3` (up to `######`) | One space after the hashes |
| Bold | `**bold text**` | |
| Italic | `_italic text_` or `*italic text*` | |
| Bold + italic | `***bold italic***` | Used for the disclaimer banner in this repo |
| Unordered list | `- item` | Indent nested items with 2 spaces: `  - subitem` |
| Ordered list | `1. item` | |
| Inline code | `` `code` `` | Single backticks |
| Multiline code block | fence with `` ~~~ `` ... `` ~~~ `` (or `` ``` `` ... `` ``` ``) | This repo consistently uses `~~~` — match that convention |
| Blockquote | `> text` | |
| Link | `[link text](https://example.com)` | |
| Image | `![alt text](https://example.com/img.png)` | |
| Table (GFM) | `\| Col A \| Col B \|` header row, then `\| --- \| --- \|` separator | |
| Strikethrough (GFM) | `~~text~~` | Don't confuse with the `~~~` code fence |

## Repo conventions in faq.txt

Follow the existing patterns already used throughout `faq.txt`:

- **Questions** are `###`-level headers with the question text bolded:
  `### **What is OADP?**`
- **Section dividers** (rarely used, for major topics) are `##`-level headers, e.g.
  `## Frequently Asked Questions`.
- **Code/YAML/CLI examples** are always fenced with `~~~` (tilde), not triple backticks.
  Keep this consistent for the whole file.
- **Bullets** use `-` or `*` for unordered lists; nested bullets are indented 2 spaces.
- **Links** are always inline style: `[descriptive text](url)` — never bare URLs or
  reference-style `[text][id]` links.
- **Inline code** (flags, field names, commands like `` `oc get vsb` ``, `` `--ttl` ``)
  uses single backticks.
- The top-of-file legal disclaimer uses the blockquote + bold-italic combo:
  `>***Disclaimer:** ...*`
- Do not use raw HTML — it will not render on the Customer Portal.

## Adding or editing a FAQ entry

1. Add a new `### **Question, phrased naturally?**` header at the appropriate place
   (grouped near related topics when possible; otherwise append near the end).
2. Write the answer as plain paragraphs and/or `-`/`*` bullets.
3. Use `~~~` fences for any YAML, CLI, or log output.
4. Use inline `` `code` `` for field names, flags, and short commands mentioned in prose.
5. Link out to docs/GitHub issues/Jira with `[text](url)` rather than pasting bare URLs.
6. Before finishing, scan the diff for: mismatched header bold (`### **Q?**` not
   `###**Q?**` or `### Q?`), backtick vs tilde code fences, and stray HTML tags.
