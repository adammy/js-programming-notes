# Chapter 1: Values, Types, and Operators #

With computing, there is only data; whether it's reading, modifying, or creating new data.

Data is stored in bits. Bits are binary, meaning they can be one of two values. The typical abstraction people refer to is 1 and 0, but there is also true and false, a high vs low electric charge, or a shiny vs dull spot on a CD.

All data can be reduced to a sequence of bits.

The following is an example of the number 13 expressed in bits/binary:

```javascript
Value:    0   0   0   0  1  1  0  1
Place:  128  64  32  16  8  4  2  1
```

This binary number equates to 8 + 4 + 1 = 13.

## Values ##

A typical modern computer has upwards of 30 billion bits. In order to work within these large quantities of bits, we separate them into chunks that represent pertinent information. In JavaScript, those chunks are called *values*.

Values can be numbers, text, functions, etc.

To create a value, you merely invoke its name. Wildly convenient.

Every value has to be stored. If you use a large amount of values at the same time, you might run out of memory. Fortunately, this only comes up if you need the values simultaneously.

As soon as you don't need a value, it disappears. The bits that were representing it can be used for something else. This process is referred to as *garbage collection*.

In essence, memory management is handled for you in JavaScript unlike a low-level language, like C.

Below is a practical example of what's happening in memory, while writing JavaScript:

```javascript
var n = 123; // allocates memory for a number
var s = 'azerty'; // allocated memory for a string

var o = {
	a: 1,
	b: null
}; // allocates memory for an object and contained values

var a = [1, null, 'abra']; // allocated memory for an array and contained values

function f(a) {
	return a + 2;
} // allocates a function (which is a callable object)

var d = new Date(); // allocates a Date object

var e = document.createElement('div'); // allocates a DOM element

var s2 = s.substr(0, 3);
/*
 * since strings are immutable values
 * JavaScript may decide to not allocate memory in this instance,
 * but instead just store the [0, 3] range
 */
```

Note: you should still be aware of memory management even though JavaScript handles these things for you. It's still important.

### Numbers ###

JavaScript represents numbers using 64 bits. This means the amount of numbers that can be represented is limited to a degree, but most (and I really mean most) will not need anything larger than a 64-bit number. The number of representations that can exist with 64 bits is 2<sup>64</sup> or about 18 quintillion.

*Overflow* is to use a value that does not fit with the number of bits allocated. For example, lets say we're have an 8-bit number that's only used for positive, whole numbers. That would leave us with a max value of 2<sup>8</sup> or 256. Attempting to represent 257 with this pattern is overflowing.

Not all whole numbers below 18 quintillion fit into a JavaScript number because those bits can also represent negative and fractional numbers.

Number expressions are written as follows:

```javascript
42 // standard whole number
-42 // negative whole number
9.81 // fractional number
-9.81 // negative fractional number
2.998e8 // scientific notation; e = exponent; 2.998 x 10^8 = 299,800,000
```

#### Arithmetic ####

Calculations with whole numbers are guaranteed to be precise. Calculations with fractional numbers are not. Some fractional numbers lose precision when only 64 bits is available to them.

Arithmetic operations take two *operands* and an *operator* and return a new value. Example below:

```javascript
10 + 4 // returns 14
10 + 4 * 11 // returns 54; see precedence
(10 + 4) * 11 // returns 154
```

One arithmetic operator that is not immediately obvious is ```%```, which returns a *remainder* of two operands. This is sometimes referred to as a modulo, the modulus operator, or the remainder operator. Example below:

```javascript
144 % 12 // returns 0 because 144 / 12 is equal to 12 with no remainder
314 % 100 // returns 14 because 314 / 100 is equal to 3 with a remainder of 14
```

#### Special Numbers ####

In JavaScript, there are three values that are considered numbers, but don't behave or look like a normal number.

The first two are ```Infinity``` and ```-Infinity```, which represent positive and negative infinities. It's nonsense really.

The last value is ```NaN```, which stands for "not a number". You will get this value if you attempt any arithmetic that won't yield a meaningful result, such as ```0 / 0``` or ```'boom' * 4```.

### Strings ###

Strings are used to represent text. They are written by enclosing content in quotes. You can use single quotes, double quotes, or backticks as seen below:

```javascript
`Down on the sea`
"Lie on the ocean"
'Float on the ocean'
```

Certain characters require *escaping* to be used properly in strings. Escaping is done with a backslash (\\) followed by some set of characters. Some examples include:
```javascript
'\n' // new line
'\'hello\'' // returns "hello"; a literal single quote
'\\' // returns "\"; a literal backslash
```

Strings have been modeled as a series of bits. JavaScript does this based on the *Unicode* Standard. This standard assigns a number to virtually every character you would ever need. If every character is associated with a number, than a string can be described by a sequence of numbers. JavaScript's representation uses 16 bits per string element, which provides up to 2<sup>16</sup> different characters. Unicode defines more characters than 16 bits would allow, so some characters take up two string elements and therefore are afforded 32 bits.

