# Cloud Init

![CloudInit funktionsweise](https://github.com/lauradubach/Projektmanagement/blob/b54d9074a289cf795378d3fca5205d6e6c9d355d/Cloud%20Init.png)

## VM & User/Gruppen via Bash erstellen

| Bash befehl | Beschreibung |
| ---- | ---- |
| $multipass launch | vm erstellen, restart computer then it works |
| $multipass list | nun sehen wir die erstellte VM |
| $cat /etc/group | gruppe auslesen |
| $cat /etc/user | user auslesen | 
| $multipass exec "name" sudo apt update | maschine updaten |
| $multipass shell "name" | auf der maschine selbst |
| $multipass delete --purge "name" | VM wieder deinstallieren |


## Cloud Init der VM mitgeben

| Bash befehl | Beschreibung |
| ---- | ---- |
| $ multipass set local.driver=hyperv | driver auf korrekten service stellen |
| $ multipass launch --cloud-init ./.cloud-init/yaml.yml -n test1 | Cloud Init yaml File mitgeben |
| $multipass ls | IP auslesen |
| $ssh "user"@ip Adresse | ssh testen |
| $cloud-init status | muss done |
| $sudo less /var/log/cloud-init.log | log file anschauen |

/var/lib/cloud/instance -> cache beim starten wird hier abgelegt

## Boot Stages Cloud Init

**Detect (Erkennen):**
    In dieser Phase erkennt das Cloud-Init-System die Umgebung, in der es ausgeführt wird. Dazu gehört die Erkennung der virtuellen Maschine, des Hypervisors oder der Cloud-Plattform, auf der die Instanz läuft.

**Local (Lokal):**
    Nach der Erkennung der Umgebung erfolgt in dieser Phase das Einlesen von Konfigurationsdaten, die lokal auf dem System gespeichert sind. Diese Daten können beispielsweise in einem Image oder einer lokalen Konfigurationsdatei vorhanden sein.

**Network (Netzwerk):**
    Anschließend versucht Cloud-Init, eine Netzwerkverbindung herzustellen, um weitere Konfigurationsdaten aus externen Quellen zu laden. Dies kann über DHCP, statische IP-Konfigurationen oder andere Netzwerkmechanismen erfolgen.

**Config (Konfiguration):**
    In diesem Stadium werden die eigentlichen Konfigurationsschritte ausgeführt. Cloud-Init liest Konfigurationsdaten aus verschiedenen Quellen wie Cloud-Metadaten, benutzerdefinierten Skripten oder Konfigurationsdateien und wendet sie auf das System an. Dies umfasst das Einrichten von Benutzern, das Konfigurieren von Netzwerkeinstellungen, das Installieren von Paketen und das Ausführen von benutzerdefinierten Skripten.

**Final (Abschluss):**
    Schließlich werden in dieser Phase abschließende Aufgaben ausgeführt, die für den erfolgreichen Abschluss des Bootvorgangs erforderlich sind. Dazu gehört beispielsweise das Ausführen von Post-Init-Skripten, das Starten von Diensten oder das Melden des Abschlusses an das zugrunde liegende Cloud-Management-System.

**Datasource (stage detect):**
Im logfile /var/log/cloud-init.log nach datasource suchen. ISO ist in /dev/vda vorhanden
Nun muss man dies mounten -> sudo mount /dev/vda /mnt -> cd /mnt  ->  ls
Nun sehen wir die entsprechenden dateien: meta-data user-data und vendor-data. 

Dieses ISO enthaltet alle Konfigurationsdateien 
