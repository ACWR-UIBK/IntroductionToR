---
title: "Introduction to R"
output: 
  html_document:
    toc: true
date: "2023-10"
author: "By:  Thomas Marke, University of Innsbruck"
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

![](Pics/ScientificComputing.png)

## Kurzeinführung in die Datenanlyse mit R {.unlisted .unnumbered}

Dies ist eine kurze Einführung in **R für (Noch-)Nichtprogrammierer** zum Einlesen, Analysieren und Darstellen exemplarischer Daten. Das Ziel ist nicht, Euch zu perfekten R ProgrammiererInnen zu machen, sondern durch Aufzeigen einiger praktischer und einfacher Funktionen die Verwendung von Programmiersprachen/Entwicklungsumgebungen schmackhaft zu machen und etwas "die Scheu" zu nehmen diese zu verwenden!

Neben der hier dargestellten Funktionalität könnt Ihr sehr einfach weitere Informationen zum Arbeiten mit R im Internet finden, z.B. durch Verwendung der **Google Suchfunktion** und den Ergebnissen auf der Seite **stackoverflow.com** - einfach mal ausprobieren.

Die hier verwendeten Beispieldaten sind **Simulationen eines Energie-Bilanz-Schneemodels** für den Standort Col de Porte (Frankreich) für die Saison 2005/2006 sowie **Beobachtungen des Schneewasseräquivalents** für den selben Standort und Zeitraum. Informationen zur Station und den Daten findet Ihr hier:

https://essd.copernicus.org/preprints/5/29/2012/essdd-5-29-2012.pdf

Die hier verwendeten Daten können hier heruntergeladen werden:

https://www.acwr.eu/Protected/R/Data/Data_ColDePorte.zip

## 1 - Arbeitsumgebungen

Das Arbeiten mit R erfordert zunächst das **R-Basispaket**, welches für die jeweilig genutzten Betriebssysteme heruntergeladen und installiert werden muss.
Pakete für die unterschiedlichen Betriebssysteme gibt es hier: https://cran.r-project.org/

Auf die dabei installierte Funktionalität (die R-Skriptsprache) kann man über unterschiedliche **Umgebungen** zugreifen:

### R in der Konsole

Alle Betriebssysteme verfügen über eine "Konsole", in dieser kann man verscheidene Kommandos eingeben um z.B. Verzeichnisse zu wechseln. 

Befehl `R`: direktes Ausführen von R-Befehlen in der Konsole

Befehl `Rscript myscript.R`: Ausführen bestehender Skripte, hier "myscript.R"

### R im Jupyter Notebook

Das Jupyter Notebook stellt eine übersichtliche Oberfläche zum Arbeiten in R dar, ist aber was die Datenverabreitung und den Funktionsumfang angeht in mancher Hinsicht etwas limitiert.

### RStudio

RStudio ist die wohl am meisten verwendete Umgebung: https://www.rstudio.com/products/rstudio/download/

Hier kann man Code schreiben, Pakete installieren, Variablen bequem einsehen und Plots betrachten. **Wir arbeiten in R-Studio**, macht es doch gleich mal auf und öffnet ein **neues Skript "Introduction.R"** das Ihr im **Ordner "R-Workspace"** auf Eurem Rechner speichert. 

Die **Daten der Station "Col de Porte"** (Frankreich) ladet Ihr auch gleich herunter und legt diese im gleichen Ordner ab!

## 2 - Grundlegendes

### Programmablauf

Ein R-Script wird Zeile für Zeile von oben nach unten ausgeführt. So können **Variablen** (z.B. `Name`) mit **Werten** (z.B. `Alex`) gefüllt werden und für numerische Variablen Berechnungen durchgeführt werden.

### Kommentare

In jeder Programmiersprache ist es wichtig den **Code** (die Befehlsabfolge) von **Kommentaren** (Erläuterungen die ein Lesen des Codes vereinfachen und den Inhalt für Andere nachvollziehbar machen) zu trennen. Kommentare können im R-Code durch `#` eingeleitet werden - diese Teile werden dann nicht ausgeführt, sondern sind nur für den Entwickler von Wert. Uns ist das Kommentieren sehr wichtig, da es den LV-Leitern ermöglicht Euren Code zu lesen und zu verstehen - bitte kommentiert doch deshalb Euren Code zur besseren Nachvollziehbarkeit - das hilft auch dabei vor langer Zeit geschriebene Skripte wieder verstehen/verwenden zu können.

Unten sehr Ihr ein Beispiel für einen Kommentar:

```{r}
# Hello ausgeben
print('Hello')
```

### Ausführen von Code

Code kann in R **zeilenweise**, für **Bereiche** oder für das **gesamte Skript** ausgeführt werden - hierfür gibt es fest definierte **Shortcuts**:

Ausführen der aktutellen Zeile/eines markierten Bereiches: `CTRL & Enter`

Ausführen des gesamten Skriptes: `Shift & CTRL & s`

### Variablen

In der Programmierung arbeitet man mit "Variablen" die durch "Operationen" miteinander verarbeitet werden. So kann man einer frei zu definierenden Variablen einen Wert zuweisen und diese Variable dann mit einer anderen verrechnen. 

Die **Wertzuweisung** erfolg in R durch `<-` oder `=`

```{r}
# Erste Berechnungen
apples = 11
oranges = 4
fruits = apples + oranges
```

Schreiben wir den Namen der Variablen in eine Zeile und führen diese Zeile aus wird der Wert der Variable ausgegeben:

```{r}
# Wert ausgeben
fruits
```

Wir können uns den **Typ** einer Variablen durch `class()` anzeigen lassen.

In diesem Fall ist es eine Variable vom Typ `numeric`, also eine Zahl. Neben Zahlen gibt es zum Beispiel noch `character` Variablen, diese enthalten eine Zeichenfolge. "15" könnte also sowohl eine numerische Variable sein, aber auch eine Zeichenfolge - mit Zeichenfolgen kann man aber natürlich nicht rechnen, es empfiehlt sich bei Problemen im workflow immer mal den Typ einer Variablen (v.a. bei Zahlen) zu checken, das erspart oft viel Kopfzerbrechen:

```{r}
# Klasse ausgeben
class(fruits)
```

Der Befehl `str()` gibt uns Information über die **Struktur** unserer Daten.

In diesem Fall ist das nur die Information, das es sich um eine Zahl mit dem Wert 15 handelt. Wir werden später mit `DataFrames` arbeiten, hier können unterschiedliche Spalten unterschiedliche Typen (z.B. Zahl, Zeichenfolge) haben.

```{r}
# Struktur ausgeben
str(fruits)
```

### Einbinden von Bibliotheken (Libraries)

Während viele Befehle zur Standardfunktion von R gehören, erfordern einige Operationen **Zusatzfunktionalität**, welche in Form von **Bibliotheken** eingebunden werden kann. 

Entsprechende Bibliotheken können in RStudio im Fenster rechts unten durch `Packages-->Install` installiert werden, oder direkt als R-Code durch den Befehl `install.packages("Paketname")`.

Wir installieren als Beispiel die Bibliothek `this.path`, die uns später den Umgang mit Arbeitsverzeichnissen erleichtert

![](Pics/InstallPackages.png)

