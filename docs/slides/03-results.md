## Resultate



#### Tic Tac Toe
<iframe style="border: none; margin-left: 250px;" width="100%" height="600" data-src="https://wildwyss.github.io/ip6-overview/wild_wyss/src/sequence/examples/tictactoe/TicTacToe.html" data-preload></iframe>

Note:
- Computergesteuerter Gegner für Spiel "Tic tac toe",
- Inspiration aus Paper "Why functional programming matters" von John Hughes
- Idee: Alle möglichen Spielfelder von der jetzigen Ausgangslage aus berechnen
    - Algo ist eigentlich für funktionale Sprachen
    - Jedem errechneten Spielfeld wird zugeordnet, ob es gut oder schlecht für den Computer ist
    - Baumstruktur mit Spielfeld als Node und möglichen Feldern als Kinder
    - Algo funktioniert für verschiedene rundenbasierte Spiele
    - Funktioniert nur mit lazy evaluation, da trees riesig werden 
- Backbonde des Algos sind Sequenzen
- Schlusswort: Sequence library bringt funktionale Konzepte zu JavaScript



### Testing
- Strukturiert testen <!-- .elements class="fragment" data-fragment-index="1" -->
- Testing basierend auf Properties <!-- .elements class="fragment" data-fragment-index="2" -->
```js
// Struktur bleibt erhalten
seq => map(x => x)(seq) ["=="] (seq);
```

Note:
- Viele Operationen müssen gleiche Grundfunktionalitäten erfüllen
- neue Operation: nur Testkonfig schreiben!
- Property based testing: 
    - für jede Operation können zusätzliche Properties/Invarianten angegeben werden
- Schlusswort: strukturiertes Testing macht den Kern stärker, wenn die SW wächst



### Limitationen durch JavaScript
Unter anderem:
```js[1-3|5-6]
// fehlendes Name-Overloading
const maybe  = Just(5);
const mapped = maybe.fmap(x => 2*x);

// fehlende higher-kinded Types
const monad = from(maybe).result();
```

Note:
- Fehlende Sprachfeatures: Higher-Kinded types, name overloading, type safety.
- Name-Overloading gibt es nicht, da JavaScript nicht typisiert ist!
    - Lösung: Funktionen sind über .-Notation verfügbar
- JINQ (oder andere Funktionen) verlieren Info, dass es ein Maybe war 
    -Lösung: Es ist ein Typecast notwendig



## Besten Dank für Ihre Aufmerksamkeit
