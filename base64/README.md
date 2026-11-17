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

## Binary data

Clay strings are bytes, so any data round-trips, including bytes above 127:

```clay
Base64 encode(String fromBytes([0, 200, 255]))   // "AMj/"
Base64 decode("AMj/") bytes                      // [0, 200, 255]
```

## Bad input

`decode` skips whitespace (so line-wrapped Base64 works) and accepts missing `=`
padding. It raises on a character outside the alphabet, misplaced or wrong
padding, and a truncated group:

```clay
r = try { Base64 decode("SGV$sbG8=") } catch { |e| e message }
r   // "Base64 decode: invalid character $ at offset 3"
```

## Roundtrip

```clay
original = "Any string at all"
Base64 decode(Base64 encode(original)) == original   // true
```

## Methods

| Method | Description |
|--------|-------------|
| `encode(str)` | Encode a string (any bytes) to Base64 |
| `decode(str)` | Decode a Base64 string; raises on invalid input |

Uses the standard Base64 alphabet (A-Z, a-z, 0-9, +, /) with `=` padding. Both directions take linear time.