Um das Paket im Code verwenden zu können, muss der Befehl `library()` in Zusammenhang mit dem Namen der einzubindenden Bibliothek eingeben werden. Wir binden Testweise die Library `this.path` ein:

```{r}
library("this.path")
```

In R arbeitet man oft mit vordefinierten **Funktionen** die in Bibliotheken definiert sind. Will ich Hilfe zu einer solchen Funktion, hilft Aufruf von `help(Funktionsname)`. Wir testen das anhand der Mittelwertsfunktion `mean()`:

```{r}
help(mean)
```

### Das Arbeitsverzeichnis

Habe ich irgendwo ein R-Skript angelegt, so ist es oft praktisch das Arbreitsverzeichnis auf den Ordner mit diesem Skript zu setzen. Da Daten in R standardmäßig (soweit nicht mit absolutem Pfad definiert) im Arbeitsverzeichnis gesucht werden, kann ich auf Daten die direkt im Arbeitsverzeichnis leigen ohne Angabe eines Pfads nur über den Dateinamen zugreifen. Liegen Daten in einem Unterverzeichnis des Arbeitsverzeichnisses, dann muss ich diesen Ordner relativ zum Arbeitsverzeichnis schon noch angeben.

Das Arbeitsverzeichnis kann durch den Befehl `setwd("/MeinOrdner")` im R-Code gesetzt werden. Alternativ kann in RStudio der aktuell angezeigte Ordner im Fenster rechts unten als Arbeitsverzeichnis gesetzt werden `Files-->More-->Set As Working Directory`.

![](Pics/SetWorkingDirectory.png)

Durch den Befehl `getwd()` kann ich mir das aktuelle Arbeitsverzeichnis anzeigen lassen.

```{r}
getwd()
```

Die eben installierte Bibliothek `this.path` ist in diesem Zusammenhang besonders praktisch - sie ermöglicht es den Pfad in einem R-Skript automatisch direkt auf den Pfad des Skriptes zu setzen. So muss ich mir über die Lage meines R-Skriptes/Ordners auf meinem Rechner keine Gedanken machen, solange alle benötigten Daten im gleichen Ordner liegen.

```{r,eval=FALSE}

# Bibliothek laden
library("this.path")

# Pfad des Skriptes auslesen und als Arbeitsverzeichnis setzen
script_path = this.path()
setwd(dirname(script_path))
```

## 3 - Einlesen von Daten

Das Einlesen tabellarischer Daten in R ist sehr einfach. Durch die Funktion `read.table()` können tabellarische Daten in unterschiedlichen Formaten eingelesen werden. Man gibt hierfür den **Namen** in "", das **Trennungszeichen** (z.B. `sep=","`) sowie die Information darüber, ob ein **Header** (eine vorangehende Nichtdatenzeile mit Spaltennamen) existiert an (z.B. `header=TRUE`). Weiter kann ich angeben, welches **Dezimaltrennzeichen** in meinen Daten verwendet wird (z.B. `dec = "."`). Mit dem Argument `skip=` könnte man noch angeben, dass eine bestimmte Anzahl an **Zeilen übersprungen** werden soll, z.B. wenn in den ersten Zeilen unnötige Zusatzinformation enthalten ist.

Wir testen das mal mit einer Datei die Meteorologische Modellinputs sowie eine Vielzahl von Modellautputs enthält.
Die Datei sollte bereits im Arbeitsverzeichnis liegen und heisst `ModelOutput.csv`.

**Tipp:** 

Schaut Euch tabellarischen Daten immer zunächst im Texteditor Eurer Wahl (Windows: Notepad, Mac: TextEdit, oder einfach in RStudio) an. So seht Ihr wie die Daten aussehen (Spalten, Header, Trennzeichen, etc.)!

Optionen für Trennzeichen `sep=""`:

* Komma --> `","`
* Strichpunkt --> `";"`
* Tabulator --> `"\t"` 
* Kein Zeichen (white space) --> `""`

```{r}
# Daten einlesen
input_file = "ModelOutput.csv"
input_data = read.table(input_file, sep=",", dec = ".", header=TRUE)
```

### Datenstruktur

Die eingelesenen Daten befinden sich nun im Speicher des Rechners als Werte der Variaben `input_data` und wir können uns diese Daten einmal ansehen. Der Befehl `names(input_data)` zeigt uns alle Spaltennamen an!

**Tipp:**

Unter Verwendung der Funktion `setNames(NameDataFrame,c("Spaltenname1","Spaltename2",...))` kann man die Spalten jederzeit umbenennen (machen wir später, hier aber gerade nicht nötig).

```{r}
# Spaltennamen ausgeben
names(input_data)
```

Frage ich die Klasse der Variablen `input_data` ab, so wird diese als `data.frame` angezeigt. **DataFrames** sind sehr ähnlich einer Excel Tabelle mit unterschiedlichen Zeilen und Spalten. Neben den DataFrames gibt es viele andere Formate (z.B. das xts Format) die alle Ihre Vorteile und evtl. leicht andere Befehlssyntax haben - aber bleiben wir bei unserem DataFrame...

```{r}
# Klasse ausgeben
class(input_data)
```

Den gesamten Inhalt der Daten kann ich mir leicht ansehen, ich muss dazu nur **alle Werte der Variablen ausgeben**. Das mache ich indem ich die Variable ohne weiteren Befehl ausführe.

Wir könnten diese Zeile nach dem Anschauen unserer Daten im Code auch mit `#` auskommentieren, damit der Output unseres Skriptes nicht unnötig unübersichtlich wird :-)

```{r}
# Alle Daten ausgeben
#input_data
```

Will ich mir nur **die ersten 10 Zeilen** `n=10` ansehen, kann ich die Funktion `head()` einsetzen! Wir sehen hier einen Fehlwert ("Not Available" = `NA`) in der Zeitreihe.

```{r}
# Header (erste 10 Zeilen) ausgeben
head(input_data, n=10)
```

Ich kann die **einzelnen Spalten der Variable ansprechen**, indem ich das `$` Zeichen verwende und den Spaltennamen angebe! Wir testen das mit einem einfachen Ausdrucken der Werte für die Stunde, wieder nur für die ersten 10 Zeilen!

```{r}
# Header einer Spalte ausgeben
head(input_data$Hour, n=10)
```

### Datenstatistik

Oft interessiert uns die Statistik der Daten, z.B. der Mittelwert oder die Standardabweichung - diese Information kann man sich über den Befehl `summary` ausgeben lassen! Wir sehen wieder die Information über enthaltene Fehlwerte `NA` in der Datenreihe.

```{r}
# Zusammenfassung ausgeben
summary(input_data)
```

## 4 - Linien und Balkendiagramme

Einfache Diagramme (= Plots) zu erstellen ist in R relativ einfach. Es gibt viele Plotting Bibliotheken (z.B. `ggplot2`), wir wollen mit der **Standard Plottingfunktion** `plot()` arbeiten, da diese für Einsteiger leichter zu verstehen ist.

Für Fortgeschrittene ist das Plotten mit `ggplot2` eine tolle Alternative, da die Plots hier oft ohne viel Aufwand schöner werden, im Internet gibt es hierzu tolle Tutorials, einfach mal googeln :-)

