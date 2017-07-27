# Convert an ascii string to a integer
> A common interview question is to write  a function that converts  a  string into an integer e.g. `"123"` => `123`.  This function is commonly called  atoi because  we  are converting  an ASCII string into an integer.

> In this lesson we cover the proper way to do this in JavaScript which is `parseInt` along with implementing it using basic ascii math.

A common interview question is to write a function that takes a string returns and returns a number.

```js
/**
 * Converts a string to a integer
 * e.g. "123" => 123
 */
export function atoi(str: string): number {

}
```

JavaScript has a function called `parseInt`, that can do this integer parsing for us.

* For simple ints we get the int,
* For ints with a negative sign we get a negative int.
* When it encounters a character that is not a numeral, it ignores it and all succeeding characters. It still returns the integer value parsed up to that point.
* You can use this fact to ignore decimal portions as well.
* Finally if a string does not start with a decimal numeral it returns NaN i.e. Not A Number.

```js
/**
 * Converts a string to a integer
 * e.g. "123" => 123
 */
export function atoi(str: string): number {
  return parseInt(str);
}

console.log(atoi('123')); // 123
console.log(atoi('-123')); // -123
console.log(atoi('-123Extra')); // -123
console.log(atoi('-123.456')); // -123
console.log(atoi('Does not start with a digit 123')); // NaN
```

Note that `parseInt` siliently ignoring invalid trailing characters can be considered a problem. So a better implementation can easily be written with a simple regex test that only allows strings containing things that we support e.g. a leading sign followed by any number of decimal digits.

```js
/**
 * Converts a string to a integer
 * e.g. "123" => 123
 */
export function atoi(str: string): number {
  if (/^\-?([0-9]+)$/.test(str))
    return parseInt(str);
  return NaN;
}

console.log(atoi('123')); // 123
console.log(atoi('-123')); // -123
console.log(atoi('-123Extra')); // NaN
console.log(atoi('-123.456')); // NaN
console.log(atoi('Does not start with a digit 123')); // NaN
```

With practical JavaScript training out of the way, when this question is commonly asked the interviewer might specify that you are not allowed to use `parseInt` or the `Number` function. They essentially want to see if you can write a function that is similar to how `parseInt` would be implemented internally.

* First we note down the character point for '0'. This will allow us to convert each decimal digit from a string to its number value.
* Next thing we need to do is parse out the sign. We can store this as sign multiplier.
* Next we create an accumulator for the integer result of parsing the digits
* We go through the string left to right. At each point we update the accumultor as the sum of
 - the current accumulator multiplied by 10
 - and the number value of the current char, which we can get from its distance from the 0 code.
* Finally we return the accumulator multipled by the sign.

If we run through an example with valid inputs you can see that it works as expected.

```js
/**
 * Converts a string to a integer
 * e.g. "123" => 123
 */
export function atoi(str: string): number {
  const zeroCode = '0'.charCodeAt(0);

  let sign = 1;
  if (str[0] === '-') {
    str = str.substring(1);
    sign = -1;
  }

  let acc = 0;
  for (const char of str) {
    acc = acc * 10 + (char.charCodeAt(0) - zeroCode);
  }

  return sign * acc;
}

console.log(atoi('123')); // 123
console.log(atoi('-123')); // -123
```

What the interviewer is really checking here is your understanding of basic math and the fact that string digits represent code points that can be diffed to get their integer representation.

The interviewer might additionally ask you about things that can go wrong:
* A good one worth mentioning is that we are assuming that the string is a valid integer to begin with. They might then ask you to fix that issue, and you can simply check the result of this difference should be in range `0-9`.