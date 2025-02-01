# -----------------------------------------------
# 2. Samba (SMB) Einrichtung
# -----------------------------------------------

# 1. Samba installieren
sudo apt update && sudo apt install samba -y

# 2. Freigabeordner erstellen
mkdir -p /home/<benutzer>/Freigaben/SMB

# 3. Berechtigungen setzen
sudo chown -R <benutzer>:<benutzer> /home/<benutzer>/Freigaben/SMB
sudo chmod -R 770 /home/<benutzer>/Freigaben/SMB

# 4. Samba-Benutzer anlegen
sudo smbpasswd -a <benutzer>

# 5. Samba-Konfiguration bearbeiten
sudo nano /etc/samba/smb.conf

# Füge den folgenden Abschnitt hinzu oder passe ihn an
[SMB-Freigabe]
   path = /home/<benutzer>/Freigaben/SMB
   browseable = yes
   writable = yes
   guest ok = no
   valid users = <benutzer>
   create mask = 0660
   directory mask = 0770

# 6. Samba-Dienst neu starten
sudo systemctl restart smbd

