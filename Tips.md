# Tips on Writing BadJavaScript

## Coercion

<details>
<summary>View</summary>
 
Coercion is going to be your best freind on making your code more unreadable. Here are a few examples to help you out!

### === or the 'Strict Equal'

In javascript if we want to check if something is equal we use the `===` statement. This is great and short however it is readable. Obviously something we don't want in our BadJavaScript code.

How do we get around this?

There are two ways one with numbers, and one with strings.

#### Numbers

In javascript any number that is not 0 is `true`. From that we can devise if two numbers are `===`. given that we have two numbers 1, 2. The most practical way to test them is with subtraction.

`1 - 2 = -1 or 2 - 1 = 1` Either way javaSricpt will evaluate it to true.

`2 - 2 = 0`  A number that is subtracted from itself is always 0 which is always false.

```JavaScript

if (1-2){
  if any number but 0
  return 'the numbers are not equal'
}
// if 0
return 'the numbers are equal'

```

##### Strings

Strings are a lot more complicated as `===` makes comparisions trivial. The best way I could think of would to use `localeCompare()`.

```JavaScript

let a = 'test'.localCompare('test')
// a equals 1 which is true.
let b = 'test'.localCompare('t')
// b equales 0 which is false

```

This works however it is readable. Instead we could use regex to make it less readable, I mean who actually learns regex :-)

```JavaScript

let text1 = 'test';
let text2 = 'test';
text2.search(new RegExp(`^${text1}$`,'g')) //Will return 0 if it matches and -1 if there are no matches
//by specifying our our regex and using it inline our code becomes more complicated and less readable.
//-1 is true and 0 is false so we need to use ! to flip that.

```

### Bool/String/Number Coercion

JavaScript is a weakly type language, and this is what allows us write BadJS. There are Two ways to convert different data types to other data types, Implicit and Explicit conversions. Explicit conversions are readable which means they are useless in BadJS.

#### To Strings

The `+` operater is the easiest and fastest way to convert any data type into a string. Another way is to use template literals this could be considered less readable at some points.

```JavaScript

let a = false

let b = a+''
//b = 'false'

let c = `${a}`
c = 'false'
```

#### To Numbers

This is where it gets a little more complicated, because the JS compiler will automatically trigger implicit conversions in certian cases including: 

- comparison operators (`>`, `<`, `<=`,`>=`)
- bitwise operators ( `|` `&` `^` `~)
- arithmetic operators (`-` `+` `*` `/` `%`). Note, that binary+ does not trigger numeric conversion, when any operand is a string.
- unary `+` operator
- loose equality operator `==` (incl. `!=`). 
- Note that `==` does not trigger numeric conversion when both operands are strings.


```JavaScript

+'123'          // implicit
123 != '456'    // implicit
4 > '5'         // implicit
5/null          // implicit
true | 0        // implicit

+undefined     //NaN
+" 12 "        //12
+"\n"          //0
+false         //0
+true          //1
+null          //0
```

JavaScript will trim whitespaces from string before converting it to a number. (This includes `\n` and `\t`)

Remember that NaN !== NaN or anything else, this is important because if you implicitly convert something to a number and JS spits out NaN all comparisions will fail.

When applying `==` to `null` or undefined, numeric conversion does not happen. `null` equals only to `null` or `undefined`, and does not equal to anything else.


#### To Bool

JavaScript implicitly converts values into bools in two cases. The first being logical contexts, and the second is triggered by logical operators. (`||` `&&` `!`)

```JavaScript

if (2) { ... }      // implicit due to logical context
!!2                 // implicit due to logical operator
2 || 'hello'        // implicit due to logical operator

```

Logical operators such as `||` and `&&` do boolean conversions internally, but actually return the value of original operands, even if they are not boolean.

```JavaScript

let x = 'hello' && 123;    // x === 123
let y = true && 'apple';   // y === apple
let z = false && 'orange'; // z === false

```

Empty arrays and Objects are converted to true as well. (Arrays are converted to true in general). The following always convert to false.

```JavaScript

!!('')      // false
!!0         // false
!!(-0)      // false
!!(NaN)     // false
!!(null)    // false
!!undefined // false
!!false     // false

```




</details>
  
## Functions

<details>
<summary>View</summary>
</details>

## If/Switch

<details>
<summary>View</summary>
</details>

## for/of/in

<details>
<summary>View</summary>
  
  I feel as though I have failed you. Don't you remember we are trying to write unreadable code. You should not need to use these things. I mean you can, but you will have to make them unreadable.
 
</details>

## Length Of Arrays/Strings

<details>
<summary>View</summary>


Normally we would use Object.length in order to find the length of arrays or strings. As this is bad javascript there is a better way. And its name is Object.keys(). In JS Arrays and Strings are both objects which have keys. An arrays keys are its 

```JavaScript
  
  let a = +Object.keys('I am a text').pop();
  //this will give you the length of a string or array
  //NOTE THAT THESE ARE KEYS WHICH START AT 0, SO IT IS NECCESARY TO ADD 1 TO GET THE ACTUAL LENGHT 
 
```

How does this work? Object keys returns an array of keys [1,2,3,4] for each index of a String or Array. Array.prototype.pop() returns the last index of an array. then + makes sure the returned item is an integer.

</details>

