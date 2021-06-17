# Array destructuring

The split assignment mechanism supported in ECMAScript 2015 (ES6)
Array elements can be assigned to multiple variables at once.

```js
const arr = [1, 2, 3];
const [x, y, z] = arr;
```

Variable length elements can be grouped together and received in the last variable.

```js
const arr = [1, 2, 3, 4, 5];
const [x, y, . .rest] = arr;

console.log(x); //=> 1
console.log(y); //=> 2
console.log(rest); //=> [3, 4, 5].
```
If there are not enough values to assign, it will be undefined.
```js
const arr = [1, 2];
const [x, y, z] = arr;

console.log(x); //=> 1
console.log(y); //=> 2
console.log(z); //=> undefined
```
You can also do things like default arguments for functions.
```js
const arr = [1, 2];
const [x=0, y=0, z=0] = arr;

console.log(x); //=> 1
console.log(y); //=> 2
console.log(z); //=> 0
```

## Example

## Returning multiple return values from a function (multi-valued function)
The following `divrem` function returns the result of division (quotient and remainder) together. The function `divrem` below returns the result of division (quotient and remainder) together, and the caller stores the result in separate variables using the division assignment mechanism.
```js
function divrem(a, b) {
  return [Math.floor(a / b), a % b]
}

[quotient, remainder] = divrem(10, 3);
console.log(quotient, remainder); //=> 3, 1
```

### Swapping values
Swap the values of two variables without using temporary variables.
```js
[a, b] = [b, a];
```
Example implementation of the function ` fibonacci ` to find the nth Fibonacci number.
Compute the values of two variables `a` and `b` by swapping them with split assignment
```js
function fibonacci(n) {
  let a = 1, b = 1;
  for (let i = 2; i < n; ++i) {
    [a, b] = [b, a + b]
  }
  return b;
}

console.log(fibonacci(1)); //=> 1
console.log(fibonacci(2)); //=> 1
console.log(fibonacci(3)); //=> 2
console.log(fibonacci(4)); //=> 3
console.log(fibonacci(5)); //=> 5
```

***

[Assigning multiple values at the same time using array destructuring](https://maku77.github.io/js/array/destructuring.html) Translated with www.DeepL.com/Translator (free version)
