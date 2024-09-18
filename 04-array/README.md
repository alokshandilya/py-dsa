# Array / List in Python

- implemented as `list` in python
- allows items of _different types_
- negative indexing _(last element is -1)_
- slicing: `a[start:stop:step]`
  - default values are `start=0`, `stop=len(a)`, `step=1`
  - eg. `a[1:3]` _returns elements from index 1 to 2_

## Some important list methods

- [documentation](https://docs.python.org/3/tutorial/datastructures.html)

| **Method**                         | **Best Case** | **Average Case** | **Worst Case** | **Notes**                                                      |
| ---------------------------------- | ------------- | ---------------- | -------------- | -------------------------------------------------------------- |
| `append(x)`                        | O(1)          | O(1)             | O(1)           | Amortized constant time, `a[len(a):] = [x]`                    |
| `insert(i, x)`                     | O(1)          | O(n)             | O(n)           | Inserting at the beginning is costly                           |
| `pop([i])`                         | O(1)          | O(n)             | O(n)           | Costly if removing from the start                              |
| `remove(x)`                        | O(1)          | O(n)             | O(n)           | Linear search, `ValueError` if not found                       |
| `extend(iterable)`                 | O(1)          | O(k)             | O(k)           | Where k is the length of the iterable, `a[len(a):] = iterable` |
| `index(x[, start[, end]])`         | O(1)          | O(n)             | O(n)           | Raises `ValueError` if not found                               |
| `count(x)`                         | O(1)          | O(n)             | O(n)           | Linear search for count                                        |
| `reverse()`                        | O(1)          | O(n)             | O(n)           | Reverses the list in place                                     |
| `sort(*, key=None, reverse=False)` | O(n log n)    | O(n log n)       | O(n log n)     | Uses Timsort algorithm                                         |
| `copy()`                           | O(n)          | O(n)             | O(n)           | Shallow copy of the list, `a[:]`                               |
| `clear()`                          | O(1)          | O(1)             | O(1)           | Removes all items from the list, `del a[:]`                    |

- **Timsort algorithm**: Hybrid sorting algorithm derived from merge sort and insertion sort, default in Python.
- **Shallow copy**: Creates a new list and copies the references of the original list to the new list.
- **Deep copy**: Creates a new list and copies the references of the original list to the new list, but also copies the references of the nested objects.
- `list.pop()` removes and returns the last element of the list, is $O(1)$.

## Important points

- **random access** is $O(1)$ because of indexing.
- **_cache locality_** - the elements are stored in contiguous memory locations.
- _dynamic size_ - no need to specify the size beforehand.
- _heterogeneous_ - the python list is implemented as an _array of references to the objects/values_ (not the objects/values themselves) allowing different types of objects in the same list.
- _mutable_ - can be changed in place.
- the array has pre-allocated memory to accommodate new elements, so the `append` operation is $O(1)$ on average.
- `list.append(x)` worst case can be $O(n)$ if the array is full and a new memory block needs to be allocated.
  - it's amortized $O(1)$ because the array is over-allocated by a factor of $1.125$.
