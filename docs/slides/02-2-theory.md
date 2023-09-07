### Weitere Abstraktionen
#### Werte in einem Kontext bearbeiten
Mögliche Kontexte: <!-- .elements class="fragment" data-fragment-index="1" -->
- Maybe            <!-- .elements class="fragment" data-fragment-index="1" -->
- Sequence         <!-- .elements class="fragment" data-fragment-index="1" -->
- Stack            <!-- .elements class="fragment" data-fragment-index="1" -->
- ...              <!-- .elements class="fragment" data-fragment-index="1" -->

Wie?                    <!-- .elements class="fragment" data-fragment-index="2" -->
Gemeinsames Interface!  <!-- .elements class="fragment" data-fragment-index="2" -->




### Monadisches Interface
Definierte Funktionen:
- `fmap` 
- `empty`
- `pure`
- `and` (in Haskell: `bind`)

Note:
- orientiert an monadischem interface von haskell
- mächtige und generalisierte Abstraktionen 



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