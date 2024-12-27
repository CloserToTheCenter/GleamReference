## Make a set

- `set.new`
- `set.from_list` (with specific items, eg `set.from_list([1, 2, 3])`)
  - *convert back with `set.to_list`*

## Query

- `set.contains` (an item)
- `set.size` (how many items?)
  - `set.is_empty` (no items?)
- `set.is_disjoint` (these two have nothing in common)
- `set.is_subset` (this is entirely contained by that)

## Modify

- `set.insert` / `set.delete` ({add/remove} a single value)
- `set.union` / `set.difference` ({add/remove} a set of values)
  - `set.drop` (special case, removes a *list* of values instead)

*note: Gleam is immutable; these all leave the original untouched returning a brand new modified set*

- `set.intersection` (the overlap)
   - `set.take` (special case, second argument is a list)
- `set.symmetric_difference` (union minus overlap, similar to `xor`)
- `set.filter` (remove on some condition)


