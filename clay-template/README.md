# clay-template

Simple string template engine for Clay using `{{placeholder}}` syntax.

## Usage

```clay
import("clay-stdlib/clay-template")
```

## Rendering

```clay
data = Dict new()
data set("name", "World")
data set("count", "3")

Template render("Hello, {{name}}! You have {{count}} items.", data)
// => "Hello, World! You have 3 items."
```

## Rendering Collections

Use `renderEach` to render a template for each item in an array of Dicts:

```clay
items = Array new()

d1 = Dict clone; d1 set("name", "Alice")
d2 = Dict clone; d2 set("name", "Bob")
items push(d1)
items push(d2)

Template renderEach("<li>{{name}}</li>", items)
// => "<li>Alice</li><li>Bob</li>"

Template renderEach("<li>{{name}}</li>", items, ", ")
// => "<li>Alice</li>, <li>Bob</li>"
```

## Methods

| Method | Description |
|--------|-------------|
| `render(template, data)` | Replace `{{key}}` placeholders with values from a Dict |
| `renderEach(template, items, sep)` | Render template for each Dict in an array, joined by optional separator |

Values are converted to strings via `toString()` automatically.
