# Markdown

Markdown is a lightweight markup language with plain-text formatting syntax. It was created by John Gruber and Aaron Swartz in 2004 with the goal of enabling people to write content in an easy-to-read and easy-to-write format, which could then be converted to HTML for web publishing.

Markdown is commonly used for writing documentation, README files, blogs, and more, because of its simplicity and readability.

## Basic Syntax

Below are some of the most commonly used Markdown elements:

### Headers

Headers are used to create titles and subtitles. Use `#` for headers. The number of `#` symbols determines the level of the header.

```markdown
# H1 Header
## H2 Header
### H3 Header
#### H4 Header
##### H5 Header
###### H6 Header
```

### Emphasis

To emphasize text, you can use asterisks or underscores:

- *Italic*: Wrap text with one `*` or `_`.
- **Bold**: Wrap text with two `**` or `__`.
- ***Bold and Italic***: Wrap text with three `***` or `___`.

Example:
```markdown
*italic* or _italic_
**bold** or __bold__
***bold and italic*** or ___bold and italic___
```

### Lists

Markdown supports both ordered and unordered lists:

- **Unordered List**: Use `*`, `-`, or `+` to create bullet points.
  
```markdown
* Item 1
* Item 2
  * Sub-item 1
  * Sub-item 2
```

- **Ordered List**: Use numbers followed by a period.

```markdown
1. First item
2. Second item
   1. Sub-item
   2. Another sub-item
```

### Links

To create hyperlinks, use the following syntax:

```markdown
[Link Text](URL)
```

Example:
```markdown
[Visit GitHub](https://github.com)
```

### Images

To insert images, use a similar syntax as links, but precede it with an exclamation mark `!`.

```markdown
![Alt Text](ImageURL)
```

Example:
```markdown
![Markdown Logo](https://upload.wikimedia.org/wikipedia/commons/4/48/Markdown-mark.svg)
```

### Code

To format code, wrap the code with backticks:

- **Inline Code**: Use single backticks `` ` ``.

```markdown
This is `inline code`.
```

- **Code Block**: Use triple backticks ```` ``` ````.

```markdown
def hello_world():
    print("Hello, World!")
```

### Blockquotes

To create blockquotes, use the `>` symbol:

```markdown
> This is a blockquote.
```

### Tables

To create tables, use pipes `|` and dashes `-`:

```markdown
| Header 1 | Header 2 |
|----------|----------|
| Cell 1   | Cell 2   |
| Cell 3   | Cell 4   |
```

## Advanced Syntax

Markdown also includes some advanced syntax for more complex content:

- **Horizontal Rules**: Use three or more asterisks, dashes, or underscores.

```markdown
***
---
___
```

- **Strikethrough**: Wrap text with two tildes `~~`.

```markdown
~~This text is strikethrough~~
```

## Extensions and Variants

Many platforms, like GitHub or GitLab, offer extended versions of Markdown with additional features like checklists, task lists, and syntax highlighting for code blocks. These variations might include:

- **Task Lists**:
  ```markdown
  - [x] Completed task
  - [ ] Incomplete task
  ```

- **Footnotes**:
  ```markdown
  Here is a sentence with a footnote.[^1]

  [^1]: This is the footnote.
  ```

## Mermaid

Mermaid is a tool for creating diagrams and flowcharts in Markdown. It allows you to create diagrams using a simple syntax and generates the corresponding SVG or PNG images.

Online Playground: [Mermaid Chart - Create complex, visual diagrams with text. A smarter way of creating diagrams.](https://www.mermaidchart.com/play)


## Resources

- [Markdown Guide](https://www.markdownguide.org)
- [GitHub Markdown Documentation](https://docs.github.com/en/get-started/writing-on-github)
- [CommonMark Specification](https://commonmark.org)

