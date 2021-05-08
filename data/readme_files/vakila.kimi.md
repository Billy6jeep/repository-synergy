# Kimi
A lispy toy programming language that keeps it minimal, interpreted in Python 3.

Made by [Anjana Vakil](https://github.com/vakila) at the [Recurse Center](https://www.recurse.com).

### Why did I build Kimi?
A few weeks into my batch at the [Recurse Center](https://www.recurse.com), resident [Prabhakar Ragde](https://cs.uwaterloo.ca/~plragde/) gave a talk called "Small, Elegant, Practical: The benefits of a minimal approach", in which he laid out a minimal set of features (see below) for a small, elegant programming language. It was interesting to know that a programming language doesn't in principle need to have a huge set of features, like most of the major languages do.

I didn't know much about how programming languages are created before coming to RC, and although I had a vague sense of what interpreters/compilers do, I didn't really know what was going on under the hood. So, with some inspiration from Prabhakar's talk, and some encouragement from RC facilitator [John Workman](http://workmajj.com/), I decided to write a little interpreter for such a minimal language myself.

### How did I build Kimi?
In crafting the language, I tried to stick as closely as possible to the set of features that a minimal, elegant language should have, as laid out by Prabhakar:
* `lambda` expressions
* Some useful built-in functions (e.g. arithmetic)
* Function application
* Variable definition
* Conditional evaluation
* Lists

To write the interpreter, I loosely followed two tutorials:
* the [Programming language project](http://eloquentjavascript.net/11_language.html) outlined by another RC resident, [Marijn Haverbeke](http://marijnhaverbeke.nl/), in his excellent and fun book [Eloquent Javascript](http://eloquentjavascript.net). Marijn himself also provided invaluable assistance by pair-programming with me on some components of the interpreter.
* [Peter Norvig]()'s tutorial [(How to Write a (Lisp) Interpreter (in Python))](http://norvig.com/lispy.html).


---
# The Kimi language

## An example program
In `samples/sample.kimi`:
~~~
(do
    (define x 3)
    (define y 4)
    (+ x y)
)
~~~
Running the program :
~~~
$ python3 kimi.py samples/sample.kimi
7
~~~


*See the `samples` directory for more examples!*


## Basics
* **Parentheses** are used to signal function calls, just like other lispy languages. Parentheses are not used for grouping, or any other purpose. An opening parenthesis must be immediately followed by a function (i.e. a builtin, the name of a `define`d function, or a `lambda` expression). For example, `(+ 1 2)` is a valid Kimi program; `( + 1 2 )`, `(((+ 1 2)))`, and `(+ (1) (2))` are not.
* **Numbers** are limited to integers (e.g. `1`, `-439`). Kimi assumes that anything that *can* be interpreted as an integer *is* an integer; for example, `2` and `+2` become `2`, and `-2` becomes `-2`. A number containing a decimal point (e.g. `2.5`) will *not* be considered an integer, but a **symbol** (see below).
* **Strings** must be wrapped in double quotes (e.g. `"my string"`). Kimi assumes anything surrounded by double quotes is a string. Escaped double quotes are not supported, but single quotes can be used (e.g. `"my \"quote\" string"` is not a valid string, but `"my 'quote' string"` is).
* **Booleans** are `true` and `false` (based on Python's `True` and `False`).
* Anything in your program that is not one of the above is considered a **symbol**.

## Defining names
* Names can be assigned like so: `(define x 5)`.
* Any symbol (see above) is a valid name, as long as it does not already exist in the given environment. For example, `x`, `123abc123`, and `--thing--` are valid names, but `define`, `-`, `nil`, and `first` are not, since they already exist as built-in functions (see below).
* Just because something *can* be used as a name doesn't mean it *should*; for example `2.5` and `-2-4` are valid names (see above), but not very good ones!

## Conditionals
* Conditional statements are written in the form `(if <test> <pass_case> <fail_case>)`.
* The first argument (the test) must be an expression that evaluates to a boolean.
* If the test evaluates to `true`, the second argument will be evaluated. If not, the third argument will be evaluated.
* For example: `(if true 1 2) => 1`, `(if false 1 2) => 2`.

## Lambda expressions
* Lambda expressions can be used to create anonymous functions. For example, `(lambda x (* x x))` evaluates to a function that takes one (integer) argument and returns its square.
* Lambdas are written in the form `(lambda args... body)`, where `args...` stands for one or more arguments and `body` stands for an expression that will evaluate to a function application.

## Lists
* All non-empty lists are built up from `nil`, Kimi's equivalent to Python's `None`. In other words, all lists contain `nil` as the last element. An empty list is represented as simply `nil`.
* Non-empty lists are written as `(list 1 2 3)`. Internally, they are represented as nested tuples of pairs of values, where the innermost tuple contains `nil` as its second value. For example, Kimi interprets `(list 1 2 3)` as `(1, (2, (3, nil)))`.
* `prepend` adds an argument to the front of a list, and `list` is essentially a shorthand for multiple `prepend` calls: `(list 1) = (prepend 1 nil) => (1, nil)`, `(list 1 2) = (prepend 1 (prepend 2 nil)) => (1, (2, nil))`
* `first` returns the first item in the list: `(first (list 1 2)) => 1`
* `rest` allow you to access the remainder of the list, i.e. the second item of the tuple: `(rest (list 1 2)) => (2, nil)`

## Using `do`
* To imperatively execute several commands one after the other, wrap them in `(do ...)`. Kimi will evaluate each expression in turn, and return the result of the last expression evaluated. For example, the following programs both give `7`:

    ~~~
    (do (define x 3) (define y 4) (+ x y))
    ~~~
    
    ~~~
    (do (+ 1 2) (+ 3 4))
    ~~~
* Each `do` block has its own scope; names defined in one `do` block are not accessible from parent or sibling blocks. For example, the following programs will throw errors when trying to access `x`:
    
    ~~~
    (do
        (do (define x 3))
        (+ 1 x)
    )
    ~~~

    ~~~
    (do
        (do (define x 3))
        (do (define y 4) (+ x y))
    )
    ~~~
* Kimi does not know how to imperatively evaluate multiple expressions if they are not wrapped in a `do` block. In this case, Kimi will evaluate the first command it finds and ignore the rest. For example, we saw above that this program evaluates to `7`:

    ~~~
    (do (+ 1 2) (+ 3 4))
    ~~~
    
    But this program evaluates to `3`:
    
    ~~~
    (+ 1 2) (+ 3 4)
    ~~~

## Built-in functions
* Arithmetic:
    * `+` (addition): `(+ 1 2) => 3`
    * `-` (subtraction): `(- 2 1) => 1`
    * `*` (multiplication): `(* 2 4) => 8`
    * `/` (floor division, as we have only integers): `(/ 6 2) => 3`, `(/ 7 2) => 3`
    * `%` (modulo): `(% 7 2) => 1`
    * *These functions take only integer arguments*
* Logic:
    * `!` (not): `(! true) => False`, `(! false) => True`
    * `&` (and): `(& true true) => True`, `(& true false) => False`
    * `|` (inclusive or): `(| true false) => True`, `(| false false) => False`
    * *These functions take only boolean arguments*
* Equality:
    * `=`: `(= 1 1) => True`, `(= "yes" "yes") => True`, `(= true false) = False`
    * *This function takes integer, string, or boolean arguments; arguments must be of the same type*
    * Test for inequality using a combination of `!` and `=`, e.g. `(! (= 1 2)) => True`
* Comparison:
    * `>` (greater than): `(> 2 1) => True`
    * `<` (less than): `(< 1 2) = True`
    * `>=` (greater than or equal to): `(>= 2 2) => True`
    * `<=` (less than or equal to): `(<= 3 2) = False`
    * *These functions take only integer arguments*

---
# Using Kimi

## Running Kimi code
You have three options for playing with Kimi code:

1. Interact with the Kimi interpreter (REPL):

        $ kimi
        Welcome to Kimi!
        See the README (https://github.com/vakila/kimi) for information about Kimi.
        To exit the interpreter, type "exit" or "quit" or "q".
        kimi> ...

2. Run a program from a `.kimi` file:

        $ kimi my_program.kimi
        ...

3. Type a program as a string on the command line (only recommended for simple programs):

        $ kimi "(+ 1 2)"
        3

Note: to run the command `kimi`, you'll need to add the path to the `kimi/` directory to your `PATH`, e.g. add these lines to `~/.profile`:

    PATH="/path/to/kimi:${PATH}"
    export PATH

But if you don't add `kimi` to your `PATH`, you can still run the commands above one of two ways:

    $ ./kimi
    $ python3 kimi


## Running tests
Using unittest (recommended):

    $ python3 tests.py

Using doctest (deprecated):

    $ python3 -m doctest -v kimi.py

---
