# Softwareentwicklung SoSe2023 - Aufgabe 04

In der Aufgabe dieses Aufgabenblatts sollen die erlernten objektorientierten Konzepte  (Klassen, Felder, Eigenschaften, Methoden) verwendet werden.

Lösen Sie die Aufgabe in den Gruppen von zwei Studierenden. Versuchen Sie der Aufwand zur Lösung der Aufgaben im Voraus abzuschätzen und teilen Sie die Teilaufgaben (1. - 5.) gleichmäßig auf. Verwenden Sie zur Organisation der Zusammenarbeit die GitHub - Features.

## Bearbeitungszeit

SWE: 29. Mai - 2. Juni 2023 (Mm, BWM, ROB, BAI, BGIP, BBWL, BBL, MGIN)

## Aufgabe

Schreiben Sie ein Programm, das in der Lage ist, einen bzw. mehrere Computer zu simulieren. Realisieren dazu die folgende Funktionalität:

+ Am Computer soll sich ein Benutzer anmelden können.
+ Ein Computer soll in der Lage sein, Dateien zu speichern und
+ über eine IP-Adresse verfügen.
+ Es soll weiterhin möglich sein die Daten in einem Web-Archiv abzulegen.
+ Jeder Computer soll über eine *Print()*-Methode verfügen, die seine relevanten Eigenschaften ausgibt.

Erstellen Sie dazu eine Klasse **Computer**. Um die geforderte Funktionalität realisieren zu können, ist es außerdem sinnvoll zwei weitere Klassen zu implementieren:

+ eine Klasse mit `static`-Methoden für die Konvertierung der IP-Adressen zwischen `byte`-Array und `string` und
+ die "Archiv"-Klasse

In der Main(...)-Methode sollen zum Testen der Klasse erst ein Objekt der Klasse Computer und dann ein Array mit 100 Computern angelegt werden, die Methoden aufgerufen und die Eigenschaften verändert werden. Lassen Sie z.B. jeden Computer eine Datei speichern und zählen Sie die Abstürze. Erstellen Sie ein paar "Archive".

