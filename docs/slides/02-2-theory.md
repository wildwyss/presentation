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



### Monadisches Interface
Definierte Funktionen:
- `fmap` 
- `empty`
- `pure`
- `and` (in Haskell: `bind`)

Note:
- orientiert an haskell monadischem interface
- Haben uns für dies entschieden, weil Haskell aufzeigt, dass dies sehr generelle programmierung zulässt



### JINQ - LINQ für JavaScript
Verarbeitet monadische Strukturen 
```js[]
 from(source)
  .where(...)
  .select(...)
  .result();
```

Note:
- Stellt Funktionen zur Verfügung, die rein auf den monadischen Funktionen arbeiten



## `Live Demo`