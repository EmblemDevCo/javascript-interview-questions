<div align="center">

<img src="https://miro.medium.com/max/512/1*YWazhGyGmNs6K3HZE7lS7Q.png"  height="100px" alt="Image of JavaScript Logo"/>

# JavaScript Interview Questions

</div>

A list of JavaScript interview questions and small coding challenges to help frontend engineers prepare for technical interviews

## Given an array of strings, create a function to return an array of unique strings.

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

Using an object store the array values as object keys

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

## Resolve array of promises (promise functions) in sequential order

### Answer

Using async await and a for of loop you can execute these promise functions sequentially

```js
const sequential = async (promises) => {
  for (const promise of promises) {
    await promise();
  }
};
```

## Resolve array of promises (promise functions) concurrently

### Answer

Using Promise.all you execute these promise functions concurrently. Read more [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)

await used here assuming there is more to execute after promises are resolved

```js
const concurrently = async (promises) => {
  await Promise.all(promises.map((fn) => fn()));
  ...
};
```

## Create a makeCalculator function that that can be used to create several calculator objects with an add, subtract, divide, and multiply methods. Add a print method to console log the running total at any time.

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
