# 1. Getting Your Appetite 

## Why Python 

1. an interpreted language; save your time during program development 
2. the high-level data types allow you to express complex operations in a single statement;
3. statement grouping is done by indentation instead of beginning and ending brackets;
4. no variable or argument declarations are necessary.

# 2.  Numbers



| notation | function                     |
| -------- | ---------------------------- |
| +        | addition                     |
| -        | subtraction                  |
| *        | multiplication               |
| /        | division (return float)      |
| //       | floor division               |
| %        | modulation (return reminder) |
| **       | power                        |
| ()       | parentheses                  |
| =        | assignment                   |

# 3. Control Flow 

## 1. if 

```python
if x < 0:
    print('Negative changed to zero')
elif x == 0:
    print('Zero')
elif x == 1:
    print('Single')
else:
    print('More')
```

There can be zero or more [`elif`](https://docs.python.org/3/reference/compound_stmts.html#elif) parts, and the [`else`](https://docs.python.org/3/reference/compound_stmts.html#else) part is optional. 

The keyword ‘`elif`’ is short for ‘else if’, and is useful to avoid excessive indentation. 

An  `if` … `elif` … `elif` … sequence is a substitute for the `switch` or `case` statements found in other languages.

## 2. For

```python
words = ['cat', 'window', 'defenestrate']
for w in words:
    print(w, len(w))
```

Python’s `for` statement iterates over the items of any sequence (a list or a string), in the order that they appear in the sequence.

```python
for w in words[:]:  # Loop over a slice copy of the entire list.
    if len(w) > 6:
        words.insert(0, w)

```

If you need to modify the sequence you are iterating over while inside the loop (for example to duplicate selected items), it is recommended that you first make a copy. 

## 3. looping technique

### range ()

```python
range(5, 10)
#5, 6, 7, 8, 9
range(0, 10, 3)
#0, 3, 6, 9
range(-10, -100, -30)
#-10, -40, -70
```

Range() is an object which returns the successive items of the desired sequence when you iterate over it, but it doesn’t really make the list, thus saving space. 

Range() is an object which is *iterable*, that is, suitable as a target for functions and constructs that expect something from which they can obtain successive items until the supply is exhausted.

for is iterator and list() is another one

### range() and len()

```python
a = ['Mary', 'had', 'a', 'little', 'lamb']
for i in range(len(a)):
    print(i, a[i])
```

### break

breaks out of the innermost enclosing[`for`](https://docs.python.org/3/reference/compound_stmts.html#for) or [`while`](https://docs.python.org/3/reference/compound_stmts.html#while) loop.

### else on loops

```python
for n in range(2, 10):
    for x in range(2, n):
        if n % x == 0:
            print(n, 'equals', x, '*', n//x)
            break
    else:
        # loop fell through without finding a factor
        print(n, 'is a prime number')
#2 is a prime number
#3 is a prime number
#4 equals 2 * 2
#5 is a prime number
#6 equals 2 * 3
#7 is a prime number
#8 equals 2 * 4
#9 equals 3 * 3
```

you can have an else clauses for while and for loop 

it is executed when the loop terminates through exhaustion of the list (with [`for`](https://docs.python.org/3/reference/compound_stmts.html#for)) or when the condition becomes false (with [`while`](https://docs.python.org/3/reference/compound_stmts.html#while)), but not when the loop is terminated by a [`break`](https://docs.python.org/3/reference/simple_stmts.html#break) statement.

## 4. If condition 

|         |                        |
| ------- | ---------------------- |
| None    | If x is None           |
| Ternary | x = 0 if y == z else 8 |
|         |                        |

5. string methods

## string

| name    | function                          | usage                            |
| ------- | --------------------------------- | -------------------------------- |
| split   | split string into two             | local, domain = email.split('@') |
| replace | replace a substr with another one | local.replace('.','')            |
| index   | get the index of substr in a str  | email.index('@')                 |
| join    | join strs                         | '.'.join(list)                   |
| lower   | get the lower case                |                                  |
| ord     | get the ascii value from letter   |                                  |
| chr     | get letter from ascii value       |                                  |

define variable and then do add, not directly add 

https://stackoverflow.com/questions/44957261/translating-formatted-strings-in-django-not-working

