# Git & GitHub Grundlagen für Einsteiger

![Git](https://img.shields.io/badge/Version_Control-Git-F05032?style=for-the-badge&logo=git&logoColor=white) 

Git ist das wichtigste Werkzeug für jeden Entwickler. In der Umschulung und später im Job kommst du nicht daran vorbei. Hier sind die absoluten Basics, um Fehler zu vermeiden und sicher im Team (oder alleine) zu arbeiten.

---

## 🛠️ Der tägiche Workflow

Der Lebenszyklus deiner Code-Änderungen in Git besteht meist aus diesen 4 Schritten:

<details>
<summary><b>1. Status prüfen (Immer!)</b></summary>

Bevor du etwas machst, schau dir an, wo du gerade bist.
```bash
git status
```
*Zeigt dir an, in welchem Branch du bist und welche Dateien verändert wurden.*
</details>

<details>
<summary><b>2. Änderungen hinzufügen (Staging Area)</b></summary>

Du hast Code geschrieben. Jetzt sagst du Git, welche geänderten Dateien für den nächsten Speicherpunkt ("Commit") vorgesehen sind.
```bash
git add dateiname.cs    # Eine bestimmte Datei hinzufügen
git add .               # Alle geänderten Dateien hinzufügen
```
</details>

<details>
<summary><b>3. Änderungen speichern (Commit)</b></summary>

Jetzt schnürst du das Paket. Ein Commit braucht immer eine kurze, aussagekräftige Nachricht.
```bash
git commit -m "feat: login formular hinzugefügt"
git commit -m "fix: berechnungsfehler in rechnung.cs behoben"
```
</details>

<details>
<summary><b>4. Hochladen (Push)</b></summary>

Bisher liegt alles nur lokal auf deinem PC. Um es auf GitHub (oder GitLab/Bitbucket) zu sichern:
```bash
git push -u origin main  # Beim allerersten Mal für den Branch 'main'
git push                 # Später reicht das hier
```
</details>

---

## 🌿 Branches: Sicher experimentieren

Arbeite **niemals** direkt auf dem `main` (oder `master`) Branch, wenn du ein größeres Feature entwickelst! Erstelle immer eine Arbeitskopie (einen Branch).

```bash
# Einen neuen Branch erstellen und direkt dorthin wechseln
git checkout -b feature/mein-neues-feature

# Zurück zum main Branch wechseln
git checkout main

# Alle Branches anzeigen
git branch
```

---

## ⚠️ Hilfe! Ich habe etwas kaputt gemacht.

Keine Panik, das passiert jedem.

<details>
<summary><b>Änderungen an einer Datei rückgängig machen (vor dem Commit)</b></summary>

```bash
git restore dateiname.cs  # Setzt die Datei auf den letzten Speicherstand zurück
```
</details>

<details>
<summary><b>Den letzten Commit ändern (Tippfehler in der Nachricht)</b></summary>

```bash
git commit --amend -m "Neue, korrekte Nachricht"
```
</details>

<details>
<summary><b>Einen fehlerhaften Commit komplett rückgängig machen</b></summary>

*Sicherer Weg (erstellt einen "Gegen-Commit", der die Änderungen aufhebt):*
```bash
git revert <commit-hash>
```
</details>

<br>

> [!TIP]
> **Best Practice:** Committe oft! Ein Commit ist kostenlos. Je öfter du speicherst, desto genauer kannst du später zu funktionierendem Code zurückspringen, wenn du dich verrannt hast.

---
[Zurück zur Übersicht](../README.md)
