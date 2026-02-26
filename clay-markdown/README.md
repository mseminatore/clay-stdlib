# clay-markdown

Markdown to HTML converter for Clay.

## Usage

```clay
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
| `- item` or `* item` | `<ul><li>item</li></ul>` |
| `1. item` | `<ol><li>item</li></ol>` |
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
