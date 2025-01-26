# Plex Dokumentation

In diesem Repository sammle ich alles rund um die Installation, Konfiguration und Optimierung von Plex. 

## Inhalte

- [Einführung](#einführung)
- [Architektur](#architektur)
- [Installation](#installation)
- [Konfiguration](#konfiguration)
- [Problemlösungen](#problemlösungen)
- [Ressourcen](#ressourcen)

---

### Einführung
Kurze Beschreibung, was Plex ist und wofür es verwendet wird.

### Architektur
Bildliche Darstellung des Setups:
- **Proxmox Server:** Hostet TrueNAS und den LXC-Container mit Docker.
- **TrueNAS:** Verwaltert RAID 5 und stellt die SMB-Freigabe für Plex bereit.
- **Plex:** Läuft als Docker-Container in Portainer und greift auf die SMB-Freigabe zu.

### Installation
Schritte zur Installation auf verschiedenen Plattformen (Proxmox, Docker, etc.).

### Konfiguration
Wie man Plex einrichtet und optimiert.

### Problemlösungen
Häufige Probleme und deren Lösungen.

### Ressourcen
Links zu hilfreichen Tools und Dokumentationen.


### Installation
Schritte zur Installation auf verschiedenen Plattformen:
- **Docker:** [Anleitung hier einfügen]
- **Proxmox:** [Anleitung hier einfügen]
- **Bare Metal Server:** [Anleitung hier einfügen]


### Konfiguration
- **Benutzerverwaltung:** Wie Benutzer und Bibliotheken erstellt werden.
- **Optimierung:** Tipps zur Leistung und Transkodierung.
- **Backups:** Wie Plex gesichert wird.


### Problemlösungen
Häufige Probleme und Lösungen:
1. **Fehler bei der Medienerkennung**
   - Lösung: Metadaten manuell bearbeiten oder Ordnerstruktur überprüfen.
2. **Transkodierung langsam**
   - Lösung: Hardware-Transcoding aktivieren, sicherstellen, dass die GPU unterstützt wird.
3. **Fernzugriff funktioniert nicht**
   - Lösung: Portweiterleitung überprüfen (Port 32400).


### Ressourcen
- [Offizielle Plex-Dokumentation](https://support.plex.tv/)
- [Docker Plex Container](https://hub.docker.com/r/linuxserver/plex)
- [Proxmox Wiki](https://pve.proxmox.com/wiki/Main_Page)

3. Markdown-Features

![Plex Logo](https://example.com/plex-logo.png)

# Plex Dokumentation 🚀

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
