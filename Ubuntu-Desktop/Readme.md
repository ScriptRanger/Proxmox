# Ubuntu Server Dokumentation

# Einleitung
# In diesem Repository sammle ich alle relevanten Informationen zur Einrichtung und Konfiguration meines Ubuntu-Servers unter Proxmox.
# Die Dokumentation ist in verschiedene Bereiche unterteilt, um eine klare Struktur zu gewährleisten.

# Inhaltsverzeichnis
# 1. Ubuntu Server
# 2. Samba (SMB) Einrichtung
# 3. Problemlösungen
# 4. Ressourcen

# -----------------------------------------------
# 1. Ubuntu Server
# -----------------------------------------------

# Installation
# Ubuntu Server ISO herunterladen und eine VM in Proxmox erstellen
# Ubuntu mit Standardoptionen installieren und Netzwerk konfigurieren

# Netzwerkkonfiguration
sudo nano /etc/netplan/00-installer-config.yaml
# Statische IP-Adresse eintragen
sudo netplan apply
