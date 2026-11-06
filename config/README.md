# stdlib/config

INI-style configuration file parser for Clay.

## Usage

```clay
import("stdlib/config")
```

## Parsing

```clay
cfg = Config parse("[database]
host = localhost
port = 5432

[server]
host = 0.0.0.0
port = 8080")

cfg get("database") get("host")   // "localhost"
cfg get("server") get("port")     // "8080"
```

## Parsing from File

```clay
cfg = Config parseFile("app.ini")
```

## Getting Values with Defaults

```clay
// Returns "localhost" if found, "127.0.0.1" if missing
Config get(cfg, "database", "host", "127.0.0.1")

// Returns default for missing sections or keys
Config get(cfg, "missing", "key", "fallback")   // "fallback"
```

## Merging Configs

```clay
base = Config parseFile("defaults.ini")
overrides = Config parseFile("local.ini")
merged = Config merge(base, overrides)   // overrides win on conflicts
```

## Listing Sections

```clay
Config sections(cfg)   // ["", "database", "server"]
```

Keys defined before any `[section]` go into the `""` (empty string) section.

## Methods

| Method | Description |
|--------|-------------|
| `parse(str)` | Parse INI config string into Dict of Dicts |
| `parseFile(path)` | Read a file and parse it |
| `get(config, section, key, default)` | Lookup a value with fallback default |
| `sections(config)` | List all section names |
| `merge(base, override)` | Merge two configs (override wins) |

Supports `[section]` headers, `key = value` pairs, `#` and `;` comments, and quoted values.
