# Dynamic

## Call dynamically a method

Structure

```python
getattr(obj, "func_name")()
```

```python
getattr(obj, "func_name")(param1, param2)
```

Example

```python
>>> class Printer:
...     def print_hi(self):
...         print("hi")
...     def print_hi_personalized(self, name):
...         print(f"hi {name}!")
...
>>> printer = Printer()
>>> printer.print_hi()
hi
>>> getattr(printer, "print_hi")()
hi
>>> printer.print_hi_personalized("Camila")
hi Camila!
>>> getattr(printer, "print_hi_personalized")("Camila")
hi Camila!
```

<details>
  <summary>Raw Code</summary>

```python
class Printer:
    def print_hi(self):
        print("hi")

    def print_hi_personalized(self, name):
        print(f"hi {name}!")

printer = Printer()
printer.print_hi()
getattr(printer, "print_hi")()
printer.print_hi_personalized("Camila")
getattr(printer, "print_hi_personalized")("Camila")
```

</details>

<details>
  <summary>More info</summary>

https://docs.python.org/3/library/functions.html#getattr

</details>
