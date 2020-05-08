# Text vs Bytes

- Byte objects are sequence of Bytes, where Strings are sequence of characters
- Byte objects are in machine readable form internally, Strings are only in human readable form.
- Since Byte objects are machine readable, they can be directly stored on the disk. Whereas, Strings need encoding before which they can be stored on disk.

![image](https://user-images.githubusercontent.com/2728804/81418683-6dc91900-9123-11ea-9b67-a04cb42e0969.png)

There are methods to convert a byte object to String and String to byte objects.

## Encoding

PNG, JPEG, MP3, WAV, ASCII, UTF-8 etc are different forms of encodings. An encoding is a format to represent audio, images, text, etc in bytes. Converting Strings to byte objects is termed as encoding. This is necessary so that the text can be stored on disk using mapping using ASCII or UTF-8 encoding techniques.

This task is achieved using `encode()`. It take encoding technique as argument. Default technique is `UTF-8` technique.

```python
>> ...: string_object = 'Apples'
   ...: byte_object = b'Apples'
   ...:
   ...: encoded_object = string_object.encode('ASCII')
   ...: print(encoded_object==byte_object)
True
```

<details>
  <summary>Raw Code</summary>

```python
string_object = 'Apples'
byte_object = b'Apples'

encoded_object = string_object.encode('ASCII')
print(encoded_object==byte_object)
```

</details>

## Decoding

Similarly, Decoding is process to convert a Byte object to String. It is implemented using `decode()`. A byte string can be decoded back into a character string, **if you know which encoding was used to encode it**. Encoding and Decoding are inverse processes.

```python
>> ...: string_object = 'Apples'
   ...: byte_object = b'Apples'
   ...:
   ...: decoded_object = byte_object.decode('ASCII')
   ...: print(decoded_object==string_object)
True
```

<details>
  <summary>Raw Code</summary>

```python
string_object = 'Apples'
byte_object = b'Apples'

decoded_object = byte_object.decode('ASCII')
print(decoded_object==string_object)
```

</details>

The same byte string can represent 2 different strings in 2 different encodings.

```python
>> ...: print(b'\xcf\x84o\xcf\x81\xce\xbdo\xcf\x82'.decode('utf-16'))
   ...: print(b'\xcf\x84o\xcf\x81\xce\xbdo\xcf\x82'.decode('utf-8'))
蓏콯캁澽苏
τoρνoς
```

<details>
  <summary>Raw Code</summary>

```python
print(b'\xcf\x84o\xcf\x81\xce\xbdo\xcf\x82'.decode('utf-16'))
print(b'\xcf\x84o\xcf\x81\xce\xbdo\xcf\x82'.decode('utf-8'))
```

</details>

## More content

- https://www.geeksforgeeks.org/byte-objects-vs-string-python/
- https://www.tutorialspoint.com/What-is-a-Python-bytestring
