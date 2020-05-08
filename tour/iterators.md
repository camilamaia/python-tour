# Iterators

## Iterable

First, let's start understanding Iterables. Iterable are objects that can be used in iteration.

Lists, tuples, dictionaries, and sets are all **iterable objects**. They are iterable containers which you can **get an iterator from**.

All these objects have an `iter()` method which is used to get an iterator.

Example

```python
>>> iter("apple")                                      # String
<str_iterator object at 0x101250290>
>>> iter(["apple", "banana", "cherry"])                # List
<list_iterator object at 0x101250310>
>>> iter(("apple", "banana", "cherry"))                # Tuple
<tuple_iterator object at 0x101250290>
>>> iter({"apple", "banana", "cherry"})                # Set
<set_iterator object at 0x101252820>
>>> iter({'apple': 1, 'banana': 2, 'cherry': 3})       # Dict
<dict_keyiterator object at 0x101251050>
```

<details>
  <summary>Raw Code</summary>

```python
iter("apple")                                      # String
iter(["apple", "banana", "cherry"])                # List
iter(("apple", "banana", "cherry"))                # Tuple
iter({"apple", "banana", "cherry"})                # Set
iter({"apple": 1, "banana": 2, "cherry": 3})       # Dict
```

</details>

Example of object types that aren’t iterable:

```python
>>> iter(42)                                   # Integer
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'int' object is not iterable
>>> iter(3.1)                                  # Float
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'float' object is not iterable
>>> iter(len)                                  # Built-in function
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'builtin_function_or_method' object is not iterable
```

<details>
  <summary>Raw Code</summary>

```python
iter(42)                                   # Integer
iter(3.1)                                  # Float
iter(len)                                  # Built-in function
```

</details>

## Iterators

An iterator is an object that contains a countable number of values.

An iterator is an object that can be iterated upon, meaning that you can traverse through all the values.

An iterator is essentially a value producer that yields successive values from its associated iterable object. The built-in function next() is used to obtain the next value from in iterator.

Example

```python
>>> fruits = ("apple", "banana", "cherry")
>>> fruits_iterator = iter(fruits)
>>> print(fruits_iterator)
<tuple_iterator object at 0x101250090>
>>> print(next(fruits_iterator))
apple
>>> print(next(fruits_iterator))
banana
>>> print(next(fruits_iterator))
cherry
```

<details>
  <summary>Raw Code</summary>

```python
fruits = ("apple", "banana", "cherry")
fruits_iterator = iter(fruits)
print(fruits_iterator)

print(next(fruits_iterator))
print(next(fruits_iterator))
print(next(fruits_iterator))
```

</details>

Notice how an iterator retains its state internally. It knows which values have been obtained already, so when you call next(), it knows what value to return next.

Another example, but now using a string

```python
>>> banana = "banana"
>>> banana_iterator = iter(banana)
>>> print(banana_iterator)
<str_iterator object at 0x10124cf90>
>>> print(next(banana_iterator))
b
>>> print(next(banana_iterator))
a
>>> print(next(banana_iterator))
n
>>> print(next(banana_iterator))
a
>>> print(next(banana_iterator))
n
>>> print(next(banana_iterator))
a
```

<details>
  <summary>Raw Code</summary>

```python
banana = "banana"
banana_iterator = iter(banana)
print(banana_iterator)

print(next(banana_iterator))
print(next(banana_iterator))
print(next(banana_iterator))
print(next(banana_iterator))
print(next(banana_iterator))
print(next(banana_iterator))
```

</details>

## StopIteration Exception

What happens when the iterator runs out of values? StopIteration is the normal, expected signal to tell that there is nothing more to be iterated.

Every time you try to call `next()` in an iterator that has already reached the end, you will face a StopIteration Exception.

Example

```python
>>> banana = "banana"
>>> banana_iterator = iter(banana)
>>> print(next(banana_iterator))
b
>>> print(next(banana_iterator))
a
>>> print(next(banana_iterator))
n
>>> print(next(banana_iterator))
a
>>> print(next(banana_iterator))
n
>>> print(next(banana_iterator))
a
>>> next(banana_iterator)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

<details>
  <summary>Raw Code</summary>

```python
banana = "banana"
banana_iterator = iter(banana)

print(next(banana_iterator))
print(next(banana_iterator))
print(next(banana_iterator))
print(next(banana_iterator))
print(next(banana_iterator))
print(next(banana_iterator))

