# stdlib/args

CLI argument parsing for Clay.

## Usage

```clay
import("stdlib/args")
```

## Parsing Arguments

```clay
parser = ArgParser new("myapp", "A sample application")
parser flag("verbose", "v", "Enable verbose output")
parser option("output", "o", "Output file", "out.txt")
result = parser parse(System args())

result get("verbose")       // true or false
result get("output")        // "out.txt" or user-provided value
result get("_positional")   // array of remaining args
```

## Defining Flags

Boolean flags are `false` by default and set to `true` when present:

```clay
parser flag("verbose", "v", "Enable verbose output")
parser flag("debug", "d", "Enable debug mode")
```

Flags can be passed as `--verbose` or `-v`.

## Defining Options

Options take a value and have a default:

```clay
parser option("output", "o", "Output file", "out.txt")
parser option("port", "p", "Port number", "8080")
```

Options are passed as `--output file.txt` or `-o file.txt`.

## Usage Help

```clay
parser usage()
```

Output:

```
myapp - A sample application
Options:
  --verbose, -v  Enable verbose output
  --output, -o <value>  Output file (default: out.txt)
```

## Methods

| Method | Description |
|--------|-------------|
| `new(name, desc)` | Create a new argument parser |
| `flag(name, short, help)` | Add a boolean flag |
| `option(name, short, help, default)` | Add an option with a default value |
| `parse(args)` | Parse an argument array, returns a Dict |
| `usage()` | Print usage help to stdout |

The API is chainable — `flag()` and `option()` return `self`.
