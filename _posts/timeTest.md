# Javascript Time log for how long a function takes to execute

## To set up the time log function

```
const timeIt = (label, fn) => {
  console.time(label);
  fn();
  console.timeEnd(label);
}
```

## Example to use it

```
const arrayOfRandoms = randomCeil => length => Array.from({length: length}, (v, i) => Math.floor(Math.random() * randomCeil));

const arrOfThousand = arrayOfRandoms(100)(1000);

// use time log
timeIt('thousand - map', () => {
  const resultFrom1000 = arrOfThousand
    .map(val => val * 3);
});
```