Wir erstellen nun unseren ersten Plot und überlassen so gut wie alles der `plot()` Funktion, d.h. wir geben ausser den X-Werten und Y-Werten keine Argumente mit an die Funktion. Testweise plotten wir die Lufttemperatur `AirTemp` gegen den Index `X`:

```{r}
# Lufttemperatur plotten
plot(input_data$X, input_data$AirTemp)
```

Das funktioniert schonmal, allerdings hat dieser Plot noch einige Mängel die wir nun anpassen wollen.

Um unsere Zeitreihe auf der X-Achse gut darstellen zu können, generieren wir nun eine **Zeitinformation** in unserem `DataFrame` (wir nennen die neue Spalte `DateTime`) **aus den Spalten für Jahr, Monat, Tag und Stunde**. Um diese Zeitinformation zusammenzustellen verwenden wir die R-Funktion `paste()` - sie ermöglicht das kombinieren von Text und Variablenwerten.

**Wichtig:**

Variablen werden hier durch Komma getrennt angegeben, dabei ist reiner Text in Anführungszeichen zu setzen, ganz am Ende wird nach einem abschliessenden Komma mit `sep=''` definiert wie die Einzeilteile zu trennen sind (hier ohne Inhalt weil wir keine automatsiche Trennung, z.B. durch Leerzeichen wollen, diese fügen wir lieber selbst ein).

```{r}
# Spalte DateTime erzeugen
input_data$DateTime = paste(input_data$Year,'-',input_data$Month,'-',input_data$Day,' ',input_data$Hour,sep='')
```

Wir sehen uns nun mit `head()` und `str()` einmal an was in der Spalte `DateTime` abgelegt wurde:

```{r}
# Header ausgeben
head(input_data$DateTime, n=10)
```

```{r}
# Struktur ausgeben
str(input_data$DateTime)
```

Noch ist unsere **Zeitinformation eine Zeichenfolge**, wir transformieren diese nun in eine **POSIX Zeitinformation**, dabei geben wir das Format mit, in dem unsere Zeichenfolge vorliegt, mit der Funktion `head()` geben wir uns gleich die ersten Zeilen aus: 

```{r}
# In Zeitinformation transformieren und Header ausgeben
input_data$DateTime = as.POSIXct(input_data$DateTime,format="%Y-%m-%d %H")
head(input_data$DateTime, n=10)
```

Nun plotten wir unsere Zeitreihe nocheinmal, diesmal die Lufttemperatur gegen unsere neue Zeitinformation:

```{r}
# Lufttemperatur plotten
plot(input_data$DateTime, input_data$AirTemp)
```

Wir sehen, dass die plot-Funktion mit der Zeitinformation gut umgehen kann, ohne weitere Eingriffe werden in der X-Achse die Monate dargestellt.

Um weitere Mängel zu korrigieren plotten wir die Daten erneut - diesmal geben der `plot()` Funktion noch ein paar Informationen mehr mit, z.B.

1) dass wir nur **Linien**, keine Punkte darstellen wollen --> `type="l"`,

2) dass wir gerne eine **rote Linie** hätten --> `col="red"` und

3) dass wir die **Beschriftung der Achsen** gerne selbst übernehmen --> `ann=FALSE`.

```{r}
# Lufttemperatur plotten
plot(input_data$DateTime, input_data$AirTemp, type="l", col="red", ann=FALSE)
```

Weitere Optionen für die Darsttellung der Daten `type=""`:

* `type=”l”` --> nur Linien
* `type=”p”` --> nur Punkte
* `type=”b”` --> beides
* `type="h"` --> vertikale Linien = Balken
* `type="n"` --> nichts

Weiter Farboptionen `col=""`:

* `red`
* `blue`
* `black`
* `...`

Einen schönen Überblick über die in R standardmäßig (es gibt viele Erweiterungspakete) verfügbaren Farben findet Ihr unter: http://www.stat.columbia.edu/~tzheng/files/Rcolor.pdf

Nun wollen wir unseren Plot wie folgt erweitern:

1) als **zweite Zeitreihe** soll die simulierte Schneetemperatur `input_data$SnowTemp` hinzugefügt werden

2) ein ***Titel**, **Beschriftungen für die X- und Y-Achse** sowie eine **Legende** soll hinzugefügt werden

3) wir wollen ein **Grid** hinter die Zeitreihen legen

* Zweite Zeitreihe:

  Wir fügen diese durch Aufruf von `lines()` hinzu und verwenden das Attribut `lty` um den Linetype (Linientyp) zu definieren. Wir geben der Lufttempertur den Stil `solid` (-) und der Schneetemperatur den Stil `twodash` (--). Beachtet, dass wir die Linientypen auch in der Legende angeben müssen, die Angaben erfolgen hier in Form eines Vektors `c()` mit den beiden Linientypen. Als Farben wählen wir `red` und `blue.`

* Titel:

  Wird eingefügt durch die Funktion `title()`, sollte der Text zu lang sein kann man mit `\n` eine neue Zeile einleiten!

* Legende:

  Diese wird durch `legend()` eingefügt, für die Legende gibt es verschiedene Platzierungsoptionen: `"bottomright"`, `"bottom"`, `"bottomleft"`, `"left"`, `"topleft"`, `"top"`, `"topright"`, `"right"` and `"center"`

  Durch Angabe eines Versatzes `inset=""` in Prozent des Achsenbereichs sorgt man dafür, dass die Legende schön positioniert ist!

* Grid:

  Hier verwenden wir die Funktion `grid()`, der wir einen Linientyp `lty`, eine Farbe `col` und eine Breite `lwd` mitgeben. Wir setzen `nx` und `ny` auf `NULL`, wenn wir eine der beiden Achsen ohne Grid-Linien anzeigen wollten, würden wir diese auf `NA` setzen.

**Tipp:**

Unterschiedliche Linientypen `lty=""`:

* `twodash`
* `longdash`
* `dotdash`
* `dotted`
* `dashed`
* `solid`
* `blank`

Diese können auch über Nummern angesprochen werden, wollt Ihr mehr über linetypes wissen besucht: http://www.sthda.com/english/wiki/line-types-in-r-lty

```{r}
# Unser ursprünglicher Plot von oben, erweitert um die Angabe des Linientyps
plot(input_data$DateTime, input_data$AirTemp, type="l", col="red", ann=FALSE, lty='solid')

# Zweite Zeitreihe SnowTemp hinzufügen
lines(input_data$DateTime, input_data$SnowTemp, type="l", col="blue", lty='twodash')

# Diagrammtitel hinzufügen
title(main="Lufttemperatur und simulierte Schneetemperatur \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Monat")
title(ylab="Temperatur (K)")

# Grid hinzufügen
grid(lty = 2, col = "gray", lwd = 1)

# Legende hinzufügen, leichten Versatz angeben
legend("topleft", inset=.05, c("Lufttemperatur","Schneetemperatur"), col=c("red","blue"), lty=c('solid','twodash'))
```

Wir wollen nun noch den Niederschlag als **Balkendiagramm** in blau plotten. Da wir am Gesamtniederschlag interessiert sind und in unseren Daten fester `SolPrecip` und flüssiger Niederschlag `LiqPrecip` getrennt vorliegen, addieren wir diese zunächst in einer neuen Spalte `Precip`. Dann plotten wir den Niederschlag unter Verwednung des Darstellungstypes `h` (`type="h"`).

