
*Gleam lists are linked lists:*
- *Prefixing is cheaper than postfixing. One idiom: prefix many times, then reverse at the end.*
- *There's no lookup by index. If you need frequent lookups, consider using a dictionary.*
- *The benefits: everything immutable AND cheap to split of leading elements with pattern matching.*  

## Have some items:

**Make new lists**

- static declaration, eg. **`let items = [1, 2, 3]`**
  - `list.new` list with no starting items
  - `list.wrap` list with one starting item
- **`list.range`** inclusive, eg. `list.range(1, 3) --> [1, 2, 3]`
- **`list.repeat`** one item repeated n times

**Work leading and trailing values**

- prepend with **`let updated = [element, ..items]`**, or with `list.prepend`
- split with **`[first, ..rest] -> ...`**, or with `list.first` / `list.rest`
  - `list.last` gets the last item, traversing the whole list to do so

**Bisect into portions:**

- **`list.split`** bisect at an index
  - `list.take` gets just the front portion; `|> list.take(5)` is the first five elements
  - `list.drop` gets just the back, by skipping the front; `|> list.drop(2)` is all elements except the first two. 
- **`list.split_while`** bisect where a condition first fails, often useful on sorted lists
  - `list.take_while` gets just the front portion
  - `list.drop_while` gets just the back portion

*note: on a **sorted** list of appointments, compare:*
- *`|> list.drop_while(event.has_passed)` skips ahead to get all the upcoming ones*
- *`|> list.find(event.in_future)` gets the next one*

## Query a list:

**How many items?**

- `list.length`, `list.is_empty` (often, prefer pattern matching to these)

**Is there a ____?**

- `list.count` (how many items meet {criteria}?)
- `list.contains` (is this one element present...?)
- `list.find` (get me the first element that...)
- `list.pop` (same as find, but also returns list with the found element removed)

**What's the biggest? Smallest?**

- `list.min` / `list.max` pass in a comparison function, like `int.compare`

## Squish Values Around:
**Merging lists end-to-end**

- `list.append` (stick two lists together)
- `list.flatten` (stick many lists together)
   - and "concat" (deprecated, renamed to "flatten")

**Merging lists element-by-element**

- **`list.zip`** merge elementwise by wrapping in tuples: `list.zip([a, b], [1, 2]) ==>> [#(a, 1), #(b, 2)]`
  - `list.strict_zip` special case, enforcing equal list lengths, otherwise trailing elements are ignored
  - `list.unzip` reverse, split a list of tuples into two lists
- **`list.map2`** merge elementwise with any function, say adding or concatenating each pair

**Rearrange: keeping same structure**

- `list.reverse`
- `list.shuffle`
- `list.sort` / `list.max` takes comparison funcs like int.compare. See [orderings](https://github.com/CloserToTheCenter/GleamReference/edit/main/gleam/order.md) for more.

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

- **`list.filter`** (accept or reject)
- **`list.map`** (transform to a new value)
- **`list.each`** (launch some other function)

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

**Key Based**

All of these operate on a list of #(key, val) tuples. These are useful for Erlang interop, and to enable pattern matching.

- `list.key_filter` (all vals where key function matches)
- `list.key_find` (first val where key matches)
- `list.key_pop` (same as above, also returns transformed list)
- `list.key_set` (insert a key and value)
