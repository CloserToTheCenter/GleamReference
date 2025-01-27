# gleam/set

## Create

- empty set with `set.new`
- specific set with **`set.from_list`**, eg `set.from_list([1, 2, 3])`
  - *convert back with `set.to_list`*

Like with Gleam dicts, these support two patterns of initialization:

```Gleam
// build the list first
list.map(cars, fn(car) { car.plate_id }) |> set.from_list

// fold into an empty set
list.fold(cars, set.new(), fn(acc, car) { set.insert(acc, car.plate_id) })
```

## Query

- **`set.contains`** an item
- **`set.size`** how many items?
  - `set.is_empty` special case, check if no items
- **`set.is_disjoint`** do these two sets have nothing in common?
- **`set.is_subset`** is this set is entirely contained by...?

## Modify


|from a set -> |to Add...|to Remove...|to keep only items in...|
|-|-|-|-|
|one item:| **`set.insert`** | **`set.delete`** |-|
|another set:| **`set.union`** | **`set.difference`** |**`set.intersection`**|
|another list:|-| **`set.drop`** | **`set.take`** |
  
- **`set.filter`** remove items on some criteria
- **`set.symmetric_difference`** in one of two sets, but not both
