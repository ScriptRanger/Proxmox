Plex-Server auf Proxmox mit TrueNAS Storage
Überblick
Dieses Projekt beschreibt die Installation und Fehlerbehebung eines Plex-Medienservers, der in einem LXC-Container mit Docker & Portainer auf einem Proxmox-Host läuft. Die Medien liegen auf einer TrueNAS-VM und werden über eine SMB-Freigabe eingebunden.

Setup & Architektur
Host: Proxmox
Container: LXC mit Docker & Portainer
Media Storage: TrueNAS SMB-Share
Mount-Pfad im LXC-Container: /mnt/medien
Docker-Stack-Verwaltung: Portainer
Problemstellung & Lösungen
1. Plex konnte nicht auf Medien zugreifen
Grund:

Plex-Docker-Container lief mit PUID=4001 / PGID=3002, während die Dateien auf TrueNAS plexuser gehörten.
CIFS-Mount in LXC ohne korrekte uid und gid.
Lösung:

Korrekte Mount-Optionen für SMB in LXC:
bash
Kopieren
Bearbeiten
mount -t cifs -o username=plexuser,password='+Plex@2025!8165',iocharset=utf8,uid=4001,gid=3002 //192.168.178.6/Medien /mnt/medien
TrueNAS plexuser wurde der Gruppe mediagroup hinzugefügt, um Schreib-/Lesezugriff zu gewähren.
Plex-Container wurde gestoppt, gelöscht und neu erstellt, damit er die neuen Berechtigungen nutzt.
2. Unterordner wurden nicht in Plex angezeigt
Grund:

Plex erkennt standardmäßig keine Unterordner rekursiv.
Berechtigungen waren nicht korrekt vererbt.
Lösung:

Manuelles Scannen der Bibliothek in Plex angestoßen.
Berechtigungen von /mnt/medien überprüft & rekursiv gesetzt:
bash
Kopieren
Bearbeiten
chmod -R 775 /mnt/medien
chown -R plexuser:mediagroup /mnt/medien
3. Performance-Optimierung für Plex
LXC-Container hat jetzt 8 Kerne & 16GB RAM.
Transkodierung: Wird aktuell CPU-basiert durchgeführt → GPU-Beschleunigung als nächster Schritt.
Offene Aufgaben
Performance-Tests mit mehreren gleichzeitigen Streams.
GPU-Beschleunigung für Plex-Transcoding testen.
TrueNAS auf CORE umstellen & SMB-Integration prüfen.
