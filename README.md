<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!--~~~~~~~~~~~~~~~~~~~~~~ readme.md of JS-Practical-Intro-to-JavaScript ~~~~~~~~~~~~~~~~~~~~~~~-->
<h1 id="#js-heading">JS - Practical Intro to Modern JavaScript</h1>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="#comments">Comments</h2>
<ul>
  <li>Everything between /* and */ is ignored by the interpreter.</li>
  <li>Everything after // on the same line is ignored by the interpreter.</li>
</ul>
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->

<h2 id="#data-types">Data Types</h2>
<h3>6 primitive types</h3>

<ol type="i">
  <li><b><mark>boolean</mark></b> (true or false)</li>
  <li><b><mark>number</mark></b> (including integers like 1, -2, and floating point numbers like 1.1, 2e-3)</li>
  <li><b><mark>string</mark></b> ( '' or "", 'ES6 in Practice' or "ES6 in Practice" )</li>
  <li><b><mark>null type</mark></b> (denoted by null)</li>
  <li><b><mark>undefined</mark></b> (denoted by undefined)</li>
  <li><b><mark>Symbol</mark></b> (don’t worry about them yet)</li>
</ol>

<h3>Some important operators are:</h3>
<ul>
  <li><b><mark>+ (plus)</mark></b> stands for addition. Example: 2 + 3 is 5.</li>
  <li><b><mark>- (minus)</mark></b> stands for subtraction. Example: 2 - 3 is -1.</li>
  <li><b><mark>* (asterisk)</mark></b> stands for multiplication. Example: 3 * 2 is 6.</li>
  <li><b><mark>/ (divisor)</mark></b> stands for division. Example: 3 / 2 is 1.5.</li>
  <li><b><mark>% (percent)</mark></b> stands for the modulus operation, which is the 
    remainder of a number divided by another
    number using the rules of integer division. Example: 5 % 2 is 1, because 5 divided by 2 is 2,
    and the remainder is 1. In other words, the mod 2 remainder of 5 is 1.</li>
  <li><b><mark>** (double asterisk)</mark></b> is the power operator. Example: 2 ** 3 
    (two to the power of three) is 2 * 2 * 2, which is 8.</li>
</ul>

<p><b>Note:</b> If there is no operand on the left of + or -, then + or - becomes a sign. Examples: +3 or -2.</p>

```
1 + +"2" // +"2" gives a sign to "2", converting it to a number
3
1 + Number("2")
3
1 + Number.parseInt( "2", 10 )
3
1 + Number.parseInt( "2" )
3
```

<p>All conversions work. The first relies on giving a sign to a numeric string which converts it to a
number. Then 1+2 becomes 3. The second type cast is more explicit: you use Number to wrap a string
and convert it to a number.</p>

<p>I recommend using the third option: <mark>Number.parseInt</mark> with a radix. <mark>parseInt</mark> 
converts a string into a number. The second argument of parseInt is optional: it describes 
the base in which we represent the number. Most of the time, we use base 10 values.</p>

```
Number.parseInt("ES6 in Practice")
NaN
Number.parseInt( "10", 2 )
2
Number.parseInt( "a" )
NaN
Number.parseInt( "a", 16 )
10
```

<p>Strings that do not start with a number are often <mark>NaN</mark>. "10" in base 2 is 2. The character "a" is not
interpreted in base 10, its value is <mark>NaN</mark>. The same "a" character in base 16 is 10.</p>

<p>Hexadecimal numbers are base 16 numbers. Hexa means 6, and decimal means 10. Ten plus six
equals sixteen, hence the hexadecimal name. The digits of hexadecimal numbers are 0123456789abcdef.
The last six digits can also be in upper case yielding ABCDEF.</p>

<p><mark>Number.parseInt</mark> recognizes the starting characters of a string as integer numbers, and throws away
the rest:</p>

```
Number.parseInt( "1234.567 89" )
1234
```

<p>The <mark>dot</mark> is not a character present in integer numbers, so everything after 
1234 is thrown away by <mark>Number.parseInt</mark>.</p>

<p>You can also use <mark>Number.parseFloat</mark> to parse floating point. It parses the 
floating point number until the terminating space:</p>

```
Number.parseFloat( "1234.567 89" )
1234.567
```

