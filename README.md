## WSL2
Dieses Repository hilft, kubernetes (minikube) inklusive aller Tools in WSL2 (Ubuntu) nutzen zu können.
Voraussetzungen sind:

* installiertes WSL2
* Ubuntu 20.04 (default)
* eingerichteter lokaler Benutzer

### Cisco AnyConnect

Im local network kein Problem, sobald mit VPN (Cisco AnyConnect) verbunden, geht die Konnektivität verloren.

### Workaround 

[github wsl-vpnkit](https://github.com/sakai135/wsl-vpnkit)

Download des [latest release](https://github.com/sakai135/wsl-vpnkit/releases) als .tar.gz

Import in WSL:  
``` powershell
# PowerShell

wsl --import wsl-vpnkit $env:USERPROFILE\wsl-vpnkit wsl-vpnkit.tar.gz
wsl -d wsl-vpnkit
```

WSL starten, Autostart fürs vpnkit in das user profile einbinden.
``` bash
# .bashrc, .zshrc, .profile
# am Ende der Datei einfügen
wsl.exe -d wsl-vpnkit service wsl-vpnkit start
```

WSL neu starten! 

``` powershell
wsl --terminate <machine>
```

#### Ansible, k8s, minikube & skaffold
Um die Installation des Toolings möglichst einfach zu gestalten, am besten das Repository der wsl2-tools klonen:
```bash
git clone https://<>:<>/wsl2-tools.git
```

Danach in der WSL2 Konsole, im wsl2-tools Verzeichnis:

```bash
user@machine$: bin/prepare-ansible
user@machine$: bin/provision
```

Hier ist eine längere Wartezeit bis zuerst Ansible + Python Abhängigkeiten installiert ist und dann die Grundeinrichtung des WSL2 Containers erfolgt.
Es werden einige Basis-Pakete installiert, Docker, Start-Scripts, diverse Tools um kubernetes etc. lauffähig zu bekommen.