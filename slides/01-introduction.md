<img src="slides/assets/kolibri-logo.png" width="200"/>

## Projekt 5 Informatik
#### Funktionale Standard Library für das Kolibri Web UI Toolkit
#### HS22

Note:
* Begrüssung
* Projekt vorstellen




### Vorstellung
<div style="display: flex; justify-content: left; align-items: center; margin-left: 100px;">
  <img src="slides/assets/profile-images/andri-wild.jpg" alt="drawing" width="200"/>
  <ul>
    <li> Andri Wild </li>
    <li> Informatik Vertiefung Web </li>
    <li> <a href="mailto:andri.wild@students.fhnw.ch">andri.wild@students.fhnw.ch</a> </li>
  </ul>
</div>
<div style="display: flex; justify-content: left; align-items: center; margin-left: 100px;">
  <img src="slides/assets/profile-images/tobias-wyss.jpg" alt="drawing" width="200"/>
  <ul>
    <li> Tobias Wyss </li>
    <li> Informatik iCompetence </li>
    <li> <a href="mailto:tobias.wyss@students.fhnw.ch">tobias.wyss@students.fhnw.ch</a> </li>
  </ul>
</div>

Note:
* Andri: Vertiefung Web, ich iCom
* beide 5. Semester
* Beide sehr an Programmierung & Web interessiert




### Aufgabenstellung
<img src="slides/assets/kolibri-logo.png" width="200"/>

- Kolibri erweitern                       <!-- .elements class="fragment" data-fragment-index="1" --> 
- Funktionale Lösungsansätze              <!-- .elements class="fragment" data-fragment-index="2" -->
- Hohe Qualität                           <!-- .elements class="fragment" data-fragment-index="3" -->
- Dokumentation mittels JSDoc             <!-- .elements class="fragment" data-fragment-index="4" -->

Note:
* Erweiterung 
  * Welche das sind, war zu Beginn offen
  * Funktionale Lösungen
  * Fokus Ring in der Aufgabenstellung -> Dazu später mehr
* Qualität & Testing im Fokus, da andere es brauchen sollen
  * Extreme Programming
    * Wöchentliche Reviews
    * Pair Programming
    * Iteratives Vorgehen
* JSDoc für einfache Handhabung



### Resultate
* Logging Framework                <!-- .elements class="fragment" data-fragment-index="1" -->
* Iterator                         <!-- .elements class="fragment" data-fragment-index="2" -->
* Focus Ring                       <!-- .elements class="fragment" data-fragment-index="3" -->

Note:
* Kurze Übersicht was erreicht wurde 
* Logging Framework -> ähnlich wie Log4J
  * console.log zu wenig
  * Hohe Anforderungen an gutes Logging
  * Erweiterbarkeit
* Iterator
  * Bekannt aus anderen Programmiersprachen
  * Setzt JS Iterator Protokoll um
  * Erweiter um funktionale Konstrukte
* Fokus ring
  * Immutable Datenstruktur
  * Elemente sind in einem Ring angeordnet
  * Simon Peyton Jones
