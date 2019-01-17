# Modules

### Need...

- If you quit from the Python interpreter, the definitions you have made (functions and variables) are lost.

   - For the longer program? Use a text editor => "script"

      - If the script gets longer...

          you may want to split it into several files for easier maintenance.

- Without copying its definition, using handy function in several programs.

### To suport the need...

Python has a way to put definitions in a file and use them in a script or in an interactive instance of the interpreter.

Such a file is called a **module**.

### Modules

   - A module is a file containing Python definitions and executable statements. 
      - statements
         - are intended to initialize the module
         - executed only the first time the module name is encountered in an import statement.
   - Definitions from a module can be imported into other modules or into the main module.
   - file name format : `*.py`

   - Within a module, the module name (as a string) is available as the value of the global variable `__name__`.

      EX) To use `fibo.py`

      ```
      # Fibonacci numbers module

      def fib(n):    # write Fibonacci series up to n
          a, b = 0, 1
          while a < n:
              print(a, end=' ')
              a, b = b, a+b
          print()

      def fib2(n):   # return Fibonacci series up to n
          result = []
          a, b = 0, 1
          while a < n:
              result.append(a)
              a, b = b, a+b
          return result
      ```

      1. Import module with module name `fibo`
         ```
         >>> import fibo
         ```

      2. Use module name to access the functions.
         ```
         >>> fibo.fib(1000)
         0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987
         >>> fibo.fib2(100)
         [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
         >>> fibo.__name__
         'fibo'
         ```

      3. If you intend to use a function often you can assign it to a local name:
         ```
         >>> fib = fibo.fib
         >>> fib(500)
         0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
         ```

> **Note**
>
> For efficiency reasons, each module is only imported once per interpreter session.
>
> Therefore, if you change your modules, you must restart the interpreter.
>
> Or, if it's just one module you want to test interactively, use `importlib.reload()`, e.g. `import importlib; importlib.reload(modulename)`.


### More on Modules

Each module has its own private symbol table,

used as the global symbol table by all functions defined in the module.

   -> The author of a module can use global variables in the module without worrying about accidental clashes with a user's global variables.

