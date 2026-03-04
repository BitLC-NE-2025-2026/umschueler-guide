# 🗄️ Datenbanken Basics & SQL Cheatsheet

![Datenbanken](https://img.shields.io/badge/Datenbanken-SQL_&_NoSQL-blue?style=for-the-badge) ![IHK-Thema](https://img.shields.io/badge/Prüfungsthema-AP1_&_AP2-critical?style=for-the-badge)

Ob Fachinformatiker für Anwendungsentwicklung (FIAE) oder Systemintegration (FISI) – relationale Datenbanken und SQL sind zwingender Prüfungsstoff in AP1 und AP2. Hier sind die absoluten Basics komprimiert zusammengefasst.

---

## 📑 Inhaltsverzeichnis
1. [🏗️ Normalisierung (1NF, 2NF, 3NF)](#-normalisierung-1nf-2nf-3nf)
2. [ER-Modell & Kardinalitäten](#-er-modell--kardinalitäten)
3. [📜 SQL-Basics (DML, DDL)](#-sql-basics-dml-ddl)

---

## 🏗️ Normalisierung (1NF, 2NF, 3NF)

Datenbank-Tabellen müssen "normalisiert" werden, um Redundanzen (doppelte Daten) und Anomalien (Fehler beim Ändern/Löschen) zu vermeiden. Die IHK fragt meist nach der 3. Normalform.

<details open>
<summary><b>Die 3 Normalformen einfach erklärt</b></summary>

- **0NF (Ursprungsform):** Eine große flache Excel-Tabelle, in der z.B. mehrere Artikel in einer Zelle per Komma getrennt stehen ("Apfel, Birne").
- **1. Normalform (1NF) - "Atomar"**: Jedes Feld (jede Zelle) darf nur **einen** unteilbaren Wert enthalten. Aus "Apfel, Birne" werden zwei separate Datensätze.
- **2. Normalform (2NF) - "Voll funktional abhängig"**: Die Tabelle ist in der 1NF. Außerdem muss jedes Nicht-Schlüssel-Attribut voll vom kompletten Primärschlüssel abhängen. *(Oft gelöst durch das Aufteilen einer großen Tabelle in zwei Tabellen, z.B. `Kunden` und `Bestellungen`, verbunden durch IDs).*
- **3. Normalform (3NF) - "Keine transitiven Abhängigkeiten"**: Die Tabelle ist in der 2NF. Kein bestimmendes Attribut darf von einem anderen bestimmenden Attribut abhängen. (z.B. PLZ und Ort zusammen in einer Tabelle mit der Kundenadresse ist böse, da Ort von PLZ abhängt -> PLZ/Ort in eigene Tabelle auslagern!).

> [!TIP]
> **Eselsbrücke für die IHK:** "Löse die Listenstruktur auf (1NF), lagere thematische Blöcke aus (2NF) und entferne versteckte Abhängigkeiten unter Nicht-Schlüsseln (3NF)."
</details>

---

## 🔀 ER-Modell & Kardinalitäten

Das Entity-Relationship-Modell (ERM) visualisiert die Datenbankstruktur.

<details open>
<summary><b>Die 3 wichtigsten Kardinalitäten</b></summary>

1. **1:1 (Eins zu Eins):** Ein Mitarbeiter hat exakt einen Firmenwagen. Ein Firmenwagen gehört exakt einem Mitarbeiter.
2. **1:n (Eins zu Viele):** Eine Abteilung hat viele Mitarbeiter (n). Ein Mitarbeiter gehört aber nur zu exakt einer Abteilung (1). *(Dies wird über einen Fremdschlüssel = Foreign Key gelöst).*
3. **m:n (Viele zu Viele):** Ein Autor schreibt viele Bücher. Ein Buch kann von vielen Autoren geschrieben werden. *(Vorsicht: RDBMS können m:n nicht direkt speichern! Du musst hierfür zwingend eine **Zwischentabelle / Auflösungstabelle** (Assoziative Entität) bauen!).*
</details>

---

## 📜 SQL-Basics (DML & DDL)

<details open>
<summary><b>DDL (Data Definition Language) - Struktur der DB ändern</b></summary>

Um Tabellen anzulegen oder zu ändern.

```sql
-- Tabelle erstellen
CREATE TABLE Kunden (
    KundenId INT PRIMARY KEY IDENTITY(1,1),
    Vorname VARCHAR(50) NOT NULL,
    Nachname VARCHAR(50) NOT NULL
);

-- Spalte hinzufügen
ALTER TABLE Kunden ADD Email VARCHAR(100);

-- Tabelle löschen (komplett!)
DROP TABLE Kunden;
```
</details>

<details open>
<summary><b>DML (Data Manipulation Language) - Daten bearbeiten</b></summary>

Das klassische **C**RUD (Create, Read, Update, Delete).

```sql
-- INSERT (Create)
INSERT INTO Kunden (Vorname, Nachname) VALUES ('Max', 'Mustermann');

-- SELECT (Read)
SELECT Vorname, Nachname FROM Kunden WHERE Nachname = 'Mustermann' ORDER BY Vorname ASC;

-- UPDATE (Update)
UPDATE Kunden SET Email = 'max@test.de' WHERE KundenId = 1;

-- DELETE (Delete)
DELETE FROM Kunden WHERE KundenId = 1; 
-- ACHTUNG: Ohne WHERE-Klausel löscht du alle Einträge der Tabelle!
```
</details>

<details open>
<summary><b>JOINs (Tabellen verknüpfen)</b></summary>

Um bei 1:n Beziehungen Daten aus beiden Tabellen gemeinsam abzufragen.

```sql
-- INNER JOIN (holt nur Datensätze, bei denen es Treffer in BEIDEN Tabellen gibt)
SELECT k.Vorname, b.Bestelldatum 
FROM Kunden k
INNER JOIN Bestellungen b ON k.KundenId = b.KundenId;

-- LEFT JOIN (holt ALLE Kunden, auch die, die noch nie was bestellt haben. Bestelldatum ist dann NULL)
SELECT k.Vorname, b.Bestelldatum 
FROM Kunden k
LEFT JOIN Bestellungen b ON k.KundenId = b.KundenId;
```
</details>

<details open>
<summary><b>Aggregatfunktionen & GROUP BY</b></summary>

Wenn man Dinge zählen oder summieren will.
```sql
-- Zähle, wie viele Bestellungen JEDER Kunde gemacht hat.
-- Jede Spalte im SELECT, die KEINE Aggregatfunktion (COUNT, SUM) ist, MUSS ins GROUP BY aufgenommen werden!
SELECT k.KundenId, k.Nachname, COUNT(b.BestellId) AS AnzahlBestellungen
FROM Kunden k
LEFT JOIN Bestellungen b ON k.KundenId = b.KundenId
GROUP BY k.KundenId, k.Nachname;
```
</details>

---
[Zurück zur Übersicht](../README.md)