```{r}
# Flüssigen und festen Niederschlag in neuer Spalte zu Gesamtniederschlag addieren
input_data$Precip = input_data$LiqPrecip + input_data$SolPrecip

# Niederschlag plotten
plot(input_data$DateTime, input_data$Precip, type="h", col="blue", ann=FALSE)

# Diagrammtitel hinzufügen
title(main="Niederschlag \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Monat")
title(ylab="Stündlicher Niederschlag (mm)")
```

Als nächstes wollen wir einen **Dichteplot** erzeugen, der uns zeigt, wie der Niederschlag über den Wertebereich verteilt ist. Hierzu verwenden wir erneut die `plot()` Funktion, berechnen uns aber mit der Funktion `density()` zunächst die Dichteverteilung `density_Precip`, die wir einfach einmal ausgeben um uns die Berechnungen einmal anzusehen:

```{r}
# Dichtefunktion berechnen und ausgeben
density_Precip = density(input_data$Precip)
density_Precip
```

Nun wollen wir uns die berechnete Dichtefunktion `density_Precip` im Plot durch eine blaue Linie (`col="blue"`) darstellen, wieder wollen wir Titel und Achsenbeschriftung selbst definieren (`ann=FALSE`).

```{r}
# Plot erstellen
plot(density_Precip, col="blue", ann=FALSE)

# Diagrammtitel hinzufügen
title(main="Dichtefunktion des Niederschlags \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Niederschlag (mm)")
title(ylab="Dichte")
```

Wir fügen nun auch den festen Niederschlag hinzu, diesmal in einer exotischeren Farbe, `darkturquoise`

```{r}
# Ursprünglicher Plot für den festen Niederschlag
plot(density_Precip, col="blue", ann=FALSE)

# Festen Niederschlag hinzufügen, vorher Dichteverteilung berechnen
density_SolPrecip <- density(input_data$SolPrecip)
lines(density_SolPrecip, col="darkturquoise")

# Diagrammtitel hinzufügen
title(main="Dichtefunktion des Niederschlags \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Niederschlag (mm)")
title(ylab="Dichte")
```

Da ist die zweite Linie wohl etwas über das Ziel hinaus geschossen. Das liegt daran, dass unser erster `plot()` Aufruf die Y-Werte auf den kleineren Wertebereich optimiert hat. Also versuchen wir es nochmal, diesmal **begrenzen wir den Wertebereich der X- und Y-Achse** durch die Argumete `xlim` und `ylim`. Die Angaben erfolgen hier in Form eines Vektors `c()` mit den Minimal- und Maximalwerten. Grid und Legende fügen wir auch gleich hinzu (beachtet, dass unser Grid zuerst hinzugefügt wird, sonst liegt es über der Legende):

```{r}
# Ursprünglicher Plot für den festen Niederschlag
plot(density_Precip, xlim=c(0,12), ylim=c(0,6), col="blue", ann=FALSE)

# Festen Niederschlag hinzufügen, vorher Dichteverteilung berechnen
density_SolPrecip <- density(input_data$SolPrecip)
lines(density_SolPrecip, col="darkturquoise")

# Diagrammtitel hinzufügen
title(main="Dichtefunktion des Niederschlags \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Niederschlag (mm)")
title(ylab="Dichte")

# Grid hinzufügen
grid(lty = 'dotted', col = "gray", lwd = 1)

# Legende hinzufügen
legend("topright", inset=.05, c("Niederschlag","Flüssiger Niederschlag"), col=c("blue","darkturquoise"), lty=c("solid","solid"))
```

## 5 - Subsets aus den Daten auswählen

Manchmal will man nur mit einem **Zeitbereich in *einer Datenreihe** arbeiten. Dann kann man auch Zeiträume extrahieren und am besten einer anderen Variablen zuordnen - so verlieren wir nicht unsere ursprünglichen Daten. 

Das Auswählen von Daten aus einer Datenreiche kann über unterschiedliche Wege erfolgen:

1) Über den **Index** (z.B. Zeile 5-20)

2) Über eine **Abfrage der Inhalte** (z.B. Datum X - Y)

3) Über den **Namen einer Spalte**

Wir testen die Ansätze an einigen Beispielen unter Verwendung unseres eingelesenen Datensatzes `input_data`.

Zunächst wollen wir alle Spalten des DataFrames, aber **nur die Zeilen 25 - 48 auswählen** und in einen neuen DataFrame `index_subset` schreiben, wir schauen diesen gleich mit `head()` an:

```{r}
# Bereich über den Index ausschneiden und Header ausgeben
index_subset = input_data[25:48,]
head(index_subset, n=50)
```

Das hat gut geklappt, aber **was bedeutet die fehlende Angabe nach dem Komma?**

Unser DataFrame ist in Zeilen und Spalten organisiert, die erste Dimension beinhaltet die Zeilen, hier haben wir mit `25:48` einen Bereich gewählt, die zweite Dimension die Spalten, hier haben wir keine Angabe gemacht, somit wurden alle Spalten gewählt!

Im Beispiel haben wir alle Stunden des 02.10.2005 ausgeschnitten! Aber natürlich muss ich hierzu vorher den zugehörigen Indexbereich kennen.

Um unabhängig von den Indizes ein Zeitfenster auszuwählen kann ich auch den **Zeitraum definieren**. Das Datum setzen uns wieder mit der paste-Funktion aus `year`, `month` und `day` zusammen und transformieren das Ergebnis dann gleich wieder in ein Datum:

```{r}
# Datumsspalte erzeugen
input_data$Date = paste(input_data$Year,'-',input_data$Month,'-',input_data$Day,sep='')
input_data$Date = as.Date(input_data$Date)

# Bereich über Datum ausschneiden und Header ausgeben
time_subset = input_data[input_data$Date>"2005-10-01" & input_data$Date<"2005-10-03",]
head(time_subset, n=50)
```

Um nun **bestimmte Variablen** aus dem `DataFrame` auszuwählen, kann ich diese bei der Auswahl wie folgt ansprechen (hier am Beispiel des Schneewasseräquivalents `SWE`), unsere Zeitinformation `DateTime` nehmen wir gleich mit:

```{r}
# Bereich über Spaltennamen auswählen
variable_subset = input_data[,c("DateTime","SWE")]
head(variable_subset, n=50)
```

## 6 - Daten aggregieren

Oft liegen Daten zeitlich feiner aufgelöst (z.B. als Stundenwerte) vor als wir sie bräuchten (z.B. Monatswerte). Um die Daten zeitlich zu aggregieren, braucht es ein **Zeitkriterium** anhand dessen aggregiert werden kann, z.B. eine Spalte die nur Jahre- und Monatsinformation enthält - ich kann dann z.B. den Mittelwert oder die Summe über dieses Kriterium berechnen.

Wir testen das anhand unserer Niederschlagsdaten, dafür fügen wir unserem `DataFrame` eine Spalte hinzu, die nur Jahr und Monat enthält und verwenden die Funktion `yearmon()` des Paketes `zoo` um diese Zeichenfolge in eine Zeitinformation zu transformieren:

