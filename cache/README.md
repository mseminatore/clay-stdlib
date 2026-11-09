# stdlib/cache

In-memory LRU/TTL key-value cache for Clay.

## Usage

```clay
cache = Cache new maxSize(100) ttl(60)
```

## Methods

### `Cache new()`

Create a new cache instance.

```clay
c = Cache new
```

### `maxSize(n)`

Set the maximum number of entries. When the limit is reached, the least recently used entry is evicted. Pass `0` for unlimited (default). Returns self for chaining.

```clay
c = Cache new maxSize(50)
```

### `ttl(seconds)`

Set the time-to-live in seconds for all entries. Expired entries are removed on the next `get` or `has` call. Pass `0` to disable expiry (default). Returns self for chaining.

```clay
c = Cache new ttl(300)
```

### `set(k, v)`

Store a value under the given key. If the cache is full, the least recently used entry is evicted first. Returns self for chaining.

```clay
c set("name", "Alice")
c set("age", 30)
```

### `get(k)`

Retrieve the value for a key. Returns `nil` if the key does not exist or has expired. Accessing a key marks it as most recently used.

```clay
c get("name")   // => "Alice"
c get("missing") // => nil
```

### `has(k)`

Check whether a key exists and has not expired. Returns `true` or `false`.

```clay
c has("name")    // => true
c has("missing") // => false
```

### `delete(k)`

Remove an entry by key. Returns self for chaining.

```clay
c delete("name")
```

### `clear()`

Remove all entries from the cache. Returns self for chaining.

```clay
c clear
```

### `size()`

Return the number of entries currently in the cache.

```clay
c size // => 0
```

### `keys()`

Return an array of all keys in LRU order (least recently used first).

```clay
c set("a", 1)
c set("b", 2)
c get("a")
c keys // => ["b", "a"]
```

## Example

```clay
cache = Cache new maxSize(3) ttl(60)

cache set("x", 10)
cache set("y", 20)
cache set("z", 30)

cache get("x")      // => 10, "x" is now most recently used

cache set("w", 40)  // evicts "y" (least recently used)

cache has("y")      // => false
cache size          // => 3
cache keys          // => ["z", "x", "w"]
```
