This chapter introduces the concepts, objects and functions used to work with and perform calculations using numbers and dates in JavaScript. This includes using numbers written in various bases including decimal, binary, and hexadecimal, as well as the use of the global [`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math "Math is a built-in object that has properties and methods for mathematical constants and functions. Not a function object.") object to perform a wide variety of mathematical operations on numbers.

## Numbers

In JavaScript, all numbers are implemented in [double-precision 64-bit binary format IEEE 754](https://en.wikipedia.org/wiki/Double-precision_floating-point_format) (i.e., a number between ±2<sup>−1022</sup> and ±2<sup>+1023</sup>, or about ±10<sup>−308</sup> to ±10<sup>+308</sup>, with a numeric precision of 53 bits). Integer values up to ±2<sup>53</sup> − 1 can be represented exactly. In addition to being able to represent floating-point numbers, the number type has three symbolic values: `+`[`Infinity`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Infinity "The global Infinity property is a numeric value representing infinity."), `-`[`Infinity`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Infinity "The global Infinity property is a numeric value representing infinity."), and [`NaN`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NaN "The global NaN property is a value representing Not-A-Number.") (not-a-number). See also [JavaScript data types and structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures) for context with other primitive types in JavaScript.

> **Note:** There is no specific data type for integers in JavaScript, although the [`BigInt`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt "BigInt is a built-in object that provides a way to represent whole numbers larger than 253, which is the largest number JavaScript can reliably represent with the Number primitive.") type lets you represent integers that may be very large. There are caveats to using `BigInt`, however; for example, you can't mix and match `BigInt` and [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number "The Number JavaScript object is a wrapper object allowing you to work with numerical values. A Number object is created using the Number() constructor. A primitive type object number is created using the Number() function.") values in the same operation, and you can't use the [`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math "Math is a built-in object that has properties and methods for mathematical constants and functions. Not a function object.") object with `BigInt` values.

You can use four types of number literals: decimal, binary, octal, and hexadecimal.

### Decimal numbers

```javascript
1234567890
42

// Caution when using leading zeros:

0888 // 888 parsed as decimal
0777 // parsed as octal in non-strict mode (511 in decimal)
```

Note that decimal literals can start with a zero (`0`) followed by another decimal digit, but if every digit after the leading `0` is smaller than 8, the number gets parsed as an octal number.

### Binary numbers
Binary number syntax uses a leading zero followed by a lowercase or uppercase Latin letter "B" (`0b` or `0B`). If the digits after the `0b` are not 0 or 1, the following [SyntaxError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SyntaxError) is thrown: "Missing binary digits after 0b". 
    
```javascript
var FLT_SIGNBIT  = 0b10000000000000000000000000000000; // 2147483648
var FLT_EXPONENT = 0b01111111100000000000000000000000; // 2139095040
var FLT_MANTISSA = 0B00000000011111111111111111111111; // 8388607
```

### Octal numbers

Octal number syntax uses a leading zero. If the digits after the `0` are outside the range 0 through 7, the number will be interpreted as a decimal number. 
    
```javascript
var n = 0755; // 493
var m = 0644; // 420
```

Strict mode in ECMAScript 5 forbids octal syntax. Octal syntax isn't part of ECMAScript 5, but it's supported in all browsers by prefixing the octal number with a zero: `0644 === 420` and`"\045" === "%"`. In ECMAScript 2015, octal numbers are supported if they are prefixed with `0o`, e.g.: 
    
```javascript
var a = 0o10; // ES2015: 8
```

### Hexadecimal numbers

