# Optional Fields...

## Default to something

```
          initial value  ~ or ~> default
option.unwrap(   Some(5),        or: 0)   --> 5
option.unwrap(   None,           or: 0)   --> 0
```

- **`option.unwrap`** gets the direct interior value (say `5`).
- **`option.or`** picks one of two options to return

Alternate versions (`option.lazy_or`, `option.lazy_unwrap`) wrap the fallback in a callback, evaluating it only when needed.

## Direct Transform

- **`option.map`** Applies a function "undercover", turning `Some(x) -> Some(y)`
- **`option.flatten`** Condense a stack of nested `Some(Some(..))`
- **`option.then`** Maps then flattens, for applying option-returning functions: `Some(x) -> Some(Some(y)) -> Some(y)`

These three act on `Some(x)` but return `None` without modification. 

## Early return on Null

The **`option.map`** is the early-exit equivalent of `bool.guard`.

```
use val <- option.map(optional_val)          // in gleam
if (optional_val == None) { return None; }   // in procedural language
```

## Query Lists of options

- **`option.all`** Asks "Is this list of options **all** present? Do we have *some* list?"
  - `list.all([Some(1), Some(2)])  --> Some([1, 2])`
  - `list.all([Some(1), None])     --> None`
  
- **`option.values`** Keeps each present value, removing null entries.
  - `list.values([None, Some("a")])  --> ["a"]`

## (rarely used) Result Conversions

Convert from `Option` to `Result` and back again with:
- **`option.from_result`**
- **`option.to_result`**

If you use these repeatedly, consider the seperation between options and results:

|||||
|-|-|-|-|
| **`Option`** | `Some(x)` or `None` | Some field happens to be empty. | Less common. |
| **`Result`** | `Ok(x)` or `Error(Nil)` | Indicates an invalid set of parameters. | More common. |

Example: query a chess board, eg `|> board.at(square: "z3")`:

- Square is invalid -> `Error(Nil)`
- Square is present and empty -> `Ok(None)`
- Square is present and contains a piece -> `Ok(Some(Piece)))`

## (rarely used) Direct Checks

You *could* check fields with `option.is_none` and `option.is_some`. 

Instead prefer other builtins, and when there's no good builtin, use pattern matching:

```
case item {
  Some(val) -> todo
  None -> todo
}
```
    
