# stdlib/base64

Base64 encoding and decoding for Clay.

## Usage

```clay
import("stdlib/base64")
```

## Encoding

```clay
Base64 encode("Hello, World!")   // "SGVsbG8sIFdvcmxkIQ=="
Base64 encode("Clay")            // "Q2xheQ=="
```

## Decoding

```clay
Base64 decode("SGVsbG8sIFdvcmxkIQ==")   // "Hello, World!"
Base64 decode("Q2xheQ==")                // "Clay"
```

## Roundtrip

```clay
original = "Any string at all"
Base64 decode(Base64 encode(original)) == original   // true
```

## Methods

| Method | Description |
|--------|-------------|
| `encode(str)` | Encode a string to Base64 |
| `decode(str)` | Decode a Base64 string |

Uses the standard Base64 alphabet (A-Z, a-z, 0-9, +, /) with `=` padding.
