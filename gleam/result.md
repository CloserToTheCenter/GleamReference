# Uncertain Results

A `Result` is the outcome of a function call, either `Ok(value)` if it went smoothly or `Error(Nil)` / `Error(Message)` otherwise.

*tangent: It's okay to `panic` or `assert` in a scrappy Gleam script, but when writing a library for many people to use, 
it is strongly encouraged to indicate errors in calling functions with the proper `Result`. If this seems hard to manage,
ask the Gleam community for help.*

*tangent: Most of the time, you want `Error(Nil)` with no message.*

## Exit on Error

**`result.try`** / **`result.then`** Short-circuit on error, otherwise run a continuation. Both names refer to the same function:

```Gleam
// "result.try" intended for use statement
use val <- result.try(operation_that_might_fail())
next_step(val)

// "result.then" intended for inline use 
operation_that_might_fail()
|> result.then(next_step)
```

- *Special Case: `result.try_recover` lets you see a potential error value*

These functions internally call **`result.flatten`**, condensing a stack of nested `Ok(Ok(foo))` to just `Ok(foo)`. Otherwise the result layers would pile up when chaining them together. 
 

## Default on Error

```Gleam
//          this if okay  ~ or ~> default
result.unwrap(  Ok(5),       or:    0 )   --> 5
result.or( Error(Nil),       or: Ok(0))   --> Ok(0)
```

- **`result.unwrap`** gets the direct interior value (say `5`).
- **`result.or`** picks one of two results to return

If you start to chain these, consider getting the first "okay" item of several with: `|> list.find(result.is_okay)`

Alternate versions (`option.lazy_or`, `option.lazy_unwrap`) wrap the fallback in a callback, evaluating it only when needed.

For getting the `Error` message, instead of defaulting on `Errors`, the following can be used:
  - `result.unwrap_error` gets only the "Error" message
  - `result.unwrap_both` extracts either message, whether on an `Ok` or an `Error`

## Bulk Unwraps

- **`result.all`** Asks "Are these all okay? Do we have an `Ok` list?"
  - `result.all([Ok(1), Ok(2)])      --> Ok([1, 2])`
  - `result.all([Ok(1), Error(Nil)]) --> Error(Nil)`
- **`result.values`** Keeps each okay value, removing errors.
  - `result.values([Error(Nil), Ok("a")])  --> ["a"]`
- **`result.partition`** Splits to two unwrapped lists: "okay values" and "error messages".

## Edit in Place

*Often these can be avoided by "sanitizing early": unwrapping to either values or error messages before continuing. * 

- **`result.replace_error`** Updates an error message, ignoring Okays.
  - `result.replace` Updates an okay value, ignoring Errors.
  - `result.nil_error` Deprecated, special case of `|> result.replace_error(Nil)`
 
**`result.map_error`** and **`result.map`** work similar to `result.replace_error`, except transform via a function, rather than replacing directly with a value.


## Check Directly

Gleam has two functions for classifying results directly, but they are less frequently used.

Prefer pattern matching for routing results:

```Gleam
case outcome {
  Ok(val) -> todo
  Error(_) -> todo
}
```

Prefer using other builtins, like `result.values` rather than calling `list.filter(result.is_ok) |> list.map(...)`, or `result.try` over something with `bool.guard`.

If you still need them, you can call or pass along the functions **`result.is_ok`** and **`result.is_error`**.




