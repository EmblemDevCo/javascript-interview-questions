<div align="center">

<img src="https://miro.medium.com/max/512/1*YWazhGyGmNs6K3HZE7lS7Q.png"  height="100px" alt="Image of JavaScript Logo"/>

# JavaScript Interview Questions

</div>

A list of JavaScript interview questions and small coding challenges to help frontend engineers prepare for technical interviews

## Given an array of strings, create a function that returns an array of unique strings.

Example:

```js
const strings = ['a', 'b', 'c', 'a', 'z'];

unique(strings); // ['a', 'b', 'c', 'z']
```

### Answer

This can be answered a few different ways:

With a nested loop

(loop through the input array, and add the string to a new result array if it doesn't exist there)

```js
const unique = (list) => {
  const results = [];
  for (const item of list) {
    if (!results.includes(item)) {
      results.push(item);
    }
  }
  return results;
};
```

Using an object, store the array values as object keys

(duplicate keys aren't allowed so need to check if it already exists)

```js
const unique = (list) => {
  const results = {};
  for (const item of list) {
    results[item] = item;
  }
  return Object.keys(results);
};
```

Using a Set. Read more [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)

```js
const unique = (list) => Array.from(new Set(list));
```

## Resolve an array of promises (promise functions) in sequential order

### Answer

Using `async` `await` and a `for of` loop you can execute these promise functions sequentially

```js
const sequential = async (promises) => {
  for (const promise of promises) {
    await promise();
  }
};
```

## Resolve an array of promises (promise functions) concurrently

### Answer

Using `Promise.all` you execute these promise functions concurrently. Read more [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

await used here assuming there is more to execute after promises are resolved

```js
const concurrently = async (promises) => {
  await Promise.all(promises.map((fn) => fn()));
  ...
};
```

## Create a makeCalculator function

It can be used to create several calculator objects with an add, subtract, divide, and multiply methods. Add a print method to console log the running total at any time.

### Answer

Using closures you can create a function that returns an objects with methods that have access to its surrounding state. Read more [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)

```js
const makeCalcuator = () => {
  let total = 0;

  return {
    multiply(x) {
      return (total *= x);
    },
    dvide(x) {
      return (total /= x);
    },
    add(x) {
      return (total += x);
    },
    subtract(x) {
      return (total -= x);
    },
    print() {
      console.log(total);
    },
  };
};

const calculator = makeCalcuator();
calculator.add(5);
calculator.subtract(2);
calculator.multiply(4);
calculator.print(); // 12
```

## Given an array of numbers, return the sum of all odd numbers

Example:

```js
const nums = [3, 23, 42, 20, 67, 48, 31, 7, 92];
sumOfOdds(nums) -> // 131
```

### Answer

You can use the Array reduce method to reduce the array values into a single value. Read more [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce).

In the reduce method you will want to check if the number is even using the modulus operator.

```js
const sumOfOdds = (nums) =>
  nums.reduce((acc, curr) => {
    if (curr % 2 !== 0) {
      acc += curr;
    }
    return acc;
  }, 0);
```

## Create function to reverse a string

### Answer

Using a combination of string and array methods you can do this simply.

(first turn the string into an array with `split` then reverse the order of the array with `reverse` then turn the array back into a string with `join`)

```js
const reverse = (word) => word.split('').reverse().join('');
```

You may also be asked to create this function without the use of string and array methods. You can do this using a for loop.

```js
const reverse = (string) => {
  let result = [];
  for (const letter of string) {
    result.unshift(letter);
  }
  return result.join('');
};
```

This function can be more efficient, we can cut the number of iterations in half.

```js
const reverse = (string) => {
  result = [];
  for (let i = 0; i < string.length / 2; i++) {
    result[i] = string[string.length - i - 1];
    result[string.length - i - 1] = string[i];
  }
  return result.join('');
};
```

## Spin Words

Write a function that takes in a string of one or more words, and returns the same string, but with all five or more letter words reversed (Just like the name of this Kata). Strings passed in will consist of only letters and spaces. Spaces will be included only when more than one word is present.

Examples: spinWords( "Hey fellow warriors" ) => returns "Hey wollef sroirraw" spinWords( "This is a test") => returns "This is a test" spinWords( "This is another test" )=> returns "This is rehtona test"

### Answer

To accomplish this you want to split the initial string into an array of words. Splitting on the space. Then, you want to map over all of words and reverse any word that has a length greater than or equal to five.

```js
const spinWords = (string) => {
  const list = string.split(' ');
  return list
    .map((word) =>
      word.length >= 5 ? word.split('').reverse('').join('') : word
    )
    .join(' ');
};
```

## Square Every Digit

Write a function that squares every digit of a number.

For example, if we run 9119 through the function, 811181 will come out, because 92 is 81 and 12 is 1.

Note: The function accepts an integer and returns an integer

### Answer

To accomplish this you want to split the initial string into an array of words. Splitting on the space. Then, you want to map over all of words and reverse any word that has a length greater than or equal to five.

```js
const squareDigits = (num) =>
  parseInt(
    `${num}`
      .split('')
      .map((x) => `${Math.pow(parseInt(x, 10), 2)}`)
      .join(''),
    10
  );
```

## Find the Outlier

You are given an array (which will have a length of at least 3, but could be very large) containing integers. The array is either entirely comprised of odd integers or entirely comprised of even integers except for a single integer N. Write a method that takes the array as an argument and returns this "outlier" N.

Examples

```js
findOutlier([2, 4, 0, 100, 4, 11, 2602, 36]);
// Should return: 11 (the only odd number)

findOutlier([160, 3, 1719, 19, 11, 13, -21]);

// Should return: 160 (the only even number)
```

### Answer

This answer is a little more "wordy" than other ones. I like doing this with a regular for loop because I can check if I have the answer already before I am done looping through the entire array. For instance, if there are 50 items in the array and the outlier is at position 3, this solution would only need 3 iterations.

We will check each number as loop through the array of integers to and place the number in the appropriate odd or even array.

At the end of the loop we check the length of both arrays, if one array has more than 2 items, and the other array has an item, we return that item.

```js
const findOutlier = (integers) => {
  const odd = [];
  const even = [];
  for (let i = 0; i < integers.length; i++) {
    if (integers[i] % 2) {
      odd.push(integers[i]);
    } else {
      even.push(integers[i]);
    }

    if (odd.length > 1 && even.length) {
      return even[0];
    }

    if (even.length > 1 && odd.length) {
      return odd[0];
    }
  }
};
```

## Flatten 2 dimensional array

Given a multidemnional array, create a function to flatten the array into a one dimensional array.

```js
const myArray = [[1], [2, 3], [4, 5, 6], [7, 8, 9, 10]];
flatten(myArray);
// Should return: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

### Answer

The `concat()` method is used to merge two **or more** arrays. Concat can take 1 on more arrays as it's arguments. In combination with the spread operator, where we are expanding the items of the array (other arrays in this case), we merge the empty array (concat is an array method) with the inner arrays of myArray. Learn more about `concat()` [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat). Learn more about `Spread syntax` [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax).

```js
const flatten = (array) => [].concat(...array);
```
