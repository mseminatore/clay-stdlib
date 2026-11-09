# stdlib/uuid

UUID v4 generation for Clay.

## Usage

```clay
uuid = Uuid v4
// => "550e8400-e29b-41d4-a716-446655440000" (example)
```

## API

### `Uuid v4`

Generates a random UUID v4 string following RFC 4122. The returned string is
formatted as `xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx` where `y` is one of
`8`, `9`, `a`, or `b`.
