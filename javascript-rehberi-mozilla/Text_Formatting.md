This chapter introduces how to work with strings and text in JavaScript.

## Strings

JavaScript's [String](https://developer.mozilla.org/en-US/docs/Glossary/String "String: In any computer programming language, a string is a sequence of characters used to represent text.") type is used to represent textual data. It is a set of "elements" of  16-bit unsigned integer values  (UTF-16 code units). Each element in the String occupies a position in the String. The first element is at index 0, the next at index 1, and so on. The length of a String is the number of elements in it. You can create strings using string literals or string objects.

### String literals

You can create simple strings using either single or double quotes: 

```javascript    
'foo' "bar"
```

More advanced strings can be created using escape sequences:

#### Hexadecimal escape sequences

The number after \\x is interpreted as a [hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal) number. 
    
```javascript    
'\xA9' // "©"
```

#### Unicode escape sequences

The Unicode escape sequences require at least four hexadecimal digits following `\u`. 

```javascript    
'\u00A9' // "©"
```

#### Unicode code point escapes

New in ECMAScript 2015. With Unicode code point escapes, any character can be escaped using hexadecimal numbers so that it is possible to use Unicode code points up to `0x10FFFF`. With simple Unicode escapes it is often necessary to write the surrogate halves separately to achieve the same result.

See also [`String.fromCodePoint()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCodePoint "The static String.fromCodePoint() method returns a string created by using the specified sequence of code points.") or [`String.prototype.codePointAt()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/codePointAt "The codePointAt() method returns a non-negative integer that is the Unicode code point value."). 

```javascript
'\u{2F804}'

// the same with simple Unicode escapes
'\uD87E\uDC04'
```

### String objects
The [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String "The String global object is a constructor for strings or a sequence of characters.") object is a wrapper around the string primitive data type. 

```javascript
const foo = new String('foo'); // Creates a String object  
console.log(foo); // Displays: [String: 'foo']
typeof foo; // Returns 'object'
```

You can call any of the methods of the `String` object on a string literal value—JavaScript automatically converts the string literal to a temporary `String` object, calls the method, then discards the temporary `String` object. You can also use the `String.length` property with a string literal.

You should use string literals unless you specifically need to use a `String` object, because `String` objects can have counterintuitive behavior. For example: 

```javascript  
const firstString = '2 + 2'; // Creates a string literal value
const secondString = new String('2 + 2'); // Creates a String object
eval(firstString); // Returns the number 4
eval(secondString); // Returns the string "2 + 2"
```

A `String` object has one property, `length`, that indicates the number of UTF-16 code units in the string. For example, the following code assigns `x` the value 13, because "Hello, World!" has 13 characters, each represented by one UTF-16 code unit. You can access each code unit using an array bracket style. You can't change individual characters because strings are immutable array-like objects: 

```javascript
const hello = 'Hello, World!';
const helloLength = hello.length;
hello[0] = 'L'; // This has no effect, because strings are immutable
hello[0]; // This returns "H"
```

Characters whose Unicode scalar values are greater than U+FFFF (such  as some rare Chinese/Japanese/Korean/Vietnamese characters and some emoji) are stored in UTF-16 with two surrogate code units each. For example, a string containing the single character U+1F600 "Emoji grinning face" will have length 2\. Accessing the individual code units in such a string using brackets may have undesirable consequences such as the formation of strings with unmatched surrogate code units, in violation of the Unicode standard. (Examples should be added to this page after MDN bug 857438 is fixed.) See also [`String.fromCodePoint()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCodePoint "The static String.fromCodePoint() method returns a string created by using the specified sequence of code points.") or [`String.prototype.codePointAt()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/codePointAt "The codePointAt() method returns a non-negative integer that is the Unicode code point value.").

A `String` object has a variety of methods: for example those that return a variation on the string itself, such as `substring` and `toUpperCase`.

The following table summarizes the methods of [`String`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String "The String global object is a constructor for strings or a sequence of characters.") objects.

#### Methods of `String` Method

|Method|Description|
|--- |--- |
|`charAt`, `charCodeAt`, `codePointAt`|Return the character or character code at the specified position in string.|
|`indexOf`, `lastIndexOf`|Return the position of specified substring in the string or last position of specified substring, respectively.|
|`startsWith`, `endsWith`, `includes`|Returns whether or not the string starts, ends or contains a specified string.|
|`concat`|Combines the text of two strings and returns a new string.|
|`fromCharCode`, `fromCodePoint`|Constructs a string from the specified sequence of Unicode values. This is a method of the String class, not a String instance.|
|`split`|Splits a String object into an array of strings by separating the string into substrings.|
|`slice`|Extracts a section of a string and returns a new string.|
|`substring`, `substr`|Return the specified subset of the string, either by specifying the start and end indexes or the start index and a length.|
|`match`, `matchAll`, `replace`, `search`|Work with regular expressions.|
|`toLowerCase`, `toUpperCase`|Return the string in all lowercase or all uppercase, respectively.|
|`normalize`|Returns the Unicode Normalization Form of the calling string value.|
|`repeat`|Returns a string consisting of the elements of the object repeated the given times.|
|`trim`|Trims whitespace from the beginning and end of the string.|


### Multi-line template literals

[Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) are string literals allowing embedded expressions. You can use multi-line strings and string interpolation features with them.