next(banana_iterator)
```

</details>

<details>
  <summary>More info</summary>

https://docs.python.org/3/library/exceptions.html#StopIteration

</details>

If all the values from an iterator have been returned already, a subsequent next() call raises a StopIteration exception. Any further attempts to obtain values from the iterator will fail.


## Multiple independent iterators on the same iterable object

You can define multiple independent iterators on the same iterable object

Example

```python
>>> fruits = ("apple", "banana", "cherry")
>>> fruits_iterator_1 = iter(fruits)
>>> fruits_iterator_2 = iter(fruits)
>>> print(fruits_iterator_1)
<tuple_iterator object at 0x101250310>
>>> print(fruits_iterator_2)
<tuple_iterator object at 0x101250250>
>>> print(next(fruits_iterator_1))
apple
>>> print(next(fruits_iterator_1))
banana
>>> print(next(fruits_iterator_1))
cherry
>>> print(next(fruits_iterator_2))
apple
```

<details>
  <summary>Raw Code</summary>

```python
fruits = ("apple", "banana", "cherry")
fruits_iterator_1 = iter(fruits)
fruits_iterator_2 = iter(fruits)
print(fruits_iterator_1)
print(fruits_iterator_2)
print(next(fruits_iterator_1))
print(next(fruits_iterator_1))
print(next(fruits_iterator_1))
print(next(fruits_iterator_2))
```

</details>

Even when iterator `fruits_iterator_1` is already at the end of the list, `fruits_iterator_2` is still at the beginning. Each iterator maintains its own internal state, independent of the other.

## Grab all the values from an iterator at once

If you want to grab all the values from an iterator at once, you can use the built-in list() function. Among other possible uses, list() takes an iterator as its argument, and returns a list consisting of all the values that the iterator yielded:

Example

```python
>>> fruits = ("apple", "banana", "cherry")
>>> fruits_iterator = iter(fruits)
>>> list(fruits_iterator)
['apple', 'banana', 'cherry']
```

<details>
  <summary>Raw Code</summary>

```python
fruits = ("apple", "banana", "cherry")
fruits_iterator = iter(fruits)
list(fruits_iterator)
```

</details>

Similarly, the built-in tuple() and set() functions return a tuple and a set, respectively, from all the values an iterator yields:

Example

```python
>>> fruits = ("apple", "banana", "cherry")
>>> fruits_iterator_1 = iter(fruits)
>>> fruits_iterator_2 = iter(fruits)
>>> tuple(fruits_iterator_1)
('apple', 'banana', 'cherry')
>>> set(fruits_iterator_2)
{'apple', 'banana', 'cherry'}
```

<details>
  <summary>Raw Code</summary>

```python
fruits = ("apple", "banana", "cherry")
fruits_iterator_1 = iter(fruits)
fruits_iterator_2 = iter(fruits)
tuple(fruits_iterator_1)
set(fruits_iterator_2)
```

</details>

Example

```python
>>> fruits = ("apple", "banana", "cherry")
>>> fruits_iterator = iter(fruits)
>>> list(fruits_iterator)
['apple', 'banana', 'cherry']
>>> list(fruits_iterator)
[]
```

<details>
  <summary>Raw Code</summary>

```python
fruits = ("apple", "banana", "cherry")
fruits_iterator = iter(fruits)
list(fruits_iterator)
list(fruits_iterator)
```

</details>

**It isn’t necessarily advised to make a habit of this. Part of the elegance of iterators is that they are “lazy.” That means that when you create an iterator, it doesn’t generate all the items it can yield just then. It waits until you ask for them with next(). Items are not created until they are requested.**

**When you use list(), tuple(), or the like, you are forcing the iterator to generate all its values at once, so they can all be returned. If the total number of objects the iterator returns is very large, that may take a long time.**

## Looping Through an Iterator

We can also use a for loop to iterate through an iterable object.

Structure:

```python
for <var> in <iterable>:
    <statement(s)>
```

The for loop actually creates an iterator object and executes the next() method for each loop.

Example

```python
>>> fruits = ("apple", "banana", "cherry")
>>> for fruit in fruits:
...   print(fruit)
...
apple
banana
cherry
```

<details>
  <summary>Raw Code</summary>

```python
fruits = ("apple", "banana", "cherry")

for fruit in fruits:
  print(fruit)
