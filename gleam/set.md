# I want to...

## Create

- empty set with `set.new`
- specific set with **`set.from_list`**, eg `set.from_list([1, 2, 3])`
  - *convert back with `set.to_list`*

Like with Gleam dicts, these support two patterns of initialization:

```Gleam
// build the list first
list.map(cars, fn(car) { car.plate_id }) |> set.from_list

// fold into an empty dict
list.fold(cars, set.new(), fn(acc, car) { set.insert(acc, car.plate_id) })
```

## Query

- **`set.contains`** an item
- **`set.size`** how many items?
  - `set.is_empty` special case, check if no items
- **`set.is_disjoint`** do these two sets have nothing in common?
- **`set.is_subset`** is this set is entirely contained by...?

## Update Elements

||to Add|to Remove|
|-|-|-|
|one item:| **`set.insert`** | **`set.delete`** |
|another set:| **`set.union`** | **`set.difference`** |
|another list:| **`set.drop`** | **`set.take`** |
  
And **`set.filter`** lets you remove items on some criteria. 

## Combine Two Sets

- **`set.union`** in either
- **`set.intersection`** in both
- **`set.difference`** in the first, but not the second
- **`set.symmetric_difference`** in exactly one but not both
