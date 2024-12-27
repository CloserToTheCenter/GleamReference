## Make a dictionary

- **`dict.new`**
- **`dict.from_list`** (with specific pairs, eg `dicts.from_list([#("a", 1), #("b", 2)])`
  - *convert back with `dict.to_list`*
 
## Check Elements
- **`dict.get`** giving `Ok(val)` or `Error(Nil)`
- **`dict.has_key`** giving `True` or `False`
- **`dict.size`** how many items?
  - `dict.is_empty` (no items?)
- **`dict.keys`** **`dict.values`** for getting those lists

## Modify at some specific key
- **`dict.insert`** overwrites with a new value
- **`dict.upsert`** performs an update on the value
- **`dict.delete`** removes kv pair

## Modify in Bulk
- **`dict.drop`** delete a list of keys
- **`dict.take`** retain only listed keys
- **`dict.filter`** remove on some condition of both key and value
- **`dict.merge`** add items to one dict from another

## Update and Transform

- **`dict.combine`** zip together dicts by key, combining values with some function
- **`dict.map_values`** update each value in a dict, based on current key and value
  - **`dict.each`** special case, discarding the return value
- **`dict.fold`** accumulates each pair into a final result
