# I want to Compare...

- an "ordering" is one of `order.Lt, order.Eq, order.Gt`
- "compare functions" turn two objects into an "ordering"

## Two objects

Use appropiate **`compare`** method for types: `int float string bit_array`

```
int.compare(123, 123)  // Eq
string.compare("foo", "bar")  // Gt (alphabetically)
```

You are encouraged to define comparisons for custom types.

*tangent: you can call `order.to_int`, converting `Lt Eq Gt -> -1 0 1`, or you can compare orders directly with `order.compare`.* 

## Items Increasing

Both `list.sort` and `list.max` take comparisons.

```
list.sort([4, 1, 2], int.compare)  // -> [1, 2, 4]
list.max(["a", "z"], string.compare)  // -> "z"
```

## Items Decreasing

**`order.negate`** toggles an order between `Gt` and `Lt`

**`order.reverse`** wraps a comparison func, "toggling" each output

```
list.max(numbers, order.reverse(int.compare))  // finds the minimum
```

## Break ties in ordering

Takes two orderings, defaults to the second if the first is `order.Eq`.

```
break_tie(int.compare(x, y), with: order.Lt)
lazy_break_tie(string.compare(a, b), with: fn() { order.Lt })
```