Modules can import other modules. The imported module names are placed in the importing module's global symbol table.

   - Variant of the import statement

      - `fibo` not defined
         ```
         >>> from fibo import fib, fib2
         >>> fib(500)
         0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
         ```
      - Import all that a module defines.
         ```
         >>> from fibo import *
         >>> fib(500)
         0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
         ```
         - names start with `_` are excepted.
         - often causes poorly readable code...
      - If module name is followed by `as`, name following `as` is bound directly to the imported module.
         ```
         >>> import fibo as fib
         >>> fib.fib(500)
         0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
         ```
         ```
         >>> from fibo import fib as fibonacci
         >>> fibonacci(500)
         0 1 1 2 3 5 8 13 21 34 55 89 144 233 377
         ```

   - Executing modules as scripts for convenient user interface, or testing

      When you run a Python module as below, the code in the module will be executed, but with the `__name__` set to `"__main__"`.
      ```
      python fibo.py <arguments>
      ```
      To do so, add this code at the end of your module
      ```
      if __name__ == "__main__":
          import sys
          fib(int(sys.argv[1]))
      ```
      It make the file usable as a script, because the code only runs if the module is executed as the "main" file:
      ```
      $ python fibo.py 50
      0 1 1 2 3 5 8 13 21 34
      ```
      If the module is imported, the code is not run:
      ```
      >>> import fibo
      >>>
      ```
   - The Module Search Path
      1. built-in module with imported name.
      2. file named `imported_name.py` in a list of directories by `sys.path`

         `sys.path` initialized from below locations:
            - The directory containing the input script (or the current directory when no file is specified).
            - PYTHONPATH (a list of directory names, with the same syntax as the shell variable `PATH`).
            - The installation-dependent default.

         The directory containing the symlink is not added to the module search path.

   - "Compiled" Python files

      To speed up, compiled version of each module as `__pycache__/module.version.pyc`

      ex) cached of CPython release 3.3 the compiled version of `spam.py` : `__pycache__/spam.cpython-33.pyc`

      - Python checks the modification date of the source against the compiled version.
      - Python doesn't check the cache if
         - loaded directly from the command line
         - no source module (compiled only). The compiled module must be in the source directory.

   - Standard Modules
   @@@

   - The `dir()` Function

      The built-in function dir() is used to find out which names a module defines.

      It returns a sorted list of strings, all types of names: variables, modules, functions, etc.
      ```
      >>> import fibo, sys
      >>> dir(fibo)
      ['__name__', 'fib', 'fib2']
      >>> dir(sys)  
      ['__displayhook__', '__doc__', '__excepthook__', '__loader__', '__name__',
       '__package__', '__stderr__', '__stdin__', '__stdout__',
       '_clear_type_cache', '_current_frames', '_debugmallocstats', '_getframe',
       '_home', '_mercurial', '_xoptions', 'abiflags', 'api_version', 'argv',
       'base_exec_prefix', 'base_prefix', 'builtin_module_names', 'byteorder',
       'call_tracing', 'callstats', 'copyright', 'displayhook',
       'dont_write_bytecode', 'exc_info', 'excepthook', 'exec_prefix',
       'executable', 'exit', 'flags', 'float_info', 'float_repr_style',
       'getcheckinterval', 'getdefaultencoding', 'getdlopenflags',
       'getfilesystemencoding', 'getobjects', 'getprofile', 'getrecursionlimit',
       'getrefcount', 'getsizeof', 'getswitchinterval', 'gettotalrefcount',
       'gettrace', 'hash_info', 'hexversion', 'implementation', 'int_info',
       'intern', 'maxsize', 'maxunicode', 'meta_path', 'modules', 'path',
       'path_hooks', 'path_importer_cache', 'platform', 'prefix', 'ps1',
       'setcheckinterval', 'setdlopenflags', 'setprofile', 'setrecursionlimit',
       'setswitchinterval', 'settrace', 'stderr', 'stdin', 'stdout',
       'thread_info', 'version', 'version_info', 'warnoptions']
      ```

      Without arguments, dir() lists the names you have defined currently:
      ```
      >>> a = [1, 2, 3, 4, 5]
      >>> import fibo
      >>> fib = fibo.fib
      >>> dir()
      ['__builtins__', '__name__', 'a', 'fib', 'fibo', 'sys']
      ```

      If you want a list of built-in functions and variables, use builtins:
      ```
      >>> import builtins
      >>> dir(builtins)  
      ['ArithmeticError', 'AssertionError', 'AttributeError', 'BaseException',
       'BlockingIOError', 'BrokenPipeError', 'BufferError', 'BytesWarning',
       'ChildProcessError', 'ConnectionAbortedError', 'ConnectionError',
       'ConnectionRefusedError', 'ConnectionResetError', 'DeprecationWarning',
       'EOFError', 'Ellipsis', 'EnvironmentError', 'Exception', 'False',
       'FileExistsError', 'FileNotFoundError', 'FloatingPointError',
       'FutureWarning', 'GeneratorExit', 'IOError', 'ImportError',
       'ImportWarning', 'IndentationError', 'IndexError', 'InterruptedError',
       'IsADirectoryError', 'KeyError', 'KeyboardInterrupt', 'LookupError',
       'MemoryError', 'NameError', 'None', 'NotADirectoryError', 'NotImplemented',
       'NotImplementedError', 'OSError', 'OverflowError',
       'PendingDeprecationWarning', 'PermissionError', 'ProcessLookupError',
       'ReferenceError', 'ResourceWarning', 'RuntimeError', 'RuntimeWarning',
       'StopIteration', 'SyntaxError', 'SyntaxWarning', 'SystemError',
       'SystemExit', 'TabError', 'TimeoutError', 'True', 'TypeError',
       'UnboundLocalError', 'UnicodeDecodeError', 'UnicodeEncodeError',
       'UnicodeError', 'UnicodeTranslateError', 'UnicodeWarning', 'UserWarning',
       'ValueError', 'Warning', 'ZeroDivisionError', '_', '__build_class__',
       '__debug__', '__doc__', '__import__', '__name__', '__package__', 'abs',
       'all', 'any', 'ascii', 'bin', 'bool', 'bytearray', 'bytes', 'callable',
       'chr', 'classmethod', 'compile', 'complex', 'copyright', 'credits',
       'delattr', 'dict', 'dir', 'divmod', 'enumerate', 'eval', 'exec', 'exit',
       'filter', 'float', 'format', 'frozenset', 'getattr', 'globals', 'hasattr',
       'hash', 'help', 'hex', 'id', 'input', 'int', 'isinstance', 'issubclass',
       'iter', 'len', 'license', 'list', 'locals', 'map', 'max', 'memoryview',
       'min', 'next', 'object', 'oct', 'open', 'ord', 'pow', 'print', 'property',
       'quit', 'range', 'repr', 'reversed', 'round', 'set', 'setattr', 'slice',
       'sorted', 'staticmethod', 'str', 'sum', 'super', 'tuple', 'type', 'vars',
       'zip']
      ```

### Packages

Collection of modules : Structuring Python's module namespace by using "dotted module names"

ex) `A.B` : In a package `A`, a submodule `B`

ex) Handling sound files and sound data:

   Should consider:

   - Modules for conversion between sound file formats (`.wav`, `.aiff`, `.au`...)

   - Modules to perform various operations (mixing, adding echo, applying an equalizer function, creating an artificial stereo effect...)

   Possible structure for your package (expressed in terms of a hierarchical filesystem):

   ```
      sound/                          Top-level package
            __init__.py               Initialize the sound package. To make Python treat the directories as containing packages
            formats/                  Subpackage for file format conversions
                    __init__.py
                    wavread.py
                    wavwrite.py
                    aiffread.py
                    aiffwrite.py
                    auread.py
                    auwrite.py
                    ...
            effects/                  Subpackage for sound effects
                    __init__.py
                    echo.py
                    surround.py
                    reverse.py
                    ...
            filters/                  Subpackage for filters
                    __init__.py
                    equalizer.py
                    vocoder.py
                    karaoke.py
                    ...
   ```

   - To import individual modules from the package

      ```
      import sound.effects.echo
      ```

      ```
      sound.effects.echo.echofilter(input, output, delay=0.7, atten=4)
      ```
   
   - Or you can import the submodule

      ```
      from sound.effects import echo
      ```

      ```
      echo.echofilter(input, output, delay=0.7, atten=4)
      ```

   - Or import the desired function or variable directly:

      ```
      from sound.effects.echo import echofilter
      ```

      ```
      echofilter(input, output, delay=0.7, atten=4)
      ```

   - Importing \* From a Package
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
