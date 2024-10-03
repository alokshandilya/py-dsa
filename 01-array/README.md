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

## Static Array

```python
# Insert n into arr at the next open position.
# Length is the number of 'real' values in arr, and capacity
# is the size (aka memory allocated for the fixed size array).
def insertEnd(arr, n, length, capacity):
    if length < capacity:
        arr[length] = n


# Remove from the last position in the array if the array
# is not empty (i.e. length is non-zero).
def removeEnd(arr, length):
    if length > 0:
        # Overwrite last element with some default value.
        # We would also the length to decreased by 1.
        arr[length - 1] = 0


# Insert n into index i after shifting elements to the right.
# Assuming i is a valid index and arr is not full.
def insertMiddle(arr, i, n, length):
    # Shift starting from the end to i.
    for index in range(length - 1, i - 1, -1):
        arr[index + 1] = arr[index]

    # Insert at i
    arr[i] = n


# Remove value at index i before shifting elements to the left.
# Assuming i is a valid index.
def removeMiddle(arr, i, length):
    # Shift starting from i + 1 to end.
    for index in range(i + 1, length):
        arr[index - 1] = arr[index]
    # No need to 'remove' arr[i], since we already shifted


def printArr(arr, capacity):
    for i in range(capacity):
        print(arr[i])
```

## Dynamic Array

```python
# Python arrays are dynamic by default, but this is an example of resizing.
class Array:
    def __init__(self):
        self.capacity = 2
        self.length = 0
        self.arr = [0] * 2 # Array of capacity = 2

    # Insert n in the last position of the array
    def pushback(self, n):
        if self.length == self.capacity:
            self.resize()

        # insert at next empty position
        self.arr[self.length] = n
        self.length += 1

    def resize(self):
        # Create new array of double capacity
        self.capacity = 2 * self.capacity
        newArr = [0] * self.capacity

        # Copy elements to newArr
        for i in range(self.length):
            newArr[i] = self.arr[i]
        self.arr = newArr

    # Remove the last element in the array
    def popback(self):
        if self.length > 0:
            self.length -= 1

    # Get value at i-th index
    def get(self, i):
        if i < self.length:
            return self.arr[i]
        # Here we would throw an out of bounds exception

    # Insert n at i-th index
    def insert(self, i, n):
        if i < self.length:
            self.arr[i] = n
            return
        # Here we would throw an out of bounds exception

    def print(self):
        for i in range(self.length):
            print(self.arr[i])
        print()
```

## Stack

```python
# Implementing a stack is trivial using a dynamic array
# (which we implemented earlier).
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, n):
        self.stack.append(n)

    def pop(self):
        return self.stack.pop()
```
