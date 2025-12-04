# Warum ich das Rad neu erfunden habe: Die Entstehung eines spezialisierten LLM-Tools
**Oder: Wenn Standard-Software an der Realität sensibler Daten scheitert.**

Als Entwickler lernt man eine goldene Regel sehr früh: *"Don't reinvent the wheel."* Nutze existierende Libraries, Frameworks und Tools. Warum etwas bauen, das es schon gibt?

Seit zehn Monaten entwickle ich als **Devmatrose** ein komplexes Ökosystem für einen Kunden. In diesem Prozess stießen wir auf eine Hürde, die mit Standard-Lösungen nicht zu nehmen war: Das Training eines spezialisierten KI-Modells (LLM) mit hochsensiblen Daten.

Dieser Artikel ist ein Einblick in meinen Denkprozess, warum ich mich gegen den Marktstandard und für eine Eigenentwicklung entschieden habe – und warum „On-Premise“ in der KI-Entwicklung oft der einzige gangbare Weg ist.

## Die Ausgangslage: Ein Dilemma in drei Akten

Wir brauchten ein Werkzeug, um Daten zu labeln und zu validieren. Das klingt trivial. Es gibt Dutzende Tools dafür (Label Studio, Prodigy, Scale AI, etc.). Doch bei genauerer Betrachtung der Anforderungen fiel das Kartenhaus der Standard-Lösungen zusammen.

**1. Das Datenschutz-Paradoxon**
Die Datenbasis bestand aus sensiblen, vertraulichen Informationen (vergleichbar mit medizinischen oder psychologischen Akten).
* **Markt-Lösung:** Die meisten nutzerfreundlichen Tools sind Cloud-basiert.
* **Das Problem:** Ein Upload dieser Daten auf fremde Server (oft in den USA) war kategorisch ausgeschlossen. [cite_start]Wir brauchten eine Lösung, die zu 100 % lokal, offline und im eigenen Netzwerk läuft – ohne "nach Hause zu telefonieren". [cite: 2, 9]

**2. Der Faktor Mensch (Expertise vs. Technik)**
Wer validiert die Daten? In unserem Fall waren es keine Data Scientists oder Entwickler, sondern Fachexperten (Domänen-Experten).
* **Markt-Lösung:** Lokale Open-Source-Tools sind oft mächtig, aber "roh". Sie erwarten oft, dass der Nutzer JSON lesen kann oder Konfigurationsdateien versteht.
* [cite_start]**Das Problem:** Setzt man einem Fachexperten (z.B. einem Psychologen oder Anwalt) ein rohes JSON-Objekt vor, sinkt die Arbeitsqualität und die Frustration steigt. [cite: 2, 7]

**3. Die Komplexität des Kontextes**
Standard-Tools labeln oft linear: "Ist das Bild eine Katze? Ja/Nein." Unsere Anforderungen waren multidimensional. [cite_start]Ein Datensatz musste aus technischer, fachlicher und ethischer Sicht bewertet werden – oft von unterschiedlichen Personen. [cite: 2, 6]

## Der Lösungsansatz: Der "Smart Editor" und die Säulen-Architektur

Da kein Tool diese Kombination aus **lokaler Sicherheit** und **fachlicher Usability** bot, habe ich es konzipiert. Der Ansatz basiert auf zwei Kernideen, die ich gerne als Inspiration teilen möchte.

### 1. Die Tab-Architektur (Säulen-Prinzip)
Statt alle Informationen in eine unübersichtliche Maske zu pressen, habe ich das Tool modular aufgebaut. [cite_start]Wir trennen die verschiedenen Dimensionen der Validierung in "Tabs" (Reiter) auf. [cite: 6]

* **Der technische Tab:** Hier sieht der Admin die Rohdaten.
* **Der fachliche Tab:** Hier sieht der Domänen-Experte nur das, was für ihn relevant ist.
* **Der Validierungs-Tab:** Hier wird nach dem Vier-Augen-Prinzip geprüft.

Diese Architektur erlaubt es, das Tool für völlig verschiedene Branchen anzupassen, ohne den Kern neu zu schreiben. Heute validieren wir psychologische Muster, morgen vielleicht juristische Texte – das Framework bleibt gleich, nur der "Tab" ändert sich.

### 2. Der Übersetzer (Smart Editor)
Die größte Hürde für nicht-technische Nutzer ist das Datenformat. Mein Tool fungiert als Echtzeit-Übersetzer.
Im Hintergrund arbeitet die KI mit komplexen JSON-Strukturen. Das Tool parst diese Strukturen und generiert daraus dynamisch eine verständliche Benutzeroberfläche (UI).

* Aus einem Array im Code wird eine Tag-Liste.
* Aus einem Boolean-Wert wird eine einfache Checkbox.
* Aus einem Score wird ein Schieberegler.

Der Experte füllt ein Formular aus – das Tool schreibt den Code. [cite_start]So erhalten wir saubere Trainingsdaten für die KI, ohne dass der Experte je eine geschweifte Klammer `{}` sehen muss. [cite: 7]

## Warum das wichtig ist (Lessons Learned)

In der KI-Entwicklung konzentrieren wir uns oft zu sehr auf Modelle und GPUs. Aber die Qualität der Daten – und damit die Qualität der menschlichen Arbeit, die in diese Daten fließt – ist der wahre Flaschenhals.

Als Entwickler und Architekt (Devmatrose) war meine Erkenntnis: **Manchmal ist die beste "Tech-Lösung" diejenige, die die Technik vor dem Nutzer versteckt.**

Indem wir eine maßgeschneiderte Lösung gebaut haben, konnten wir:
1.  [cite_start]Die Datenhoheit komplett beim Kunden behalten (On-Premise). [cite: 9]
2.  [cite_start]Die Fehlerrate bei der Validierung drastisch senken. [cite: 8]
3.  Experten befähigen, mit KI zu arbeiten, ohne Programmierer zu sein.

## Demo & Ausblick

Die volle Version dieses Tools ist tief in die Prozesse meines Kunden integriert und enthält spezifisches Know-how, das nicht öffentlich ist.

Aber der **architektonische Ansatz** – die Idee des modularen, lokalen Smart Editors – ist zu wertvoll, um ihn nicht zu teilen. Ich werde in den kommenden Tagen eine **abgespeckte Demo-Version** auf GitHub veröffentlichen. Sie zeigt das Prinzip der dynamischen Formular-Generierung und das Tab-System, bereinigt um die spezifische Business-Logik.

Damit möchte ich zeigen, wie wir moderne Web-Technologien nutzen können, um die Lücke zwischen komplexer KI und menschlicher Expertise zu schließen.

***

**Über mich:**
Ich bin Devmatrose. Ich baue digitale Ökosysteme und löse Probleme, für die es noch keinen Stack Overflow Eintrag gibt. Folgt mir hier für Updates zur Demo.