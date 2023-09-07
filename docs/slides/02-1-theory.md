### Sequence Library
#### Was ist eine Sequence?
_Eine endliche oder unendliche Folge von Werten ._<!-- .elements class="fragment" data-fragment-index="1" -->

`1, 3, 5, 7, 9, ...`<!-- .elements class="fragment" data-fragment-index="2" -->

`True, True, False, True, True, False`<!-- .elements class="fragment" data-fragment-index="2" -->

`a, ab, abc, abcd, abcde, ...`<!-- .elements class="fragment" data-fragment-index="2" -->

Note:
- keine normale Liste - lazy
- basiert auf Iteratoren



### Basis der Sequence - Die Iteration Protocols
```js[1| 1-2 | 1-4 | 1-5 |1-6 | 1-7]
const list = [0, 1];
const iterator = list[Symbol.iterator]();

iterator.next(); // returns { done: false, value: 0 }
iterator.next(); // returns { done: false, value: 1 }
iterator.next(); // returns { done: true,  value: undefined }
iterator.next(); // returns { done: true,  value: undefined }
```

Note:
- kann nur einmal iteriert werden
- folgt den JS Iteration Protokollen



### Implementierung der Iteration Protocols 
```js[1-7|9-13]
const InfiniteOnesIterable = () => {
  const next = () => ({ done: false, value: 1 });

  return {
    [Symbol.iterator]: () => ({ next })
  }
};

const [one, anotherOne, andOneAgain] = InfiniteOnesIterable();

for (const _one of InfiniteOnesIterable()) { 
  // hangs forever, since done is always false
}
```



### Implementierung der Sequence 
```js[1 | 3-11 | 1-16]
const Sequence = (start, whileFunction, incrementFunction) => {

  const iterator = () => {
    ...
    const next = () => {
      ...
      return { done, value: current };
    };
    
    return { next };
  };

  return {
    [Symbol.iterator]: iterator
  } 
};
```

Note:
- logik weggelassen



### Verwendung einer Sequence 
```js[1-3 | 5 | 7-10]
const startValue        = 0;
const whileFunction     = x => x < 10;
const incrementFunction = x => x + 2;

const seq = Sequence(startValue, whileFunction, incrementFunction);

for (const elem of seq) {
  console.log(elem);
}
// => Logs '0, 2, 4, 6, 8'
```



### Verarbeiten einer Sequence

Ziel: Funktionalitäten wie filter, map, usw. auf Sequence anwenden! <!-- .elements class="fragment" data-fragment-index="1" -->

Lösung: Decorator Pattern<!-- .elements class="fragment" data-fragment-index="2" -->



### Decorator Pattern 
<img src="slides/assets/decorator.png" width="800"/>

Note:
- Beispiel map: jeder Wert wird auf einen anderen abgebildet



### Implementierung von _map_
```js[1 | 3,17 | 8 | 8,9 | 1-19]
const map = mapper => iterable => {
  
  const mapIterator = () => {
    const inner = iteratorOf(iterable);
    let mappedValue;
    
    const next = () => {
      const { done, value } = inner.next();
      if (!done) mappedValue = mapper(value);
      return { done, value: mappedValue };
    };
    
    return { next };
  };

  return {
    [Symbol.iterator]: mapIterator
  } 
};
```



### Vorteile der Architektur 
```js[]
const values = [0,1,2,3];
const mapped = map(x => x * 2)(values);
```

- Receiver ist letztes Argument
- Alle iterables prozessierbar