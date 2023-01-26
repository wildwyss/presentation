# Logging Framework




## Kernidee
* Eine zentrale Funktion 
  * Konfigurierbar über Parameter
* Allgemeine Einstellungen auf Environment
  * Wo wird hin geloggt? 
  * Einschränken was geloggt wird 




## Konzepte
* Logging Levels `LOG_DEBUG`
* Appender
* Kontext




## Konfiguration
__Environment__
* Aktive Appender
* Aktiver Logging Level
* Aktiver Kontext

__Logger__
* Loggt auf Loglevel
* Formatiert Log Messages




## Konfiguration
__Environment__: Appender
* Wohin wird geloggt?

```js [4-5] 
import { addToAppenderList } from "./logger/logger.js";
import { Appender }          from "./logger/appender/consoleAppender.js";

const consoleAppender = Appender();
addToAppenderList(consoleAppender);
```




## Konfiguration
__Environment__: Logging Level
* Welche Levels werden geloggt?

```js [3-4] 
import { LOG_DEBUG } from "./logger.js";

setLoggingLevel(LOG_DEBUG);
const loggingLevel = getLoggingLevel();
```




## Konfiguration
__Environment__: Kontext 
 * Welche Logger dürfen loggen?

```js [3-4] 
import { setGlobalContext } from "./logger.js";

const myLogContext = "GLOBAL.CONTEXT"
setGlobalContext(myLogContext);
```



## Konfiguration
__Logger__: Die Funktion
```js [1|2|4|5-7|9-10]
const logger = loggerLevel => context => formatMsg => msg =>
  LazyIf( messageShouldBeLogged(loggerLevel)(context) )
  (Then(() =>
    appenderList.map(appender => {
        const levelName = loggerLevel(snd);
        const levelCallback = appender[levelName.toLowerCase()];
        return levelCallback(formatMsg(context)(levelName)(evaluateMessage(msg)))
      })
      // return True if log message has been appended to every appender
      .reduce((acc, cur) => and(acc)(cur), True)) 
  )
  (Else(() => False));
```




## Demo
<iframe width="100%" height="600" data-src="https://wildwyss.github.io/ip5-overview/contrib/p5_wild_wyss/src/logger/example/loggerExample.html" data-preload></iframe>
