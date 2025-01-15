## Built Ins

Integers come baked into the language, eg. `3 + 3` and `5 > 3 - 2`. See also [number formats].

- For operators, like (`/`, `/.`, `%`), dividing by 0 yields 0 to keep it simple.
  - Functions, like `int.divide`, have divsion by 0 as an error.
- Floats use a whole second set of operators, like "+."

## Parse to-and-from Int

- **`int.parse`** **`int.to_string`** Convert to-and-from `String`.
- **`int.to_float`** converts to float, convert back with `float.round` or `float.truncate`.

Gleam supports numeric bases from 2-36:
- **`int.base_parse`** parses Str -> Int
- **`int.to_base_string`** parses Int -> Str
  - special cases: `int.to_base2` `int.to_base8` `int.to_base16` `int.to_base36`

## Arithmetic

Builtin Operators:
```
a + b 
a * b
a - b
a / b   // division rounds toward 0 by default
a % b   // division and modulo operators are okay with division by 0, returning 0
```

Some corresponding functions:

- `int.add`, or **`int.sum`** a list of ints
- `int.multiply`, or **`int.product`** a list of ints
- `int.subtract`
- `int.divide` and `int.floor_divide` which indicate division by zero with an `Error`
  -  `int.floor_divide` rounds towards negative infinity instead of zero
- `int.modulo` or its alias `int.remainder`, which again indicate division by zero with a potential `Error`
  - **`int.is_even`** and **`int.is_odd`** as shorthand 
- **`int.power`** raise an int to a float, `Error`s for complex results, otherwise `Ok(float)`
  - **`int.square_root`** special case

These functions can be curied and piped around easier,
```
list.map(items, int.add(_, 1))
```

## Comparisons

Builtin Operators:
```
a > b       a >= b
a < b       a <= b
a == b      a != b
```

These operators are covered by:
- **`int.compare`** yields an ordering (`Lt` `Gt` `Eq`), see [link ordering])

Some functions you would use comparisons to build:
- **`int.clamp`** within a range
- **`int.max`** and **`int.min`** of two distinct ints

And related to signs:
- **`int.absolute_value`** remove sign
- **`int.negate`** flip fign

## Misc

- **`int.random`** up through the limit: `random(6)` can give `[0, 1, 2, 3, 4, or 5]`
- **`int.digits`** **`int.undigits`** split into base 10 digits and back again: `"34" <--> ["3", "4"]`

## Bitwise Operations

See also [link bit_array] for finer control.

- **`bitwise_and`**
- **`bitwise_or`**
- **`bitwise_not`**
- **`bitwise_exclusive_or`**
- **`bitwise_shift_left`**
- **`bitwise_shift_right`**
