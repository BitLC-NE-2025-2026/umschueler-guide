# 🐙 Git & GitHub Grundlagen für Einsteiger

![Git](https://img.shields.io/badge/Version_Control-Git-F05032?style=for-the-badge&logo=git&logoColor=white) ![Workflow](https://img.shields.io/badge/Daily_Basis-Must_Know-blue?style=for-the-badge) ![GitHub](https://img.shields.io/badge/Plattform-GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

Git ist das absolut wichtigste Werkzeug für jeden Entwickler. In der Umschulung und später im Job kommst du (zum Glück) nicht daran vorbei. Hier sind die absoluten Basics, um Versions-Chaos zu vermeiden und sicher im Team (oder an eigenen Projekten) zu arbeiten.

---

## 📑 Inhaltsverzeichnis
1. [🛠️ Der tägliche Workflow (Die 4 Schritte)](#-der-tägliche-workflow-die-4-schritte)
2. [🌿 Branches: Sicher experimentieren](#-branches-sicher-experimentieren)
3. [⚠️ Hilfe! Ich habe etwas kaputt gemacht](#-hilfe-ich-habe-etwas-kaputt-gemacht)

---

## 🛠️ Der tägliche Workflow (Die 4 Schritte)

Der Lebenszyklus deiner Code-Änderungen in Git besteht fast immer aus diesen rotierenden 4 Schritten:

<details open>
<summary><b>1. Status prüfen (Mache das vor allem anderen!)</b></summary>

Bevor du etwas commitest oder pullst, schau dir an, wo du gerade bist. Das verhindert 90% aller Anfängerfehler.
```bash
git status
```
*Zeigt dir an, in welchem Branch du dich befindest und welche Dateien seit dem letzten Speichern verändert wurden.*
</details>

<details open>
<summary><b>2. Änderungen hinzufügen (Staging Area)</b></summary>

Du hast Code geschrieben. Jetzt sagst du Git, welche der geänderten Dateien für den nächsten Speicherpunkt ("Commit") vorgesehen sind.
```bash
git add dateiname.cs    # Nur eine ganz bestimmte Datei hinzufügen
git add .               # Einfach ALLES im aktuellen Ordner hinzufügen
```
</details>

<details open>
<summary><b>3. Änderungen speichern (Commit)</b></summary>

Jetzt schnürst du das Paket zusammen. Ein Commit braucht immer eine kurze, aussagekräftige Nachricht, damit du später noch weißt, was du da eigentlich getan hast.
```bash
git commit -m "feat: login formular hinzugefügt"
git commit -m "fix: berechnungsfehler in rechnung.cs behoben"
```
</details>

<details open>
<summary><b>4. Hochladen (Push)</b></summary>

Bisher liegt alles nur lokal (!) auf deinem eigenen PC. Um es "in die Cloud" auf GitHub (oder GitLab/Bitbucket) zu sichern:
```bash
git push -u origin main  # Beim allerersten Mal für einen neuen Branch 'main'
git push                 # Bei allen weiteren Malen reicht das kurze Kommando
```
</details>

> [!TIP]
> **Best Practice:** Committe oft! Ein Commit ist völlig kostenlos. Je öfter (und kleinteiliger) du speicherst, desto genauer kannst du später zu funktionierendem Code zurückspringen, wenn du dich in einem Bug verrannt hast.

---

## 🌿 Branches: Sicher experimentieren

Arbeite **niemals** direkt auf dem `main` (oder `master`) Branch, wenn du ein größeres, potenziell fehlerhaftes Feature entwickelst! Erstelle immer eine frische Arbeitskopie, einen sogenannten "Branch". So bleibt der `main` Branch immer funktionsfähig (deployable).

<details open>
<summary><b>Wichtige Branching-Befehle</b></summary>

```bash
# Einen neuen Branch namens 'feature/login' erstellen und direkt dorthin wechseln
git checkout -b feature/login

# Zurück zum 'main' Branch wechseln (deine Feature-Änderungen bleiben im anderen Branch sicher!)
git checkout main

# Alle lokalen Branches auflisten (um zu sehen, wo man gerade ist)
git branch
```
</details>

---

## ⚠️ Hilfe! Ich habe etwas kaputt gemacht

Keine Panik, Fehler in Git lassen sich fast immer beheben (solange du noch nicht gepusht hast, ist es super einfach).

<details open>
<summary><b>Ich habe Code in einer Datei gelöscht/geändert und will den ursprünglichen Stand zurück (vor dem Commit)</b></summary>

```bash
git restore dateiname.cs  # Setzt die Datei hart auf den letzten Speicherstand zurück
```
</details>

<details open>
<summary><b>Ich habe einen Tippfehler in meiner allerletzten Commit-Nachricht gemacht</b></summary>

```bash
git commit --amend -m "Neue, korrekte Nachricht ohne Tippfehler"
```
</details>

<details open>
<summary><b>Ich habe einen fehlerhaften Code commitet und will den GANZ rückgängig machen</b></summary>

Ein Revert ist der sicherste Weg, besonders wenn du schon auf GitHub gepusht hast. Es löscht den fehlerhaften Commit nicht aus der Historie (was böse wäre), sondern erstellt einen *neuen "Gegen-Commit"*, der exakt die entgegengesetzten Änderungen vornimmt.
```bash
# Finde zuerst die Commit-ID heraus:
git log --oneline

# Mache die Änderungen dieses Commits rückgängig:
git revert <commit-hash>
```

> [!CAUTION]
> Verwende niemals Befehle wie `git reset --hard`, wenn du die Änderungen bereits auf GitHub `gepusht` hast und mit anderen zusammenarbeitest. Das zerschießt die Historie deiner Kollegen!
</details>

---
[Zurück zur Übersicht](../README.md)
