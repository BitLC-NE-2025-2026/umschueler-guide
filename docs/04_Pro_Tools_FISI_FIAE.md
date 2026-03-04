# 🔧 Die wichtigsten Tools für FISI & FIAE (Praxis-Setup)

![Tools](https://img.shields.io/badge/Hardware-Entwickler_Tools-purple?style=for-the-badge) ![FISI](https://img.shields.io/badge/SysAdmin-FISI-darkblue?style=for-the-badge) ![FIAE](https://img.shields.io/badge/Developer-FIAE-teal?style=for-the-badge)

Die erste Woche im Praktikumsbetrieb. Du bekommst einen (oft völlig leeren) Rechner hingestellt. Was musst du sofort installieren, um professionell und effizient arbeiten zu können?

Hier ist die Checkliste für das ultimative Setup, getrennt nach den Fachrichtungen.

---

## 📑 Inhaltsverzeichnis
1. [🛠️ Allgemeine Must-Haves (Für beide Fachrichtungen)](#-allgemeine-must-haves-für-beide-fachrichtungen)
2. [💻 Setup für Anwendungsentwickler (FIAE)](#-setup-für-anwendungsentwickler-fiae)
3. [⚙️ Setup für Systemintegratoren (FISI)](#-setup-für-systemintegratoren-fisi)

---

## 🛠️ Allgemeine Must-Haves (Für beide Fachrichtungen)

<details open>
<summary><b>1. Ein vernünftiger Browser (Edge / Chrome / Firefox Developer)</b></summary>

Das wichtigste Tool. Nutze niemals den Standard-Internet-Explorer. Installiere mindestens Chrome oder – noch besser für Entwickler – **Firefox Developer Edition** oder **Brave**.
- *Pflicht-Addons:* uBlock Origin (Adblocker), Bitwarden (Passwortmanager), ein JSON-Formatter (damit APIs im Browser nicht wie Datenmüll aussehen).
</details>

<details open>
<summary><b>2. Das Terminal (Windows Terminal)</b></summary>

Die Standard `cmd.exe` ist tot. Installiere das neue **Windows Terminal** (aus dem Microsoft Store).
- Richte Tabs ein.
- Installiere *PowerShell 7* (nicht die vorinstallierte 5er Version!) oder *Git Bash*.
- **Tipp:** Installiere dir [Oh My Posh](https://ohmyposh.dev/), das gibt dir ein wunderschönes Terminal mit Git-Branch-Anzeigen und Farben direkt in der Kommandozeile!
</details>

<details open>
<summary><b>3. Git & Die Macht der GUI (GitKraken)</b></summary>

Jeder Terminal-Purist sagt dir: *"Du musst Git in der Kommandozeile tippen!"* Das stimmt für `git commit` und `git push`. Aber im Berufsalltag mit 15 Kollegen hilft ein gutes **G**raphical **U**ser **I**nterface massiv bei Merge-Konflikten und Tracing!
- **GitKraken** (kostenlos mit dem [GitHub Student Pack](./03_Software_Tools.md)!). Die visuell unschlagbare Lösung. 
  - *Warum?* Es zeigt einen wunderschönen, bunten Commit-Graphen. Du kannst Branches einfach per "Drag & Drop" übereinanderziehen, um sie zu mergen. Du kannst per Klick ein "Interactive Rebase" machen (Commits zusammenfassen), wofür du in der Kommandozeile Kryptologie studiert haben müsstest.
- **Fork** (Extrem schnell, Mac & Windows. Einmalig ~50$, aber unbegrenzt gratis testbar).
- **GitHub Desktop** (Sehr simpel, für den absoluten Einstieg am besten. Wer Angst vor Git hat, startet hier).
</details>

---

## 💻 Setup für Anwendungsentwickler (FIAE)

Als Entwickler bist du 8 Stunden am Tag in deiner IDE. Verbring die Zeit, sie perfekt auf dich abzustimmen!

<details open>
<summary><b>1. Die IDE (Integrated Development Environment)</b></summary>

- **Für C# / .NET:** **Visual Studio 2022 (Community/Professional)** oder – wenn du es dir über die [Schüler-Lizenz](./03_Software_Tools.md) geholt hast – **JetBrains Rider** (extrem schnell und modern).
- **Für Frontend (JS, TS, React) / Python / Go:** **Visual Studio Code (VS Code)**.
- *Visual Studio Code Pflicht-Extensions:*
  - C# Dev Kit (falls du .NET in VS Code machst).
  - Prettier (Code Formatter).
  - GitLens (Zeigt an, wer welche Codezeile wann geschrieben hat – *blame*).
  - Live Server (Für reine HTML/CSS Projekte ohne Backend).
</details>

<details open>
<summary><b>2. Datenbank-Tools (GUI)</b></summary>

Blindes SQL tippen auf der Konsole ist mühsam.
- **DBeaver:** Der Open-Source König. Unterstützt ALLES (MySQL, PostgreSQL, SQLite) aus einer einzigen App heraus.
- **SQL Server Management Studio (SSMS) oder Azure Data Studio:** Wenn deine Firma rein auf Microsoft SQL Server läuft.
</details>

<details open>
<summary><b>3. API Testing (Postman vs. Insomnia vs. Bruno)</b></summary>

Um deine geschriebenen C#-Controller (`[HttpGet] api/users`) zu testen, ohne erst ein Frontend programmieren zu müssen.
- **Postman:** Der Klassiker, aber mittlerweile sehr featurereich und erfordert zwingend einen Cloud-Account.
- **Insomnia:** Etwas aufgeräumter als Postman.
- **Bruno:** **(Geheimtipp!)** Die neue, extrem schlanke Open-Source Alternative. Speichert alles lokal als reine Textdateien (perfekt um sie in Git einzuchecken!).
</details>

<details open>
<summary><b>4. Docker Desktop</b></summary>

Moderne Entwicklung läuft in Containern. Installiere **Docker Desktop** (oder Rancher Desktop). Damit kannst du z.B. eine PostgreSQL Datenbank auf deinem PC hochfahren (`docker run postgres`), ohne den ganzen Müll physisch auf Windows zu installieren.
</details>

---

## ⚙️ Setup für Systemintegratoren (FISI)

Als Sysadmin verbringst du mehr Zeit mit Servern, Netzwerken und Remote-Verbindungen als mit Code.

<details open>
<summary><b>1. SSH & Remote Management (Das Cockpit)</b></summary>

Du kannst dich nicht für jeden Linux-Server über ein separates Terminal anmelden.
- **Termius:** Ein fantastischer, synchronisierter SSH-Client. (Pro-Version ist kostenlos im [GitHub Student Pack](./03_Software_Tools.md)!).
- **mRemoteNG:** Ein Open-Source Tool, um hunderte RDP (Windows Remote Desktop), VNC und SSH Verbindungen in einer einzigen Oberfläche als Tabs zu verwalten. Ein Traum für FISIs.
- **PuTTY:** Der unzerstörbare Klassiker. Sieht aus wie aus 1995, funktioniert immer.
</details>

<details open>
<summary><b>2. Netzwerk-Analyse (Traffic & Ports)</b></summary>

*"Warum erreiche ich den Server nicht?"*
- **Wireshark:** Der weltweite Standard zur Paket-Aufzeichnung. (Achtung: Erfordert ein tiefes Verständnis des OSI-Modells, Layer 2-4). Zeigt absolut* jeden* Traffic an, der durch deine Netzwerkkarte geht.
- **Advanced IP Scanner:** Ein kleines, schnelles Tool, um das lokale Netzwerk (`192.168.x.x`) auf aktive IP-Adressen und geöffnete Ports zu scannen.
- **Nmap (Zenmap):** Das mächtigste Port-Scanning Tool auf dem Markt (Kommandozeile).
</details>

<details open>
<summary><b>3. Virtualisierung (Labor-Umgebung)</b></summary>

Du musst neue Firewall-Roules oder Active-Directory-Setups testen, willst aber nicht die echte Firma lahmlegen?
- **VMware Workstation Pro** oder **VirtualBox:** Um komplette Windows Server oder Linux-Boxen direkt auf deinem Desktop laufen zu lassen. 
- *Achtung Hardware:* Für FISIs gilt: RAM ist Hubraum. Du brauchst auf deinem Arbeitsrechner zwingend **32 GB RAM** oder mehr, um 2-3 VMs gleichzeitig hochfahren zu können.
</details>

<details open>
<summary><b>4. Text-Editor & Scripting</b></summary>

- **Notepad++:** Öffnet Logfiles (`.log`), die 2 Gigabyte groß sind, in Sekundenbruchteilen (dabei würde der normale Windows Texteditor abstürzen).
- **Visual Studio Code:** Auch FISIs scripten! Die IDE deiner Wahl für lange PowerShell-Scripte (`.ps1`) oder Bash-Scripte (`.sh`), um tägliche Sysadmin-Aufgaben zu automatisieren.
</details>

---
[Zurück zur Übersicht](../README.md)
