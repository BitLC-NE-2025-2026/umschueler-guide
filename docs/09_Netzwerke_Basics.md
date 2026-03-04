# 🌐 Netzwerke, IPv4 & VLAN Basics

![Netzwerke](https://img.shields.io/badge/Netzwerktechnik-OSI_&_Subnetting-teal?style=for-the-badge) ![IHK-Thema](https://img.shields.io/badge/Prüfungsthema-AP1_&_AP2-critical?style=for-the-badge)

Netzwerktechnik ist der absolute Kern der FISI-Ausbildung, wird in der AP1 aber auch zwingend von Anwendungsentwicklern (FIAE) verlangt. Subnetting kommt in gefühlt jeder zweiten IHK-Prüfung dran!

---

## 📑 Inhaltsverzeichnis
1. [Das OSI-Modell (Die 7 Schichten)](#-das-osi-modell-die-7-schichten)
2. [IPv4 & Subnetting Basics](#-ipv4--subnetting-basics)
3. [VLANs (Virtual Local Area Networks)](#-vlans-virtual-local-area-networks)

---

## 🥪 Das OSI-Modell (Die 7 Schichten)

Um Netzwerke zu verstehen, muss man ihre Schichten kennen. Gehe von unten (Kabel) nach oben (App im Browser):

<details open>
<summary><b>Die 7 Layer + Hardware/Protokolle</b></summary>
1. **Physical Layer (Bitübertragungsebene):** Kabel, Funkwellen, Hubs, Repeater. Verarbeitet nur rohe Bits (1, 0).
2. **Data Link Layer (Sicherungsebene):** **Switches**. Arbeitet mit **MAC-Adressen**. (Pakete heißen hier *Frames*).
3. **Network Layer (Vermittlungsebene):** **Router**. Arbeitet mit **IP-Adressen** (IPv4/IPv6). Hier findet das Routing statt. (Pakete heißen hier *Packets*).
4. **Transport Layer (Transportschicht):** TCP (zuverlässig) und UDP (schnell, unzuverlässig). Arbeitet mit **Ports**.
5. **Session Layer (Sitzungsschicht):** Steuert den Aufbau und Abbau der Verbindungen.
6. **Presentation Layer (Darstellungsschicht):** Datenformatierung, Verschlüsselung (TLS), Komprimierung (z.B. JPG, MPEG).
7. **Application Layer (Anwendungsschicht):** Das, was die App nutzt (HTTP, FTP, SMTP, DNS).
</details>

> [!TIP]
> **Eselsbrücke (Englisch):** **P**lease **D**o **N**ot **T**hrow **S**ausage **P**izza **A**way (Physical, DataLink, Network, Transport, Session, Presentation, Application).

---

## 🧮 IPv4 & Subnetting Basics

IPv4-Adressen bestehen aus 32 Bits (4 Blöcke à 8 Bits / 1 Oktett).

<details open>
<summary><b>Netzanteil, Hostanteil & CIDR</b></summary>

Eine IP ist in zwei Teile gespalten: Welches Teilnetz? Welches Gerät im Teilnetz?
Die **Subnetzmaske** sagt dem PC, wo der Cut gemacht wird.

- IP: `192.168.1.1`
- Subnetzmaske: `255.255.255.0`
- CIDR-Schreibweise: `/24` (Es sind 24 Einsen in der Maske gesetzt: `11111111.11111111.11111111.00000000`)
- **Ergebnis:** Das Netzwerk (`192.168.1.0`) hat Platz für 256 IPs.
</details>

<details open>
<summary><b>Die 2 abgezogenen IPs (Netz- und Broadcast)</b></summary>

In *jedem* Subnetz gibt es zwei IPs, die du **nicht** an Computer/Server vergeben darfst:
1. **Netzwerk-ID:** Die allererste IP im Netz (z.B. `192.168.1.0`). Sie bezeichnet das Netz selbst.
2. **Broadcast-ID:** Die allerletzte IP im Netz (z.B. `192.168.1.255`). Sie ruft alle Geräte im Netz gleichzeitig (als "Schreihals").

*Formel für nutzbare Hosts:* `2^n - 2` (wobei n = Anzahl der Null-Bits im Hostanteil der Subnetzmaske).
*Beispiel bei einem /24 Netz (8 Host-Bits):* `2^8 - 2` = `256 - 2` = **254 nutzbare IPs**.
</details>

---

## 🔪 VLANs (Virtual Local Area Networks)

Ein VLAN zerteilt einen *physikalischen* Switch logisch in mehrere *virtuelle*, komplett voneinander getrennte Switches (Layer 2 - Data Link Layer).

<details open>
<summary><b>Warum VLANs?</b></summary>

- **Sicherheit:** Die Buchhaltung in VLAN 10 kann nicht den Code der Entwickler in VLAN 20 sehen, obwohl beide in den gleichen Hardware-Switch eingesteckt sind.
- **Performance:** Kleinere Broadcast-Domänen. Wenn ein PC in die Gegend "schreit" (Broadcast), hören das nur die PCs in seinem VLAN, nicht das gesamte Firmennetzwerk.
</details>

<details open>
<summary><b>Access Ports vs. Trunk Ports</b></summary>

- **Access Port:** Der Port an dem der PC oder Drucker hängt. Dieser Switch-Port ist ungetaggt und gehört fix zu genau einem VLAN. Der PC weiß gar nicht, dass er in einem VLAN ist.
- **Trunk Port:** Die Verbindungsleitung zwischen *zwei Switches* (oder Switch zu Router). Über diese Leitung müssen oft Pakete für *verschiedene* VLANs fließen. Daher kriegt das Paket hier vorübergehend einen "Tag" (Ein Schild) angeheftet, auf dem steht: *"Ich bin VLAN 10!"* (Protokoll: 802.1Q). Der Ziel-Switch reißt das Schild ab und leitet es an den richtigen Access-Port weiter.
</details>

<details open>
<summary><b>Inter-VLAN Routing</b></summary>
Da VLANs auf Schicht 2 getrennt sind, können sie nicht von sich aus miteinander reden! Will VLAN 10 mit VLAN 20 kommunizieren, zwingen wir das Paket hoch auf Layer 3 (Network Layer). Es muss erst zu einem **Router** (oder einem performanten Layer-3-Switch) fließen. Der Router leitet ("routet") es von Subnetz A (VLAN 10) in Subnetz B (VLAN 20).
</details>

---
[Zurück zur Übersicht](../README.md)
