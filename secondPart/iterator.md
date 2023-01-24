## Iterator
- Das Iterator Protokoll
- Der Kolibri Iterator
- Implementation
- Vergleich zu anderen Sprachen




### Das Iterator Protokoll
Wie funktioniert ein Iterator in JavaScript?
```js [8-9|3-5|1-12]
const Iterator = (value, inc, stop) => {
  ...
  const next = () => {
    return { done: false, value: 7 }
  };

  ...
  const iteratorObject = {
    [Symbol.iterator]: () => ({ next }),
    ...
  };
}
```



### Create & Usage
```js []
const startValue    = 0;
const incFunction   = value => value + 1;
const stopDetection = value => value < 5;

const it = Iterator(startValue, incFunction, stopDetection);
```



### Create & Usage
```js [1-3|5-12]
for (const element of it) {
  console.log(element);
}

it.retainAll(x => x < 10 || x > 90 )
    .map(x => 10 * x)
    .copy()
    .map(x => x.toString())
    .rejectAll(x => x.length >= 4)
    .takeWhile(x => x !== "90")
    .map(Number)
    .dropWhile(x => x < 40);
```



### Implementierte Funktionen
- dropWhile
- takeWhile
- retainAll
- rejectAll
- forEach$
- reverse$
- eq$
- ...



### Implementierungsdetail
Die `transform` function
```js []
  const map = mapper => {
    // 1. remember previous transform operation
    const oldTransform = transform;
    // 2. reassign transform
    transform = x => {
      // 2.1 apply previous transformation
      const  { done, current, nextValue } = oldTransform(x);
      // 2.2 & 2.3 apply map operation and return the next value.
      return { done, current: mapper(current), nextValue };
    };
    return iteratorObject;
  };
```



### Vergleich
Kolibri Iterator vs. Haskell vs. Kotlin vs. Python
```haskell
ghci > [3,2..11]
[3,5,7,9,11]
```
```python
for value in range(3, 11, 2):
  print(value)   # => 3,5,7,9
```
```kotlin
for (value in 3..11 step 2) {
    print(value) // => 3,5,7,9,11
}
```
```js
for (const value of Range(3, 11, 2)) {
  console.log(value); // => 3,5,7,9,11
}
```