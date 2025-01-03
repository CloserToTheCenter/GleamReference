# Strings!

## Format 
- use string concat operator **`<>`**, or
  - **`string.append`** two strings together
  - **`string.join`** many strings together
    - variant **`string.concat`** has no delimeter
- **`string.inspect`** to a debuggable format, like what's used by `io.debug`

## As Components
- **`string.to_graphemes`** or **`string.pop_grapheme`** to iterate one "character" at a time.
- **`string.split`** / **`string.join`** {split on / rejoin on} a delimeter
  - **`string.split_once`** special case, split on the first ocurrence of..
  - **`string.concat`** special case with no delimiter

**checking length**
- **`string.length`** number of graphemes
- **`string.byte_size`** number of bytes

**handling empty strings**
- **{"" -> ...}** pattern matching works great
- **`string.is_empty`** checks length equals 0
- **`string.to_option`** either `Some(...)` or `None` on an empty string

## What's at either end?
- **`string.first`** **`string.last`** gets a grapheme, or errors on empty string
- **`string.starts_with`** **`string.ends_with`** checks substring prefix/suffix

## Substring Based
- **`string.contains`** has some
- **`string.crop`** remove up until
- **`string.replace`** all occurences of one with another
- **`string.slice`** extract by index
 
## Modify Ends
**modify ends**
- **`string.drop_start`** **`string.drop_end`** drop *n* graphemes from the {start/end}
- **`string.pad_end`** **`string.pad_start`** add extra to hit a fixed length
- **`string.trim`** **`string.trim_start`** **`string.trim_end`** trim whitespace from {both/start/end}

*the "start" and "end" functons here have deprecated versions: `string.drop_left` `string.drop_right` `string.pad_left` `string.pad_right` `string.trim_left` `string.trim_right`*

**generally**
- **`string.repeat`** repeat x times
- **`string.reverse`** flip it!

## Capitalization
- **`string.capitalise`** Uppercases the first grapheme in the string
- **`string.lowercase`** lowercases the string
- **`string.uppercase`** UPPERCASES THE STRING

## Alphabetical Order
- **`string.compare`** and in use `list.sort(items, string.compare)`