<!-- page 29 -->
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<h2 id="#boolean">The boolean type</h2>
<p>Let’s see some booleans values. Booleans are either true or false.</p>
<p>The <mark>! (exclamation)</mark> operator symbolizes negation. <mark>!true</mark> 
becomes false, while <mark>!false</mark> becomes true.</p>

```
!true
false
!false
true
```

<p>An arbitrary value can be converted to boolean using the Boolean function:</p>

```
Boolean(0)
false
Boolean(1)
true
Boolean(2)
true
Boolean(null)
false
```

<p>The <mark>!operator</mark> not only negates a value, but also converts it to a boolean. 
For instance, the negation of a string can be described as follows:</p>

<ul>
  <li>the <mark>empty string ("")</mark> is evaluated as false by default in a boolean 
    expression. Negating this value yields true.</li>
  <li>An arbitrary at least one character long string is evaluated as true in a boolean 
    expression. Negating this value yields false.</li>
</ul>

```
!""
true
!" "
false
```

In JavaScript, we differentiate between truthy and falsy values. These values are not necessarily
booleans. Their value only becomes true or false after a type conversion.

A truthy value is a value v for which Boolean(v) is true. Example truthy values are:
nonzero integers, strings containing at least one character. A falsy value is a value w for
which Boolean(w) is false. Example falsy values are: empty string, 0, null, undefined.

Question: Why do we need type conversion using the Boolean function?

Answer: Because otherwise automatic type conversion would produce unintended results. For
instance, in the expression 2 == true, both sides of the comparison are converted to numbers.
As the value of Number(true) is 1, the 2 == 1 expression is evaluated to false:

```
2 == true ---> 2 == Number(true) ---> 2 == 1 ---> false

2 == false ---> 2 == Number(false) ---> 2 == 0 ---> false
```

Furthermore, null and undefined are neither true, nor false:

```
null == true
false

null == false
false

undefined == true
false

undefined == false
false
```

However,
    • Boolean( null ) and Boolean( undefined ) are both false
    • !null and !undefined are both true
    • !!null and !!undefined are both false


Similarly to the Boolean function, double negation also converts an arbitrary value into boolean:
    • if v is truthy, then !v is false, and !!v is true
    • if w is falsy, then !w is true, and !!w is false

Examples:

```
!!""
false

!!"a"
true

!!0
false

!!1
true

!!NaN
false

!!Infinity
true

!!null
false

!!undefined
false
```

Once you start writing complex software, use the Boolean function instead of double negation to
convert values to booleans. This way, your code becomes more readable.

We can compare two numbers with >, >=, ==, ===, <=, <. We will discuss the difference between ==
and === soon. For the rest of the operators, the result of the comparison is a boolean.

```
5 <= 5
true

5 < 5
false

!(5 < 5) // ! stands for negation. !true = false, !false = true.
true
```

The = symbol is not used for comparison. It is used for assigning a value to a variable (see later).
For values a and b, a == b is true if and only if both a and b can be converted to the same value via
type casting rules. This includes:

    • null == undefined is true
    • If an operand is a string and the other operand is a number, the string is converted to a number
    • If an operand is a number and the other operand is a boolean, the boolean is converted to a
    number as follows: true becomes 1, and false becomes 0.

Don’t worry about the exact definition, you will get used to it.

For values a and b, a === b is true if and only if a == b and both a and b have the same types.

```
5 == '5' // '5' is converted to 5
true

5 === '5' // types have to be the same
false

0 == '' // '' is converted to 0
true

0 === '' // types have to be the same
false

NaN == NaN // I know... just accept this as something odd and funny
false
```

The negation of == is !=. Read it as is not equal to. For instance, !(a == b) becomes a != b. It is
time mentioning that you are free to use parentheses to group your values and override the default
priority of the operators.
The negation of === is !==.

```
5 != '5'
false

5 !== '5'
true
```

```
0.1 + 0.2
0.30000000000000004

3.1e-3
0.0031
```

Some more info on floating points. Due to the way how numbers are represented, 0.1 + 0.2 is not
exactly 0.3. This is normal and occurs in most programming languages.

3.1e-3 is the normal form of 0.0031. Read it like the exact value of 3.1 times ten to the power of
minus three. Although the form is similar to 3.1 * (10 ** -3), there are subtle differences. 3.1e-3
describes the exact value of 0.0031. 3.1 * (10 ** -3) describes a composite expression that needs
to be calculated:

