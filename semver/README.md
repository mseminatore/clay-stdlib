# stdlib/semver

[Semantic Versioning 2.0.0](https://semver.org) for Clay: parse and compare versions, and test
them against npm-style ranges.

## Usage

```clay
import("stdlib/semver")

v = Semver parse("v1.4.2-beta.1+build.5")
v major         // 1
v prerelease    // "beta.1"
v toString      // "1.4.2-beta.1+build.5"

Semver compare("1.2.3", "1.10.0")                 // -1
Semver sort(["1.10.0", "1.2.0", "1.2.0-rc.1"])    // ["1.2.0-rc.1", "1.2.0", "1.10.0"]
Semver satisfies("1.4.2", "^1.2")                 // true
Semver maxSatisfying(["1.2.0", "1.9.1", "2.0.0"], "~1.9")   // "1.9.1"
Semver inc("1.4.2", "minor")                      // "1.5.0"
```

| Method | Description |
|--------|-------------|
| `parse(s)` | A version with `major`, `minor`, `patch`, `prerelease`, `build`; a leading `v` is allowed. Raises on invalid input |
| `valid(s)` | `true` if `s` is a full `x.y.z` version |
| `compare(a, b)` | `-1`, `0` or `1` by precedence (build metadata ignored); `lt`, `gt`, `eq` too |
| `sort(list)` / `max(list)` | Ascending order / the highest |
| `inc(v, part)` | The next `"major"`, `"minor"` or `"patch"` version |
| `satisfies(v, range)` | Whether `v` is in the range |
| `maxSatisfying(list, range)` | The highest version in the range, or `nil` |

Methods take version strings or parsed versions.

## Ranges

| Range | Means |
|-------|-------|
| `1.2.3`, `=1.2.3` | exactly 1.2.3 |
| `>1.2.3`, `>=1.2`, `<2`, `<=1.4` | comparisons (partial versions fill with zeros, or bump past `<=1.4` / `>1.4`) |
| `^1.2.3` | `>=1.2.3 <2.0.0` (`^0.2.3` is `<0.3.0`, `^0.0.3` is `<0.0.4`) |
| `~1.2.3`, `~1.2` | `>=1.2.3 <1.3.0` |
| `1.x`, `1.2.*`, `1`, `*` | wildcards |
| `1.0.0 - 2.3` | `>=1.0.0 <2.4.0` |
| `>=1.0 <2.0` | both (space means and) |
| `^1 \|\| ^3` | either |

As in npm, a prerelease version only matches a range that names a prerelease of the same
`major.minor.patch`: `^1.2.3-beta.2` matches `1.2.3-beta.3`, but `^1.0.0` doesn't match
`2.0.0-beta`.
