# clay-env

Environment variable management with `.env` file support for Clay.

## Usage

```clay
import("clay-stdlib/clay-env")
```

## Loading .env Files

```clay
// .env file format:
// APP_NAME=MyCoolApp
// PORT=3000
// SECRET="my-secret-value"
// # comments are ignored

vars = Env load(".env")
vars get("APP_NAME")   // "MyCoolApp"
```

## Reading Variables

```clay
// Get with a default fallback
Env get("PORT", "3000")

// Require a variable (exits if missing)
Env require("API_KEY")

// Check if a variable exists
Env has("DEBUG")   // true or false
```

## All Variables

```clay
Env load(".env")
allVars = Env all()   // Dict of all loaded variables
```

## Methods

| Method | Description |
|--------|-------------|
| `load(path)` | Load a `.env` file, returns Dict of parsed variables |
| `get(name, default)` | Get a variable with fallback (checks loaded vars, then system env) |
| `require(name)` | Get a variable, exit with error if not set |
| `has(name)` | Check if a variable is set |
| `all()` | Return Dict of all loaded variables |

Supports `KEY=VALUE`, double-quoted values (`KEY="value"`), single-quoted values (`KEY='value'`), and `#` comments.
