# stdlib/toml

A [TOML 1.0](https://toml.io) parser and writer for Clay.

## Usage

```clay
import("stdlib/toml")

cfg = Toml parse("[server]\nhost = \"localhost\"\nport = 8080\n")
(cfg get("server")) get("port")    // 8080

cfg = Toml parseFile("app.toml")
File write("out.toml", Toml stringify(cfg))
```

## Types

| TOML | Clay |
|------|------|
| table, inline table | `Dict` |
| array, array of tables | `Array` (of `Dict`s for `[[tables]]`) |
| string (all four kinds) | `String` |
| integer (decimal, `0x`, `0o`, `0b`, `_` separators) | `Number` |
| float | `Number` (Clay floats are 32-bit, so about 7 significant digits) |
| boolean | `true` / `false` |
| date, time, date-time | `String`, as written (`"1979-05-27T07:32:00Z"`) |

`inf` and `nan` are rejected, since Clay numbers can't hold them.

## Writing

`Toml stringify(dict)` writes plain keys first, then `[tables]` and `[[arrays of tables]]`, with
keys sorted and quoted when they aren't bare. Strings are written as basic strings with escapes, so
a date read as text comes back as a quoted string, and a float with no fractional part (`72.0`)
is written as an integer (`72`).

## Errors

Invalid input raises an error naming the line: `Toml: line 3: key 'port' is defined twice`. Keys
and `[tables]` can't be defined twice, and a key can't later become a table.