```
3.1 * (10 ** -3)
0.0031000000000000003
```

Floating point arithmetics does not even make this expression exact.

If you need precise values, you have two options: one is rounding or truncating the result, and the
other is to convert the floating point operands to integer numbers. For instance, instead of 0.25
dollars, you can write 25 cents. This works when you always expect the same number of precision
after the decimal point.

Let’s see an example for rounding:

<!-- page 18 -->
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Data types in JavaScript

Most programming languages help you create values that symbolize a number, a character in a text,
or a longer text. You can also symbolize the concept of true and false values using booleans. You can
also create values that symbolize the absence of a value. These values are all called primitive data
types.

The name primitive does not come from a negative place. These data types are neither stupid, nor
inferior to any other data types we use in JavaScript. The name primitive comes from their simplicity.
The other data types you will learn later are composite, and they consist of many primitive data types.

Why are data types important for us?

For instance, whenever you check your emails, go on Facebook, or check your bank account, you
always see data: your name, your messages, the current date and time, and in the settings, you can
also see other features of your account.

Data have types. We tend to use an integer (whole number, without a fractional part) than text. A
checkbox can have two possible values: true or false. These data types are also unique. For each data
type, different operations apply, and their possible values are also different.

In JavaScript, there are six primitive types:

<!-- page 19 -->

    • boolean (true or false)
    • number (including integers like 1, -2, and floating point numbers like 1.1, 2e-3)
    • string ( '' or "", 'ES6 in Practice' or "ES6 in Practice" )
    • null type (denoted by null)
    • undefined (denoted by undefined)
    • Symbol (don’t worry about them yet)

Floating point numbers typically contain a decimal separator character, most often a dot. The
precision of floating point numbers is limited, because there are a limited number of bits available.

We will soon learn more about anomalies arising from restrictions on floating point precision.

Operations can be performed on data of given types. Operations are denoted by an operator
symbolizing the operation. Examples: +, -, *, /. Operators perform operations on data that are called
the operands of the operation.

For instance, in the 2 * 3 operation, * is the operator symbolizing multiplication. Multiplication has
two operands: 2 and 3.

Some important operators are:

    • + stands for addition. Example: 2 + 3 is 5.
    • - stands for subtraction. Example: 2 - 3 is -1.
    • If there is no operand on the left of + or -, then + or - becomes a sign. Examples: +3 or -2.
    • * stands for multiplication. Example: 3 * 2 is 6.
    • / stands for division. Example: 3 / 2 is 1.5.
    • % stands for the modulus operation, which is the remainder of a number divided by another
    number using the rules of integer division. Example: 5 % 2 is 1, because 5 divided by 2 is 2,
    and the remainder is 1. In other words, the mod 2 remainder of 5 is 1.
    • ** is the power operator. Example: 2 ** 3 (two to the power of three) is 2 * 2 * 2, which is
    8.

At the bottom of the console in CodePen²², there is a line with a > sign. This is where you can enter
JavaScript expressions. Let’s try some. Enter the expression you see after the >
sign. Then press enter. You can see the result appear on the next line.

<!-- page 20 -->

```
5
5

5 + 2
7

7 % 5
2

5 ** 2
25
```

Operations can be grouped together using parentheses. Parentheses override the priority of executing
operations. For instance, in mathematics, multiplication has higher priority than addition. This
means, 1 + 2 * 3 is the same as 1 + (2 * 3).
Let’s see an example for using parentheses:

```
5 * ( 1 + 2 * ( 3 + 4 ) )
// 5 * ( 1 + 2 * 7 )
// 5 * ( 1 + 14 )
// 5 * 15
75
```

Opposed to mathematics, we do not use brackets or braces to group operations. Parentheses can be
used within parentheses. It is also important to construct valid expressions with parentheses, which
means that each closing parenthesis should belong to a preceding opening parenthesis.
Similarly to mathematics, different operators have different priority (also referred to as precedence).
When an operation has to be performed before another operation, we say that this operator:

    • has higher priority,
    • binds stronger.

Most operators have either one or two operands. This means the operator transforms either one or
two values to a new value. Examples:

    • The operands of 5 + 2 are 5 and 2. The + operator transforms these operands to 7.
    • The operand of -(2) is (2). I put parentheses around the 2 to emphasize that - is an operator
    and not a symbol to describe an integer.

