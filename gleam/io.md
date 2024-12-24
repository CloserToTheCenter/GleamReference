# I want to...

## Output text 

- **`io.print` `io.println`** a string to console.
- **`io.print_error` `io.println_error`** a string to standard error.
- **`io.debug`** takes any object, printing its representation (like `#(0, 1)` for a tuple)

*note: the `ln` suffix denotes "print this on a new line"; `io.debug` always prints to a newline.*

## Format text for printing

Use **`<>`** to concatenate strings.
```
let name = "Lucy"
io.println("Hello my name is " <> name <> "!")
```

Use **`string.inspect`** to format arbitrary objects. These two are equivalent:
```
// these two are equivalent
io.debug(foo)   <------>    io.println(string.inspect(foo))

// and with concatenation
io.println("items: " <> string.inspect(items))
```

## View values partway through a pipeline

As they return their original input, io functions are easy to drop into chained pipelines.

```
[1, 2]
|> list.map(fn(x) { x + 1 })
|> io.debug               // prints "[2, 3]"
|> list.map(fn(x) { x * 2 })
|> io.debug               // prints "[4, 6]"
```
