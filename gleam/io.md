# I want to print...

## Arbitrary Objects

Use the keyword **`echo`** to assist during debugging. It uses the same formatting as Gleam's error messages.

```Gleam
echo list.range(1, 3)   // prints -> [1, 2, 3]
```

- **`string.inspect`** does the formatting, so `echo x` is equivalent to `echo string.inspect(x)`
- `io.debug` does the same formatting as `echo`, just without the line number

## Strings

- **`io.print` `io.println`** to console.
- **`io.print_error` `io.println_error`** to standard error.

## Formatted Text

Use **`<>`** to concatenate strings. There is no string interpolation.
```Gleam
let name = "Lucy"
io.println("Hello my name is " <> name <> "!")
```

## Values Partway through a Pipeline

As they return their input unchanged, `io` functions can be added anywhere in an existing pipeline.

```Gleam
[1, 2]
|> list.map(fn(x) { x + 1 })
|> io.println               // prints "[2, 3]"
|> list.map(fn(x) { x * 2 })
|> echo                    // prints "[4, 6]"
```
