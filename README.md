# clay-stdlib

The Clay standard library — a collection of bricks providing common functionality for Clay programs.

## Installation

```sh
clay bricks add github.com/user/clay-stdlib#clay-collections
```

Import individual bricks by name:

```clay
import("clay-stdlib/clay-json")
import("clay-stdlib/clay-collections")
```

## Bricks

| Brick | Description |
|-------|-------------|
| [clay-args](clay-args/) | CLI argument parsing |
| [clay-cache](clay-cache/) | In-memory LRU/TTL key-value cache |
| [clay-cli](clay-cli/) | ANSI terminal colors and styles for CLI tools |
| [clay-collections](clay-collections/) | Data structures: Set, Stack, Queue, and Range |
| [clay-csv](clay-csv/) | CSV parsing and generation |
| [clay-event](clay-event/) | Event emitter (pub/sub) pattern |
| [clay-format](clay-format/) | String formatting utilities |
| [clay-functional](clay-functional/) | Functional programming utilities (map, filter, reduce, pipe) |
| [clay-http-server](clay-http-server/) | Simple HTTP server with routing |
| [clay-iter](clay-iter/) | Lazy iterator pipelines |
| [clay-json](clay-json/) | JSON parsing and serialization |
| [clay-markdown](clay-markdown/) | Markdown to HTML converter |
| [clay-match](clay-match/) | Pattern matching with a chainable API |
| [clay-orm](clay-orm/) | ActiveRecord-style ORM over Clay's Db prototype |
| [clay-path](clay-path/) | Path manipulation utilities |
| [clay-queue](clay-queue/) | SQLite-backed persistent job queue |
| [clay-router](clay-router/) | URL pattern matching with `:param` capture |
| [clay-template](clay-template/) | String template engine using `{{placeholder}}` syntax |
| [clay-test](clay-test/) | Simple, colorful testing framework |
| [clay-uuid](clay-uuid/) | UUID v4 generation |
| [clay-validate](clay-validate/) | Schema validation for Dicts |
