# Uncertain Results

A `Result` is the outcome of a function call, either `Ok(value)` if it went smoothly or `Error(Nil)` / `Error(Message)` otherwise.

*tanget: It's okay to `panic` or `assert` in a scrappy Gleam script, but when writing a library for many people to use, 
it is strongly encouraged to indicate errors in calling functions with the proper `Result`. If this seems hard to manage,
ask the Gleam community for help.`*

*tangent: Most of the time, you want `Error(Nil)` with no message.*

## Early Return
- **`result.try`** early-exit on an error, otherwise run a callback. Often called with `use`.
  - `result.then` is an alias, the name sounds better inline than "try"
  - `result.try_recover` special case, lets you see any potential error value
  - **`result.flatten`** Condense a stack of nested `Ok(Ok(..))`, done for you by `try/then`
 
```
use val <- result.try(operation_that_might_fail())
perform_validation(val)
```
```
operation_that_might_fail()
|> result.then(perform_validation)
```

## Extract some value

```
         this if okay  ~ or ~> default
result.unwrap(  Ok(5),       or:    0 )   --> 5
result.or( Error(Nil),       or: Ok(0))   --> Ok(0)
```

- **`result.unwrap`** gets the direct interior value (say `5`).
- **`result.or`** picks one of two results to return

Alternate versions (`option.lazy_or`, `option.lazy_unwrap`) wrap the fallback in a callback, evaluating it only when needed.

For getting the `Error` message, instead of defaulting on `Errors`, the following can be used:
  - `result.unwrap_error` gets only "Error" messages, skipping rest
  - `result.unwrap_both` extracts every message, whether on an `Ok` or an `Error`


## Bulk Processing
- **`result.all`** Asks "Are these all okay? Do we have an `Ok` list?"
  - `result.all([Ok(1), Ok(2)])      --> Ok([1, 2])`
  - `result.all([Ok(1), Error(Nil)]) --> None`
- **`result.values`** Keeps each okay value, removing errors.
  - `result.values([Error(Nil), Ok("a")])  --> ["a"]`
- **`result.partition`** Splits to two unwrapped lists: "okay values" and "error messages".

## (rarely used) Direct Transform 
  
- **`result.replace_error`** Updates an error message, ignoring Okays.
  - `result.replace` Updates an okay value, ignoring Errors.
  - `result.nil_error` Deprecated, special case of `|> result.replace_error(Nil)`
 
**`result.map_error`** and **`result.map`** work similar to `replace/replace_error`, except they provide a tranformation function rather than a direct replacement value.

*"rarely used" due to the principle of "sanitize early": often there's a way to `unwrap` into normal values before you would have to call these.* 

## (rarely used) Direct Checks

You *could* check fields with `result.is_error` and `result.is_okay`. 

Instead prefer other builtins, and when there's no good builtin, use pattern matching:

```
case outcome {
  Ok(val) -> todo
  Error(_) -> todo
}
```
