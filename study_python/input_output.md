# Input and Output

### Need...

- To present the output of a program;

   - human-readable form
   - written to a file for future use
   - ...

- Fancier Output Formatting

   - Formatted string literals

      Begin a string with `f` or `F`

      Python expression between `{` and `}` : variables or literal values

      ```
      >>> year = 2016
      >>> event = 'Referendum'
      >>> f'Results of the {year} {event}'
      'Results of the 2016 Referendum'
      ```

   - str.format()

      `{` and `}` for variables

      Need to provide detailed formatting directives

      ```
      >>> yes_votes = 42_572_654
      >>> no_votes = 43_132_495
      >>> percentage = yes_votes / (yes_votes + no_votes)
      >>> '{:-9} YES votes  {:2.2%}'.format(yes_votes, percentage)
      ' 42572654 YES votes  49.67%'
      ```

- For Quck display

   Convert value to a string with the `repr()` or `str()` function :

   - `str()` : human-readable return

   - `repr()` : Return read by the interpreter

   - Numbers or structures like lists and dictionaries : Same representation using either function

   - Strings : Distinct representations.
   
   ```
   >>> s = 'Hello, world.'
   >>> str(s)
   'Hello, world.'

   >>> repr(s)
   "'Hello, world.'"

   >>> str(1/7)
   '0.14285714285714285'

   >>> x = 10 * 3.25
   >>> y = 200 * 200
   >>> s = 'The value of x is ' + repr(x) + ', and y is ' + repr(y) + '...'

   >>> print(s)
   The value of x is 32.5, and y is 40000...

   >>> # The repr() of a string adds string quotes and backslashes:
   ... hello = 'hello, world\n'
   >>> hellos = repr(hello)
   >>> print(hellos)
   'hello, world\n'

   >>> # The argument to repr() may be any Python object:
   ... repr((x, y, ('spam', 'eggs')))
   "(32.5, 40000, ('spam', 'eggs'))"
   ```
   
- **Formatted String Literals(`f` or `F`)**

   - Possible to use Python expressions in a string with `{expression}`

      ```
      >>> import math
      >>> print(f'The value of pi is approximately {math.pi:.3f}.')
      The value of pi is approximately 3.142.
      ```

   - Integer after the ':' : field to be a minimum number of characters wide

      ```
      >>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 7678}
      >>> for name, phone in table.items():
      ...     print(f'{name:10} ==> {phone:10d}')
      ...
      Sjoerd     ==>       4127
      Jack       ==>       4098
      Dcab       ==>       7678
      ```

   - `'!a'` applies ascii(), `'!s'` applies str(), and `'!r'` applies repr():

      ```
      >>> animals = 'eels'
      >>> print(f'My hovercraft is full of {animals}.')
      My hovercraft is full of eels.
      >>> print(f'My hovercraft is full of {animals!r}.')
      My hovercraft is full of 'eels'.
      ```

- **String format() Method**

   - Basic usage of the str.format()

      ```
      >>> print('We are the {} who say "{}!"'.format('knights', 'Ni'))
      We are the knights who say "Ni!"

      >>> print('{0} and {1}'.format('spam', 'eggs'))
      spam and eggs
      >>> print('{1} and {0}'.format('spam', 'eggs'))
      eggs and spam
      ```

   - keyword arguments are used in the `str.format()`

      ```
      >>> print('This {food} is {adjective}.'.format(
      ...       food='spam', adjective='absolutely horrible'))
      This spam is absolutely horrible.
      ```

   - Combining positional and keyword arguments

      ```
      >>> print('The story of {0}, {1}, and {other}.'.format('Bill', 'Manfred',
                                                             other='Georg'))
      The story of Bill, Manfred, and Georg.
      ```

   - For log format string : use dict and `[]` to access the keys

      ```
      table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
      print('Jack: {0[Jack]:d}; Sjoerd: {0[Sjoerd]:d}; '
            'Dcab: {0[Dcab]:d}'.format(table))
      ```

      or, pass the table as keyword arguments with the '**' notation.
      ```
      >>> table = {'Sjoerd': 4127, 'Jack': 4098, 'Dcab': 8637678}
      >>> print('Jack: {Jack:d}; Sjoerd: {Sjoerd:d}; Dcab: {Dcab:d}'.format(**table))
      Jack: 4098; Sjoerd: 4127; Dcab: 8637678
      ```

   - Tidily-aligned set of columns giving integers and their squares and cubes:
      ```
      >>> for x in range(1, 11):
      ...     print('{0:2d} {1:3d} {2:4d}'.format(x, x*x, x*x*x))
      ...
       1   1    1
       2   4    8
       3   9   27
       4  16   64
       5  25  125
       6  36  216
       7  49  343
       8  64  512
       9  81  729
      10 100 1000
      ```

