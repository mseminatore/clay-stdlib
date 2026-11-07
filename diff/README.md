# stdlib/diff

Line-by-line diffs for Clay, using Myers' algorithm (the one behind `diff` and `git diff`), with
output in the unified format.

## Usage

```clay
import("stdlib/diff")

Diff lines("a\nb\nc\n", "a\nc\nd\n")
// [["=", "a"], ["-", "b"], ["=", "c"], ["+", "d"]]

Diff unified(File read("old.txt"), File read("new.txt"), "old.txt", "new.txt") print
Diff stats("a\nb\n", "a\nc\nd\n")    // #{"added": 2, "removed": 1}
```

| Method | Description |
|--------|-------------|
| `lines(a, b)` | The edit script: `["=", line]` kept, `["-", line]` only in `a`, `["+", line]` only in `b` |
| `unified(a, b, fromName, toName, context)` | A unified diff (`--- a` / `+++ b` / `@@ -l,n +l,n @@` hunks), `""` if the inputs are equal. Names default to `"a"` and `"b"`, context to 3 lines |
| `stats(a, b)` | `#{"added": n, "removed": n}` |

Inputs are strings, split into lines (a final newline doesn't add an empty line), or arrays of
lines. The diff is minimal — no shorter edit exists — and `unified` matches `diff -u` output. It
doesn't mark a missing final newline (`\ No newline at end of file`).
