[Work In Progress]

# Generators

Generator functions allow you to declare a function that **behaves like an iterator**, i.e. it can be used in a for loop.

There is a lot of overhead in building an iterator in Python; we have to implement a class with `__iter__()` and `__next__()` method, keep track of internal states, raise `StopIteration` when there was no values to be returned etc.

Python generators are a simple way of creating iterators. All the overhead we mentioned above are automatically handled by generators in Python.

Simply speaking, a generator is a function that returns an object (iterator) which we can iterate over (one value at a time).

## How to create a generator in Python?

It is fairly simple to create a generator in Python. It is as easy as defining a normal function with yield statement instead of a return statement.

If a function contains at least one yield statement (it may contain other yield or return statements), it becomes a generator function.

Both yield and return will return some value from a function. The difference is that, while a return statement terminates a function entirely, yield statement pauses the function saving all its states and later continues from there on successive calls.

```python
>>> def vowels():
...     yield "a"
...     yield "e"
...     yield "i"
...     yield "o"
...     yield "u"
...
>>> print(vowels())
<generator object vowels at 0x10c1587d0>
>>> generator_obj = vowels()
>>> print(next(generator_obj))
a
>>> print(next(generator_obj))
e
>>> print(next(generator_obj))
i
>>> print(next(generator_obj))
o
>>> print(next(generator_obj))
u
>>> print(next(generator_obj))
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

<details>
  <summary>Raw Code</summary>

```python
def vowels():
    yield "a"
    yield "e"
    yield "i"
    yield "o"
    yield "u"

print(vowels())
generator_obj = vowels()

print(next(generator_obj))
print(next(generator_obj))
print(next(generator_obj))
print(next(generator_obj))
print(next(generator_obj))
print(next(generator_obj))
```

</details>



## Differences between Generator function and a Normal function

# A simple generator function

```python
def my_gen():
    n = 1
    print('This is printed first')
    # Generator function contains yield statements
    yield n
    n += 1
    print('This is printed second')
    yield n
    n += 1
    print('This is printed at last')
    yield n
```

## Python Generators with a Loop

```python
def rev_str(my_str):
    length = len(my_str)
    for i in range(length - 1,-1,-1):
        yield my_str[i]
```


## More content

https://docs.python.org/3/c-api/gen.html
https://www.python.org/dev/peps/pep-0255/
https://wiki.python.org/moin/Generators
https://www.programiz.com/python-programming/generator