Operators bind their operands. We have already seen that some operators bind stronger than others.
For instance, multiplication binds stronger than addition:

<!-- page 21 -->

```
5 * 2 + 3 ----> 10 + 3 ----> 13
```

We have also seen that the priority of operators can be overridden using parentheses:

```
1 5 * (2 + 3) ----> 5 * 5 ----> 25
```

The basic arithmetic operations (+, -, *, /, **) and the two signs (+, -) have the following priority:

    1. Signs: + or - can stand in front of a number. This sign is evaluated first.
    2. Power: ** binds the strongest out of the operators with two operands.
    3. Multiplication and division: * and /
    4. Finally, addition and subtraction: + and -

If you use more complex operations in JavaScript and you are not sure about their priority, use
parentheses. Relying too much on the evaluation priority of operations reduces the readability of
your code, which means others may have a hard time cooperating with you if you tend to give them
riddles.

The modulus operation was not placed in the above priority order, because most of the time, you
won’t need it in a complex expression. In the unlikely case you used it together with other operators,
use parentheses. The % operator binds just as strongly as multiplication and division does. However,
when using % in a complex expression, parentheses increase the readability of your code.

<!-- page 22 -->
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## The number type
Handling numbers is mostly straightforward. You have the four arithmetic operations ( +, -, *, /)
available for addition, subtraction, multiplication, and division respectively.

The % operator is called modulus. a % b returns the remainder of the division a / b. In our example,
7 / 5 is 1, and the remainder is 2. The value 2 is returned.

The ** operator is called the exponential operator. 5 ** 2 is five raised to the second power.

Let’s see some more surprising floating point operations.
<!-- page 23 -->

```
0.1 + 0.2
0.30000000000000004

Number( 0.1 + 0.2 ).toFixed( 1 );
0.3
```

In the above example, the precision of the result is fixed to one decimal point.

The division 0 / 0 or using mismatching types creates a special number called not a number or NaN.
Ironically, we will soon see that the type of the NaN value is number.

```
0 / 0
NaN

'ES6 in Practice' * 2
NaN
```

The latter is interesting to Python users, because in Python, the result would have been 'ES6 in
PracticeES6 in Practice'. JavaScript does not work like that.

There is another interesting numeric value: Infinity.

<!-- page 24 -->

```
1 / 0
Infinity

Infinity * Infinity
Infinity

-1 / 0
-Infinity

1e308
1e+308

1e309
Infinity
```

JavaScript registers very large numbers as infinity. For instance, ten to the power of 309 is represented
as infinity. Division by zero also yields infinity.

Let’s see some strings.

```
'ES6 in ' + 'Practice'
"ES6 in Practice"
```

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Strings and escape sequences
Moving on to string data:

```
1 > 'ES6 in ' + 'Practice'
2 "ES6 in Practice"
```

The plus operator concatenates strings. Concatenation means that you write the contents of two
strings after each other. Concatenation means that you join the values on the left and on the right
of the concatenation operator (+).

A frequent question is, how to write quotes inside a string if quotes represent the boundaries of a
string. In JavaScript, there are multiple solutions:

<!-- page 25 -->

```
// Solution 1:
console.log( '--- "This is a quote" ---' );

// Solution 2:
console.log( "--- 'This is a quote' ---" );

// Solution 3:
console.log( "--- \"This is a quote\" ---" );
```

You can use any number of double quotes inside single quotes, and any number of single quotes
inside double quotes. However, using a single quote inside a string defined using single quote would
mean that we terminate the string. The same holds for using a double quote inside a string defined
using double quotes.

As both single quotes and double quotes are used frequently, the need arises to use both the single
quote and the double quote characters inside a string at any time. We can do this by escaping the
quote using the \ (backslash) character.

The backslash (\) character means that a special character (or characters) is coming. The backslash
and the special character(s) together are called an escape sequence. Escape sequences symbolize
special characters.

Examples for escape sequences:
    • \' and \": single or double quote characters. In JavaScript, escaped quotes do not start or
    terminate a string.
    • \n: newline character. We can put a line break in the string, making the character after \n
    appear on the next line.
    • \\: as the backslash character creates an escape sequence, it is a special character itself and
    has to be escaped. The first backslash tells the JavaScript interpreter that a special character is
    coming. The second backslash says that this character is the backslash. This escape sequence
    is important to keep in mind when describing Windows file paths in JavaScript or node.js:

