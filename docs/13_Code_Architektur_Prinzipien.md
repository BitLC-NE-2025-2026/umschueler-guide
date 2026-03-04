# 📐 Clean Code, Architektur & Prinzipien

![CleanCode](https://img.shields.io/badge/Qualität-Clean_Code-brightgreen?style=for-the-badge) ![Architektur](https://img.shields.io/badge/Struktur-Best_Practices-blue?style=for-the-badge) ![CSS](https://img.shields.io/badge/Frontend-CSS_Methoden-ff69b4?style=for-the-badge)

Code wird einmal geschrieben, aber hundertmal gelesen. Deshalb reicht es nicht, dass ein Programm *irgendwie funktioniert*. Es muss wartbar, verständlich und erweiterbar sein. Hier sind die wichtigsten Konzepte, die dich vom blutigen Anfänger zum respektierten Junior-Entwickler machen.

---

## 📑 Inhaltsverzeichnis
1. [🧠 Die Heilige Dreifaltigkeit: DRY, KISS, YAGNI](#-die-heilige-dreifaltigkeit-dry-kiss-yagni)
2. [🧹 Clean Code & Struktur](#-clean-code--struktur)
3. [🏛️ Die SOLID Prinzipien (Tieferer Einblick)](#-die-solid-prinzipien-tieferer-einblick)
4. [🎨 Frontend & CSS Architekturen (SFC, BEM, Utility-First)](#-frontend--css-architekturen-sfc-bem-utility-first)

---

## 🧠 Die Heilige Dreifaltigkeit: DRY, KISS, YAGNI

Das sind die drei absoluten Basis-Regeln, bevor man überhaupt eine Zeile Code schreibt.

<details open>
<summary><b>DRY (Don't Repeat Yourself)</b></summary>

- **Die Regel:** Schreibe denselben Code niemals zweimal.
- **Warum:** Kopierst du einen Code-Block an drei verschiedene Stellen und entdeckst später darin einen Bug, musst du ihn an drei Stellen fixen (und vergisst garantiert eine).
- **Die Lösung:** Ziehe den Code in eine eigene Methode oder Klasse (Helper/Service) heraus und rufe diese Methode von den drei Stellen aus auf.
</details>

<details open>
<summary><b>KISS (Keep It Simple, Stupid)</b></summary>

- **Die Regel:** Vermeide unnötige Komplexität. Mach es so simpel wie möglich.
- **Warum:** Entwickler lieben es, schlau zu wirken und "clevere" Einzeiler (wie extrem verschachtelte LINQ-Queries oder Regex) zu schreiben. In 6 Monaten versteht das niemand mehr – nicht einmal du selbst.
- **Die Lösung:** Schreibe klaren, logischen Code. Lieber 5 Zeilen lesbaren Code als 1 kryptischen "magischen" Einzeiler.
</details>

<details open>
<summary><b>YAGNI (You Aren't Gonna Need It)</b></summary>

- **Die Regel:** Baue niemals Features oder Architektur auf Vorrat.
- **Warum:** "Lass uns hier noch ein Interface und einen Generic-Typen einbauen, falls wir später mal statt SQL eine MongoDB nutzen wollen." -> In 99% der Fälle tritt die Zukunft anders ein als gedacht, und du pflegst jahrelang extrem unnötigen Boilerplate-Code ohne Business-Value.
- **Die Lösung:** Löse nur das Problem, das HEUTE existiert (Refactoren kann man später immer noch).
</details>

---

## 🧹 Clean Code & Struktur

<details open>
<summary><b>Regel: 1 Datei = 1 Klasse</b></summary>

Besonders in Sprachen wie C# oder Java ist es eine Todsünde, mehrere Klassen (oder Interfaces und Klassen) in dieselbe physische Datei (`.cs`) zu quetschen.
- **Falsch:** In `Datenbank.cs` liegen die Klassen `DatabaseConnection`, `UserEntity` und `ArticleEntity` alle untereinander.
- **Warum:** Niemand findet diese Klassen über den Solution-Explorer (Order-Baum). Jeder Entwickler erwartet, dass eine Datei `UserEntity.cs` existiert.
</details>

<details open>
<summary><b>Sinnvolle Namensgebung (Bedeutungsvoll)</b></summary>

Variablen sind keine mathematischen Formeln. Sie dürfen (und sollen) lang sein!
- **Schlecht:** `var list = GetL();` (Was ist list? Was ist L?)
- **Besser:** `var aktiveBenutzerListe = HoleLetzteLogins();`
- **Tipp:** Wenn du Mühe hast, einer Methode einen passenden, kurzen Namen zu geben, macht sie wahrscheinlich zu viele verschiedene Dinge auf einmal (Verletzung des *Single Responsibility Principles*).
</details>

<details open>
<summary><b>Kommentare erklären das WARUM, nicht das WAS</b></summary>

Kommentiere niemals, *was* der Code tut – das sollte der Code durch sinnvolle Variablennamen selbst erzählen. Kommentiere das *Warum*.
- **Schlechter Kommentar:** `// Addiert Menge 1 und Menge 2` (Das sehe ich beim Lesen des Codes selbst).
- **Guter Kommentar:** `// Hack: Die API von Stripe ignoriert Zeitzonen. Deshalb füge ich hier manuell 2 Stunden hinzu, weil es sonst zu Abstürzen beim Speichern kommt. (Stripe Ticket #12345)`
</details>

---

## 🏛️ Die SOLID Prinzipien (Tieferer Einblick)

SOLID ist ein Akronym aus 5 Design-Prinzipien der objektorientierten Programmierung (OOP), geprägt von "Uncle Bob" (Robert C. Martin).

<details open>
<summary><b>S - Single Responsibility Principle (SRP)</b></summary>
Eine Klasse (oder Funktion) sollte **nur einen einzigen Grund haben, sich zu ändern**.
Beispiel: Eine `Rechnung`-Klasse sollte kalkulieren, was sie kostet. Sie sollte ABER NICHT den Code enthalten, um eine PDF zu generieren oder eine E-Mail zu verschicken! Baue dafür stattdessen einen `PdfGenerator` und einen `EmailSender`.
</details>

<details open>
<summary><b>O - Open/Closed Principle (OCP)</b></summary>
Software-Komponenten sollten **offen für Erweiterungen, aber geschlossen für Änderungen** sein.
Wenn du eine neue Zahlungsart (z.B. PayPal) zu deinem Shop hinzufügst, solltest du keinen bestehenden Code anfassen müssen (kein gigantisches `if(bezahlArt == "paypal")` um ein `else` erweitern). Stattdessen nutzt du Polymorphie und baust einfach eine neue Klasse `PayPalPayment`, die das Interface `IPayment` implementiert. Der bestehende "geschlossene" Code kann dieses Interface automatisch ohne Anpassung nutzen.
</details>

<details open>
<summary><b>L - Liskov Substitution Principle (LSP)</b></summary>
Objekte einer Superklasse müssen durch Objekte ihrer Unterklassen **ersetzt werden können, ohne dass das Programm abstürzt**.
Klassisches Beispiel: Eine Basisklasse `Vogel` hat die Methode `Fliegen()`. Wir leiten die Klassen `Hund` und `Katze` nicht von Vogel ab, aber was ist mit einem `Pinguin`? Er ist ein Vogel. Rufen wir aber beim Pinguin (der nicht fliegen kann) `Fliegen()` auf, stürzt das Programm ab oder wirft einen Fehler. Pinguin verletzt als erbende Klasse hier das LSP! Lösung: Eine Klasse `Flugvogel` erschaffen.
</details>

<details open>
<summary><b>I - Interface Segregation Principle (ISP)</b></summary>
**Viele kleine, extrem spezifische Interfaces** sind besser als ein riesiges "Gott-Interface". 
Ein Interface `IAlleskönner` verlangt `Drucken()`, `Scannen()` und `Kopieren()`. Wenn du jetzt einen einfachen Tintenstrahldrucker programmierst, zwingt dich das Interface, hohle / leere Methoden für `Scannen()` anzulegen, die einfach nur `throw new NotImplementedException()` werfen. Das ist unsauber. Teile das Interface auf in `IDrucker`, `IScanner`.
</details>

<details open>
<summary><b>D - Dependency Inversion Principle (DIP)</b></summary>
Abhängigkeiten sollten **in Richtung abstrakter Interfaces** verlaufen, niemals in Richtung konkreter Klassen.
Ganz simpel: Ein Controller sollte als Parameter im Konstruktor ein Interface `IDatabase` fordern, niemals die konkrete fest verbaute Klasse `MySQLDatabase`. Warum? Wenn du morgen die Datenbank auf PostgreSQL wechselst, musst du nur "unter der Haube" via Dependency Injection (IoC Container) das Interface neu verknüpfen, ohne den gesamten Controller-Code umschreiben zu müssen.
</details>

---

## 🎨 Frontend & CSS Architekturen (SFC, BEM, Utility-First)

Das Front-End wird bei wachsenden Web-Apps schnell zu einem einzigen Chaos aus globalen Styles, die sich gegenseitig überschreiben ("CSS Bleeding"). Hier sind die modernen Lösungsansätze:

<details open>
<summary><b>BEM (Block Element Modifier) - Die klassische CSS Namenskonvention</b></summary>

Eine strikte Regel zur Benennung von Klassen, um Konflikte zu vermeiden. BEM verzichtet auf verschachtelte CSS (`.menu a { ... }`). Alles wird extrem eindeutig und damit modular!
- **Block:** Das übergeordnete Bauteil (`.card`)
- **Element:** Ein Kind-Teil davon (`.card__image` - verbunden durch zwei Underscores)
- **Modifier:** Eine Abwandlung/Zustand (`.card__image--large` - verbunden durch zwei Bindestriche)

Ergebnis im HTML: `<button class="btn btn--primary btn--disabled">`
</details>

<details open>
<summary><b>OOCSS (Object Oriented CSS)</b></summary>

Behandle CSS wie Code. Die Hauptregel lautet: **Trenne Struktur vom Aussehen (Skin).**
Statt eine Klasse `.submit-button-rot` zu schreiben, die Rand (Struktur) und die Farbe (Skin) enthält, trennst du sie in abstrakte Ojekte:
- Klasse 1 (Struktur): `.btn { padding: 10px; border-radius: 5px; }`
- Klasse 2 (Skin): `.btn-danger { background-color: red; }`
- Im HTML kombinierst du: `<button class="btn btn-danger">`
</details>

<details open>
<summary><b>Utility-first CSS (Der moderne Tailwind-Weg)</b></summary>

Der aktuelle Industrie-Standard (oft via Tailwind CSS umgesetzt). Anstatt hunderte Datei mit eigenen CSS-Klassenamen (wie `.my-header-box`) zu erfinden und zu tippen, nutzt du **tausende winzige Utility-Klassen**.
Jede Utility-Klasse macht genau EINE Sache, z.B. `.flex` oder `.p-4` (Padding von 4) oder `.text-red-500`.

- **Vorteil:** Du musst dir nie wieder Namen für dumme Wrapper-DIVs ausdenken. Die Dateigröße deines CSS wächst in riesigen Projekten effektiv nicht mehr an (es wird gecached). Man baut die UIs absurd schnell zusammen.
- **Nachteil:** Das HTML wird absolut überladen (`<button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">`).
</details>

<details open>
<summary><b>SFC (Single File Components)</b></summary>

Ein modernes Architekturkonzept (bekannt durch Vue.js, Svelte, React, aber auch in Blazor und Razor Pages via "CSS Isolation").

**Das Konzept:** Eines der stärksten Probleme früherer Websites war die Trennung nach **Technologie** (Ein Ordner für alle HTMLs, ein Ordner für alle JS-Dateien, einer für CSS). Oft musste man durch 3 Dateien springen, um einen einzigen Button anzupassen.
**SFC ändert das (Trennung nach Komponente):** 
Dein "Button" bekommt *eine einzige Datei*. In dieser Datei lebt das HTML (Struktur), das Button-CSS (Aussehen, isoliert nur auf diesen Button) und das JavaScript (Verhalten) direkt beieinander. Löst du den Button, wird sein CSS automatisch mit gelöscht und hinterlässt keine Altlasten!
</details>

---
[Zurück zur Übersicht](../README.md)
