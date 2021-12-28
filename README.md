# Harulang

Harulang is a simple scripting language for visual novels.

## Minimum example

```
config
  let resource-directory =  "/resources"
end config
character reimu
  let name = "Reimu Hakurei"
  let img = "/img/reimu"
end character
character marisa
  let name = "Marisa Kirisame"
  let img = "/img/marisa"
end character
global
  let san = 6
end global
scene main
  show background "/img/hakurei-shrine.jpg"
  show reimu at left
  show marisa at right
  marisa happy "This is a line spoken by Marisa"
  reimu happy "This is a line spoken by Reimu"
  for i = 0 to 10
    aside "This is a for loop, now i = ${i}"
  end for
  select
    choice "Choice 1"
      let san = san - 1
    end choice
    choice "Choice 2"
      let san = san + 1
      jump scene1_1
    end choice
  end select
  if san < 6
    aside "Your san is less than 6"
  end if
end scene
```

## Syntax

### Building blocks
#### Reserved words
These words have syntatic meaning and cannot be used as identifiers.

#### Identifiers
Identifiers begin with an underscore `_` or a latin letter, and may contain only
numbers, letters, and underscores. Identifiers cannot be reserved words.

For example: `Hey __gcd getElementById1` are valid identifiers, `1AA a12-34 let`
are not.
#### Assignments
An assignment is defined as follows
```bnf
<assignment> ::= "let" <identifier> "=" <expressions>
```

For example:
```
let a = 10
let b = "A string"
```

Harulang does not have a dedicated variable definition structure, a variable becomes
"defined" when it is first assigned a value. Harulang is dynamically typed -
variables do not hold types, only values, thus the following line is valid:

```
let a = 10
let a = "10"
```

If you attempt to use a variable without defining it first, it defaults to integer
literal `0`.

#### Expressions
Expressions in Harulang are similar to that in most programming languages.

Here are some distinctions that may need notice:

+ Exponetion operator is `^`, integer division operator is `\`
+ Bit manipulation is not required
+ To test for equality, use `==` or `===`. In `==` type casting is done
(see appendix for notes on type casting), while `===` tests for strict equality.
+ To test for inequality, the `<>` operator (instead of `!=`) is used. This design
idea came from Visual Basic.
+ The logical opertors are `and or not xor`, as in Python.

#### Literals

String literals are enclosed in double quotes.

In string literals, variables may be substituted with the `${var}` syntax, for example:

```
let a = 10
aside "Variable a is set to ${a}"
```

Number literals may be written in `aEb` notation, where a is a floating point and
b is an integer.


### Program structure

The program contains four parts: config, character, global and scene. They may be
omitted but must appear in this order.

#### config
Config items go into the `config ... end config` block, and is a list of assignments.

Configuration items *themselves* are implementation-defined and will not be
documented here.

#### character
Character definition go into the `character ... end character` block, and is a list of assignments.

Character configuration items *themselves* are implementation-defined and will not be
documented here.

#### global
Global variables go into the `global ... end global` block, and is a list of assignments.

#### scene

Scenes are a collection of instructions. Instructions may themselves be blocks
(namely, `if ... elseif ... else ... end if` blocks, `for ... end for` blocks,
and `while ... end while` blocks)

If an instruction does not begin with a reserved word, it is treated as a line of
the character and must be followed by a string literal containing the line to be spoken.

The following documents special instructions that begin with reserved words.
