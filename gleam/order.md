# I want to Compare...

A "compare" method has three possible outcomes:
```
case int.compare(guess, secret) { 
  order.Lt -> "You guessed too low."   
  order.Eq -> "That's correct!"
  order.Gt -> "You guessed too high."
}
```

## The Methods

Use builtin **`compare`** method for types: `int float string bit_array`

```
int.compare(123, 123)  // Eq
string.compare("foo", "bar")  // Gt (alphabetically)
```

You are encouraged to define comparisons for custom types.

*tangent: can call `order.to_int`, converting `Lt Eq Gt -> -1 0 1`, or compare orders directly with `order.compare`* 

## Items Increasing

Both `list.sort` and `list.max` take comparisons:

```
list.sort([4, 1, 2], int.compare)  // -> [1, 2, 4]
list.max(["a", "z"], string.compare)  // -> "z"
```

## Items Decreasing

**`order.negate`** toggles an individual order between `Gt` and `Lt`

**`order.reverse`** wraps a comparison func, "toggling" each output

```
list.max(numbers, order.reverse(int.compare))  // finds the minimum
```

## Break ties in ordering

- `order.break_tie(ordering, with: second_ordering)` Defaults to the second ordering if the first is `order.Eq`.
  - `order.lazy_break_tie` special case with the second ordering wrapped in a callback

*tangent: this, and other "lazy" functions with callbacks, make it easy to chain with `use` statements:* 

```
fn get_winner(p1, p2) {
  use <- order.lazy_break_tie(int.compare(p1.score, p2.score))
  use <- order.lazy_break_tie(compare_recency(p1.birthday, p2.birthday))
  order.Lt
}
```
