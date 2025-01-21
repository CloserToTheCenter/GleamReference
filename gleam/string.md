# Strings!

## Format 
- use string concat operator **`<>`**, or
  - **`string.append`** two strings together
  - **`string.join`** many strings together
    - variant **`string.concat`** has no delimeter
- **`string.inspect`** to a debuggable format, like what's used by `io.debug`

## Conversions
- `int.parse` or the other int functions, see [link](https://github.com/CloserToTheCenter/GleamReference/blob/main/gleam/int.md#parse-to-and-from-int)
- `bit_array.from_string` and `bit_array.to_string` for working directly with bits

## Iteration
- **`string.to_graphemes`** or **`string.pop_grapheme`** to iterate one "character" at a time.

**check length**
- **`string.length`** number of graphemes
- **`string.byte_size`** number of bytes

**handling empty strings**
- **{"" -> ...}** pattern matching works great
- **`string.is_empty`** checks length equals 0
- **`string.to_option`** either `Some(...)` or `None` on an empty string

## What's at either end?
- **`string.first`** **`string.last`** gets a grapheme, or errors on empty string
- **`string.starts_with`** **`string.ends_with`** checks substring prefix/suffix

## Split and (re-)Join
- **`string.split`** or **`string.join`** on a delimeter
  - **`string.split_once`** special case, on first occurence, returns at most 2 parts
  - **`string.concat`** special case, no delimeter

## Substring Based
- **`string.contains`** has some substring
- **`string.crop`** remove up until substring
- **`string.replace`** all occurences of one substring with another
- **`string.slice`** extract a substring between indices
 
## Transform
**modify ends**
- **`string.drop_start`** **`string.drop_end`** drop *n* graphemes from the {start/end}
- **`string.pad_start`** **`string.pad_end`** add extra to hit a fixed length
- **`string.trim_start`** **`string.trim_end`** trim whitespace from {start/end}, or **`string.trim`** both

*the "start" and "end" functons here have deprecated versions, listed for searchability: `string.drop_left` `string.drop_right` `string.pad_left` `string.pad_right` `string.trim_left` `string.trim_right`*

**generally**
- **`string.repeat`** repeat x times
- **`string.reverse`** flip it!

**capitalization**
- **`string.capitalise`** Uppercases the first grapheme in the string
- **`string.lowercase`** lowercases the string
- **`string.uppercase`** UPPERCASES THE STRING

## Alphabetical Order
- `string.compare` and in use **`list.sort(items, string.compare)`**