```{r}
# Bibliothek einbinden
library(zoo)

# Spalte mit Jahr und Monat erstellen
input_data$YearMonth = paste(input_data$Year,'-',input_data$Month,sep='')
input_data$YearMonth = as.yearmon(input_data$YearMonth,format="%Y-%m")

# Header ausgeben
head(input_data$YearMonth, n=10)
```

Nun verwenden wir die `aggregate()` Funktion um die **Niederschlagssumme für die Monate** zu berechnen, das Ergebnis schauen wir gleich mit `head()` an:

```{r}
# Monatliche Niederschläge berechnen
monthly_Precip <- aggregate(input_data$Precip,FUN = sum,by = list(Group.date = input_data$YearMonth))

# Header ausgeben
head(monthly_Precip, n=10)
```

Die **Spaltenüberschriften** passen wir noch so an, dass man auch weiss was hier enthalten ist! Wir verwenden hierzu die Funktion `setNames()`: 

```{r}
# Spaltennamen definieren
monthly_Precip = setNames(monthly_Precip,c("Month","Precip"))

# Header ausgeben
head(monthly_Precip, n=10)
```

Die hier erhaltenen Monatswerte stellen wir nun als Balkendiagramm in blau dar. Verwendet dabei den Typ `type="h"` sowie das Argument `lwd` um die Dicke Eurer Balken anzupassen:

**Tipp:**

Die Farbe kann wie gewohnt einfach unter Angabe einer Farbe gesetz werden (`col="blue"`) oder über einen RGB Wert definiert werden:

`col=rgb(0,0,0,alpha=0.3)`

Diese Option bietet auch die Möglichkeit einen Transparenzwert `alpha` zu definieren, allerdings ist aufzupassen, da RGB Werte in der Regel einen Bereich von 0-255 haben, hier aber eine Intensität von 0-1 eingesetzt werden muss! Man muss die RGB-Werte falls im 0-255er Wertebereich vorliegend, also normieren, d.h. durch den Maximalwert teilen:

Für die Farbe blau heisst das: `rgb(0,0,255)` --> `rgb(0/255,0/255,255/255)` 

Eine Übersicht über verschiedene Farben und deren RGB Werte findet Ihr unter http://www.farb-tabelle.de/de/farbtabelle.htm!

```{r}
# Monatlichen Niederschlag plotten
plot(monthly_Precip$Month, monthly_Precip$Precip, type="h", col=rgb(0/255,0/255,255/255, alpha=0.5), ann=FALSE, lwd=20)

# Diagrammtitel hinzufügen
title(main="Monatlicher Niederschlag \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Monat")
title(ylab="Niederschlag (mm)")
```

Der Plot sieht soweit ganz gut aus, lediglich die Zeitachse ist noch eine Mischung aus Monat und Jahr - R tut das um uns den Jahreswechsel zu zeigen, aber das sieht nicht so schön aus. Wir werden die Formatierung der Zeitachse also selbst in die Hand nehmen, dafür geben wir in unserem plot-Aufruf den Parameter `xaxt="n"` mit so dass zunächst keine Achsenbeschriftung erfolgt, dann fügen wir am Schluss ein eigenes Axen-Element mit entsprechend formatierter Zeitinformation über den Befehl `axis()` hinzu: 

```{r}
# Monatlichen Niederschlag plotten
plot(monthly_Precip$Month, monthly_Precip$Precip, type="h", col=rgb(0/255,0/255,255/255, alpha=0.5), xaxt = "n", ann=FALSE, lwd=20)

# Diagrammtitel hinzufügen
title(main="Monatlicher Niederschlag \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Monat")
title(ylab="Niederschlag (mm)")

# Add dates to x-axis
axis(1,monthly_Precip$Month,format(monthly_Precip$Month, "%Y-%m"))
```

## 7 - Scatterplots

Scatterplots (deutsch: Streudiagramme) ermöglichen es den **Zusammenhang zweier Größen** darzustellen. Dabei wird die abhängige Variable (Y) als Funktion der unabhängigen Variable (X) dargestellt.

Wir wollen nun Scatterplots auf Basis simulierter und beobachteter Schneegrößen erstellen - diese Art der Auswertung stellt eine wichtige Säule in der **Evaluation von Modellergebnissen** dar.

Wir lesen dazu beobachte Werte des Schneewasseräquivalents zum Vergleich mit den Simulationen ein - diese Daten befinden sich in der Datei `Observations.txt` im Arbeitsverzeichnis.

Schaut Euch die Daten zunächst im Editor an und versucht den Lesebefehl richtig zu konfigurieren, ohne unten nachzusehen!

```{r}
# Beobachtungsdaten einlesen
observation_file = "Observations.txt"
daily_observed_SWE = read.table(observation_file, sep="", dec = ".", header=TRUE)
```

Wir sehen uns das Ergebnis des Einlesens mit `head()` an: 

```{r}
# Header ausgeben
head(daily_observed_SWE, n=10)
```

Wir sehen dass alles geklappt hat, allerdings liegen die Beobachtungen als Tageswerte vor - wir müssen also zunächts die **Simulationen auf Tageswerte aggregieren**. Dafür verwenden wir wieder die `aggregate()` Funktion zusammen mit unserem vorhin erzeugten Datum:

```{r}
# Stündliche SWE Simulationen auf Tageswerte aggregieren 
daily_simulated_SWE <- aggregate(input_data$SWE,FUN = mean,by = list(Group.date = input_data$Date))
```

Ein Blick auf das Ergebnis:

```{r}
# Header ausgeben
head(daily_simulated_SWE, n=60)
```

Das Ergebnis schaut gut aus, wieder sind die **Spaltenbeschriftungen** nicht sehr aussagekräftig, wir ändern diese deshalb unter Verwendung der `setNames()` Funktion:

```{r}
# Spaltenbeschriftung anpassen
daily_simulated_SWE = setNames(daily_simulated_SWE,c("Date","SWE"))
```

Wir schauen kurz auf die Anzahl der Messungen und Simulationen, in unserem Fall sollten diese beiden Zeitreihen gleich lag sein, wäre das nicht so müssten wir einen Überlapppungszeitraum verwenden! Wir verwenden hierzu die Funktion `nrow()`, welche die **Anzahl der Zeilen** eines `DataFrames` ausgibt:

```{r}
# Anzahl der Zeilen ausgeben
nrow(daily_simulated_SWE)
nrow(daily_observed_SWE)
```

Die beiden Zeitreihen sind gleich lang (auch wenn das nicht unbedingt heisst, dass die Tage die gleichen sind), **wir erstellen uns nun eine neue Liste** mit den SWE Beobachtungen und Simulationen, nur der Übersichtlichkeit wegen: 

```{r}
# Liste mit Beobachtungen und Simulationen anlegen
scatter_input = NULL
scatter_input$Observed_SWE = daily_observed_SWE$SWE
scatter_input$Simulated_SWE = daily_simulated_SWE$SWE

# Struktur ausgeben
str(scatter_input)
```

Diese Liste übergeben wir nun an die `plot()` Funktion, dabei plotten wir die Beobachtungen auf die X-Achse und die Simulationen auf die Y-Achse. Dabei können wir Vieles anwenden, das wir eben über das Formatieren von Plots gelernt haben:

