# GitHub Flavored Markdown (GFM) – Feature Examples

This document demonstrates **GitHub Flavored Markdown (GFM)** features as rendered by the **GitHub Markdown viewer**.

| WHAT | LINK |
| --- | --- |
| Supported Code Languages in Codeblock | [https://rouge-ruby.github.io/docs/file.Languages.html](https://rouge-ruby.github.io/docs/file.Languages.html) |

---

## Table of Contents
- [Headings](#headings)
- [Text Formatting](#text-formatting)
- [Blockquotes](#blockquotes)
- [Lists](#lists)
- [Task Lists](#task-lists)
- [Links](#links)
- [Images](#images)
- [Code](#code)
- [Tables](#tables)
- [Horizontal Rules](#horizontal-rules)
- [Collapsible Sections](#collapsible-sections)
- [Footnotes](#footnotes)
- [Mentions & References](#mentions--references)
- [Emoji](#emoji)
- [Escaping Characters](#escaping-characters)

---

## Headings

```md
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```

---

## Text Formatting

```md
*Italic*
_Italic_

**Bold**
__Bold__

***Bold Italic***

~~Strikethrough~~

`Inline code`
```

Rendered:

*Italic*  
**Bold**  
***Bold Italic***  
~~Strikethrough~~  
`Inline code`

---

## Blockquotes

```md
> This is a blockquote.
>
> > Nested blockquote
```

Rendered:

> This is a blockquote.
>
> > Nested blockquote

---

## Lists

### Unordered List
```md
- Item A
- Item B
  - Subitem B1
  - Subitem B2
```

Rendered:

- Item A
- Item B
  - Subitem B1
  - Subitem B2

### Ordered List
```md
1. First
2. Second
3. Third
```

Rendered:

1. First
2. Second
3. Third

---

## Task Lists

```md
- [x] Completed task
- [ ] Incomplete task
- [ ] Another task
```

Rendered:

- [x] Completed task
- [ ] Incomplete task
- [ ] Another task

---

## Links

```md
[GitHub](https://github.com)
```

Rendered:

[GitHub](https://github.com)

---

## Images

```md
![GitHub Logo](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)
```

Rendered:

![GitHub Logo](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png)

---

## Code

### Inline Code
```md
Use `git status` to check the repository state.
```

### Fenced Code Block
```bash
git clone https://github.com/user/repo.git
cd repo
```

### Syntax Highlighting
```python
def hello(name: str) -> str:
    return f"Hello, {name}"
```

---

## Tables

```md
| Name   | Language | Stars |
|--------|----------|-------|
| Repo A | Python   | ⭐ 120 |
| Repo B | Go       | ⭐ 95  |
```

Rendered:

| Name   | Language | Stars |
|--------|----------|-------|
| Repo A | Python   | ⭐ 120 |
| Repo B | Go       | ⭐ 95  |

---

## Horizontal Rules

```md
---
***
___
```

---

## Collapsible Sections

```md
<details>
  <summary>Click to expand</summary>
  Hidden content
</details>
```

Rendered:

<details>
  <summary>Click to expand</summary>
  Hidden content
</details>

---

## Footnotes

```md
Here is a statement with a footnote.[^1]

[^1]: This is the footnote text.
```

Rendered:

Here is a statement with a footnote.[^1]

[^1]: This is the footnote text.

---

## Mentions & References

```md
@github-user

#123

user/repository#456
```

---

## Emoji

😄 🚀 🎉

---

## Escaping Characters

```md
\*Not italic\*
\# Not a heading
\`Not code\`
```

---

## Notes

- Uses GitHub Flavored Markdown (GFM)
- Best viewed on github.com
