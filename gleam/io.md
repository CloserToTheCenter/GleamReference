## I want to... Print Things!

- **`io.print` `io.println`** a string to *console*.
- **`io.print_error` `io.println_error`** a string to *standard error*.
- **`io.debug`** any object, `io.println`ing its representation

```
io.println("1 2 3")         // -> 1 2 3
io.debug(list.range(1, 3))  // -> [1, 2, 3]
```

## ... Print Text that I've formatted

Use **`<>`** to concatenate strings. There is no string interpolation.
```
let name = "Lucy"
io.println("Hello my name is " <> name <> "!")
```

Use **`string.inspect`** to format arbitrary objects.
```
// these two are equivalent
io.debug(foo)   <------>    io.println(string.inspect(foo))

// and with concatenation
io.println("items: " <> string.inspect(items))
```

## ... Print Values partway through a pipeline

As they return their original input, io functions are easy to drop into chained pipelines.

```
[1, 2]
|> list.map(fn(x) { x + 1 })
|> io.debug               // prints "[2, 3]"
|> list.map(fn(x) { x * 2 })
|> io.debug               // prints "[4, 6]"
```
