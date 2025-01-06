## Have some items:

**Make new lists**

- static declaration, eg. `let items = [1, 2, 3]`
  - `list.new` (list with no items)
  - `list.wrap` (list with one item)
- `list.range` (inclusive, eg. `list.range(1, 3) --> [1, 2, 3]`)
- `list.repeat` (one item repeated n times)

**Look at leading and trailing values**

- `list.prepend` (prefer pattern matching [a, ..rest] =)
- `list.rest` (prefer pattern matching [first, ..rest] ->)
- `list.first` (first item, error on empty)
- `list.last` (last item, error on empty)

*note: all lists are linked lists
- there's no "get by index".
- prefixing is more performant.
- this is functional land baby.

**Bisect at some index:**

- `list.take` (items up to index)
- `list.drop` (inverse of "take", the portion after index)
- `list.split` (front and back halves, split at index)

**Bisect by some criteria:**

- `list.take_while` (items while condition holds, a prefix)
- `list.drop_while` (the back half)
- `list.split_while` (both halves)

## Query a list:

**How many items?**

- `list.length`, `list.is_empty` (often, prefer pattern matching to these)

**Is there a ____?**

- `list.count` (how many items meet {criteria}?)
- `list.contains` (is this one element present...?)
- `list.find` (get me the first element that...)
- `list.pop` (same as find, but also returns list with the found element removed)

**Are they all True? False?**

- `list.all` / `list.any` (do {all/any} items fulfill {criteria}?)

## Squish Values Around:
**Merging lists end-to-end**

- `list.append` (stick two lists together)
- `list.flatten` (stick many lists together)
   - and "concat" (deprecated, renamed to "flatten")

**Merging lists element-by-element**

- `list.zip` (merge elementwise into tuples)
 - `list.map2` (merge elementwise with any func)
 - `list.strict_zip` (enforce list lengths are the same)
- `list.unzip` (list of tuples back into two lists)

**Rearrange: keeping same structure**

- `list.reverse`
- `list.shuffle`
- `list.sort` (takes a comparison func like int.compare)

**Rearrange: by changing array boundaries**

- `list.transpose` (flips rows to cols, and cols to rows)
- `list.interleave` (take 1 card at a time from alternating piles)
- `list.intersperse` (like string.join, but with any type)
- `list.chunk` (by any criteria, grouped into arrays)
  - `list.partition` (instead always two groups, for true and false)
  - `list.sized_chunk` (group items by index, ie paginate)
  - `list.group` (instead returns a "dict" with labelled groups)

**View just Unique Elements**

- `list.unique` (list of unique values)
*note: also see "group" above for a way to count uniques**

**View possible Orderings**

- `list.combinations` (all orderings of n elements)
 - `list.combination_pairs` (special case n=2)
 - `list.permutations` (special case using every element)

**View through Sliding Windows**

- `list.window` (for stuff like sliding averages)
 - `list.window_by_2` (special case n=2)

## Transform a list with an external function:
**For each element...**

- `list.filter` (accept or reject)
- `list.map` (transform to a new value)
- `list.each` (launch some other function)

**Fold up a list**

- `list.fold` (combine one element at a time towards a final goal)
  - `list.fold_right` (starting at the other end)
  - `list.fold_until` (possibly stopping early)
  - see `int.sum` for an easy way to add ints*
- `list.reduce` (no given start, uses first item instead, can error)
- `list.scan` (returns the intermediate values in a list)

**With indices visible as I go**

- `list.index_fold` / `index_map` (the provided function sees each value in a tuple with its index)

**Handling errors as I go**

- `list.try_each` / `try_fold` / `try_map` (each step returns a result; on error the process aborts)

**Combining two list utilities into one**

- `list.list.map_fold` (during a map operation, maintain and pass a value around)
- `list.filter_map` (map then filter)
- `list.find_map` (map then find)
- `list.flat_map` (map then flatten)
- `list.pop_map` (map then pop)

**Key Based (for Erlang interop mostly)**

All of these operate on a list of #(key, val) tuples.

- `list.key_filter` (all vals where key function matches)
- `list.key_find` (first val where key matches)
- `list.key_pop` (same as above, also returns transformed list)
- `list.key_set` (insert a key and value)

[todo: gleam linked list meme]
