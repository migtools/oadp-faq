# CLAUDE.md

Guidance for AI assistants (Claude and others) working in this repo.

## About this repo

This repo contains `faq.txt`, the source content for the OADP (OpenShift API for Data
Protection) FAQ, which is published/consumed as a Red Hat Knowledgebase (KCS) article on
the Red Hat Customer Portal. All content must use the Markdown dialect supported by the
Customer Portal — **not HTML**. Raw HTML tags will not render.

As a customer or support technician, clear and concise information about OADP is very helpful.
This document should be written to avoid duplication and must not conflict with the official
[OADP backup and restore documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/latest/html-single/backup_and_restore/index).


Reference: [Markdown Help - Red Hat Customer Portal](https://access.redhat.com/articles/7056942)
(the official help page linked from the KCS article editing form). See also
[Case Comment Formatting (Markdown)](https://access.redhat.com/articles/4729621), which
documents the same underlying `marked.js` engine (CommonMark + GitHub Flavored Markdown)
used across the Customer Portal, including KCS articles.

## KCS Markdown formatting rules

| Element | Syntax | Notes |
|---|---|---|
| Headers | `# H1`, `## H2`, `### H3` (up to `######`) | One space after the hash(es) |
| Bold | `**bold text**` | |
| Italic | `_italic text_` or `*italic text*` | |
| Bold + italic | `***bold italic text***` | |
| Unordered list | `- item` or `* item` | Indent nested items by 2 spaces |
| Ordered list | `1. item` | |
| Inline code | `` `code` `` | Single backticks |
| Multiline code block | `~~~` ... `~~~` (tildes) | Triple backticks (`` ``` ``) also work, but this repo standardizes on tildes |
| Blockquote | `> text` | |
| Link | `[link text](https://example.com)` | Always use descriptive inline links, never bare URLs |
| Image | `![alt text](https://example.com/img.png)` | |
| Table (GFM) | `\| Col A \| Col B \|` header row + `\| --- \| --- \|` separator row | |
| Strikethrough (GFM) | `~~text~~` | Don't confuse with the `~~~` code fence |

**Do not use raw HTML** — the Customer Portal renders Markdown only; HTML tags will
display as literal text instead of being rendered.

## Conventions used in this repo's `faq.txt`

- **Questions** are `###` headers with the question bolded:
  `### **What is OADP?**`
- **Section dividers** (major topic groupings, used sparingly) are `##` headers, e.g.
  `## Frequently Asked Questions`.
- **Code, YAML, and CLI examples** are always fenced with `~~~`, not triple backticks.
  Keep this consistent throughout the file.
- **Bullets** use `-` or `*`; nested bullets are indented 2 spaces.
- **Links** are inline style only: `[descriptive text](url)`.
- **Inline code** (flags, field names, short commands like `` `oc get vsb` ``, `` `--ttl` ``)
  uses single backticks.
- The disclaimer at the top of the file uses a blockquote combined with bold-italic:
  `>***Disclaimer:** ...*`

## Checklist when adding/editing a FAQ entry

1. New questions get a `### **Question, phrased naturally?**` header, placed near
   related topics when possible (otherwise appended near the end of the file).
2. Write answers as plain paragraphs and/or bullets.
3. Fence any YAML/CLI/log output with `~~~`.
4. Use inline backticks for field names, flags, and short commands mentioned in prose.
5. Link to docs, GitHub issues, and Jira tickets with `[text](url)` instead of pasting
   bare URLs.
6. Before finishing, verify: header bold formatting is exactly `### **Q?**`, code fences
   use `~~~` not `` ``` ``, and no raw HTML was introduced.
