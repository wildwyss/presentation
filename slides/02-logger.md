## Logging Framework
Note:
In den nächsten Minuten erkläre ich das Logging Framework




### Kernidee
* Eine zentrale Funktion                   <!-- .elements class="fragment" data-fragment-index="1" -->
  * Konfigurierbar über Parameter 
  * Log Statements absetzen
* Allgemeines Environment                  <!-- .elements class="fragment" data-fragment-index="2" --> 
    * Wo wird hin geloggt? 
    * Einschränken was geloggt wird 

Note:
2 Ideen die man verstehen muss:
* es gibt eine zentrale Logging Funktion
  * Konfigurierbar über Parameter
  * Log Statements absetzen
* Environment 
  * Konfiguration die für alle Aufrufe der Logging-Funktion gelten



### Features
<ul>
<li> Logging Levels (<code>LOG_DEBUG</code>)</li>   <!-- .elements class="fragment" data-fragment-index="1" -->
<li> Appender </li>                               <!-- .elements class="fragment" data-fragment-index="2" -->
<li> Kontext </li>                                <!-- .elements class="fragment" data-fragment-index="3" -->
</ul>

Note:
Erläuterung der Features
* Features aus anderen Logging Frameworks bekannt
* Loglevel
  * Jede Message wird auf Log level geloggt 
  * Loglevel Einschränkung
* Appender
  * definieren wo hin geloggt wird. ArrayAppender, ConsoleAppender
  * Eigene Appender hinzufügen
* Kontext
  * Jede Message hat einen Context
  * Herkunft des Log Statements




### Konfiguration
__Environment__                           <!-- .elements class="fragment" data-fragment-index="1" -->
* Zur Laufzeit konfigurierbar             <!-- .elements class="fragment" data-fragment-index="3" -->
* Aktive Appender                         <!-- .elements class="fragment" data-fragment-index="4" -->
* Aktiver Logging Level                   <!-- .elements class="fragment" data-fragment-index="5" -->
* Aktiver Kontext                         <!-- .elements class="fragment" data-fragment-index="6" -->

__Logger__                                <!-- .elements class="fragment" data-fragment-index="1" -->
* Loggt auf Loglevel                      <!-- .elements class="fragment" data-fragment-index="7" -->
* Formatiert Log Messages                 <!-- .elements class="fragment" data-fragment-index="8" -->

Note:
Zwei Orte um zu konfigurieren, Logger & Environment

Environment => gelten für alle Log Statements
* Zur Laufzeit konfigurierbar 
* Appender: wohin wird geloggt?
* Logging Level: Logstatements mit tieferen Levels verwerfen
  * Logging Level zu Log_ERROR, LOG_DEBUG wird verworfen
* Kontext: Nur Log Messages von diesem Kontext aus werden geloggt
  * bsp: Grosse App aus mehreren Modulen

Logger:
* auf welchem Loglevel wird diese Message geloggt?
* Wie soll die Nachricht formatiert werden




### Konfiguration
__Environment__: Appender
* Wohin wird geloggt?

```js [1-2|4-5] 
import { addToAppenderList } from "./logger/logger.js";
import { Appender }          from "./logger/appender/consoleAppender.js";

const consoleAppender = Appender();
addToAppenderList(consoleAppender);
```

Note:
* Appender definieren für jedes Loglevel, ob und wie geloggt werden soll
* Appender hinzufügen durch globale Funktion
* jetzt werden alle Messages auf der Konsole ausgegeben




### Konfiguration
__Environment__: Logging Level
* Welche Levels werden geloggt?

```js [1-4| 6] 
import { 
  LOG_DEBUG,
  setLoggingLevel
  } from "./logger/logger.js";

setLoggingLevel(LOG_DEBUG);
```

Note:
* Aktiver LoggingLevel 
* globale Funktion `setLoggingLevel`
* Nur messages höher als Debug können geloggt werden
* => Zur Laufzeit könnte jetzt logginglevel verändert werden




## Konfiguration
__Environment__: Kontext 
 * Welche Logger dürfen loggen?

```js [1|3-4] 
import { setGlobalContext } from "./logger/logger.js";

const myLogContext = "GLOBAL.CONTEXT"
setGlobalContext(myLogContext);
```

Note:
* Aktiver Context 
* globale Funktion `setGlobalContext`
* Nur messages deren Kontext mi "GLOBAL.CONTEXT" beginnt




### Konfiguration
__Logger__: Die Funktion
```js [1|2|12|4|5-7|9-10]
const logger = loggerLevel => context => formatMsg => msg =>
  LazyIf( messageShouldBeLogged(loggerLevel)(context) )
  (Then(() =>
    appenderList.map(appender => {
        const levelName = loggerLevel(snd);
        const levelCallback = appender[levelName.toLowerCase()];
        return levelCallback(formatMsg(context)(levelName)(evalMessage(msg)))
      })
      // return True if log message has been appended to every appender
      .reduce((acc, cur) => and(acc)(cur), True)) 
  )
  (Else(() => False));
```

Note:
Hier sehen Sie die Logger Funktion
* Momentan im Highlight alle Parameter die sie nimmt
* Zeile 2: Darf die Message geloggt werden? Abgleich mit Environment 
* Zeile 4: über alle Appender iterieren 
* Zeile 5-7: die Message mit allen wichtigen Infos an appender anhängen
* Zeile 10: gibt True zurück, wenn an alle Appender erfolgreich angehängt wurde




### Verwendung
Wiederverwendbarkeit durch Partial Application!
```js [3|4|5|7-8]
const logger = loggerLevel => context => formatMsg => msg => ... ;

let debug = logger(LOG_DEBUG);
debug     = debug("ch.fhnw.ip5");
debug     = debug(formatMsg);

debug("Andri Wild");
debug("Tobias Wyss");
```

Note:
* Mit Partial Application einfach wiederverwendbar.
* Neuer Logger erstellen -> `logger` aufrufen.




### Demo
<iframe style="border: none; margin-left: 250px" width="100%" height="600" data-src="https://wildwyss.github.io/ip5-overview/contrib/p5_wild_wyss/src/logger/example/loggerExample.html" data-preload></iframe>
