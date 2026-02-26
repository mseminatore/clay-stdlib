# clay-validate

Schema validation for Dicts — validate form data, API inputs, and configuration.

## Usage

```clay
import("clay-stdlib/clay-validate")
```

## Defining a Schema

```clay
schema = Schema new()
schema required("title", "string")
schema required("email", "string")
schema optional("age", "number", 0)
schema optional("role", "string", "user")
```

## Validating Data

```clay
data = Dict clone
data set("title", "Hello")
data set("email", "test@example.com")

errors = schema validate(data)
(errors size() == 0) ifTrue {
    "Valid!" println
} ifFalse {
    errors each { |e| e println }
}
```

Missing optional fields are filled with their default values after validation.

## Constraints

```clay
// Length constraints (strings and arrays)
schema minLength("title", 1)
schema maxLength("title", 100)

// Numeric range
schema min("age", 0)
schema max("age", 150)

// Regex pattern
schema pattern("email", "^[^@]+@[^@]+$")

// Allowed values
schema oneOf("role", ["admin", "user", "guest"])

// Custom rule (block receives value, returns true/false)
schema rule("title", { |v| v length() > 0 })
```

## Methods

| Method | Description |
|--------|-------------|
| `new()` | Create a new schema |
| `required(name, type)` | Add a required field with type check |
| `optional(name, type, default)` | Add an optional field with default |
| `minLength(name, n)` | Minimum length for strings/arrays |
| `maxLength(name, n)` | Maximum length for strings/arrays |
| `min(name, n)` | Minimum value for numbers |
| `max(name, n)` | Maximum value for numbers |
| `pattern(name, regex)` | Regex pattern for strings |
| `oneOf(name, values)` | Restrict to a set of allowed values |
| `rule(name, fn)` | Custom validation block |
| `validate(data)` | Validate a Dict, returns array of error strings |

Supported types: `"string"`, `"number"`, `"array"`, `"bool"`.

The API is chainable — all constraint methods return `self`.
