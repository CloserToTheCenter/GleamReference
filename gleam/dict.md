## Make a dictionary

- **`dict.new`** empty dictionary
- **`dict.from_list`** with specific pairs, eg `dicts.from_list([#("a", 1), #("b", 2)])`
  - *convert back with **`dict.to_list`***
 
## Check Elements
- **`dict.get`** giving `Ok(val)` or `Error(Nil)`
- **`dict.has_key`** giving `True` or `False`
- **`dict.size`** how many items?
  - `dict.is_empty` (no items?)
- **`dict.keys`** **`dict.values`** for getting those as lists

## Modify at some specific key
- **`dict.insert`** overwrites with a new value
- **`dict.upsert`** applies a function to a value, overwriting it with the result
- **`dict.delete`** removes kv pair

## Remove Some Items
- **`dict.drop`** delete a list of keys
- **`dict.take`** retain only listed keys
- **`dict.filter`** remove on some condition of both key and value

## Combine Dictionaries
- **`dict.merge`** add items to one dict from another
- **`dict.combine`** zip together dicts by key, combining values with some function

## Iterate On
- **`dict.map_values`** update each value in a dict, based on current key and value
  - **`dict.each`** special case, discarding the return value
- **`dict.fold`** accumulates each pair into a final result

## Note: Using a list of tuples as a Dict

The following are in the `list` module, but perform dictionary related functions. They operate directly on a list of #(key, val) tuples.

- `list.key_filter` (all vals where key function matches)
- `list.key_find` (first val where key matches)
- `list.key_pop` (same as above, also returns transformed list)
- `list.key_set` (insert a key and value)