```
console.log( `c:\\js\\hello.js` )
"c:\js\hello.js"
```

<!-- page 26 -->

```
console.log( `
<p>
  paragraph
</p>
  <ul>
    <li>first list item</li>
    <li>second list item</li>
  </ul>
);
```

The above expression prints the text in-between backticks, including the newline characters. The
usage of template literals is an advanced topic, we will not deal with them in this chapter.

Strings are immutable which means that their value cannot be changed. The word immutable comes
from the fact that strings cannot be mutated. If strings were mutable, we would be able to change
the b character in the 'abc' string without creating a new string. In reality, in order to make an
'aXc' string from an 'abc' string, we need to create a new string from scratch.

Similarly, the result of "a" + "b" is a brand new string: "ab". Even after the result is created, "a"
and "b" stay in memory. This is why strings are immutable in JavaScript.

If any of the operands of plus is an integer, while the other operand is a string, then the result
becomes a string. JavaScript automatically converts the operands of an operator to the same type.
This is called automatic type casting:

<!-- page 27 -->

```
1 + '2'
"12"

'1' + 2
"12"
```

Rules may become confusing, so don’t abuse automatic type casting. Most software developers do
not know these rules by heart, as it generally pays off more to write code that is obvious and
understandable for everyone.

Implicit type conversion happens when the JavaScript interpreter automatically converts a datum
of one type to a datum of another type. Explicit type conversion occurs when the type conversion
is specified in the code.

Examples:

```
1 + +"2" // +"2" gives a sign to "2", converting it to a number
3

1 + Number("2")
3

1 + Number.parseInt( "2", 10 )
3

1 + Number.parseInt( "2" )
3
```

All conversions work. The first relies on giving a sign to a numeric string which converts it to a
number. Then 1+2 becomes 3. The second type cast is more explicit: you use Number to wrap a string
and convert it to a number.

I recommend using the third option: Number.parseInt with a radix. parseInt converts a string into
a number. The second argument of parseInt is optional: it describes the base in which we represent
the number. Most of the time, we use base 10 values.

Let’s see some more Number.parseInt values:
<!-- page 28 -->

```
Number.parseInt("ES6 in Practice")
NaN

Number.parseInt( "10", 2 )
2

Number.parseInt( "a" )
NaN

Number.parseInt( "a", 16 )
10
```

Strings that do not start with a number are often NaN. "10" in base 2 is 2. The character "a" is not
interpreted in base 10, its value is NaN. The same "a" character in base 16 is 10.

Hexadecimal numbers are base 16 numbers. Hexa means 6, and decimal means 10. Ten plus six
equals sixteen, hence the hexadecimal name. The digits of hexadecimal numbers are 0123456789abcdef.
The last six digits can also be in upper case yielding ABCDEF.

Number.parseInt recognizes the starting characters of a string as integer numbers, and throws away
the rest:

```
Number.parseInt( "1234.567 89" )
1234
```

The dot is not a character present in integer numbers, so everything after 1234 is thrown away by
Number.parseInt.
You can also use Number.parseFloat to parse floating point. It parses the floating point number until
the terminating space:

```
Number.parseFloat( "1234.567 89" )
1234.567
```

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!-- page 29 -->
## The boolean type

Let’s see some booleans values. Booleans are either true or false.

The ! operator symbolizes negation. !true becomes false, while !false becomes true.

```
!true
false

!false
true
```

An arbitrary value can be converted to boolean using the Boolean function:

```
Boolean(0)
false

Boolean(1)
true

Boolean(2)
true

Boolean(null)
false
```

<!-- page 30 -->
The !operator not only negates a value, but also converts it to a boolean. For instance, the negation
of a string can be described as follows:

    • the empty string ("") is evaluated as false by default in a boolean expression. Negating this
    value yields true.
    • An arbitrary at least one character long string is evaluated as true in a boolean expression.
    Negating this value yields false.

```
!""
true

