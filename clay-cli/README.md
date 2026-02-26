# clay-cli

ANSI terminal colors and styles for CLI tools.

> **Note:** This brick requires `String chr(code)` to be available in the
> Clay runtime so that the ESC character (ASCII 27) can be produced.

## Usage

```clay
cli = Cli
cli red("Error!") println()
cli success("All tests passed") println()
```

## API

### Foreground Colors

| Method        | ANSI Code | Example                      |
|---------------|-----------|------------------------------|
| `red(s)`      | 31        | `cli red("text")`            |
| `green(s)`    | 32        | `cli green("text")`          |
| `yellow(s)`   | 33        | `cli yellow("text")`         |
| `blue(s)`     | 34        | `cli blue("text")`           |
| `magenta(s)`  | 35        | `cli magenta("text")`        |
| `cyan(s)`     | 36        | `cli cyan("text")`           |
| `white(s)`    | 37        | `cli white("text")`          |

### Background Colors

| Method         | ANSI Code | Example                       |
|----------------|-----------|-------------------------------|
| `bgRed(s)`     | 41        | `cli bgRed("text")`           |
| `bgGreen(s)`   | 42        | `cli bgGreen("text")`         |
| `bgYellow(s)`  | 43        | `cli bgYellow("text")`        |
| `bgBlue(s)`    | 44        | `cli bgBlue("text")`          |

### Styles

| Method          | ANSI Code | Example                        |
|-----------------|-----------|--------------------------------|
| `bold(s)`       | 1         | `cli bold("text")`             |
| `dim(s)`        | 2         | `cli dim("text")`              |
| `italic(s)`     | 3         | `cli italic("text")`           |
| `underline(s)`  | 4         | `cli underline("text")`        |

### Custom Codes

| Method           | Description                          | Example                         |
|------------------|--------------------------------------|---------------------------------|
| `color(s, code)` | Apply a custom foreground ANSI code  | `cli color("text", 33)`        |
| `bg(s, code)`    | Apply a custom background ANSI code  | `cli bg("text", 44)`           |

### Utilities

| Method     | Description                              | Example                          |
|------------|------------------------------------------|----------------------------------|
| `strip(s)` | Remove ANSI escape sequences from string | `cli strip(colored)`             |

### Convenience Methods

| Method        | Effect      | Example                          |
|---------------|-------------|----------------------------------|
| `success(s)`  | Green bold  | `cli success("OK")`             |
| `warning(s)`  | Yellow bold | `cli warning("Caution")`        |
| `error(s)`    | Red bold    | `cli error("Failed")`           |

## ANSI Escape Format

Each method wraps text in ANSI escape sequences:

```
ESC[<code>m  +  text  +  ESC[0m
```

Where `ESC` is the ASCII escape character (byte 27). The reset code
`ESC[0m` restores the terminal to its default style after the text.

## Composing Styles

Methods can be nested to combine styles:

```clay
// Bold red text
cli bold(cli red("Error!")) println()

// Underlined cyan
cli underline(cli cyan("link")) println()
```

The convenience methods `success`, `warning`, and `error` already combine
a color with bold for common use cases.
