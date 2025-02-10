# [Kaprekar 6174](https://en.wikipedia.org/wiki/6174)

This number is renowned for the following rule:

Take any four-digit number, using at least two different digits (leading zeros are allowed). Arrange the digits in descending and then in ascending order to get two four-digit numbers, adding leading zeros if necessary. Subtract the smaller number from the bigger number. Go back to step 2 and repeat.

This process is known as Kaprekar's routine. It will always reach its fixed point, 6174, in at most 7 iterations. Once 6174 is reached, the process will continue yielding 7641 – 1467 = 6174.

For example, choose 9701:
```
9710 - 0179 = 9531
9531 - 1359 = 8172
8721 - 1278 = 7443
7443 - 3447 = 3996
9963 - 3699 = 6264
6642 - 2466 = 4176
7641 - 1467 = 6174
```

Code representation:
```
// Convert the number to string, sort ascending
const asc = (n) => `${n}`.split("")
                         .sort((a, b) => a - b)
                         .join("");
// Convert the number to string, sort descending
const desc = (n) => `${n}`.split("")
                          .sort((a, b) => b - a)
                          .join("");
// subtract the number sorted and its reverse sort
const calc = (a, b) => a - b;
```

Using recursion:
```
function kaprekarIteration(num) {
  const a = asc(num);
  const d = desc(num);
  const result = calc(parseInt(d), parseInt(a));

  console.log(`${d} - ${a.padStart(4, "0")} = ${result}`);

  if (result === 6174) {
    return;
  }

  return kaprekarIteration(result);
}

kaprekarIteration(9701);
```

Using a loop:
```
function kaprekarIteration(num) {
  while (num !== 6174) {
    const a = asc(num);
    const d = desc(num);
    num = calc(parseInt(d), parseInt(a));

    console.log(`${d} - ${a.padStart(4, "0")} = ${num}`);

    if (num === 6174) break;
  }
}

kaprekarIteration(9701);
```
