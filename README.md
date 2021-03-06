# spam

[![Travis status](https://api.travis-ci.com/jalan/spam.svg?branch=master)](https://travis-ci.com/jalan/spam)
[![Coveralls status](https://coveralls.io/repos/github/jalan/spam/badge.svg?branch=master)](https://coveralls.io/github/jalan/spam)
[![Codecov status](https://codecov.io/gh/jalan/spam/branch/master/graph/badge.svg)](https://codecov.io/gh/jalan/spam)

An example Python C extension module, based on
[the fantastic official documentation](https://docs.python.org/3/extending/).
The module itself doesn't do anything useful, but serves as a demonstration of

 - Python 2 and 3 support
 - some functions
 - an exception type
 - tests
 - continuous integration via [Travis](https://travis-ci.com)
 - code coverage via both [Coveralls](https://coveralls.io) and
   [Codecov](https://codecov.io)

Consider it a starting point for building a new extension module.


## Building

First you need a C compiler and the Python development libraries. Then:

```
python setup.py build
```


## Testing

Just run the tests:

```
python setup.py test
```

Or check the coverage with
[gcov](https://gcc.gnu.org/onlinedocs/gcc/Gcov.html):

```
export CFLAGS=--coverage
python setup.py test
find . -name '*.gcno' -exec gcov {} +
less *.gcov
```


## Using

You really shouldn't use this, but I guess you could.

```
>>> import spam
>>> help(spam)

NAME
    spam - An example Python C extension module.

CLASSES
    class Error(exceptions.Exception)

FUNCTIONS
    check_system(...)
        Execute a system command.

        If the command cannot be executed or returns a non-zero exit status,
	raise Error.

    system(...)
        Execute a system command and return its exit status.

        If the command cannot be executed, return -1.

>>> status = spam.system("echo why would you use this?")
why would you use this?
>>> status
0
>>> spam.check_system("seriously")
sh: seriously: command not found
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
spam.Error: Command returned non-zero exit status 127
```
