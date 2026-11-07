# stdlib/fs

File system helpers for Clay: walk a directory tree, match paths with globs, and copy, move or
remove whole directories. Built on the core `File` object.

## Usage

```clay
import("stdlib/fs")
```

## Walking a tree

```clay
Fs walk("src")                          // every file under src, as sorted paths
Fs walk("src") { |path| path println }  // or one at a time
```

Paths start with the directory you pass (`src/lib/a.clay`); directories themselves aren't listed.

## Globs

```clay
Fs glob("src/*.clay")       // .clay files directly in src
Fs glob("src/**/*.clay")    // ... and in every directory below it
Fs glob("**/README.md")     // anywhere under the current directory
Fs match("*.clay", "main.clay")   // true: match one name
```

Within a name, `*` matches any run of characters, `?` one character, and `[abc]`, `[a-z]` or
`[!abc]` one character from (or not from) a set. A path part that is exactly `**` matches any
number of directories, including none. Results are sorted; relative patterns are relative to the
current directory. Names starting with `.` are only matched by a pattern part that starts with `.`
(so `src/*` skips `src/.git`, and `src/.*` finds it).

## Creating, copying, moving, removing

| Method | Description |
|--------|-------------|
| `mkdirs(path)` | Create a directory and any missing parents; fine if it exists |
| `copyTree(from, to)` | Copy a file, or a directory and everything in it (existing files are replaced) |
| `move(from, to)` | Rename a file or directory; across file systems, copy then remove |
| `removeTree(path)` | Delete a file, or a directory and everything in it; `false` if it wasn't there |
| `withTempDir { \|dir\| ... }` | Run the block with a new empty temp directory, removed afterwards (also on error); returns the block's result |

```clay
Fs mkdirs("build/out/logs")
Fs copyTree("assets", "build/out/assets")
Fs withTempDir { |dir|
    File write(dir + "/scratch.txt", "...")
    // ...
}
Fs removeTree("build")
```

Paths use `/`, which Windows accepts too. Symbolic links are followed, so a link back up the tree
makes `walk` and `copyTree` loop.
