# stdlib/path

Path manipulation utilities for Clay.

## Usage

```clay
import("stdlib/path")
```

## Examples

```clay
Path join(["src", "main.clay"])       // "src/main.clay"
Path dirname("/usr/bin/clay")         // "/usr/bin"
Path basename("/usr/bin/clay")        // "clay"
Path extension("file.clay")           // ".clay"
Path stem("file.clay")                // "file"
```

## Methods

| Method | Description |
|--------|-------------|
| `join(parts)` | Join an array of path segments with the path separator |
| `dirname(path)` | Return the directory portion of a path |
| `basename(path)` | Return the filename portion of a path |
| `extension(path)` | Return the file extension (including `.`) |
| `stem(path)` | Return the filename without extension |
| `sep()` | Return the path separator (`/`) |

Both `/` and `\` are recognized as separators for cross-platform compatibility.