```{r}
# Scatterplot erzeugen
plot(scatter_input$Observed_SWE, scatter_input$Simulated_SWE, type="p", col="black", ann=FALSE)

# Diagrammtitel hinzufügen
title(main="Simuliertes vs. beobachtetes Schneewasseräquivalent \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Beobachtetes SWE (mm)")
title(ylab="Simuliertes SWE (mm)")

# Grid hinzufügen
grid(lty = 'dotted', col = "gray", lwd = 1)
```

Unser Scatterplot schaut schon ganz gut aus, ein paar Details wollen wir aber noch ändern:

1) Bei einem Scatterplot muss der **Wertebereich der X- und Y-Achse** immer gleich sein, nur so wäre das perfekte Modell eine Linie im 45 Grad Winkel!

2) Wir wollen den **Wertebereich auf minimal 0 umstellen**, negative SWE-Werte gibt es nicht und somit brauchen wir auch keinen Bereich < 0

3) Die **Kreissymbole** wollen wir größer machen und auch füllen

Den Wertebereich können wir mit den bereits bekannten Parameter `xlim` bzw. `ylim` anpassen, damit ist sicher gestellt, dass X- und Y-Achse gleich skaliert sind. 

**Merke: **

Wenn wir später unseren Plot speichern, stellen wir durch Wahl einer Höhe und Breite sicher, dass unser Plot bei gleicher X- und Y-Skalierung dann auch quadratisch ist, also dass das Verhältnis 1:1 sichergestellt ist. Wenn wir in RStudio selbst plotten, ist das Grafikfenster "Plots" je nach Rechner/Bildschirm unterschiedlich groß (wir können dieses ja sogar größer und kleiner ziehen, was den Plot neu skaliert). Wenn wir auch hier in der Polt-Ansicht in jedem Fall wollen, dass unser Plot in einem Achsenverhältnis 1:1 dargestellt wird, können wir das durch das Setzen von `par(pty="s")` for dem Plot Befehl tun. Alternativ gibt es einen Parameter `asp=`, wenn wir diesen im Plotaufruf auf 1 setzen, wird das Verhältnis zwischen X- und Y-Achse auf 1 gesetzt, aber dieser Parameter ignoriert unsere `xlim` bzw. `ylim` Einstellungen und ist somit hier nicht hilfreich.

Die **Art des Symbols** können wir über den Parameter `pch` einstellen. Folgende Optionen sind hier möglich (wollt Ihr diese Symbole als Grafik sehen oder mehr über den Umgang mit diesen erfahren besucht: https://r-charts.com/base-r/pch-symbols/):

* `pch = 0`,square
* `pch = 1`,circle
* `pch = 2`,triangle point up
* `pch = 3`,plus
* `pch = 4`,cross
* `pch = 5`,diamond
* `pch = 6`,triangle point down
* `pch = 7`,square cross
* `pch = 8`,star
* `pch = 9`,diamond plus
* `pch = 10`,circle plus
* `pch = 11`,triangles up and down
* `pch = 12`,square plus
* `pch = 13`,circle cross
* `pch = 14`,square and triangle down
* `pch = 15`, filled square
* `pch = 16`, filled circle
* `pch = 17`, filled triangle point-up
* `pch = 18`, filled diamond
* `pch = 19`, solid circle
* `pch = 20`,bullet (smaller circle)
* `pch = 21`, filled circle blue
* `pch = 22`, filled square blue
* `pch = 23`, filled diamond blue
* `pch = 24`, filled triangle point-up blue
* `pch = 25`, filled triangle point down blue
    
Die **Größe des Symbols** kann über `cex` eingestellt werden, wobei der Wert 1 den Standard repräsentiert, größere (z.B. 1.5) oder kleinere (z.B. 0.5) Werte vergrößern/verkleinern entsprechend.
 
```{r}
# Scatterplot erzeugen
par(pty="s")
plot(scatter_input$Observed_SWE, scatter_input$Simulated_SWE, xlim=c(0,600), ylim=c(0,600), type="p", pch = 19, cex=1.2, col="black",ann=FALSE)

# Diagrammtitel hinzufügen
title(main="Simuliertes vs. beobachtetes Schneewasseräquivalent \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Beobachtetes SWE (mm)")
title(ylab="Simuliertes SWE (mm)")

# Grid hinzufügen
grid(nx = NULL, ny = NULL, lty = 'dotted', col = "gray", lwd = 1)
```

Um den Zusammenhang zwischen Simulationen und Beobachtungen statistisch zu beschreiben, braucht es (hier) eine **lineare Regressionsfunktion**. Diese wollen wir uns im Folgenden näher ansehen.

## 8 - Lineare Regression

Die lineare Regression versucht einen Y-Wert in linearer Abhängigkeit eines X-Wertes zu berechnen. 

Heraus kommt eine Regressionsfunktion: 

`y = Achsenabschnitt + Steigung * x = b + m * x`

Solche **Regressionsfunktionen** kommen zum Beispiel bei **Streudiagrammen** (wie hier) oder bei **Trendanalysen** in Klimawandelstudien zum Einsatz. In Letzteren versucht man damit die Veränderung einer abhängigen Variablen (z.B. der Temperatur, Y-Achse) in Abhängigkeit einer unabhängigen Variablen (den Jahren, X-Achse) zu untersuchen. 

Um die **lineare Beziehung** zwischen Simulationen und Beobachtungen herzuleiten verwenden wir die Funktion `lm()` (linear model) und übergeben dieser zunächst die Y-Werte (die Simulationen) und dann die X-Werte (die Beobachtungen). Die Ergebnisse schreiben wir in die Variable `fit_model`:

```{r}
# Lineare Regression berechnen
fit_model = lm(scatter_input$Simulated_SWE ~ scatter_input$Observed_SWE)
```

Durch diesen Aufruf haben wir eine Variable `fit_model` definiert, die alle Information zur berechneten Regression enthält. Die Koeffizienten (Achsenabschnitt = Intercept) und die Steigung (hier: `scatter_input$Observed_SWE`) kann man sich über Aufruf von `coefficients()` und Angabe der Regressionsfunktion `fit_model` ausgeben lassen:

```{r}
# Koeffizieneten ausgeben
coefficients(fit_model)
```

**Was heisst das nun?** Das bedeutet, ausgehend von einem Wert von 20 (mm SWE) an der Y-Achse steigt unsere Regressionsgerade mit einer Steigung von 1.12 mit jedem weiteren beobachteten mm SWE! Aber schauen wir uns das später gleich im Plot genauer an...

Will man sich gleich die gesamte **Zusammenfassung der Linearen Regression** ansehen, verwendet man die Funktion `summary()` unter Angabe der Regressionsfunktion `fit_model.`

Ausgeben werden dann:

1) unter `Call` die verwendete Funktion
2) die Statistik der Abweichungen (Residuen) unter `Residuals`
3) die Regressionskoeffizienten (Achsenabschnitt und Steigung) zusammen mit den Ergebnissen des Signifikanztests unter `Coefficients`
4) der Standardfehler, das R2 und die F-Statistik.

