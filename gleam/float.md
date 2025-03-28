# gleam/float
## Built-ins

Floats come with the language, eg. `1.5 +. 1.5` and `5.0 >. 3.13`.

- For operators, like (`/`, `/.`, `%.`), dividing by 0 yields 0 to keep it simple.
  - Functions, like `float.divide`, have divsion by 0 as an Error.
- Float operators all have trailing dots like "+."

## Parsing
- **`float.parse`** **`float.to_string`** convert back-and-forth say `1.23 <--> "1.23"`, the parsing can error

## Arithmetic

Generally, prefer builtin "dot" operators like `+.` and `>.`

- `float.add`, or **`float.sum`** a list of ints
- `float.multiply`, or **`float.product`** a list of ints
- `float.subtract`
- `float.divide` which gives `Error` on division by zero, unlike the operator
- `float.modulo` which gives `Error` on division by zero, unlike the operator
- **`float.power`** Errors for complex results, otherwise `Ok(float)`
  - **`float.square_root`** special case
- **`float.exponential`** **`float.logarithm`** with respect to Euler's contstant: `e^x` and `ln(x)`

## Comparisons
- **`float.compare`** yields an ordering (`Lt` `Gt` `Eq`), see [gleam/order](https://github.com/CloserToTheCenter/GleamReference/blob/main/gleam/order.md)
  - `float.loosely_compare` `float.loosely_equals` consider floats equal within a provided tolerance
- **`float.max`** and **`float.min`** of two distinct floats

## Constrain
- **`float.clamp`** within a range
- **`float.ceiling`** **`float.floor`** Move to the nearest whole-number float.
   - `float.to_precision` Round to some significant decimal place.
- **`float.truncate`** returns an int with decimals truncated (similar to "floor" on positive numbers and "ceiling" on negative ones)
- **`float.round`** returns an int, with `x.5` rounding up

## Misc
- **`float.absolute_value`** remove sign
- **`float.negate`** flip sign
- **`float.random`** An even distribution from zero up through (but not including) one.



