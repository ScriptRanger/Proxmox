Problemlösungen SMB Freigabe
# -----------------------------------------------

# Windows blockiert den Zugriff?
reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" /v AllowInsecureGuestAuth /t REG_DWORD /d 1 /f

# Firewall-Einstellungen für Samba korrigieren
sudo ufw allow 445/tcp
sudo ufw allow 139/tcp
sudo ufw reload

# Systemfehler 5 („Zugriff verweigert“) in Windows lösen
net use \\<server-ip>\SMB-Freigabe /user:<benutzer>
