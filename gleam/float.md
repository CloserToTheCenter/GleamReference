## Built-ins

Floats come with the language, eg. `3.0 +. 3.0` and `5.0 >. 3 -. 2`. See also [number formats].

- For operators, like (`/`, `/.`, `%.`), dividing by 0 yields 0 to keep it simple.
  - Functions, like `int.divide`, have divsion by 0 as an error.
- Float operators all have trailing dots like "+."

## Parsing
- **`float.parse`** **`float.to_string`** Convert to-and-from `String`.

## Arithmetic

Generally, prefer the builtin operators.

- `float.add`, or **`float.sum`** a list of ints
- `float.multiply`, or **`float.product`** a list of ints
- `float.subtract`
- `float.divide` which gives `Error` on division by zero, unlike the operator
- `float.modulo` which gives `Error` on division by zero, unlike the operator
- **`float.power`** `Error`s for complex results, otherwise `Ok(float)`
  - **`float.square_root`** special case
- **`float.exponential`** **`float.logarithm`** with respect to Euler's contstant: `e^x` and `ln(x)`

## Comparisons
- **`float.compare`** yields an ordering (`Lt` `Gt` `Eq`), see [link ordering])
  - **`float.loosely_compare`** **`float.loosely_equals`** consider floats equal within a provided tolerance

## Constrain
- **`float.clamp`** within a range
- **`float.max`** and **`float.min`** of two distinct floats
- **`float.to_precision`** Round float to some significant decimal place.

**Rounding Options**
- **`float.ceiling`** **`float.floor`** Move to the nearest float.
   - **`float.truncate`** removes all decimals (similar to "floor" on positive numbers and "ceiling" on negative ones)
- **`float.round`** Returns an int, `x.5` rounds up.

## Misc
- **`float.absolute_value`** remove sign
- **`float.negate`** flip fign

- **`float.random`** an even distribution from zero up through (but not including) one



