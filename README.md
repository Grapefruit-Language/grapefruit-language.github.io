<div align="center">
  <img src="https://i.imgur.com/qJ4n8Sq.png" alt="Grapefruit logo">
</div>

# The Grapefruit Programming Language

## :hammer_and_wrench: Status

⏳ Currently a work in progress.

- [ ] Draft specification.
- [ ] Sample programs.
- [ ] Interpreter implementation.
- [ ] VSCode plugins.
- [ ] Transpiler implementation.

## 📖 Description

> **Grapefruit** is an easy-to-learn programming language that is meant to be _runnable pseudocode_. It reads like English but almost all basic data structures and algorithms can be implemented in this langauge.

It does not aim to be the fastest, or the best langauge (there isn't such a thing). It is meant to help people understand algorithms, and reduce the barrier of entry for new programmers.

Grapefruit does not attempt to protect you from the underlying complexity (although it does support abstractions). Instead, it is like a readable version of C, minus the memory management.

If you want to do the memory management yourself, you can certainly do that. Grapefruit will transpile into C (at least) with no _compiler magic_ ✨. You can dig into the code and tweak stuff as much as you want.

## Philosophy

1. Grapefruit allows you to prototype quickly and debug your code using the interpreter.

2. When you are confident about your Grapefruit program, transpile it into a language like C and then continue to refine and tweak the generated source to meet your performance target, space limit, and other goals.

## Examples

### Hello, World! 👋

```grapefruit
function main
{
  display("Hello, world! Grapefruit works.")
}
```

### Arithmetic

```grapefruit
function main
{
  a is 10
  b is 20
  sum is a + b
  display("The sum of `a` and `b` is `sum`")
}
```

### Palindrome

```grapefruit
use [reversed, trimmed] from string_functions

function main
{
  assume user_input is a string and mutable

  user_input is get_token()

  loop if user_input != Nothing
  {
    user_input is trimmed(user_input)

    if user_input = reversed(user_input)
    {
      display("`user_input` is a palindrome!")
    }
    else
    {
      display("`user_input` is NOT a palindrome.")
    }

    user_input is get_token()
  }
}
```

### Armstrong Number

```grapefruit
use pow from math_functions

function digit_count on num (unsigned) returns unsigned
{
  digits is 0 and mutable
  copy is num and mutable

  loop if copy > 0
  {
    digits is digits + 1
    copy is copy / 10
  }

  return digits
}

function get_digits_of takes [num (unsigned)] returns array(unsigned)
{
  digits is array(unsigned, num.digit_count) and mutable
  copy is num and mutable

  loop over index from digits.size - 1 to 0 with step -1
  {
    current_digit is copy mod 10
    copy is copy / 10
    digits at index is current_digit
  }

  return digits
}

function is_armstrong on num (integer) returns boolean
{
  digit_sum is 0 and mutable
  exponent is num_length
  digits is get_digits_of(num)

  loop over digit in digits
  {
    digit_sum is digit_sum + pow(digit, exponent)
    exponent is exponent - 1
  }

  return digit_sum = num
}

function main
{
  num is 153
  if num.is_armstrong
  {
    display("`num` is an Armstrong number!")
  }
  else
  {
    display("`num` is NOT an Armstrong number.")
  }
}
```

## Features

1. Resembles English in readability.
2. Can be both interpreted and transpiled.
3. The tools do not perform any source code optimisation. Do it yourself or rely on the transpiler target language's compiler.
4. Strictly-typed. Type inference shortens the code but a variable can only have one type.
5. Variables are immutable by default. Use the `and mutable` phrase to mark them as mutable.
6. Single-threaded only. Multi-threading can be addded to the transpiled source code. For example, one can use OpenMP or pthreads for C code.

## Installation Instructions

_Currently a work in progress._

## Contact Us

You can contact us through:

1. Twitter DM ([@grapefruit_lang](https://twitter.com/grapefruit_lang))
2. Email (info@grapefruit-lang.com)

## Contribution Guidelines

Right now, external code contributions are not accepted. You may, however, contact us regarding suggestions, questions, and other related topics.

Contributions will be accepted after the "ecosystem" has an MVP and is stable enough for demonstration.

## Inspiration and Alternatives

### Python

Python is one of the most popular programming in the world. It is easy to read and quick to write. However, it is not strictly-typed. Grapefruit aims to be simple to read and write programs in while preventing implementation lock-in.

Bindings are immutable by default. They can be made mutable using the `and mutable` phrase. This idea is not new. It is borrowed from Rust, Haskell, OCaml, V, and several others.
