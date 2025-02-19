# gleam/bit_array

Use double brackets to indicate literals. Use `inspect` to debug.

```
bit_array.inspect(<<0, 20, 0x20, 255>>)
// -> "<<0, 20, 32, 255>>"

bit_array.inspect(<<100, 5:3>>)
// -> "<<100, 5:size(3)>>"   (not supported on js backend)
```

## Working with utf-8
```
    /-----> bit_array.from_string ----\
UTF-8 String                       BitArray
    \------ bit_array.to_string <-----/
```
Parsing to a string fails if the bits are not valid utf-8.

Can check first with `bit_array.is_utf8`

## Other encodings

|to string|from string|
|-|-|
|`base16_decode`|base16_encode`|
|`base64_decode`|base64_encode`|
|`base64_url_decode`|base64_url_encode`|

## Helpers

**combine**
- `bit_array.append` stick two together
- `bit_array.concat` stick many together

**sizing**
- `bit_array.bit_size` how many bits
- `bit_array.byte_size` how many bytes, rounding up
  - `bit_array.pad_to_bytes` fill to an even byte number

**query**
- `bit_array.slice` constant-time extraction of a portion
- `bit_array.starts_with` has these bits as a prefix
- `bit_array.compare` how are these two ordered?
