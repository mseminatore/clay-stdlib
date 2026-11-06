# stdlib/enum

Enum type for Clay — named constants with integer values.

## Usage

```clay
import("stdlib/enum")

Color = Enum from(["red", "green", "blue"])
Color red       // → 0
Color green     // → 1
Color blue      // → 2
```

## Examples

```clay
// Create an enum
Direction = Enum from(["north", "south", "east", "west"])

// Access values by name
Direction north   // → 0
Direction west    // → 3

// Reverse lookup by index
Direction name(0)   // → "north"
Direction name(3)   // → "west"
Direction name(99)  // → nil

// Check membership
Direction contains("north")  // → true
Direction contains("up")     // → false

// Inspect
Direction size      // → 4
Direction values    // → ["north", "south", "east", "west"]
Direction toString  // → "Enum(["north", "south", "east", "west"])"
```

## API

| Method          | Description                                      |
|-----------------|--------------------------------------------------|
| `from(names)`   | Create a new Enum from an array of string names  |
| `name(idx)`     | Get the name for an integer index (nil if out of range) |
| `contains(n)`   | Check if a name exists in the enum               |
| `values`        | Get the array of all enum names                  |
| `size`          | Get the number of entries                        |
| `toString`      | String representation: `Enum(["a", "b", ...])`  |