Hexadecimal number syntax uses a leading zero followed by a lowercase or uppercase Latin letter "X" (`0x` or `0X)`. If the digits after 0x are outside the range (0123456789ABCDEF),  the following [`SyntaxError`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SyntaxError) is thrown: "Identifier starts immediately after numeric literal". 
    
```javascript
0xFFFFFFFFFFFFFFFFF // 295147905179352830000
0x123456789ABCDEF   // 81985529216486900
0XA                 // 10
```

### Exponentiation

```javascript
1E3   // 1000
2e6   // 2000000
0.1e2 // 10
```

## `Number` object

The built-in [`Number`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number "The Number JavaScript object is a wrapper object allowing you to work with numerical values. A Number object is created using the Number() constructor. A primitive type object number is created using the Number() function.") object has properties for numerical constants, such as maximum value, not-a-number, and infinity. You cannot change the values of these properties and you use them as follows: 

```javascript
var biggestNum = Number.MAX_VALUE;
var smallestNum = Number.MIN_VALUE;
var infiniteNum = Number.POSITIVE_INFINITY;
var negInfiniteNum = Number.NEGATIVE_INFINITY;
var notANum = Number.NaN;
```

You always refer to a property of the predefined `Number` object as shown above, and not as a property of a `Number` object you create yourself.

The following table summarizes the `Number` object's properties.

#### Properties of `Number`

|Property|Description|
|--- |--- |
|`Number.MAX_VALUE`|The largest representable number (`±1.7976931348623157e+308`)|
|`Number.MIN_VALUE`|The smallest representable number (`±5e-324`)|
|`Number.NaN`|Special "not a number" value|
|`Number.NEGATIVE_INFINITY`|Special negative infinite value; returned on overflow|
|`Number.POSITIVE_INFINITY`|Special positive infinite value; returned on overflow|
|`Number.EPSILON`|Difference between 1 and the smallest value greater than 1 that can be represented as a Number (`2.220446049250313e-16`)|
|`Number.MIN_SAFE_INTEGER`|Minimum safe integer in JavaScript (−2^53 + 1, or `−9007199254740991`)|
|`Number.MAX_SAFE_INTEGER`|Maximum safe integer in JavaScript (+2^53 − 1, or `+9007199254740991`)|


#### Methods of `Number`

|Method|Description|
|--- |--- |
|`Number.parseFloat()`|Parses a string argument and returns a floating point number. Same as the global `parseFloat()` function.|
|`Number.parseInt()`|Parses a string argument and returns an integer of the specified radix or base. Same as the global `parseInt()` function.|
|`Number.isFinite()`|Determines whether the passed value is a finite number.|
|`Number.isInteger()`|Determines whether the passed value is an integer.|
|`Number.isNaN()`|Determines whether the passed value is `NaN`. More robust version of the original global `isNaN()`.|
|`Number.isSafeInteger()`|Determines whether the provided value is a number that is a safe integer.|

The `Number` prototype provides methods for retrieving information from `Number` objects in various formats. The following table summarizes the methods of `Number.prototype`.

#### Methods of `Number.prototype`

|Method|Description|
|--- |--- |
|`toExponential()`|Returns a string representing the number in exponential notation.|
|`toFixed()`|Returns a string representing the number in fixed-point notation.|
|`toPrecision()`|Returns a string representing the number to a specified precision in fixed-point notation.|


## `Math` object

The built-in [`Math`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math "Math is a built-in object that has properties and methods for mathematical constants and functions. Not a function object.") object has properties and methods for mathematical constants and functions. For example, the `Math` object's `PI` property has the value of pi (3.141...), which you would use in an application as 

```javascript
Math.PI
```

Similarly, standard mathematical functions are methods of `Math`. These include trigonometric, logarithmic, exponential, and other functions. For example, if you want to use the trigonometric function sine, you would write 

```javascript
Math.sin(1.56)
```

Note that all trigonometric methods of `Math` take arguments in radians.

The following table summarizes the `Math` object's methods.

#### Methods of `Math`

|Method|Description|
|--- |--- |
|`abs()`|Absolute value|
|`sin()`, `cos()`, `tan()`|Standard trigonometric functions; with the argument in radians.|
|`asin()`, `acos()`, `atan()`, `atan2()`|Inverse trigonometric functions; return values in radians.|
|`sinh()`, `cosh()`, `tanh()`|Hyperbolic functions; argument in hyperbolic angle.|
|`asinh()`, `acosh()`, `atanh()`|Inverse hyperbolic functions; return values in hyperbolic angle.|
|`pow()`, `exp()`, `expm1()`, `log10()`, `log1p()`, `log2()`|Exponential and logarithmic functions.|
|`floor()`, `ceil()`|Returns the largest/smallest integer less/greater than or equal to an argument.|
|`min()`, `max()`|Returns the minimum or maximum (respectively) value of a comma separated list of numbers as arguments.|
|`random()`|Returns a random number between 0 and 1.|
|`round()`, `fround()`, `trunc()`,|Rounding and truncation functions.|
|`sqrt()`, `cbrt()`, `hypot()`|Square root, cube root, Square root of the sum of square arguments.|
|`sign()`|The sign of a number, indicating whether the number is positive, negative or zero.|
|`clz32()`, `imul()`|Number of leading zero bits in the 32-bit binary representation. The result of the C-like 32-bit multiplication of the two arguments.|


Unlike many other objects, you never create a `Math` object of your own. You always use the built-in `Math` object.

## `Date` object

JavaScript does not have a date data type. However, you can use the [`Date`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date "Creates a JavaScript Date instance that represents a single moment in time. Date objects use a Unix Time Stamp, an integer value that is the number of milliseconds since 1 January 1970 UTC.") object and its methods to work with dates and times in your applications. The `Date` object has a large number of methods for setting, getting, and manipulating dates. It does not have any properties.

JavaScript handles dates similarly to Java. The two languages have many of the same date methods, and both languages store dates as the number of milliseconds since January 1, 1970, 00:00:00, with a Unix Timestamp being the number of seconds since January 1, 1970, 00:00:00.

The `Date` object range is -100,000,000 days to 100,000,000 days relative to 01 January, 1970 UTC.

To create a `Date` object: 
    
```javascript
var dateObjectName = new Date([parameters]);
```

where `dateObjectName` is the name of the `Date` object being created; it can be a new object or a property of an existing object.

Calling `Date` without the `new` keyword returns a string representing the current date and time.

The `parameters` in the preceding syntax can be any of the following:

- Nothing: creates today's date and time. For example, `today = new Date();`.
- A string representing a date in the following form: "Month day, year hours:minutes:seconds." For example, `var Xmas95 = new Date("December 25, 1995 13:30:00")`. If you omit hours, minutes, or seconds, the value will be set to zero.
- A set of integer values for year, month, and day. For example, `var Xmas95 = new Date(1995, 11, 25)`.
- A set of integer values for year, month, day, hour, minute, and seconds. For example, `var Xmas95 = new Date(1995, 11, 25, 9, 30, 0);`.

### Methods of the `Date` object
The `Date` object methods for handling dates and times fall into these broad categories:

* "set" methods, for setting date and time values in `Date` objects.
* "get" methods, for getting date and time values from `Date` objects.
* "to" methods, for returning string values from `Date` objects.
* parse and UTC methods, for parsing `Date` strings.

With the "get" and "set" methods you can get and set seconds, minutes, hours, day of the month, day of the week, months, and years separately. There is a `getDay` method that returns the day of the week, but no corresponding `setDay` method, because the day of the week is set automatically. These methods use integers to represent these values as follows:

* Seconds and minutes: 0 to 59
* Hours: 0 to 23
* Day: 0 (Sunday) to 6 (Saturday)
* Date: 1 to 31 (day of the month)
* Months: 0 (January) to 11 (December)
* Year: years since 1900

For example, suppose you define the following date: 

```javascript
var Xmas95 = new Date('December 25, 1995');
```

Then `Xmas95.getMonth()` returns 11, and `Xmas95.getFullYear()` returns 1995\.

The `getTime` and `setTime` methods are useful for comparing dates. The `getTime` method returns the number of milliseconds since January 1, 1970, 00:00:00 for a `Date` object.

For example, the following code displays the number of days left in the current year: 
    
```javascript
var today = new Date();
var endYear = new Date(1995, 11, 31, 23, 59, 59, 999); // Set day and month
endYear.setFullYear(today.getFullYear()); // Set year to this year
var msPerDay = 24 * 60 * 60 * 1000; // Number of milliseconds per day
var daysLeft = (endYear.getTime() - today.getTime()) / msPerDay;
var daysLeft = Math.round(daysLeft); //returns days left in the year
```

This example creates a `Date` object named `today` that contains today's date. It then creates a `Date` object named `endYear` and sets the year to the current year. Then, using the number of milliseconds per day, it computes the number of days between `today` and `endYear`, using `getTime` and rounding to a whole number of days.

The `parse` method is useful for assigning values from date strings to existing `Date` objects. For example, the following code uses `parse` and `setTime` to assign a date value to the `IPOdate` object: 
    
```javascript
var IPOdate = new Date();  
IPOdate.setTime(Date.parse('Aug 9, 1995'));
```

### Example

In the following example, the function `JSClock()` returns the time in the format of a digital clock. 

```javascript
function JSClock() {
  var time = new Date();
  var hour = time.getHours();
  var minute = time.getMinutes();
  var second = time.getSeconds();
  var temp = '' + ((hour > 12) ? hour - 12 : hour);
  if (hour == 0)
    temp = '12';
  temp += ((minute < 10) ? ':0' : ':') + minute;
  temp += ((second < 10) ? ':0' : ':') + second;
  temp += (hour >= 12) ? ' P.M.' : ' A.M.';
  return temp;
}
```

The `JSClock` function first creates a new `Date` object called `time`; since no arguments are given, time is created with the current date and time. Then calls to the `getHours`, `getMinutes`, and `getSeconds` methods assign the value of the current hour, minute, and second to `hour`, `minute`, and `second`.

The next four statements build a string value based on the time. The first statement creates a variable `temp`, assigning it a value using a conditional expression; if `hour` is greater than 12, (`hour - 12`), otherwise simply hour, unless hour is 0, in which case it becomes 12\.

The next statement appends a `minute` value to `temp`. If the value of `minute` is less than 10, the conditional expression adds a string with a preceding zero; otherwise it adds a string with a demarcating colon. Then a statement appends a seconds value to `temp` in the same way.

Finally, a conditional expression appends "P.M." to `temp` if `hour` is 12 or greater; otherwise, it appends "A.M." to `temp`.