!" "
false
```

In JavaScript, we differentiate between truthy and falsy values. These values are not necessarily
booleans. Their value only becomes true or false after a type conversion.

A truthy value is a value v for which Boolean(v) is true. Example truthy values are:
nonzero integers, strings containing at least one character. A falsy value is a value w for
which Boolean(w) is false. Example falsy values are: empty string, 0, null, undefined.

Furthermore, null and undefined are neither true, nor false:

<!-- page 31 -->

```
null == true
false

null == false
false

undefined == true
false

undefined == false
false
```

However,
    • Boolean( null ) and Boolean( undefined ) are both false
    • !null and !undefined are both true
    • !!null and !!undefined are both false

Similarly to the Boolean function, double negation also converts an arbitrary value into boolean:
    • if v is truthy, then !v is false, and !!v is true
    • if w is falsy, then !w is true, and !!w is false

Examples:

```
!!""
false

!!"a"
true

!!0
false

!!1
true

!!NaN
false

!!Infinity
true
 
!!null
false

!!undefined
false
```

<!-- page 32 -->
Once you start writing complex software, use the Boolean function instead of double negation to
convert values to booleans. This way, your code becomes more readable.

We can compare two numbers with >, >=, ==, ===, <=, <. We will discuss the difference between ==
and === soon. For the rest of the operators, the result of the comparison is a boolean.

```
5 <= 5
true

5 < 5
false
 
!(5 < 5) // ! stands for negation. !true = false, !false = true.
true
```

The = symbol is not used for comparison. It is used for assigning a value to a variable (see later).

For values a and b, a == b is true if and only if both a and b can be converted to the same value via
type casting rules. This includes:

    • null == undefined is true
    • If an operand is a string and the other operand is a number, the string is converted to a number
    • If an operand is a number and the other operand is a boolean, the boolean is converted to a
    number as follows: true becomes 1, and false becomes 0.

Don’t worry about the exact definition, you will get used to it.

For values a and b, a === b is true if and only if a == b and both a and b have the same types.

<!-- page 33 -->

```
5 == '5' // '5' is converted to 5
true

5 === '5' // types have to be the same
false

0 == '' // '' is converted to 0
true

0 === '' // types have to be the same
false

NaN == NaN // I know... just accept this as something odd and funny
false
```

The negation of == is !=. Read it as is not equal to. For instance, !(a == b) becomes a != b. It is
time mentioning that you are free to use parentheses to group your values and override the default
priority of the operators.

The negation of === is !==.

```
5 != '5'
false

5 !== '5'
true
```

<!-- page 34 -->
So far, all operators have been unary or binary meaning that they bind one or two values:

    • the expression 5 + 2 has the operands 5 and 2
    • the expression +'2' has the operand '2'

Recall that operators bind their operands. Some operators are said to bind stronger than others. For
instance, multiplication binds stronger than addition:

```
5 * 2 + 2 ----> 10 + 2 ----> 12
```

Also recall that is possible to override the precedence of the operators with parentheses:

```
5 * (2 + 2) ----> 5 * 4 ----> 20
```

There is one ternary operator in JavaScript.

The value of a ? b : c is:

    • b if a is truthy
    • c if a is falsy

It is important to note the difference between 2 == true and !!2.

```
2 == true // true is converted to 1
false

!!2 // 2 is a truthy value
true

2 == true ? 'the condition is true' : 'the condition is false'
"the condition is false"

!!2 ? 'the condition is true' : 'the condition is false'
"the condition is true"
```

I have seen the nastiest bug in my life in a code, where a condition was in a format num == true.
As I never felt like learning boring definitions, my lack of knowledge shot me in the foot, because I
assumed the opposite conversion in 2 == true. I can save you some headache by highlighting this
common misconception. In 2 == true, true is converted to 1, and not the other way around.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
<!-- page 35 -->
## null, undefined, symbol types

Null, undefined, and Symbols are primitive types.

Null represents an intentional absence of a primitive or composite value of a defined variable.

Undefined represents that a value is not defined. We will deal with the difference between null and
undefined later.

A Symbol() is a unique value without an associated literal value. They are useful as unique keys,
because Symbol() == Symbol() is false. Imagine a symbol as a unique key that opens one specific
lock, in a world, where each created key is different from all other keys previously created. At this
stage, just accept that symbols exist. You don’t have to use them for anything yet.

```
null
null

undefined
undefined

void 0
undefined