- **Manual String Formatting**

   - `str.rjust()` : right-justifies a string, padding with spaces on the left

      ```
      >>> for x in range(1, 11):
      ...     print(repr(x).rjust(2), repr(x*x).rjust(3), end=' ')
      ...     # Note use of 'end' on previous line
      ...     print(repr(x*x*x).rjust(4))
      ...
       1   1    1
       2   4    8
       3   9   27
       4  16   64
       5  25  125
       6  36  216
       7  49  343
       8  64  512
       9  81  729
      10 100 1000
      ```

   - `str.zfill()` : pads a numeric string on the left with zeros. It understands about plus and minus signs.

      ```
      >>> '12'.zfill(5)
      '00012'
      >>> '-3.14'.zfill(7)
      '-003.14'
      >>> '3.14159265359'.zfill(5)
      '3.14159265359'
      ```

   - `%` operator : interprets the left argument to be applied to the right argument.
      ```
      >>> import math
      >>> print('The value of pi is approximately %5.3f.' % math.pi)
      The value of pi is approximately 3.142.
      ```

### Reading and Writing Files

#### open(filename, mode)

   - `r` : read only. default
   - `w` : writing only (an existing file with the same name will be erased)
   - `a` : appending (add written data to the end of the file)
   - `r+` : for both reading and writing
   - `b` : open  the file in binary mode

      ```
      >>> f = open('workfile', 'w')
      ```
   
   - `with` keyword is recommended to close the file properly
   
      ```
      >>> with open('workfile') as f:
      ...     read_data = f.read()
      >>> f.closed
      True
      ```

#### Other methods

- `f.read(size)`

   - reads some quantity of data
   - return a string (in text mode) or bytes object (in binary mode)
   - if omitted or negative `size`,

      entire contents of the file will be read and returned
   - If the end of the file has been reached, `f.read()` will return an empty string (`''`).
   
   ```
   >>> f.read()
   'This is the entire file.\n'
   >>> f.read()
   ''
   ```

- `f.readline()`

   - reads a single line from the file
   - left new newline character (`\n`)

   ```
   >>> f.readline()
   'This is the first line of the file.\n'
   >>> f.readline()
   'Second line of the file\n'
   >>> f.readline()
    ''
   ```

   ```
   >>> for line in f:
   ...     print(line, end='')
   ...
   This is the first line of the file.
   Second line of the file
   ```

   to read lines, use ` list(f)` or `f.readlines()`

- `f.write(string)`

   - writes the contents of **string** to the file
   - returning the number of characters written

      ```
      >>> f.write('This is a test\n')
      15
      ```

   - for other types

      ```
      >>> value = ('the answer', 42)
      >>> s = str(value)  # convert the tuple to string
      >>> f.write(s)
      18
      ```
- `f.tell()`

   file object's current position in integer

- `f.seek(offset, from_what)`

   - change the file object's position
   - adding `offset` to `from_what`
   - from_what
      - beginning of the file (default) : 0
      - current file position : 1
      - end of the file : 2
   ```
   >>> f = open('workfile', 'rb+')
   >>> f.write(b'0123456789abcdef')
   16
   >>> f.seek(5)      # Go to the 6th byte in the file
   5
   >>> f.read(1)
   b'5'
   >>> f.seek(-3, 2)  # Go to the 3rd byte before the end
   13
   >>> f.read(1)
   b'd'
   ```

#### Saving structured data with json

`json`
   - serializing : Taking Python data hierarchies and convert them to string representations
   - deserializing : Reconstructing the data from the string representation


If you have an object x, you can view its JSON string representation

   ```
   >>> import json
   >>> json.dumps([1, 'simple', 'list'])
   '[1, "simple", "list"]'
   ```

if `f` is a text file object opened for writing, we can do this:
   ```
   json.dump(x, f)
   ```

To decode the object again, if `f` is a text file object
   ```
   x = json.load(f)
   ```
