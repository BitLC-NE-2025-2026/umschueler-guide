# 🤖 Künstliche Intelligenz (ChatGPT, Claude & Co.) richtig nutzen

![KI](https://img.shields.io/badge/Tools-AI_&_LLMs-purple?style=for-the-badge) ![Prompting](https://img.shields.io/badge/Skill-Prompt_Engineering-yellow?style=for-the-badge) ![Formate](https://img.shields.io/badge/Code-Markdown_vs_JSON-brightgreen?style=for-the-badge)

Wer in der IT heute KI ignoriert, ist in 3 Jahren als Entwickler abgehängt. KI ersetzt uns (noch) nicht, aber **ein Entwickler MIT KI ersetzt jeden Entwickler OHNE KI.** 

Das Problem: Die meisten nutzen ChatGPT absolut ineffizient ("Warum geht das nicht?"). Hier lernst du den echten Unterschied zwischen Top-Modellen, Formaten und dem sogenannten *Prompt Engineering*.

---

## 📑 Inhaltsverzeichnis
1. [🧠 Der Modell-Vergleich (Nicht alles ist ChatGPT)](#-der-modell-vergleich-nicht-alles-ist-chatgpt)
2. [✍️ Richtiges Prompting in der IT (Der System Prompt)](#-richtiges-prompting-in-der-it-der-system-prompt)
3. [📄 Markdown vs. JSON (Struktur für die KI)](#-markdown-vs-json-struktur-für-die-ki)
4. [🛑 Die Gefahren: Halluzinationen & Datenschutz](#-die-gefahren-halluzinationen--datenschutz)

---

## 🧠 Der Modell-Vergleich (Nicht alles ist ChatGPT)

"ChatGPT" ist nur das Produkt. "GPT-4" ist das Sprachmodell (LLM, Large Language Model) dahinter. Es gibt auf der Welt aktuell ein hart umkämpftes "Wettrennen" der Big-Tech-Firmen. 

<details open>
<summary><b>Die Top 3 Modelle (Stand: März 2026)</b></summary>

- **1. Anthropic Claude 4.6 (Opus & Sonnet):**
  - *Stärke:* Anthropic hat Anfang 2026 **Claude Opus 4.6** (mit 1-Millionen-Token Fenster) und **Sonnet 4.6** veröffentlicht. Sie sind die unbestrittenen Könige der Code-Generierung. Mit Tools wie *Claude Cowork* und *Claude Code 2.1* agieren sie autonom im Terminal. Claude formuliert deutlich "menschlicher" und halluziniert bei komplexem Refactoring von großen Architektur-Codebases viel seltener als die Konkurrenz.
- **2. OpenAI GPT-5.3 Instant & o3-mini (ChatGPT):**
  - *Stärke:* OpenAI liefert mit **GPT-5.3 Instant** (veröffentlicht März 2026) das flüssigste Konversations- und Programmier-Erlebnis mit drastisch reduzierter Halluzinationsrate. Wenn es allerdings an extrem harte Logik- und Mathematikfragen geht, schaltet man auf das **o3-mini** Modell um, welches durch intensive *Gedankenketten (Reasoning)* C#-Algorithmen vorab tiefgreifend durchdenkt, bevor es tippt.
- **3. Google Gemini 3.1 (Pro & Flash-Lite):**
  - *Stärke:* Die neue "Gemini 3 Ära". **Gemini 3.1 Pro** ist ein gigantischer Alles-Könner, der Code-Repositories, Videos und riesige Datenmengen durch sein riesiges Kontext-Fenster schluckt. **Gemini 3.1 Flash-Lite** besticht durch absurde Geschwindigkeit und Skalierbarkeit.
</details>

<details open>
<summary><b>Code Assistant in der IDE (GitHub Copilot)</b></summary>

Wir tippen Code nicht mehr selbst im Browser bei ChatGPT ein, das dauert zu lange ("Copy & Paste Hell"). 
Als Umschüler mit dem [GitHub Student Pack](./03_Software_Tools.md) erhältst du die **GitHub Copilot** Extension für Visual Studio und VS Code umsonst!
- *Tipp-Vervollständigung (Ghost Text):* Du schreibst einfach den Kommentar `// Generiere eine Methode, die alle Umlaute aus einem String entfernt` und Copilot tippt den perfekten C#-Code in Millisekunden für dich hin. Du bestätigst nur mit der TAB-Taste.
</details>

<details open>
<summary><b>🔥 Der Gamechanger: MCP (Model Context Protocol) & Agentic Workflows</b></summary>

Bis vor kurzem konnten LLMs nur Text im Browser generieren. **MCP (Model Context Protocol)** – ein von Anthropic gestarteter Open-Source-Standard, der 2025/2026 die IT eroberte – ändert alles: Es erlaubt KIs (wie Claude oder GPT), über standardisierte APIs *direkt* und bidirektional mit deinen Enterprise Tools zu sprechen!

- **Wie es funktioniert:** Ein lokaler oder Remote "MCP Server" stellt eine Schnittstelle zu einem Tool bereit (z.B. Slack, GitHub, PostgreSQL, Notion oder deinem Dateisystem). KIs in modernen IDEs (wie *Cursor* oder *Zed*) verbinden sich mit dem Server.
- **Der Nutzen:** Die KI kann nun autonom Befehle ausführen. Du sagst: *"Finde das letzte Ticket in Jira, lese die Bug-Beschreibung, analysiere meine lokale Datenbank dazu und behebe den Fehler im C#-Code."* Die KI lädt die Tickets und DB-Schemas über MCP-Server selbstständig herunter, führt `dotnet build` aus, checkt auf Fehler und liefert die Lösung, ohne dass du auch nur einmal Copy & Paste nutzt!
- **Agentic AI:** Dadurch wird die KI vom reinen "Chatbot" zum "Agenten", der echte Geschäftsprozesse automatisiert und dir wie ein realer Kollege zuarbeitet. Mit den neuesten Updates (2026) können **"MCP Apps"** sogar ihre eigenen kleinen Benutzeroberflächen (UIs) direkt in den Chat rendern.
</details>

---

## ✍️ Richtiges Prompting in der IT (Der System Prompt)

Ein Prompt ist schlichtweg dein "Befehl" an die KI. KIs sind extrem intelligent, aber auch extrem faul und raten gerne, wenn man ungenau ist.

<details open>
<summary><b>Die Anatomie eines perfekten Prompts</b></summary>

Ein guter Entwickler-Prompt besteht aus 3 Teilen:
1. **Rolle (Persona):** *"Du bist ein Senior .NET Backend-Entwickler mit 15 Jahren Erfahrung in Clean Code."* (Das zwingt das Modell, schlechten Anfänger-Code auszublenden).
2. **Kontext & Aufgabe:** *"Hier ist mein aktueller C#-Controller. Er wirft eine NullReferenceException. Finde den Fehler, erkläre ihn kurz und gib mir nur die korrigierte Funktion."*
3. **Einschränkungen (Constraints):** *"Nutze kein Pattern Matching aus C# 12, wir sind noch auf .NET 6. Gib mir nicht das gesamte 300-Zeilen-File zurück, sondern nur den geänderten Snippet."*
</details>

<details open>
<summary><b>Beispiel: Schlechter vs. Guter Prompt</b></summary>

- ❌ **Schlecht:** *"Mein C# Code hat einen Fehler mit der Datenbank. Mach das weg."* (Ergebnis: Die KI rät wild umher, löscht Code und textet dich mit 10 Absätzen voll).
- ✅ **Gut:** *"Rolle: Senior C# Dev. Kontext: Ich nutze Entity Framework Core 8. Wenn ich `_db.Users.ToList()` ausführe, stürzt es ab wegen Timeout. Aufgabe: Erkläre die zwei wahrscheinlichsten Ursachen für einen Timeout in EF Core bei großen Tabellen und zeige ein Code-Beispiel mit asynchronem `ToListAsync()` und `AsNoTracking()` als Lösung."*
</details>

---

## 📄 Markdown vs. JSON (Struktur für die KI)

LLMs verarbeiten Text auf magische Weise, aber auch sie lieben Struktur. Wenn du eine KI bittest, einen Projektplan, ein Formular oder Daten auszuspucken, musst du ihr sagen, *wie* es aussehen soll.

<details open>
<summary><b>Markdown (.md): Für die Lesbarkeit durch den Menschen</b></summary>

Markdown ist das Format, in dem dieser gesamte Guide hier geschrieben ist (Überschriften mit `#`, Listen mit `-`, Fettgedrucktes mit `**`).
- **Anwendung beim Prompten:** *"Erstelle mir einen Lernplan für C#-Grundlagen. Bitte *formatiere die Antwort in sauberem Markdown*, nutze eine Tabelle für den Wochenplan und verwende Emojis zur Strukturierung."*
- **Ergebnis:** Die KI gibt dir einen wunderschön lesbaren, farbigen Text aus, den du sofort in dein Jira, Confluence, GitHub oder ins Notion kopieren kannst.
</details>

<details open>
<summary><b>JSON (JavaScript Object Notation): Für die Weiterverarbeitung durch Maschinen</b></summary>

JSON ist das absolute Standardformat im Backend (APIs). Es nutzt strikte Schlüssel-Wert-Paare (Keys/Values).
- **Anwendung beim Prompten:** Wenn du Daten für eine App generieren möchtest. *"Generiere mir 5 fiktive Deutsche Namen mit Adresse und Alter. **Formatiere deine Antwort EXAKT als gültiges JSON-Array.** Gib absolut keinen Text vor oder nach dem JSON aus!"*
- **Ergebnis (Reine Daten):**
```json
[
  { "name": "Thomas Müller", "alter": 34, "stadt": "München" },
  { "name": "Lisa Schmidt", "alter": 28, "stadt": "Berlin" }
]
```
- **Vorteil:** Du kannst diese JSON-Antwort einfach per "Copy/Paste" nehmen und in deinem C#-Programm in eine Liste aus Objekten deserialisieren (`JsonSerializer.Deserialize<List<User>>(text)`).
</details>

---

## 🛑 Die Gefahren: Halluzinationen & Datenschutz

<details open>
<summary><b>Halluzinationen (Die KI lügt selbstbewusst)</b></summary>

Eine KI "denkt" nicht wirklich, sie berechnet nur das statistisch wahrscheinlichste nächste Wort. 
- Wenn die KI eine Antwort nicht weiß, sagt sie extrem selten *"Ich weiß es nicht"*. Sie **erfindet** eine API, eine C#-Klasse oder eine Methode, die exakt so aussieht, als existiere sie – tut sie aber nicht!
- *"Vertraue, aber verifiziere!"* Führe den generierten Code *immer* in deiner Entwicklungsumgebung aus, bevor du ihn auf Kollegen im Pull-Request loslässt.
</details>

<details open>
<summary><b>Datenschutz in der Firma (Extrem kritisch!)</b></summary>

- Wenn du Code in das Frontend von ChatGPT einfügst, **nutzt OpenAI diesen Code oft, um ihr Modell weiter zu trainieren!**
- Wenn du im Praktikum sensible Daten hast (Datenbank-Passwörter in `.env` Dateien, Kundennamen, streng geheimen Code der neuen Firmen-App) und diesen in ChatGPT einfügst, landest du im schlimmsten Fall vor Gericht, weil das eine Verletzung der Firmengeheimnisse (NDA) oder des Datenschutzes ist.
- **Tipp:** Viele Unternehmen haben für Chatbots eigene Enterprise-Lizenzen (Datenschutz ist dort vertraglich gesichert) oder betreiben eigene kleine LMMs. **Frage im Praktikum explizit nach den Regeln der Firma bezgl. KI-Nutzung!**
</details>

---
[Zurück zur Übersicht](../README.md)