Symbol('ES6 in Practice')
[object Symbol] {}
```

The value undefined can also be created using the void prefix operator.

Symbols can have a string description. This string description does not have an influence on the
value of the symbol:

```
Symbol('a') == Symbol('a')
false
```

```
// A. Arithmetics
console.log( 2*2+4 );  // 8

// B. Ternary operator
console.log( 3 % 2 ? 'egy' : 'nulla' );  // egy

// C. Not a Number
console.log( (0/0) == NaN );  // false
```

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Variables: let, const, and var // page 36

<!-- page 37 -->

```
console.log( 1, 2, 3 )
1 2 3
```

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
### The let keyword

We can create variables with the let keyword. Think of a variable like a drawer. Let declares a
variable, which means to you that a drawer is created with a handle. Declaration is a process that
creates a drawer, and hands the key of the drawer to us so that we can access its contents.

```
let myDrawer;
```

You can put a value in your drawer:

```
myDrawer = '$1.000';
```

In order to access the value, you have to grab the handle of the drawer and open it. In this example,
you have a drawer called myDrawer. It contains a string written '$1.000' on it. To access your
thousand bucks, you have to open the drawer:

<!-- page 38 -->

```
myDrawer
'$1.000'
```

You can assign an initial value to your variable with the = sign. This is called assignment, because
we assign a value to a variable. The first assignment in the lifecycle of a variable is called definition
or initialization.

The declaration and initialization steps can be combined in one step. Let’s create a second drawer,
where we both declare and initialize a variable:

```
let mySecondDrawer = '$500';
```

Initialization can occur either in the same statement where you declared the variable (see declaredAndDefined),
or after the declaration (see declaredButOnlyLaterDefined). You may access a declared variable
even if you have not initialized it. Its value becomes undefined.

```
let declaredAndDefined = 5;

let declaredButOnlyLaterDefined;
declaredButOnlyLaterDefined = declaredAndDefined ** 2;

let declaredButNotDefined;

console.log(
  declaredAndDefined,
  declaredButOnlyLaterDefined,
  declaredButNotDefined
);
```

    • The variable declaredAndDefined is declared on the same line where it is defined
    • The variable declaredButOnlyLaterDefined is only defined later in another line
    • The variable declaredButNotDefined is not defined at all, therefore, its value becomes undefined

Let’s see what happens if we move the line declaredButNotDefined below the console.log statement.

<!-- page 39 -->

```
let declaredAndDefined = 5;

let declaredButOnlyLaterDefined;
declaredButOnlyLaterDefined = declaredAndDefined ** 2;

console.log(
  declaredAndDefined,
  declaredButOnlyLaterDefined,
  declaredButNotDefined
);
// The following error message is displayed:
// ReferenceError: declaredButNotDefined is not defined

let declaredButNotDefined;
```

If you execute the above code, a ReferenceError should be displayed while executing the console.log
statement. This is because the following sequence of events: you ask for the contents of your post
box in the post office. However, the box you are asking for does not exist in the post office. This box
is only accessible once you create it using the statement let declaredButNotDefined.

```
console.log( declaredButNotDefined ); // ReferenceError

let declaredButNotDefined;
```

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
### Constants

Constants behave in a similar way as variables. Constants can be created using the const keyword:

```
const PI = 3.14;
```

The value of a constant cannot be changed later:

```
PI = 2;
Uncaught TypeError: Assignment to constant variable.
```

As the value of constants stay unchanged, they have to be initialized in the same statement where
they are declared. If we forget this necessary step, we get an error message:

<!-- page 40 -->

```
const c;
Uncaught SyntaxError: Missing initializer in const declaration
```

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
### Scope of a variable

The scope of a variable shows where the variable is visible and where it is not.
In JavaScript, there are many different scopes available:

    1. Global scope
    2. Block scope (let, const)
    3. Function scope (var)
    4. Lexical scope (see later)
    5. Module scope (we will not deal with this scope here)

In most programming languages, the first two scopes are available. Function scope is a unique
feature of JavaScript. Since the 2015 version of JavaScript, ES6 (or ES2015), function scope is losing
its popularity, as the well known block scoped let and const variables emerged.

Regarding block scope, blocks can be created anywhere in your code. Blocks are created using braces
({ and }):

```
{
// This is a block
}
```

Variables created using let and const are only visible inside the block where they are created:

```
{
  let box = 5;
  console.log( box );
}
```

The above code displays the value of box.

```
{
  let innerBox = 6;
}
console.log( innerBox );
```

In the above code segment, we get a ReferenceError as soon as we reach the console.log statement:

<!-- page 41 -->

```
VM124:4 Uncaught ReferenceError: belsoDoboz is not defined
```

This is because the innerBox is not visible from outside the box.

<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
### Global scope

Similarly to other programming languages, JavaScript also has global variables. For instance, you
have already used the global console variable to log messages. Besides console, open the Google
Chrome developer tools console to explore other global variables:

```
document.location.href
"http://zsoltnagy.eu"

