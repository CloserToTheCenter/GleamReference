
# gleam.bool

- `True`
- `False` 

## Prefer

**Custom Types -over- boolean flags**

```Gleam
Account(role: Teacher)    // prefered over "is_teacher: Bool"
```

**Pattern Matching -over- explicit equality**

```Gleam
case eggs {               // preferred over "case eggs == 12 { ... }"
  12 -> "full dozen"
  _ -> "not quite"
}
```

## Bool Functions

|||
|-------------------|---------------------
`bool.and`          | `bool.nand`
 `bool.or`           | `bool.nor`
`bool.exclusive_or` | `bool.exclusive_nor`

These always evaluate both sides.

The built-in operators short-circuit: `&&` for "and", `||` for "or".

**Negation**

Negate with the builtin `!` operator,
or the `bool.negate` function.

## The Guards

*Guards! Guards! They're trying to execute the branch!*

**`bool.guard`** is a form of ternary if, used for early returns.

Based on a condition guards returns 1 of 2 values, either:
- an early return value 
- the result of executing the "rest" of the function

The rest of the function is executed only when proper -
thereby it is guarded from unsafe or uneeded execution.

```Gleam
// in Gleam
use <- bool.guard(when: condition, return: 0)
```

```Java
// same thing in an imperative language
if (condition) { return 0; }
```

The `bool.lazy_guard`, who is lazy in some ways but not others,
guards both paths from early execution, not just the continuation.

## Conversions

Convert to `bool` by comparing objects, say `a == b`. 

Convert out with **`bool.to_string`** and **`bool.to_int`**.

 value | bool.to_string | bool.to_int
-------|----------------|-------------
 True  | "True"         | 1
 False | "False"        | 0

 **`bool.compare`** compares by int values, putting `False` first

