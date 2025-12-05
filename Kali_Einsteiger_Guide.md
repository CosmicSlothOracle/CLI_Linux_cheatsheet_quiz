# Kali Linux Einsteiger-Guide – Kompakte Checkliste & Tool-Übersicht

## 1. Grund-Setup nach Installation

### System aktualisieren
```bash
sudo apt update && sudo apt full-upgrade -y
```

### Kali-Tweaks nutzen
```bash
sudo kali-tweaks
```
Empfohlen:
- Shell konfigurieren (Zsh)
- Mirrors optimieren
- VM-Optimierungen aktivieren
- Hardening-Optionen setzen

### Firewall einrichten (UFW)
```bash
sudo apt install ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable
```

---

## 2. Wichtige Metapackages
Metapackages = Tool-Sammlungen.

**Für Einsteiger besonders geeignet:**
- `kali-linux-top10` – wichtigste Standardtools  
- `kali-linux-default` – vollständige Desktop-Grundausstattung

Installation:
```bash
sudo apt install kali-linux-top10
```

Weitere Sets (optional):
- `kali-tools-web` – Web-Pentesting
- `kali-tools-802-11` – WLAN
- `kali-tools-reverse-engineering` – RE & Exploit-Dev

---

## 3. Must-Have Tools für Einsteiger

### Netzwerk & Recon
- **Nmap** – Portscanner  
- **Wireshark** – Traffic analysieren  

Installation:
```bash
sudo apt install nmap wireshark
```

### Web & Dienste
- **Burp Suite Community** – HTTP/S interception  
- **sqlmap** – SQL Injection Tests

```bash
sudo apt install burpsuite sqlmap
```

### Exploitation
- **Metasploit Framework**
```bash
sudo apt install metasploit-framework
```

### Passwörter
- **Hydra** – Passwort-/Service-Bruteforce  
- **John the Ripper** – Cracken offline-Hashes

```bash
sudo apt install hydra john
```

### WLAN (optional)
- **Aircrack-ng Suite**
```bash
sudo apt install aircrack-ng
```

---

## 4. Komfort- und Entwickler-Tools

### Shell und Workflow
```bash
sudo apt install zsh tmux
```

### Entwicklungsumgebung
```bash
sudo apt install git curl build-essential neovim
```

### GUI-Werkzeuge
```bash
sudo apt install kali-system-gui
```

---

## 5. Netzwerk, VPN & Remote

### VPN
```bash
sudo apt install openvpn wireguard
```

### SSH
```bash
sudo apt install openssh-server
```

### VM-Optimierungen
- VMware Tools / VirtualBox Guest Additions installieren  
- Bessere Grafik-Performance  
- Datei-Sharing  
- Copy/Paste  

---

## 6. Lernressourcen (für Einsteiger empfohlen)
- Kali-Dokumentation  
- Nmap/Wireshark Learning Guides  
- Burp Suite Academy (kostenlos)  
- Einsteiger-Checklisten wie „Things to do after installing Kali Linux“  
- Cheat-Sheets für Nmap, Metasploit, sqlmap  

---

## 7. TL;DR – Minimale Setup-Empfehlungen

1. System updaten  
2. Kali Tweaks durchgehen  
3. `kali-linux-top10` installieren  
4. Basis-Tools:  
   - `nmap`, `wireshark`, `burpsuite`, `sqlmap`,  
   - `metasploit-framework`, `hydra`, `john`  
5. Komfort:  
   - `zsh`, `tmux`, `git`, `curl`, `build-essential`, `neovim`  
6. VPN + SSH + VM-Optimierung  

---

## 8. Best Practices für Einsteiger
- Nicht dauerhaft als root arbeiten  
- Tools an Dummy-Zielen (Test-Labs) ausprobieren  
- Schrittweise lernen, kein Tool-Overkill  
- Logs lesen & dokumentieren  
- Skripte langsam und bewusst erweitern  

---

## 9. Abschluss
Diese Datei bietet die wesentlichen Schritte für einen erfolgreichen Einstieg in Kali Linux, ohne den Anfänger zu überfordern. Folge der Reihenfolge von oben nach unten und du hast ein stabiles, funktionsreiches, aber kontrolliertes System.
