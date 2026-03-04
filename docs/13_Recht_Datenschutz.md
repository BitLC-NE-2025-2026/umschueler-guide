# ⚖️ IT-Recht, Datenschutz (DSGVO) & Barrierefreiheit (BFSG)

![Recht](https://img.shields.io/badge/IT_Recht-DSGVO_&_BFSG-darkred?style=for-the-badge) ![Modern](https://img.shields.io/badge/Fokus-Top_Aktuell-yellow?style=for-the-badge)

Das Thema Recht hat in den letzten Jahren enorm in der IHK-Prüfung an Gewicht gewonnen. Insbesondere der Datenschutz und – seit Neuestem – die Barrierefreiheit sind absolute Hype-Themen für Projektanträge und mündliche Prüfungen.

---

## 📑 Inhaltsverzeichnis
1. [🔒 Datenschutzgrundverordnung (DSGVO)](#-datenschutzgrundverordnung-dsgvo)
2. [♿ Barrierefreiheitsstärkungsgesetz (BFSG)](#-barrierefreiheitsstärkungsgesetz-bfsg)
3. [© Urheberrecht & Lizenzen (Open Source)](#-urheberrecht--lizenzen-open-source)

---

## 🔒 Datenschutzgrundverordnung (DSGVO)

Die wichtigste Regel der IT lautet: Personenbezogene Daten sind extrem schützenswert. 

<details open>
<summary><b>Was sind "personenbezogene Daten"?</b></summary>

Alle Einzelangaben, durch die sich eine natürliche Person identifizieren lässt.
- **Eindeutig:** Name, E-Mail (`tobia@gmail.com`), Telefonnummer, Adresse, Ausweisnummer.
- **Indirekt:** Eine dynamische IP-Adresse, eine Kontonummer (IBAN), Standortdaten, ein Gesichtsfoto, ein KFZ-Kennzeichen.

*(Eine Firmen-Info wie z.B. der Konzernumsatz von Microsoft fällt NICHT unter die DSGVO, da es keine private, natürliche Person betrifft!)*
</details>

<details open>
<summary><b>Die Grundprinzipien der DSGVO (Die goldenen 6 Regeln)</b></summary>

Wenn diese Begriffe im Fachgespräch fallen, gewinnst du sofort Punkte:

1. **Rechtmäßigkeit & Transparenz:** Du darfst Daten nur erheben, wenn es ein Gesetz erlaubt (z.B. fürs Finanzamt) oder wenn der Nutzer **aktiv** eingewilligt hat (z.B. Checkbox beim Newsletter).
2. **Zweckbindung:** Wenn der Nutzer seine E-Mail für den Kauf eines Schuhs angibt, darfst du diese E-Mail NICHT heimlich für Werbemails deines Partnershops nutzen!
3. **Datenminimierung:** Du darfst nur abfragen, was du *zwingend* für den aktuellen Zweck brauchst. (Wer einen Newsletter bestellt, muss sein Geburtsdatum nicht zwingend angeben. Das Feld darf kein Pflichtfeld sein!).
4. **Richtigkeit:** Daten müssen aktuell gehalten werden (Pflicht zur Korrektur bei Fehlerhinweis).
5. **Speicherbegrenzung (Recht auf Vergessenwerden):** User können verlangen, dass ihre Profile und Daten endgültig gelöscht werden. Außerdem: Daten müssen gelöscht werden, sobald der Zweck erfüllt ist (und wenn gesetzliche Aufbewahrungsfristen wie das HGB abgelaufen sind).
6. **Integrität und Vertraulichkeit:** Du musst die Daten gegen Hacking sichern (Verschlüsselung, Passwörter hashen, Firewall).
</details>

<details open>
<summary><b>Der DSGVO-Trick für dein Abschlussprojekt!</b></summary>

> [!TIP]
> **IHK-Punkte-Garant:** Baue in deine Bewertungsmatrix (beim Projektantrag oder in der Doku) Kriterien für den Datenschutz ein. Beispiele: *"Ich nutze PostgreSQL statt einen US-Cloud-Service, da die personenbezogenen Daten der Kunden laut DSGVO auf europäischen Servern verbleiben müssen."* oder *"Alle Passwörter werden vor dem Speichern mit BCrypt gehasht (verschlüsselt), um dem Grundsatz der Datenintegrität gerecht zu werden."*
</details>

---

## ♿ Barrierefreiheitsstärkungsgesetz (BFSG)

**Achtung, topaktuelles Pflichtwissen!** Ab Juni 2025 gilt in Deutschland das BFSG. Es ist das Lieblings-Neue-Thema der IHK-Ausschüsse für Web-Entwickler!

<details open>
<summary><b>Was ist das BFSG? (Accessibility / a11y)</b></summary>

Das Gesetz verpflichtet private Unternehmen (Onlineshops, Banken, Streamingdienste, Ticketverkäufer) dazu, ihre digitalen Angebote (Websites, Apps, Geldautomaten) so zu gestalten, dass sie von **Menschen mit Behinderungen (Blinde, Sehbehinderte, Motorisch Eingeschränkte) problemlos genutzt werden können**. 
*(Früher galt das nur für staatliche Behörden, jetzt für fast die gesamte freie Wirtschaft!)*
</details>

<details open>
<summary><b>Wie setzt man Barrierefreiheit (a11y) technisch um?</b></summary>

Das WCAG (Web Content Accessibility Guidelines) gibt die Regeln vor. Wichtige technische Umsetzungen (Perfekt für FIAE Abschlussprojekte!):
- **Alt-Texte:** Jeder `<img src="hund.jpg" alt="Ein brauner Hund spielt im Gras">` muss zwingend mit einem aussagekräftigen Text versehen sein, den der Screenreader blinden Nutzern vorlesen kann.
- **Tastatur-Navigation:** Webseiten müssen komplett **ohne Maus**, nur mit der `TAB`-Taste, `Enter` und `Space` steuerbar sein. (Jeder Button braucht einen `:focus` Outline-Rahmen).
- **Semantisches HTML:** Niemals `<div class="button">` nutzen, immer `<button>`. Elemente wie `<header>`, `<main>`, `<nav>` und saubere Hierarchien (`<h1>` dann `<h2>` dann `<h3>`) nutzen.
- **Farbkontrast:** Der Kontrast zwischen Textfarbe und Hintergrund muss hoch genug sein, damit Sehbehinderte ihn lesen können (z.B. graue kleine Schrift auf weißem Grund ist nun illegal für Shops).
- **ARIA-Tags:** Spezielle HTML-Attribute (`aria-hidden="true"`, `aria-label="..."`) helfen Screenreadern bei komplizierten Elementen (Popups).
</details>

---

## © Urheberrecht & Lizenzen (Open Source)

Wenn du im Praktikum Code schreibst, wem gehört er? Darfst du einfach Code aus GitHub kopieren?

<details open>
<summary><b>Urheberrecht im Betrieb</b></summary>
Das Urheberrecht an sich ist in Deutschland nicht übertragbar. Du bleibst immer der Schöpfer des Codes. ABER: Im Arbeitsvertrag wird zu 100% geregelt, dass die **ausschließlichen Nutzungs- und Verwertungsrechte** an allem, was du während der Arbeitszeit erschaffst, automatisch auf deinen Arbeitgeber übergehen. Du darfst ein Feature aus der Frima *nicht* auf deinen privaten USB-Stick ziehen und verkaufen!
</details>

<details open>
<summary><b>Open Source Lizenzen (Die großen 3)</b></summary>

Ein fiktiver Fall: Du findest einen tollen Slider auf GitHub. Darfst du ihn in dein kommerzielles Projekt kopieren? Das hängt von der Lizenzdatei (`LICENSE`) ab!

1. **MIT License:** Freifahrtschein. Du darfst den Code kopieren, verändern und kommerziell verkaufen. Du musst nur den Original-Urheberrechtsvermerk (die Lizenzdatei) im Source Code belassen. *(Wird für 80% aller Web-Projekte genutzt).*
2. **Apache 2.0:** Sehr ähnlich wie MIT (kommerziell nutzbar). Bietet zusätzlich Schutz vor Patentklagen.
3. **GPL (GNU General Public License) - Der "Virus":** **Vorsicht!** Die GPL hat einen "Copyleft"-Effekt. Wenn du GPL-lizenzierten Code in dein kommerzielles, geschlossenes Projekt einbaust (und es veröffentlichst), wendet sich das Gesetz gegen dich: Du MUSST daraufhin **deinen eigenen, gesamten Quellcode auch unter die GPL stellen und als Open Source freigeben!** Firmen verbieten meist strikt den Einsatz vom GPL-Code, da es das eigene Firmengeheimnis vernichtet.
</details>

---
[Zurück zur Übersicht](../README.md)