The plus operator (+) can be used on strings for the purpose of concatenation. See below:

```javascript
'con' + 'cat' + 'e' + 'nate' // returns "concatenate"
```

There is one difference of note between the three quoting methodologies: using backticks (\`) creates a *template literal*, which can span multiple lines and allows you to embed expressions and values without using concatenation. Example below:
```javascript
var name = 'Adam';

// Without template literal
'My name is ' + name  // returns "My name is Adam"

// With template literal
`My name is ${name}` // returns "My name is Adam"

// Template literal with an expression to be evaluated
`Half of 100 is ${100 / 2}` // returns "Half of 100 is 50"
```

### Unary Operators ###

All of the operations we've seen thus far use *binary* operators, meaning that they require two operands. A *unary* operator only requires one operand.

The minus operator can serve as a binary or unary operator. In the context of a calculation such as `10 -2`, the operator is binary. When setting a number to be negative `-20`, the operator is unary.

Another example of an unary operator is `typeof`, which returns the type of the operand it's provided as a string. Example below:

```javascript
typeof 2.5 // returns "number"
typeof 'hello' // returns "string"
```

### Boolean Values ####

JavaScript has a *Boolean* type, which can have only one of two values: ```true``` or ```false```.

#### Comparison ####

Comparison operators can be used compare operands against each other and return Boolean values. Comparison operators includes:

* ```>``` - greater than
* ```>=``` - greater than or equal to
* ```<``` - less than
* ```<=``` - less than or equal to
* ```==``` - equal to (uses type coercion)
* ```!=``` - not equal to (uses type coersion)
* ```===``` - equal to (compares value and type)
* ```!==``` - not equal to (compares value and type)

Examples below:

```javascript
3 > 2 // returns true

3 < 2 // returns false

(3 + 3) >= 6 // returns true

// strings can also be compared
// it's ordered by the Unicode bit value
// which is roughly in alphabetical order
'Aardvark' < 'Zoroaster' // returns true

'Itchy' != 'Scratchy' // returns true

'Apple' == 'Orange' // returns false

// using == or != will coerce the type to be the same
// so the second operand gets converted to a string
'true' == true // returns true

// using === or !== will not coerce the type
// resulting in a different outcome
'true' === true // returns false
```

For string comparison, note that the order is uppercase letters, lowercase letters, and non-alphabetic characters.

#### Logical Operators ####

There are three logical operators that can be applied to Boolean values: *and*, *or*, and *not*.

The *and* operator is represented by ```&&```. It is a binary operator that returns ```true``` if both operands provided to it evaluated to true (maybe start to mention truthy/falsy). Example below:

```javascript
(1 > 0) && (2 > 1) // returns true
(1 > 0) && (2 === 1) // returns false
```

The *or* operator is represented by ```||```. It is a binary operator that returns ```true``` if either of the operands provided to it are true. Example below:

```javascript
(1 > 0) || (2 > 1) // returns true
(1 > 0) || (2 === 1) // returns true
(1 < 0) || (2 === 1) // returns false
```

The *not* operator is represented by an exclamation mark (!). It is a unary operator the reverses/flips the value given to it. If the operand provided would evaluate to true, applying the *not* operator flips it and returns false and vice versa. Example below:

```javascript
!(1 > 0) // returns false
!('Adam' === 'Adam') // returns false
!(1 > 5) // returns true
```

There is one more logical operator that is called a *ternary* operator. It differs from unary and binary operators in that it operates on three operands. It is defined with a question mark (?) and a colon (:). The operand left of the question mark is evaluated. To the right of the question mark are two other operands, separated by a colon. If the condition on the left evaluates to true, the overall expression returns the operand left of the colon. If false, it returns the operand to the right of the colon. In essence, it will look like ```(expressionToEvaluate) ? returnIfTrue : returnIfFalse```. Additionally, it is sometimes referred to as a *conditional* operator. Examples below:
```javascript
true ? 1 : 2 // returns 1
false ? 1 : 2 // returns 2
(1 > 5) ? 'Boom' : 'Pow' // returns 'Pow'
```

### Empty Values ###

There are two special values that are used to denote the absence of a meaningful value: ```null``` and ```undefined```.

```undefined``` means a variable has been declared, but has not been assigned a value. ```null``` is an assignment in and of itself. It can be assigned to a variable as a representation of no value. Examples below:

```javascript
var name; // create a variable, but don't assign a value
name; // returns undefined

var age = null; // create a variable and assign it to null in the immediate future
age; // returns null
```

### Automatic Type Conversion ###

This was mentioned briefly before, but when an operator is applied to the wrong type of value, JavaScript will convert that value to the type is needs using what is called *type coercion*. Examples below:

```javascript
8 * null // returns 0; null is converted to the number 0
'5' - 1 // returns 4; the string "5" is converted to the number 5
'5' + 1 // returns "51"; the number 1 is converted to a string and the operands are concatenated
"five" * 2 // returns NaN; NaN is returned when meaningless arithmetic is attempted
false == 0 // returns true; the number 0 is converted to the Boolean false
```

The examples above help demonstrate why you should use the three-character comparison operators (```===``` and ```!==```) liberally. It prevents misinterpretations and unexpected type conversions.

### Short-Circuiting of Logical Operators ###

The logical operators ```&&``` and ```||``` handle values in a different peculiar way. They will convert the value on the left side to a Boolean type in order to decide what to do. Depending on the result, the operator will return either the left- or right-hand value.

The ```||``` operator will return the value to its left when that can be converted to true, otherwise it returns the value on the right. We can use this as a way to have a default value of sorts. Example below:

```javascript
null || 'user' // returns "user"
'Adam' || 'user' // returns "Adam"
```

The ```&&``` operator works similarly, but the other way around. When the value to its left converts to false, it returns that value, otherwise it returns the right value.

Another important property of these two operators is that the operand to the right is evaluated only when necessary. In the case of ```true || x```, it doesn't matter what ```x``` is because the first operand will result to true. This means that ```x``` is never evaluated and is flat-out ignored. This is called *short-circuit evaluation*.

## Summary ##

We explored four types of JavaScript values: numbers, strings, Booleans, and undefined.

You can combine and transform values with operators. We saw binary operators for arithmetic (+, -, \*, /, and %), string concatenation (+), comparison (==, !=, ===, !==, <=, >=), and logic (&& and ||), as well as several unary operators (- to negate a number, ! to negate logically, and ```typeof``` to find a value's type), and a ternary operator (?:).

## Quiz Yourself

1. Express the number 45 in binary.
> 00101101

2. Describe *garbage collection*.
> Garbage collection is a form of automatic memory management that abstracts that complexity away from the developer. In this process, values that are no longer needed are automatically thrown out and the bits that represented that value can be used for something else.

3. What is *overflowing*?
> Overflowing is using a value that does not fit with the number of bits allocated for that value. In our context, JavaScript utilizes 64-bit numbers, which includes bits for negative and fractional numbers. It typically should not be a problem as your maximum number is still very large.

4. In what instances are arithmetic calculations guaranteed to return a precise number? What instances are they not? Why?
> Calculations with whole numbers are guaranteed to be precise. Calculations with fractional numbers are not. Some fractional numbers lose precision when only 64 bits is available to them.

5. Describe the *modulus* operator.
> The modulus operator returns the remainder of two operands when they're divided.

6. What is NaN? What type is it?
> NaN stands for "not a number". It is the result of any arithmetic that won't yield a meaningful result, such as ```0 / 0``` or ```'boom' * 4```. It's of type number even though its an abbreviation for "not a number".

7. What is the *Unicode Standard*? How does it help with setting a value to strings in JavaScript (or any programming language really)?
> The Unicode Standard is a character coding system designed to support worldwide interchange of written text. The Unicode Standard assigns a number to virtually every character you would ever need. With every character being associated to a number, strings can then be described by a sequence of numbers, and in turn a sequence of bits. JavaScript string elements are 16 bits. Unicode defines more characters than 16 bits would allow, so some characters take up two string elements and therefore are afforded 32 bits.

8. How is a *template literal* defined? What benefits does it provide?
> Template literals are defined using backticks (\`). The two benefits it offers are that it can span multiple lines and it allows you to embed expressions and values without using concatenation. The embedded expression or value is defined using a dollar sign and curly braces (```${value}```).

9. What is the difference between a unary, binary, and ternary operator?
> The operators take 1, 2, and 3 operands respectively.

10. What type of value would you use to represent "on" and "off" for a light bulb?
> Boolean

11. What is the difference between the ```==``` and ```===``` comparison operators?
> Both operators are checking for equality. The ```==``` operator will coerce the type of one operand to match the other operand. The ```===``` operator will not coerce types. This in essence makes the ```==``` operator check for equality of value, whereas the ```===``` operator will check for equality of value and type.

12. What is the difference between ```undefined``` and ```null```?
> ```undefined``` means a variable has been declared, but has not been assigned a value. ```null``` is an assignment in and of itself. It can be assigned to a variable as a representation of no value.

13. What happens when you try to evaluate ```'8' - 2```? What about ```'8' + 2```? Explain your answer.
> In the first expression, evaluating the string "8" minus the number 2 will result in the string being converted to a number type. This would then leave you with ```8 - 2```, which will return 6. This happens due to type coercion. In the second expression, type coercion still happens, but it happens differently. Instead the string "8" is kept the same and the number 2 is converted into a string. This would leave you with ```'8' + '2'```, which would return "82" due to the two strings being concatenated.

14. Describe *short-circuit evaluation*.
> When using certain logical operators, such as the *or* operator (```||```), the second operand is only executed/evaluated if the first operand is falsy. This prevents the program from doing unnecessary work.
