# clay-url

URL parsing, building, and encoding for Clay.

## Usage

```clay
import("clay-stdlib/clay-url")
```

## Parsing

```clay
parts = Url parse("https://example.com:8080/api/users?page=1#top")
parts get("protocol")   // "https"
parts get("host")       // "example.com"
parts get("port")       // "8080"
parts get("path")       // "/api/users"
parts get("query")      // "page=1"
parts get("fragment")   // "top"
```

## Building

```clay
parts = Dict new()
parts set("protocol", "https")
parts set("host", "example.com")
parts set("path", "/search")
parts set("query", "q=clay")

Url build(parts)   // "https://example.com/search?q=clay"
```

## Query Strings

```clay
params = Url parseQuery("name=Clay&version=1&lang=en")
params get("name")      // "Clay"
params get("version")   // "1"
```

## Percent Encoding

```clay
Url encodeComponent("hello world&foo=bar")   // "hello%20world%26foo%3Dbar"
Url decodeComponent("hello%20world")          // "hello world"
```

## Methods

| Method | Description |
|--------|-------------|
| `parse(url)` | Parse URL string into a Dict with protocol, host, port, path, query, fragment |
| `build(parts)` | Build URL string from a parts Dict |
| `parseQuery(qs)` | Parse query string `a=1&b=2` into a Dict |
| `encodeComponent(str)` | Percent-encode a string (RFC 3986) |
| `decodeComponent(str)` | Decode a percent-encoded string |
