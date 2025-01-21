## Make an...

- empty set with `set.new`
- specific set with **`set.from_list`**, eg `set.from_list([1, 2, 3])`
  - *convert back with `set.to_list`*

These support two patterns of initialization:

```Gleam
// build the list first
let plates = cars |> list.map(fn (car) { car.plate_number }) |> set.from_list

// repeatedly add to an empty set
let plates = list.fold(cars, from: set.new(), with: fn (seen, car) { set.insert(seen, car.plate_number) })
```

## Query

- **`set.contains`** (an item)
- `set.size` (how many items?)
  - `set.is_empty` (no items?)
- `set.is_disjoint` (these two sets have nothing in common)
- `set.is_subset` (this set is entirely contained by that set)

## Construct new Sets:

**By Adding/Removing elements**
- one item: **`set.insert`** / **`set.delete`**
- another set: `set.union` / `set.difference`
- another list: `set.drop` / `set.take`
  
And `set.filter` lets you remove items some criteria. 

**Combining two Sets**

- **`set.union`**: in either
- **`set.intersection`**: in both
- `set.difference` : in the first, but not the second
- `set.symmetric_difference` : in exactly one but not both
