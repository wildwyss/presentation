### Iterator
- Das Iterator Protokoll
- Der Kolibri Iterator
- Implementation
- Vergleich zu anderen Sprachen




### Das Iterator Protokoll
__Wie funktioniert ein Iterator in JavaScript?__
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

Note:
- iterator = JS Objects, welches dem JS Iterator und Iterable Protokoll folgt
- iterator Merkmal: nur einmal ausführbar
- Iterierbarkeit => Objekt muss Property mit Key Symbol.iterator haben, dann ist es ein Iterator
- Iterator muss eine Funktion `next` haben, welche `value` und `done` returned



### Erstellen
```js [1|2|3|5]
const startValue    = 0;
const incFunction   = value => value + 1;
const stopDetection = value => value < 5;

const it = Iterator(startValue, incFunction, stopDetection);
```



### Verwenden
```js [3-4|7-14]
const it = Iterator(startValue, incFunction, stopDetection);

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
- copy
- forEach$
- reverse$
- eq$
- ...



### Implementierungsdetail
Die `transform` function
```js [1-2|4|4-15] 
  const range = Range(10);
  range.map(x => 2 * x);

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
__Kolibri Iterator vs. Haskell vs. Kotlin vs. Python__
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