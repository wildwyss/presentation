### RESULTS
* Logging Framework                <!-- .elements class="fragment" data-fragment-index="1" -->
* Iterator                         <!-- .elements class="fragment" data-fragment-index="2" -->
* Focus Ring                       <!-- .elements class="fragment" data-fragment-index="3" -->

Note:
* Logging Framework -> ähnlich wie Log4J
  * console.log zu wenig
  * Hohe Anforderungen an gutes Logging
* Iterator
  * Bekannt aus anderen Programmiersprachen
  * Wie funktioniert es in JS?
  * Was können wir damit bauen?
* Fokus ring
  * Einfache Datenstruktur
  * In der Aufgabenstellung beschrieben




### Logging Framework
* Verschiedene Loglevels          <!-- .elements class="fragment" data-fragment-index="1" -->
* Formatierung von Log Messages   <!-- .elements class="fragment" data-fragment-index="2" -->
* Appender                        <!-- .elements class="fragment" data-fragment-index="3" -->
* Erweiterbarkeit                 <!-- .elements class="fragment" data-fragment-index="4" -->

Note:
Features des Logging Framework, von Log4j inspiriert
* Loglevels, DEBUG, ERROR => nur gewisse Levels loggen
* Log messages formatieren
* Appender => wo wird hingeloggt? 
* Erweiterbar 




### Iterator
<ul>
<li>Setzt JS Iteration Protocols um</li> <!-- .elements class="fragment" data-fragment-index="1" -->
<li>Funktionen wie <code>filter</code> oder <code>map</code></li>  <!-- .elements class="fragment" data-fragment-index="2" -->
</ul>

Note:
* Setzt JS Iteration Protokoll um
* zb Zahlen generieren
* Erweitert um funktionale Konstrukte




### Focus Ring
* Immutable Datenstruktur                        <!-- .elements class="fragment" data-fragment-index="1" -->
* Basiert auf dem Iterator                       <!-- .elements class="fragment" data-fragment-index="2" -->                        <!-- .elements class="fragment" data-fragment-index="1" -->

Note:
 * Eine Immutable Datenstruktur
 * Basiert auf unserem Iterator, schöne Anwendung davon.
 * Simon Peyton Jones hat einen Talk darüber -> xmonad
