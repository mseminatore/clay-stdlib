# clay-markdown

Markdown to HTML converter for Clay.

## Usage

```clay
import("clay-stdlib/clay-markdown")

md = Markdown render("# Hello\n\nThis is **bold** and *italic*.")
// => "<h1>Hello</h1>\n<p>This is <strong>bold</strong> and <em>italic</em>.</p>"
```

## Supported Syntax

| Markdown | HTML |
|---|---|
| `# Heading` through `###### Heading` | `<h1>` through `<h6>` |
| `**bold**` | `<strong>bold</strong>` |
| `*italic*` | `<em>italic</em>` |
| `` `code` `` | `<code>code</code>` |
| `[text](url)` | `<a href="url">text</a>` |
| `![alt](src)` | `<img src="src" alt="alt">` |
| `- item`, `* item`, or `+ item` | `<ul><li>item</li></ul>` |
| `1. item` | `<ol><li>item</li></ol>` |
| Indented list items (`  - sub`) | Nested `<ul>`/`<ol>` |
| `\| col \| col \|` with separator | `<table>` with `<thead>`/`<tbody>` |
| `> quote` | `<blockquote>` |
| ` ``` ` fenced code blocks | `<pre><code>...</code></pre>` |
| `---`, `***`, `___` | `<hr>` |
| Blank lines | Paragraph breaks (`<p>`) |

## Examples

### Headings

```clay
Markdown render("# Title\n## Subtitle")
// => "<h1>Title</h1>\n<h2>Subtitle</h2>"
```

### Lists

```clay
Markdown render("- apples\n- oranges\n- bananas")
// => "<ul>\n<li>apples</li>\n<li>oranges</li>\n<li>bananas</li>\n</ul>"
```

### Nested Lists

```clay
Markdown render("- item 1\n  - sub a\n  - sub b\n- item 2")
// => "<ul>\n<li>item 1</li>\n<ul>\n<li>sub a</li>\n<li>sub b</li>\n</ul>\n<li>item 2</li>\n</ul>"
```

Indent by 2 spaces per nesting level. All three UL markers (`-`, `*`, `+`) are supported.

### Tables

```clay
Markdown render("| Name | Age |\n| :--- | ---: |\n| Alice | 30 |")
// => "<table>\n<thead>\n<tr><th>Name</th><th style=\"text-align: right\">Age</th></tr>
//     \n</thead>\n<tbody>\n<tr><td>Alice</td><td style=\"text-align: right\">30</td></tr>
//     \n</tbody>\n</table>"
```

Alignment markers in the separator row:
- `:---` — left (default)
- `:---:` — center
- `---:` — right

### Blockquotes

```clay
Markdown render("> This is a quote\n> with **bold** text")
// => "<blockquote><p>This is a quote\nwith <strong>bold</strong> text</p></blockquote>"
```

### Code Blocks

````clay
Markdown render("```\nx = 1\ny = 2\n```")
// => "<pre><code>x = 1\ny = 2</code></pre>"
````

### Links and Images

```clay
Markdown render("[Clay](https://clay-lang.org)")
// => "<p><a href=\"https://clay-lang.org\">Clay</a></p>"

Markdown render("![logo](logo.png)")
// => "<p><img src=\"logo.png\" alt=\"logo\"></p>"
```
