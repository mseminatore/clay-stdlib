# stdlib

The Clay standard library — a collection of bricks providing common functionality for Clay programs.

## Installation

```sh
clay bricks add github.com/mseminatore/clay-stdlib stdlib
```

The second argument names the brick `stdlib`, which is both its directory under `bricks/` and its
import path. Import everything at once:

```clay
import("stdlib")
```

or just the bricks you need:

```clay
import("stdlib/json")
import("stdlib/collections")
```

## Bricks

| Brick | Description |
|-------|-------------|
| [args](args/) | CLI argument parsing |
| [base64](base64/) | Base64 encoding and decoding |
| [cache](cache/) | In-memory LRU/TTL key-value cache |
| [cli](cli/) | ANSI terminal colors and styles for CLI tools |
| [collections](collections/) | Data structures: Set, Stack, Queue |
| [config](config/) | INI-style configuration file parser |
| [csv](csv/) | CSV parsing and generation |
| [enum](enum/) | Enum type with named constants |
| [env](env/) | Environment variable management with .env file support |
| [event](event/) | Event emitter (pub/sub) pattern |
| [format](format/) | String formatting utilities |
| [functional](functional/) | Functional programming utilities (map, filter, reduce, pipe) |
| [http-server](http-server/) | Simple HTTP server with routing |
| [iter](iter/) | Lazy iterator pipelines |
| [json](json/) | JSON parsing and serialization |
| [log](log/) | Structured logging with levels |
| [markdown](markdown/) | Markdown to HTML converter |
| [match](match/) | Pattern matching with a chainable API |
| [orm](orm/) | ActiveRecord-style ORM over Clay's Db prototype |
| [path](path/) | Path manipulation utilities |
| [queue](queue/) | SQLite-backed persistent job queue |
| [router](router/) | URL pattern matching with `:param` capture |
| [template](template/) | String template engine using `{{placeholder}}` syntax |
| [test](test/) | Simple, colorful testing framework |
| [url](url/) | URL parsing, building, and percent encoding |
| [uuid](uuid/) | UUID v4 generation |
| [validate](validate/) | Schema validation for Dicts |

## License

MIT — see [LICENSE](LICENSE). Applies to every brick in this repository.
