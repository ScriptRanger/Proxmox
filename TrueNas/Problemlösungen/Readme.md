🚨 Problemlösungen
Hier sind die wichtigsten Herausforderungen und Lösungen, die wir während der Einrichtung und Migration gefunden haben.

📆 28.01.2025 - TrueNAS CORE & Plex Jail Setup
❌ Problem 1: Plex konnte nicht auf Medien zugreifen
📌 Ursache:

Plex-Docker-Container lief mit PUID=4001 / PGID=3002, während die SMB-Freigabe auf TrueNAS einen anderen Benutzer nutzte.
Falsche Mount-Optionen führten dazu, dass Plex keinen Zugriff hatte.
✅ Lösung:

Richtige UID/GID in Docker-Container setzen
SMB-Freigabe mit korrekten Mount-Optionen eingebunden
Plex-Container neu erstellt
❌ Problem 2: Plugins lassen sich nicht installieren (Fehler: 13.2-RELEASE not found!)
📌 Ursache:

TrueNAS CORE versuchte alte FreeBSD 13.2-Plugins zu laden, die nicht mehr verfügbar sind.
Offizielle Plugin-Unterstützung in TrueNAS CORE wurde praktisch eingestellt.
✅ Lösung:

Manuelle Installation der Jails mit FreeBSD 13.4-RELEASE
Netzwerkprobleme behoben, VNET & Bridge0 für Plex optimiert
📆 29.01.2025 - Entscheidung für TrueNAS SCALE & Docker
Nachdem sich herausgestellt hat, dass TrueNAS CORE nicht mehr zukunftssicher für Plugins ist, wurde die Entscheidung getroffen:

🚀 Umstieg auf TrueNAS SCALE

Docker & Kubernetes statt veralteter Jails
Industrie-Standard für Containerisierung nutzen
Volle Flexibilität für Plex, Nextcloud & zukünftige Services
✅ Warum SCALE?

Docker-Support ohne Hacks
Einfache Integration von Apps & Updates
Kubernetes für fortgeschrittene Skalierung
🎯 Lessons Learned & Fazit
TrueNAS CORE ist für Storage top, aber Plugins sind tot.
Für moderne Setups ist Docker/Kubernetes in SCALE der bessere Weg.
VNET & Bridge0 sind essenziell für Netzwerkstabilität.
UID/GID-Berechtigungen sauber setzen, um SMB-Probleme zu vermeiden.
Plex läuft besser unter Docker als in einer Jail.
🔗 Ressourcen
📌 Offizielle TrueNAS-Dokumentation → TrueNAS Docs
📌 Proxmox & TrueNAS Integration → Proxmox Wiki
📌 Plex Media Server Setup → Plex Support
📌 Docker & Kubernetes Einführung → Docker Docs

🚀 Nächste Schritte
1️⃣ TrueNAS SCALE final einrichten
2️⃣ Plex als Docker-Container sauber installieren
3️⃣ Docker-Volumes für Medienstruktur optimieren
4️⃣ Zusätzliche Apps testen (Nextcloud, Home Assistant, etc.)

📌 Fazit:
💡 TrueNAS CORE war ein guter Test, aber die Zukunft liegt in SCALE & Docker.
💡 Die Entscheidung für SCALE war ein logischer Schritt in Richtung professionelle, skalierbare Lösungen.
💡 Mit diesem Setup ist Plex optimal für Zukunft & Industrie-Standards gerüstet.