![Klassendiagramm](http://www.plantuml.com/plantuml/png/fL9HQy8m47xlhyXZPFDj-52aA1r3GKPHzpJsSBOtMqYRaLmh8lxtfIQBhbAHhGyfkVk-xxwxoqGJAAfB4SIo_Ae95HiE8pPLQLuq-3iuJzPI2Xsa0hHcFdK8cFaUs9j6zGebif1fKaMrPUFn5YcAN7wrAoZDMnIlSFU33YrsO5YDB3A7dO6E5UWSCnFVcAfTBMZmfH38FytH9zE19K2vWpsosxmbcfh4Ez5vCiqoXLfVTMZ--i9Th108tGovW0qANpYj22loLx2Wq84x5HC3wjhmW-TBgBAmFMGv28vkBKx8RsN-RDYraUbCSD6wwbjLB4yk-z8zdSdBriwEtBDfPqH0HHf5tjp1Heucfn0oMOczoIva2c8czRb-5-utiPQh4u23lOURFU7xn-06itcwujvD7Vsrh8MlfJVEBMvgwUT7Q8LwwSRzVmL6zmjukbiXRvSwmIghI_4D)

## Vorgehen

Realisieren Sie im Einzelnen die folgenden Schritte:

1. Um den Benutzername festhalten zu können wird ein Property (z. B. *UserName*) benötigt. Der Benutzername soll nach außen hin zwar les- aber nicht schreibbar sein. Bitte fügen Sie Ihrer Klasse ein solches Property hinzu und initialisieren Sie es in einem eigens erstellten Konstruktor mit dem Startwert "Administrator".

    Um den aktuellen Benutzer zu wechseln, soll eine Methode implementiert werden, die den neuen Benutzernamen als Zeichenkette übernimmt. Dazu wartet die Methode einen kurzen Moment und gibt passende Ausgaben auf der Konsole aus, bevor der neue Name zugewiesen wird:

      *Logging out ...*

      *Logging in as root*

2. Zum Speichern der Dateien implementieren Sie bitte eine Methode, die einen Pfad zu einem Verzeichnis sowie einen Dateinamen übernimmt. Verwenden Sie zur Erstellung des zusammengesetzten Dateipfades die *Combine(...)*-Methoden der Klasse `System.IO.Path`. Der eigentliche Speichervorgang wird als Konsolenausgabe realisiert, z. B.:

      *Saving file: C:\Users\root\Desktop\Dissertation.tex*

    Überladen Sie Ihre Methode zum Speichern mit einer zweiten Version, die nur einen Dateinamen übernimmt und als Verzeichnis den Desktop des aktuellen Benutzers wählt. Die eigentliche Programmlogik soll nicht doppelt implementiert werden, d.h. realisieren Sie die Funktionalität der zweiten Methode über den Aufruf der ersten.

    Beim Speichern wichtiger Dateien stürzen Computer erfahrungsgemäß gern ab. Implementieren Sie dazu eine zufällige Abfrage in der Speichermethode. In einem von vier Fällen findet ein Absturz statt und eine `InvalidOperationException` wird geworfen.

    Sobald ein Absturz einmal aufgetreten ist, funktioniert das Speichern von Dateien bis zum nächsten Neustart des Computers nicht mehr und wirft immer eine `InvalidOperationException`. Implementieren Sie dieses Verhalten mittels einer automatischen Boolean-Property und einer *Reboot()*-Methode. Nach außen hin soll die Property nur lesbar sein.

    Lassen Sie Ihren Computer in der Main(...)-Methode in einer Endlosschleife Dateien speichern. Starten Sie ihn neu, sobald er abstürzt.

3.  Implementieren Sie die IP-Adresse in der Computer-Klasse als privates byte-Array-Feld. Als initialer Wert soll *LocalHost* gesetzt sein. Nach außen wird die IP-Adresse über eine Property vom Typ `String` angesprochen. Verwenden Sie in den set- und get-Teilen der Property die statischen Methoden der Klasse **IPTools**.

    Erstellen Sie die `static` Klasse **IPTools**, die über die Methoden zum Konvertieren zwischen den IP-Adressen als `byte`-Array und `string` verfügt und die Verarbeitung sowohl IPv4- als auch IPv6-Adressen unterstützt.

    Die IPv4-Adressen bestehen aus 4 Blocken, die durch einen Punkt getrennt sind. Die IPv6-Adressen bestehen aus 16 Bytes und werden in hexadezimaler Form als 8 Blöcke (je 2 Bytes) notiert, z. B.: ffee:ddcc:bbaa:9988:7766:5544:3322:1100

    Erstellen Sie außerdem in der Klasse ein `static readonly byte`-Feld, das LocalHost (127.0.0.0) representiert und zum Initialisieren der IP-Adresse in der Klasse Computer verwendet wird.


4. Um die Archivierung zu ermöglichen, legen Sie bitte zunächst eine Archiv-Klasse an. Die Klasse soll über eine ID, eine Beschriftung (Zeichenkette) und einen Inhalt (ebenfalls Zeichenkette) verfügen. Implementieren Sie alle drei Elemente als nicht-schreibbare, automatische Properties.

    Implementieren Sie einen Konstruktor, der die Bezeichnung und den Inhalt als Parameter übernimmt. Die ID soll mit jedem neu erzeugten Archiv hochgezählt, und nicht als Konstruktor-Parameter übergeben werden.

    Fügen Sie Ihrer Computer-Klasse eine Methode zum Archivieren hinzu. Übergeben werden an die Methode die Bezeichnung und der Inhalt, die zum Erstellen eines Archiveintrags benötigt werden. Der eigentliche Archivierungsvorgang wird als Konsolenausgabe realisiert, z. B.:

      *Archiving data ...*

    Erstellen Sie in der Main(...)-Methode zwei Archive und geben Sie die Bezeichner, den Inhalt und die IDs aus, z. B.:

      [0] "Absatz von Smartphones" ("173.5, 304.7, 494.5, 725.3, 1019.4, 1301.7, 1437.6, 1469, 1465.5, 1402.6, 1372.6, 1280")

      [1] "Netflix Abonnenten" ("26.253, 33.267, 44.350, 57.391, 74.762, 93.796, 117.582, 148.455, 171.769, 203.663, 221.844, 230.747")

5. Implementieren Sie außerdem in der Computerklasse eine Print()-Methode, die die relevanten Eigenschaften des Computers ausgibt (Benutzername, IP-Adresse, Absturzzustand).

**Vermeiden Sie das Einchecken von unnötigen Dateien im Repository! Die Präsenz von kompiliertem Code erschwert die Übersichtlichkeit bezüglich des Entwicklungsflusses.**

Organisieren Sie die Implementierung von Teilaufgaben in verschiedenen `feature-branches`. Realisieren Sie die Zuordnung über die Issues, benennen Sie dabei die zustädigen Developer und ggf. die Milestones. Evaluieren Sie gegenseitig die "eingehenden" Pull Requests als Reviewer.

