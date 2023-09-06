### Sequence Library
#### Was ist eine Sequence?
_Eine endliche oder unendliche Folge von Werten ._<!-- .elements class="fragment" data-fragment-index="1" -->

`1, 3, 5, 7, 9, ...`<!-- .elements class="fragment" data-fragment-index="2" -->

`True, True, False, True, True, False`<!-- .elements class="fragment" data-fragment-index="2" -->

`a, ab, abc, abcd, abcde, ...`<!-- .elements class="fragment" data-fragment-index="2" -->

Note:
- Was ist eine Sequence? In anderen Sprachen würde man vllt von Liste sprechen, aber lazy liste
- Die Sequence ist aber lazy, was bedeutet das? Die Sequence hat ein Startwert, jeder weiterer wird basierend auf dem vorhergehenden berechnet
- Der Speicherplatz ist also minimal, egal ob die Sequence 1 oder und unendlich viele Elemente erzeugt.



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
- Wie wird eine lazy Sequence erstellt? Dafür müssen wir die Iteration Protokolle von JS betrachten
- Dafür betrachten wir ein ganz einfaches Beispiel eines gewöhnlichen JavaScript Array, welches ebenfalls ein Objekt ist, das die Iteration Protokolle implementert
- Auf einem Object, welches die Iteration Protokolle befolgt, ist es möglich, eine Funktion mit dem Namen [Symbol.iterator] zu erhalten.
- Dies returniert nun ein Objekt, welches die Funktion next() bereitstellt.
- Über diese Funktion erhält man nun Wert für Wert, bei jedem Aufruf den nächsten, bis das Iterable. also ein iterierbares Objekt aufgebraucht ist
- ein Iterable kann nur einmal durchloffen werden, anschliessen ist done auf true.



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

Note:
- Ein kurzer Blick auf die Implementierung der Iteration Protokolle
- In diesem Beispiel definieren wir ein Iterable, welches eine unendliche Folge von Einsen generiert
- Dabei sehen wir auf Linie 4-6, dass eine Funktion mit dem Namen Symbol.iterator definiert ist - Symbol.iterator ist ein keyword definiert von der Sprach JS
- die Funktion liefert ein Objekt zurück, welches eine Funktion mit dem Namen next hat.
- Die Funktion next, definiert auf Linie 2, returniert nun eine Objekt, welches aus done und value besteht




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
<img src="assets/decorator.png" width="800"/>

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



### Vorteile der Umsetzung 
```js[]
const values = [0,1,2,3];
const mapped = map(x => x * 2)(values);
```

- Receiver ist letztes Argument
- Lazy evaluation
- Alle iterables prozessierbar

Note:
- Receiver letztes Argument: 
  - ermöglicht eta-reduzierung des receiver
  - ermöglicht konfigurierbare Funktionen
  - ermöglicht Verwendung mit allen Iterables
-Lazy evaluation
  - Durch befolgen der Iteration Protokolle der Sequence und der Decorators werden alle Werte lazy evaluiert