Aber was heisst **Signifikanz** eigentlich: Der hier verwendete Signifikanztest testet die Regressionskoeffizienten gegen "0". Er testet also, mit welcher Wahrscheinlichkeit ich richtig liege dass z.B. die Steigung ungleich "0" ist, also ein deutlicher Zusammenhang besteht.

Wir schauen uns nun die Zusammenfassung der Regression einmal an:

```{r}
# Zusammenfassung ausgeben
summary(fit_model) 
```

Wir sehen, dass ein signifikanter Zusammenhang besteht, das Signifikanzniveau ist mit mind. zwei Sternen angegeben, also min. 0.001. Wir gehen also mit einer Irrtumswahrscheinlichkeit von 0.1 % fälschlicherweise von einem Zusammenhang der beiden Größen aus, wir liegen also mit einer Wahrscheinlichkeit von 99.9% richtig wenn wir einen Zusammenhang annehmen!

Wir wollen nun die **Regressionslinie auch im Plot einfügen** und ansehen. Dazu plotten nochmal unser Streudiagramm und verwenden die Funktion `abline()` um die Regressionslinie hinzuzufügen. Wir geben dieser einen gestrichelten Linientyp `lty='dashed'`, eine Linienstärke von 3 `lwd=3` und die Farbe rot `col='red'`.


```{r}
# Scatterplot erzeugen
par(pty="s")
plot(scatter_input$Observed_SWE, scatter_input$Simulated_SWE, xlim=c(0,600), ylim=c(0,600), type="p", pch = 19, cex=1.2, col="black", ann=FALSE)

# Diagrammtitel hinzufügen
title(main="Simuliertes vs. beobachtetes Schneewasseräquivalent \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Beobachtetes SWE (mm)")
title(ylab="Simuliertes SWE (mm)")

# Grid hinzufügen
grid(lty = 'dotted', col = "gray", lwd = 1)

# Regressionslinie hinzufügen
abline(fit_model, lty = 'dashed', col = 'red', lwd = 3)
```

Zu einer Regressionsgerade gehört aber immer die **zugehörige Regressionsfunktion**, und am besten auch das **Bestimmtheitsmaß (R2)**, beides wollen wir nun als Text hinzufügen.

Dazu müssen wir zunächst durch Zuhilfenahme der Funktion `round(Variable,Dezimalstellen)` die in der Variable `coefficients` gespeicherten Regressionskoeffizienten sowie das unter `r.squared` zu findende Bestimmtheitsmaß **auf zwei Stellen hinter dem Komma runden**.

Danach basteln wir uns eine **Textvariable** `regress_function` in die wir mit der Funktion `paste()` nacheinander Textbausteine und Variablen einbauen.

Die Funktion `text()` erlaubt dann das **Einfügen der generierte Zeichenfolge in das Diagramm**.

**Nun das Ganze Schritt für Schritt:**

Zunächst runden wir alle Variablen, stellen den Text zusammen und geben diesen Testweise ohne Diagramm aus:

```{r}
# Parameter der Regressionsgleichung auf 2 Dezimalstellen runden
slope = round(summary(fit_model)$coefficients[2], 2)
intercept = round(summary(fit_model)$coefficients[1], 2)
rsquared = round(summary(fit_model)$r.squared, 2)

# Zeichenfolge mit Regressionsgleichung definieren
regress_function = paste("y = ", intercept, " + ", slope, " * x",sep='')

# Zeichenfolge mit Bestimmtheitsmaß definieren
rsquared_text = paste("R2 = ", rsquared, sep='')

# Text ausgeben
print(regress_function)
print(rsquared_text)
```

Nun bauen wir diesen Text in unser Diagramm ein. Dies tun wir unter Verwendung der `text()` Funktion, diese benötigt die **X-Koordinaten** im Plot, die **Y-Koordinaten** im Plot und den **Text** in Form von:

`text(X-Koordimnate,Y-Koordinate,MeinText)`

Durch Hinzufügen des Parameters `pos` können wir noch die **Position** definieren, d.h. ob der Text unter `1`, links `2`, über `3` oder rechts `4` von den angegeben Koordinaten platziert werden soll. Wir vewenden den Wert `4` (rechts).

Wollt Ihr mehr über die text-Funktion erfahren, besucht: https://www.rdocumentation.org/packages/graphics/versions/3.6.2/topics/text

Die X- und Y-Koordinaten sind dabei über dei Werte der Achsen zu skalieren, sie stellen also **Werte in der Plotfläche** dar!

Nach Abgleich mit unseren Achsenwerten setzen wir die Regressionsfunktion auf die X-koordinate `0` und die Y-Koordinate `550`. Den Text mit dem R2 setzen wir knapp darunter auf die X-koordinate `0` und die Y-Koordinate `500`. Bis auf die text-Funktion ganz unten verwenden wir unseren vorherigen plot-Aufruf!

**Tipp:** 

Während die Angabe der Koordinaten nach Sichtung des Achsenbereichs gut über absolute Werte klappt, geht das natürlich nicht mehr wenn sich der Wertebereich ändert! Man kann mit etwas Aufwand die Koordinaten relativ zum Wertebereich setzen, natürlich nur wenn man diesen vorher über `xlim` bzw. `ylim` definiert, also kennt. Wenn ich meinen Text z.B. immer auf 95% des Wertebereiches (der Y-Achse) setzen will kann ich das so tun:

`ypos = ymin + (0.95 * (ymax - ymin))`

Analog funktiomiert das auch mit der X-Achse!

```{r}
# Scatterplot erzeugen
par(pty="s")
plot(scatter_input$Observed_SWE, scatter_input$Simulated_SWE, xlim=c(0,600), ylim=c(0,600), type="p", pch = 19, cex=1.2, col="black", ann=FALSE)

# Diagrammtitel hinzufügen
title(main="Simuliertes vs. beobachtetes Schneewasseräquivalent \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Beobachtetes SWE (mm)")
title(ylab="Simuliertes SWE (mm)")

# Grid hinzufügen
grid(nx = NULL, ny = NULL, lty = 'dotted', col = "gray", lwd = 1)

# Regressionslinie hinzufügen
abline(fit_model, lty = 'dashed', col = 'red', lwd = 3)

# Regressionsfunktion als Text hinzufügen
text(0, 550, regress_function, pos=4)

# Bestimmtheitsmaß als Text hinzufügen
text(0, 520, rsquared_text, pos=4)
```

Das hat gut geklappt! Allerdings ist das Bestimmtheitsmaß allein nur wenig geeignet um Modellergebnisse zu bewerten, wir wollen im Folgenden deshalb weitere Effizienzkriterien kennenlernen!

## 9 - Effizienzkriterien

Effizienzkriterien können herangezogen werden, um Modellergebnisse zu bewerten. Folgende Kriterien sollten wir kennen:

1) Bestimmtheitsmaß `R2`, Wertebereich: 0 <--> 1:
    
    R2 (das Quadrat des Korrelationskoeffizienten R) sagt uns welcher Teil der Gesamtvarianz durch die abhängige Variable (im Plot: Y-Achse) erklärt wird. In unserem Fall erklärt das Modell 91% der Gesamtvarianz.
