# MathX

Extended Math object for JavaScript. Collection of useful math functions that I personally need almost on every occasion and that are lacking in standard Math object. The goal is not to gather every possible math function outthere, but rather keep it lightweight and only add stupidly obvious fuctions to this collection.

## Usage

In the terminal:
```

% npm install @lost-types/mathx

```

Then in the module:
```js
// JavaScript modules
import MathX from '@lost-types/mathx';

// CommonJS
const MathX = require('@lost-types/mathx');

const num = MathX.toNumber('33%'); // 0.33

```

## Story behind MathX

There is always a time in every developer's life when he's starting to notice some small functions that he's re-using almost in every project. Sound familiar? The only reasonable step from there is to make it a package and re-use in centralized manner. Also keep it open-source so people can benefit from it and this is exacly what MathX is.

The treshold for the function to enter the collection - I have to use it at least in 3 projects, and I've just started, so right now there are not many fuctions, but I guarantee that they 100% useful!

## Functions

***

#### `MathX.approx()`

Checks if the first argument approximately equals to the second argument within delta, the third argument. Tries best to account for precision errors. Returns boolean.

| **Parameter** | **Type** | **Default value** | **Notes**                                      |
|---------------|----------|-------------------|------------------------------------------------|
| `a`           | `number` |                   |                                                |
| `b`           | `number` |                   |                                                |
| `delta`       | `number` | 0                 | Optional, default to 0                         |

```js

MathX.approx(0.34, 0.45, 0.1); // false
MathX.approx(0.34, 0.44, 0.1); // true
// While 0.3 === 0.2 + 0.1 -> false
MathX.approx(0.3, 0.2, 0.1); // true

```

***

#### `MathX.getPrecision()`

Calculates precision of provided number, including negative precision, aka number of trailing zeros of the integer

| **Parameter** | **Type** | **Default value** | **Notes**                                      |
|---------------|----------|-------------------|------------------------------------------------|
| `number`      | `number` |                   |                                                |

```js

MathX.getPrecision(0.45); // 2
MathX.getPrecision('12.300'); // 1
MathX.getPrecision(-1.2e-11); // -12
MathX.getPrecision(0.45); // 2
MathX.getPrecision(0.45); // 2
MathX.getPrecision(0.45); // 2
MathX.getPrecision(12000000); // -6
MathX.getPrecision(1.45e+100); // -98
MathX.getPrecision(Infinity); // 0

```

***

#### `MathX.modulo()`

Calculates modulo in the correct way including negative numbers. Fixes so called JavaScript modulo bug: https://web.archive.org/web/20090717035140if_/javascript.about.com/od/problemsolving/a/modulobug.htm

| **Parameter** | **Type**  | **Default value** | **Notes**      |
|---------------|-----------|-------------------|----------------|
| `a`           |`number`   |                   |                |
| `b`           |`number`   |                   |                |

```js

MathX.modulo(-2, 5); // 3
MathX.modulo(2, -5); // -3
MathX.modulo(21, 4); // 1

```

***

#### `MathX.random()`

This one is super obvious and I know that many libraries has it, but still. Generates random number within range with certain precision. Negative precision will work as well. Returns generated number.

| **Parameter** | **Type**  | **Default value** | **Notes**                                        |
|---------------|-----------|-------------------|--------------------------------------------------|
| `range`       |`number[]` |                   | Array in [min, max] format                       |
| `precision`   |`number`   | 12                | Optional                                         |

```js

MathX.random([-5, 5], 4); // -4.7824
MathX.random([0, 10000], -2); // 2200
MathX.random([0, 100], 0); // 71
MathX.random(); // 0.897057820671

```

***

#### `MathX.round()`

Another popular one. Similarly to _.round(), rounds number to certain precision. Negative precision will work as well. Digests strings if needed. Returns rounded number.

| **Parameter** | **Type**  | **Default value** | **Notes**                                        |
|---------------|-----------|-------------------|--------------------------------------------------|
| `number`      |`number`   |                   |                                                  |
| `precision`   |`number`   | 12                | Optional                                         |

```js

MathX.round('0.45876453', 4); // 0.4588
MathX.round(0.1 + 0.2); // 0.3
MathX.round(23567, -3); // 24000
MathX.round(23567, -2); // 23600
MathX.round(23567, -1); // 23570
MathX.round(23567, -5); // 0

```

**Note unusual behavior:** while many would expect defaul precision to be 0, `MathX.round()` uses default precision of 12

***

#### `MathX.toNumber()`

Converts string or number to a certain precision. Understands percentage and **do not** coerses any other types into number.

| **Parameter** | **Type**  | **Default value** | **Notes**                                        |
|---------------|-----------|-------------------|--------------------------------------------------|
| `number`      |`number`   |                   |                                                  |
| `precision`   |`number`   | 12                | Optional                                         |

```js

MathX.toNumber('3.45e2'); // 345
MathX.toNumber(0.1 + 0.2); // 0.3
MathX.toNumber('13.359%', 4); // 0.1336
// Be careful with following:
MathX.toNumber(true); // NaN
MathX.toNumber(null); // NaN
MathX.toNumber(); // NaN
MathX.toNumber([1]); // NaN

```
