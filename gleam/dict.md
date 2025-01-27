# gleam/dict

## Create

- `dict.new` a new empty dictionary
- **`dict.from_list`** with specific pairs, eg `dicts.from_list([#("a", 1), #("b", 2)])`
  - *convert back with `dict.to_list`*

Like Gleam sets, these support two patterns of initialization:

```Gleam
// build the list first
list.map(cars, fn(car) { #(car.plate_id, car.year) }) |> dict.from_list

// repeatedly add to an empty dict
list.fold(cars, dict.new(), fn(acc, car) {
  dict.insert(acc, car.plate_id, car.year)
})
```

## Check Contents
- **`dict.get`** giving `Ok(val)` or `Error(Nil)`
- **`dict.has_key`** giving `True` or `False`
- **`dict.size`** how many items?
  - `dict.is_empty` special case, check if no items
- **`dict.keys`** **`dict.values`** for getting those as lists

## Modify at some specific key
- **`dict.insert`** overwrites with a new value
- **`dict.upsert`** applies a function to a value, overwriting it with the updated result
- **`dict.delete`** removes kv pair

## Remove Multiple
- **`dict.drop`** delete a list of keys
- **`dict.take`** retain only listed keys
- **`dict.filter`** remove on some condition of both key and value

## Combine Dictionaries
- **`dict.merge`** add items from one dict to another, "end-to-end"
- **`dict.combine`** combine values with some function, "key-to-matching-key"

## Iterate Through
- **`dict.map_values`** update each value in a dict, based on current key and value
  - `dict.each` special case, discarding the return value
- **`dict.fold`** accumulates each pair into a final result

## Use a List-of-Tuples as a Dict

These perform dictionary related functions, operating directly on lists of #(key, val) tuples:

- `list.key_filter` all vals where key function matches
- `list.key_find` first val where key matches
- `list.key_pop` same as above, also returns transformed list
- `list.key_set` insert a key and value