R2 hat aber große Nachteile, da es nur die Kovarianz betrachtet, aber nie die absoluten Differenzen zwischen Beobachtung und Modell. So kann das R2 1 sein, wenn ein Modell immer 1000 mm SWE über den Beobachtungen liegt, da beide auch dann perfekt kovarieren, mit einer guten Modellperformanz hat das natürlich dann nichts zu tun.


2) Nash-Suttcliffe Koeffizient `NSE`, Wertebereich: minus undendlich <--> 1:
    
    Der Nash-Sutcliffe Koeffizient (auch Nash-Sutcliffe Model Efficiency, NSE) betrachtet auch die Differenzen zwischen Beobachtung und Modellergebnis und ist somit kritischer und in der Hydrologie ein Standard Kriterium. Das Perfekte Modell hätte einen NSE Wert von 1, ab einem Wert von 0 ist der Mittelwert eine bessere Vorhersage als das Modell.


3) `PBIAS`, Wertebereich: minus unendlich <--> plus unendlich:
    
    Der PBIAS gibt den Grad der Über-/Unterschätzung durch das Modell an. Ein PBIAS von -20 beschreibt eine Unterschätzung von 20%, ein PBIAS von +20 beschreibt eine Überschätzung von 20%. Das perfekte Modell liefert einen PBIAS Wert von 0.
    
Das waren nur einige wichtige Vertreter, für einen **umfassenden Überblick zu verschiedenen Effizienzkriterien in der Hydrologie**, schaut Euch folgende Artikel an: 

https://adgeo.copernicus.org/articles/5/89/2005/

https://swat.tamu.edu/media/1312/moriasimodeleval.pdf

Um `NSE` zu berechnen könnt Ihr die Bibliothek `topmodel` verwenden. Die Formel zur Berechnung von NSE lautet: 

$$
NSE=1 - [\sum_{i = 1}^{n}{(obs_i-sim_i)^2}: \sum_{i = 1}^{n}{(obs_i-obs_m)^2}]
$$
Dabei stehen `obs` und `sim` für die Beobachtungen und Simulationen, `i` und `m` für die Werte eines Zeitschrittes bzw. das Mittel aller Werte.

Verwendet doch gleich einmal die enthaltene Funktion `NSeff(Qobs,Qsim)` um `NSE` zu berechnen und setzt `NSE` noch unter dem `R2` in Euren Plot ein!

Zur Berechnung des `PBIAS` habe ich Euch eine kleine Funktion gebaut, die mit `PBIAS(Qobs,Qsim)` gerufen werden kann. Sie tut nichts anderes, als für jeden Zeitschritt die Abweichung des Simulationswertes vom Beobachtungswert zu berechnen und diese Abweichungen dann aufzusummieren. Die Summe der Abweichungen wird dann geteilt durch die Summe aller Messwerte, mit 100 Multipliziert ergibt sich die durchschnittliche prozentuale Abweichung:

$$
PBIAS=100 * [\sum_{i = 1}^{n}{(sim_i-obs_i)}  : \sum_{i = 1}^{n}{(obs_i)}]
$$

Die unten aufgeführte Funktion müsst Ihr in Eurem Skript einbauen, nachdem man die Definition einmal ausgeführt hat, kann man die Funktion immer wieder aufrufen.

```{r}
# define function
PBIAS = function(Qobs,Qsim) {

# get indices with valid values
valid_obs=which(!is.na(Qobs))
valid_sim=which(!is.na(Qsim))
valid_values=intersect(valid_obs,valid_sim)

# get bias
bias=Qsim[valid_values]-Qobs[valid_values]
sum_bias=sum(bias)
sum_obs=sum(Qobs[valid_values])
pbias=100*sum_bias/sum_obs

# return result
return(pbias)
}

# use funtion to derive PBIAS
pbias=PBIAS(scatter_input$Observed_SWE,scatter_input$Simulated_SWE)
pbias
```

Wir überschätzen das beobachtete SWE also im Schnitt um 21%.
Verwendet nun diese Funktion um Euren `PBIAS` zu berechnen und setzt den berechneten Wert noch unter dem `NSE` in Euren Plot ein!

Eine grobe Richtlinie zur Bewertung von Modellergebnissen über NSE und PBIAS geben Morasi et al. (2007):

![](Pics/Evaluation.png)

## 10 - Plots speichern

Für das Speichern von Plots gibt es verschiedene Möglichkeiten. 

1) Wir können das händisch in RStudio tun, indem wir in der Plotansicht auf `Export->Save as Image` gehen

2) Wenn wir im Jupyter arbeiten, könnt Ihr die generierten Grafiken auch mit `Rechtsklick --> Speichern unter ...` im Browser speichern

3) Alternativ (und für Skripte meist besser weil automatisert möglich) können wir den Plot im Code selbst durch den `png()` Befehl (vor dem Plotten einzufügen) gefolgt von `dev.off()` (nach dem Plotten einzufügen) speichern

Option 3) probieren wir gleich mal anhand eines Plots aus, wir verwenden dafür nochmal den oben generierten Scatterplot, geben dabei der `png()` Funktion auch noch die **Breite und Höhe unseres pngs** mit, da die Qualität (Auflösung) standardmäßig redzuiert ist. Beachtet dass wir durch eine geeignete Wahl der Breite und Höhe dafür sorgen müssen, dass unser **Achsenverhältnis nicht verzerrrt** ist, wir wählen eine leicht erhöhte Höhe um dem Titel Platz zu geben:

```{r}
# Datei aufmachen
png(file = "Scatterplot.png", width=500, height=520)

# Scatterplot erzeugen
par(pty="s")
plot(scatter_input$Observed_SWE, scatter_input$Simulated_SWE, xlim=c(0,600), ylim=c(0,600), type="p", pch = 19, cex=1.2, col="black", ann=FALSE)

# Diagrammtitel hinzufügen
title(main="Simuliertes vs. beobachtetes Schneewasseräquivalent \nStation Col de Porte 2005/2006")

# Beschriftung für X- und Y-Achse hinzufügen
title(xlab="Beobachtetes SWE (mm)")
title(ylab="Simuliertes SWE (mm)")

# Grid hinzufügen
grid(nx = NULL, ny = NULL, lty = 'dotted', col = "gray", lwd = 1)

# Regressionslinie hinzufügen
abline(fit_model, lty = 'dashed', col = 'red', lwd = 3)

# Regressionsfunktion als Text hinzufügen
text(0, 550, regress_function, pos=4)

# Bestimmtheitsmaß als Text hinzufügen
text(0, 520, rsquared_text, pos=4)

# NSE als Text hinzufügen
library(topmodel)
nse_text=paste("NSE = ", round(NSeff(scatter_input$Observed_SWE,scatter_input$Simulated_SWE),2), sep='')
text(0, 490, nse_text, pos=4)

# PBIAS als Text hinzufügen
pbias_text=paste("PBIAS = ", round(PBIAS(scatter_input$Observed_SWE,scatter_input$Simulated_SWE),2), sep='')
text(0, 460, pbias_text, pos=4)

# Device schliessen
dev.off()
```

Die so erzeugte Datei `Scatterplot.png` liegt nun im Arbeitsverzeichnis und sollte etwa so aussehen:

![](Scatterplot.png)











