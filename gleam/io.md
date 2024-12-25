# I want to Print... 

## Arbitrary Objects

Use **`io.debug`** to print an object's representation. This uses the same formatting found in Gleam's error messages.

```
io.debug(list.range(1, 3))   // prints -> [1, 2, 3]
```

*tangent: `string.inspect` does the formatting, so `io.debug(x)` is equivalent to `io.println(string.inspect(x))`*

## Strings

- **`io.print` `io.println`** to console.
- **`io.print_error` `io.println_error`** to standard error.

## Format Text

Use **`<>`** to concatenate strings. There is no string interpolation.
```
let name = "Lucy"
io.println("Hello my name is " <> name <> "!")
```



## Values Partway through a Pipeline

As they return their input unchanged, `io` functions can be added anywhere in an existing pipeline.

```
[1, 2]
|> list.map(fn(x) { x + 1 })
|> io.debug               // prints "[2, 3]"
|> list.map(fn(x) { x * 2 })
|> io.debug               // prints "[4, 6]"
```