```

</details>

This loop can be described entirely in terms of the concepts you have just learned about. To carry out the iteration this for loop describes, Python does the following:

- Calls `iter()` to obtain an iterator for `fruits`
- Calls `next()` repeatedly to obtain each item from the iterator in turn
- Terminates the loop when `next()` raises the `StopIteration` exception

The loop body is executed once for each item next() returns, with loop variable i set to the given item for each iteration.

## Why make an iterator?

Iterators allow you to make an iterable that computes its items as it goes. Which means that you can make iterables that are lazy, in that they don’t determine what their next item is until you ask them for it.


## Create an Iterator

Iterators are also iterables and their iterator is themselves.

Technically, in Python, an iterator is an object which implements the iterator protocol, which consist of the methods `__iter__()` and `__next__()`.

Calling the built-in `iter` function on an object will attempt to call its `__iter__` method. Calling the built-in `next` function on an object will attempt to call its `__next__` method.

The iter function is supposed to return an iterator. So our `__iter__` function must return an iterator. But our object is an iterator, so should return ourself. Therefore our Count object returns self from its `__iter__` method because it is its own iterator.

The `next` function is supposed to return the next item in our iterator or raise a `StopIteration` exception when there are no more items. We’re returning the current number and incrementing the number so it’ll be larger during the next `__next__` call.

Example

```python
>>> class CounterUpToThree:
...   """Iterator that counts up to three."""
...   def __init__(self, start=0):
...       self.current_number = start
...   def __iter__(self):
...       return self
...   def __next__(self):
...       if self.current_number > 3:
...         raise StopIteration
...       current_number = self.current_number
...       self.current_number += 1
...       return current_number
...
>>> counter = CounterUpToThree()
>>> next(counter)
0
>>> next(counter)
1
>>> next(counter)
2
>>> next(counter)
3
>>> next(counter)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "<stdin>", line 9, in __next__
StopIteration
```

<details>
  <summary>Raw Code</summary>

```python
class CounterUpToThree:

  """Iterator that counts up to three."""

  def __init__(self, start=0):
    self.current_number = start

  def __iter__(self):
    return self

  def __next__(self):
    if self.current_number > 3:
      raise StopIteration

    current_number = self.current_number
    self.current_number += 1
    return current_number

counter = CounterUpToThree()
next(counter)
next(counter)
next(counter)
next(counter)
next(counter)
```

</details>

Let's build a simpler version of python [`range`](https://docs.python.org/3/library/stdtypes.html#range).

```python
>>> class SimpleRange(object):
...     def __init__(self, start, stop):
...         self.current = start
...         self.stop = stop
...     def __iter__(self):
...         return self
...     def __next__(self):
...         if self.current == self.stop:
...             raise StopIteration
...         self.current += 1
...         return self.current - 1
...
>>> simple_range_1 = SimpleRange(0,4)
>>> print(list(simple_range_1))
[0, 1, 2, 3]
>>> simple_range_2 = SimpleRange(10,20)
>>> print(list(simple_range_2))
[10, 11, 12, 13, 14, 15, 16, 17, 18, 19]
```

<details>
  <summary>Raw Code</summary>

```python
class SimpleRange(object):
  def __init__(self, start, stop):
    self.current = start
    self.stop = stop

  def __iter__(self):
    return self

  def __next__(self):
    if self.current = self.stop:
        raise StopIteration

    self.current += 1
    return self.current - 1

simple_range_1 = SimpleRange(0,4)
print(list(simple_range_1))
simple_range_2 = SimpleRange(10,20)
print(list(simple_range_2))
```

</details>

## Iterators Length

Additionally, iterators have abilities that other iterables don’t. For instance, the laziness of iterables can be used to make iterables that have an **unknown length**. In fact, you can even make infinitely long iterators.

The `itertools.count` utility, for example, will give us an iterator that will provide every number from 0 upward as we loop over it:

```python
>>> from itertools import count
>>> for number in count():
...     print(number)
...
0
1
2
(this goes on forever)
```

<details>
  <summary>Raw Code</summary>

```python
from itertools import count

for number in count():
  print(number)
```

</details>

We could implement our own endless count:

```python
>>> class Counter:
...   """Iterator that counts forever."""
...   def __init__(self, start=0):
...     self.current_number = start
...   def __iter__(self):
...     return self
...   def __next__(self):
...     self.current_number += 1
...     return self.current_number - 1
...
>>> counter = Counter()
>>> for number in counter:
...     print(number)
...
0
1
2
3
(this goes on forever)
```

<details>
  <summary>Raw Code</summary>

```python
class Counter:

  """Iterator that counts forever."""

  def __init__(self, start=0):
    self.current_number = start

  def __iter__(self):
    return self

  def __next__(self):
    self.current_number += 1
    return self.current_number - 1

counter = Counter()
for number in counter:
    print(number)
```

</details>

## More content

- https://docs.python.org/3/c-api/iterator.html
- https://www.python.org/dev/peps/pep-0234/
- https://anandology.com/python-practice-book/iterators.html#iterators
- https://www.w3schools.com/python/python_iterators.asp
- https://www.programiz.com/python-programming/iterator
- https://www.datacamp.com/community/tutorials/python-iterator-tutorial
- https://wiki.python.org/moin/Iterator
- https://dbader.org/blog/python-iterators
- https://treyhunner.com/2018/06/how-to-make-an-iterator-in-python/
- https://realpython.com/python-for-loop/
