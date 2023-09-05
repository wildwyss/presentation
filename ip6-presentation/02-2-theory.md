### Weitere Abstraktionen
#### Werte in einem Kontext bearbeiten
Mögliche Kontexte: <!-- .elements class="fragment" data-fragment-index="1" -->
- Maybe            <!-- .elements class="fragment" data-fragment-index="1" -->
- Sequence         <!-- .elements class="fragment" data-fragment-index="1" -->
- Stack            <!-- .elements class="fragment" data-fragment-index="1" -->
- ...              <!-- .elements class="fragment" data-fragment-index="1" -->

Wie?                    <!-- .elements class="fragment" data-fragment-index="2" -->
Gemeinsames Interface!  <!-- .elements class="fragment" data-fragment-index="2" -->

Note:
- praktische Abstraktionen für das Verarbeiten von Daten unabhängig vom Kontext
- ermöglicht durch das implementieren von Interfaces



### Beispiel - Monadisches Interface
Definierte Funktionen:
- fmap
- empty
- and
- pure

Note:
- Beispiel für ein solches Interface - monadisches Interface wie in Haskell implementiert
- ermöglicht das Verarbeiten von Daten in einem Kontext



### JINQ - LINQ für JavaScript
Verarbeitet monadische Strukturen mittels:
- from
- where
- select
- pairWith
- inside
- map

Note:
- Stellt Funktionen zur Verfügung, die rein auf den monadischen Funktionen arbeiten



### JINQ verwenden
Kann mit allen monadischen Typen umgehen:
```js[]
const range  = Range(7);

const result =
  from(range)
    .where(x => x % 2 === 0)
    .result();
```

```js[]
const maybe = Just(3);

const result =
  from(maybe)
    .where(x => x % 2 == 0)
    .result()
```