Template literals are enclosed by the back-tick (\` \`) ([grave accent](https://en.wikipedia.org/wiki/Grave_accent)) character instead of double or single quotes. Template literals can contain place holders. These are indicated by the Dollar sign and curly braces (`${expression}`).

#### Multi-lines

Any new line characters inserted in the source are part of the template literal. Using normal strings, you would have to use the following syntax in order to get multi-line1 strings: 

```javascript
console.log('string text line 1\n\
string text line 2');
// "string text line 1
// string text line 2"
```

To get the same effect with multi-line strings, you can now write: 

```javascript
console.log(`string text line 1
string text line 2`);
// "string text line 1
// string text line 2"
```

#### Embedded expressions

In order to embed expressions within normal strings, you would use the following syntax: 
    
```javascript
const five = 5;
const ten = 10;
console.log('Fifteen is ' + (five + ten) + ' and not ' + (2 * five + ten) + '.');
// "Fifteen is 15 and not 20."
```

Now, with template literals, you are able to make use of the syntactic sugar making substitutions like this more readable: 
    
```javascript
const five = 5;
const ten = 10;
console.log(`Fifteen is ${five + ten} and not ${2 * five + ten}.`);
// "Fifteen is 15 and not 20."
```

For more information, read about [Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) in the [JavaScript reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference).

## Internationalization

The [`Intl`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl "The Intl object is the namespace for the ECMAScript Internationalization API, which provides language sensitive string comparison, number formatting, and date and time formatting. The INTL object provides access to several constructors as well as functionality common to the internationalization constructors and other language sensitive functions.") object is the namespace for the ECMAScript Internationalization API, which provides language sensitive string comparison, number formatting, and date and time formatting. The constructors for [`Collator`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Collator "The Intl.Collator object is a constructor for collators, objects that enable language sensitive string comparison."), [`NumberFormat`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat "The Intl.NumberFormat object is a constructor for objects that enable language sensitive number formatting."), and [`DateTimeFormat`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat "The Intl.DateTimeFormat object is a constructor for objects that enable language-sensitive date and time formatting.") objects are properties of the `Intl` object.

### Date and time formatting

The [`DateTimeFormat`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/DateTimeFormat "The Intl.DateTimeFormat object is a constructor for objects that enable language-sensitive date and time formatting.") object is useful for formatting date and time. The following formats a date for English as used in the United States. (The result is different in another time zone.) 
    

```javascript
const msPerDay = 24 * 60 * 60 * 1000;
 
// July 17, 2014 00:00:00 UTC.
const july172014 = new Date(msPerDay * (44 * 365 + 11 + 197));

const options = { year: '2-digit', month: '2-digit', day: '2-digit',
                hour: '2-digit', minute: '2-digit', timeZoneName: 'short' };
const americanDateTime = new Intl.DateTimeFormat('en-US', options).format;
 
console.log(americanDateTime(july172014)); // 07/16/14, 5:00 PM PDT
```

### Number formatting

The [`NumberFormat`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/NumberFormat "The Intl.NumberFormat object is a constructor for objects that enable language sensitive number formatting.") object is useful for formatting numbers, for example currencies. 
    

```javascript
const gasPrice = new Intl.NumberFormat('en-US',
                        { style: 'currency', currency: 'USD',
                          minimumFractionDigits: 3 });
 
console.log(gasPrice.format(5.259)); // $5.259

const hanDecimalRMBInChina = new Intl.NumberFormat('zh-CN-u-nu-hanidec',
                        { style: 'currency', currency: 'CNY' });
 
console.log(hanDecimalRMBInChina.format(1314.25)); // ￥ 一,三一四.二五
```

### Collation

The [`Collator`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Collator "The Intl.Collator object is a constructor for collators, objects that enable language sensitive string comparison.") object is useful for comparing and sorting strings.

For example, there are actually two different sort orders in German, *phonebook* and *dictionary*. Phonebook sort emphasizes sound, and it's as if "ä", "ö", and so on were expanded to "ae", "oe", and so on prior to sorting. 
    
```javascript
const names = ['Hochberg', 'Hönigswald', 'Holzman'];
 
const germanPhonebook = new Intl.Collator('de-DE-u-co-phonebk');
 
// as if sorting ["Hochberg", "Hoenigswald", "Holzman"]:
console.log(names.sort(germanPhonebook.compare).join(', '));
// logs "Hochberg, Hönigswald, Holzman"
```

Some German words conjugate with extra umlauts, so in dictionaries it's sensible to order ignoring umlauts (except when ordering words differing *only* by umlauts: *schon* before *schön*). 
    
```javascript
const germanDictionary = new Intl.Collator('de-DE-u-co-dict');
 
// as if sorting ["Hochberg", "Honigswald", "Holzman"]:
console.log(names.sort(germanDictionary.compare).join(', '));
// logs "Hochberg, Holzman, Hönigswald"
```

For more information about the [`Intl`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl "The Intl object is the namespace for the ECMAScript Internationalization API, which provides language sensitive string comparison, number formatting, and date and time formatting. The INTL object provides access to several constructors as well as functionality common to the internationalization constructors and other language sensitive functions.") API, see also [Introducing the JavaScript Internationalization API](https://hacks.mozilla.org/2014/12/introducing-the-javascript-internationalization-api/).