document.location.host
"zsoltnagy.eu"

screen.width
1920

let globalVariable = true
true

globalVariable
 true

secondGlobalVariable = true
true

secondGlobalVariable
true
```

As you can see, it is possible to create global variables in the global scope. It does not matter if you
use let, const, or a var (see later) keyword to create these variables, or you just write an assignment.

In case of an assignment, the following happens:

    • The program checks if there is a variable declared locally in the same block (let, const) or
    function (var).
    • if not, the program checks blocks and functions encapsulating the block or function, where our
    variable was declared from inside - out. This is the process of accessing the lexical scope, and
    we will deal with this later in depth.
    • If there are no variables defined in the lexical scope, the global scope is accessed, a global
    variable is created, and its value is set to the value of the assignment.

<!-- page 42 -->
In the following example, we will only use blocks for simplicity, as we have not learned how function
scope works.

```
// first file:

{
  let firstBox = 1;
{
  firstBox = 2;
  secondBox = 3;
  console.log( firstBox, secondBox );
  }
}
```

If we execute the above code, the values 2 3 are printed to the console. The variable firstBox
exists in the block encapsulating the block we are in. The variable secondBox was created using an
assignment, and there are no var, let, or const variables declared with this name. Therefore, this
variable exists in the global scope.

Now let’s suppose the contents of the first file have been loaded, and we also load the following
code segment titled second file:

```
// second file:
 
{
  let firstBox = 4;
  {
    console.log( firstBox, secondBox );
  }
}
```

Once we execute this code, the values 4 3 are printed. The variable firstBox is defined in the block
outside the block of the console.log. The variable secondBox is global, and it was created when
loading firstFile. The secondBox variable is from now on shared across all files that we load.

```
// third file:
console.log( secondBox );
```

Executing this code also has access to the secondBox global variable.

```
// fourth file:
console.log( firstBox );
```

The result of loading the fourth file is a ReferenceError, because firstBox does not exist inside
this scope: it only exists within the block it was defined in first file and second file.

```
VM5519:1 Uncaught ReferenceError: firstBox is not defined
at <anonymous>:1:14
```

When writing software, often times we create and maintain hundreds of thousands of lines of code,
in some cases even millions. The number of files are usually in the hundreds if not in the thousands.
As the size of your program grows, it becomes harder and harder to keep track of which code accesses
and modifies which global variables in which order. Therefore, as a generic rule, it is advised to use
locally scoped variables, while avoiding global variables whenever you can.

Using global variables is not advised. Most often the time, global variables are created because of
a mistake from a developer. Remember, if you forget the let, const, or var keywords in front of a
variable assignment, you create a global variable.
<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
### The var keyword and function scope  <!-- page 43 -->


<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
### Naming variables


<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
### Creating multiple variables in one statement


<!--~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~-->
## Arrays

An array is an ordered list of items. The items may be of any type. You know, in most post offices,
there are hundreds or thousands of post boxes. Each post box may or may not contain something.
Each post box has a numeric handle. Post box 25 may be your box. You unlock it, grab its handle,
and access its contents.

The trick is that in case of arrays, you have to imagine the post boxes with handles called keys of 0,
1, 2, and so on. Typically, arrays have continuous keys.

```
let days = [ 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday' ];
```

If you are looking for post box 3 among the days post office, you get Thursday, because Monday is
the 0th element, Tuesday is the 1st element, Wednesday is the 3rd element, and Thursday is the 4th
element of the array.

Arrays do not have to contain elements of the same type. We can place strings, null, undefined,
symbols, objects, and other arrays in the array:

```
let storage = [ 1, 'Monday', null ];
```
