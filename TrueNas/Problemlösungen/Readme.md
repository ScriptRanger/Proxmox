🚨 Problemlösungen
Hier sind die wichtigsten Herausforderungen und Lösungen, die wir während der Einrichtung und Migration gefunden haben.

_________________________________________________________________________________________________________________________________

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

__________________________________________________________________________________________________________________________________

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

__________________________________________________________________________________________________________________________________

📆 30.01.2025 - Wiederherstellung der HDDs nach PCIe Passthrough-Änderung

❌ Problem 3: Nach Rückbau von PCIe Passthrough wurden die HDDs nicht mehr erkannt
📌 Ursache:
Nach dem Entfernen von PCIe-Passthrough in Proxmox war der AHCI-Controller nicht mehr aktiv. Das führte dazu, dass die SATA-HDDs in Proxmox nicht mehr sichtbar waren.

✅ Lösung:

Überprüfung des Controllers mit lspci -nnk | grep -iA3 sata
→ Ergebnis: Der AHCI-Controller war sichtbar, aber ohne aktiven Treiber.
Manuelles Laden des AHCI-Treibers mit modprobe ahci
→ Die HDDs wurden sofort wieder erkannt.
Dauerhafte Lösung für Neustarts:
Systemd-Service erstellt, um modprobe ahci beim Booten auszuführen:
bash
Kopieren
Bearbeiten
echo -e "[Unit]
Description=Load AHCI Module
After=systemd-modules-load.service

[Service]
Type=oneshot
ExecStart=/sbin/modprobe ahci

[Install]
WantedBy=multi-user.target" | sudo tee /etc/systemd/system/load-ahci.service
Service aktiviert und gestartet:
bash
Kopieren
Bearbeiten
systemctl enable load-ahci.service
systemctl start load-ahci.service
Neustart-Test durchgeführt:
→ HDDs wurden nach dem Booten automatisch erkannt.
🎯 Lessons Learned:

Nach Deaktivierung von PCIe-Passthrough muss der AHCI-Treiber manuell oder über einen Systemd-Service geladen werden.
Ohne den Treiber bleiben die SATA-HDDs in Proxmox unsichtbar.
Systemd-Service als Fix: Damit wird modprobe ahci bei jedem Boot automatisch ausgeführt.

______________________________________________________________________________________________________________________________________

