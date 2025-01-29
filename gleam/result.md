# gleam/result

- `Ok`
- `Error` if something went wrong.

A result holds a value: like the `5` in `Ok(5)`, or `Nil` in `Error(Nil)`.

A result's type is composed of the values it could possibly hold, like `Result(Int, Nil)` for the example above.

*note: When writing production Gleam, it is proper to use `Result` for indicating errors, rather than crashing with `panic` or `assert`.*

## Update in Place

||for just `Ok` results...|for just `Error` results...|
|-|-|-|
|Upsert the value with some function |**`result.map`**|`result.map_error`|
|Overwrite the value |`result.replace`|**`result.replace_error`***|


- **`result.flatten`** Condense nested `Ok`s: `Ok(Ok(foo))` -> `Ok(foo)`.
- **`result.try`** Map a function that returns a result, then flatten the outcome to remove potential nesting.
  - `result.try_recover` special case, lets you see any error value if present.
  - `result.then` alias for `result.try`, better ergonomics for inline usage:

```Gleam
// result.try lets you "early return" on error
use val <- result.try(func1())
func2(val)

// result.then looks better inline, but is the exact same function
func1() |> result.then(func2)
```
\* *`result.nil_error` is deprecated, a special case of `|> result.replace_error(Nil)`*

## Extract value...

**From an Ok**

```Gleam
//          this if okay  ~ or ~> default
result.unwrap(  Ok(5),       or:    0 )   --> 5
result.or( Error(Nil),       or: Ok(0))   --> Ok(0)
```

- **`result.unwrap`** gets the interior value. *(here an `Int`)*
- **`result.or`** picks one of two results to return. *(here a `Result(Int, Nil)`)*

Alternate versions (`option.lazy_or`, `option.lazy_unwrap`) generate the default value only if needed, by running the provided function.

**From an Error**
  - `result.unwrap_error` gets the interior value for an `Error`, or returns the default for an `Ok`.
  - `result.unwrap_both` extracts either message, whether `Ok` or `Error`. Requires the types match, say `Result(a, a)`.

## Bulk Unwraps

- **`result.all`** Asks "Are these all okay? Do we have an `Ok` list?"
  - `result.all([Ok(1), Ok(2)])      --> Ok([1, 2])`
  - `result.all([Ok(1), Error(Nil)]) --> Error(Nil)`
- **`result.values`** Keeps each okay value, removing errors.
  - `result.values([Error(Nil), Ok("a")])  --> ["a"]`
- **`result.partition`** Splits to two unwrapped lists: "okay values" and "error messages".

## Check Directly

Gleam has two functions for classifying results directly, but they are less frequently used.

Prefer pattern matching:

```Gleam
case outcome {
  Ok(val) -> todo
  Error(_) -> todo
}
```

Prefer builtins, like `result.try` for an early-return without needing to construct something with `bool.guard`.

If you still need them, you can call or pass along the functions **`result.is_ok`** and **`result.is_error`**.




