# I want to Compare...

A "compare" method has three outcomes or "orderings":
```Gleam
case int.compare(guess, secret) { 
  order.Lt -> "Guessed low."   
  order.Eq -> "That's correct!"
  order.Gt -> "Guessed high."
}

case int.compare(speed, speed_limit) {
  order.Lt | order.Eq -> "Okay."
  ordre.Gt -> "Please slow down."
}
```

## The Methods

Use builtin **`compare`** method for types: `int float string bit_array`

```Gleam
int.compare(123, 123)  // Eq
string.compare("foo", "bar")  // Gt (alphabetically)
```

You are encouraged to define `compare` methods for custom types.

*note: can call `order.to_int`, converting `Lt Eq Gt -> -1 0 1`, or compare orders directly with `order.compare`* 

## Items Increasing

Both `list.sort` and `list.max` take comparisons:

```Gleam
list.sort([4, 1, 2], int.compare)  // -> [1, 2, 4]
list.max(["a", "z"], string.compare)  // -> "z"
```

## Items Decreasing

**`order.negate`** toggles an individual order between `Gt` and `Lt`

**`order.reverse`** wraps a comparison func, "toggling" each output

```Gleam
list.max(numbers, order.reverse(int.compare))  // finds the minimum
```

## Break ties in ordering

- `order.break_tie` Takes two orderings; if the first is tied (`order.Eq`) use the second ordering instead.
  - `order.lazy_break_tie` special case, the second ordering is evaluated only when needed. Can chain with use statements:
 
```Gleam
fn get_winner(p1, p2) {
  use <- order.lazy_break_tie(int.compare(p1.score, p2.score))
  use <- order.lazy_break_tie(compare_recency(p1.birthday, p2.birthday))
  order.Lt
}
```
