# Cloud Init

![CloudInit funktionsweise](https://github.com/lauradubach/Modul-IaC/blob/a869c8ce114075558f7655bf471369ec33210e4f/Cloud%20Init.png) 

## VM & User/Gruppen via Bash erstellen

| Bash befehl | Beschreibung |
| ---- | ---- |
| `$multipass launch` | vm erstellen, restart computer then it works |
| `$multipass list` | nun sehen wir die erstellte VM |
| `$cat /etc/group` | gruppe auslesen |
| `$cat /etc/user` | user auslesen | 
| `$multipass exec "name" sudo apt update` | maschine updaten |
| `$multipass shell "name"` | auf der maschine selbst |
| `$multipass delete --purge "name"` | VM wieder deinstallieren |


## Cloud Init der VM mitgeben

| Bash befehl | Beschreibung |
| ---- | ---- |
| `$multipass set local.driver=hyperv` | driver auf korrekten service stellen |
| `$multipass launch --cloud-init ./.cloud-init/yaml.yml -n test1` | Cloud Init yaml File mitgeben |
| `$multipass ls` | IP auslesen |
| `$ssh "user"@ip Adresse` | ssh testen |
| `$cloud-init status` | status abrufen |
| `$sudo less /var/log/cloud-init.log` | log file anschauen |

## Weitere Infos

| Standort | Nutzen |
| ---- | ---- |
| `/var/lib/cloud/instance` | cache beim starten wird hier abgelegt |
| `- touch /etc/cloud/cloud-init.disabled` | Cloud Init deaktivieren |
| `cloud init generator log` | log vom Cloud Init |
| `/var/lib/cloud/instance/skripts` | Shell skript hinterlegt |

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

## Worpress Server aufsetzten mit Cloud Init

Neue Vm erstellen und erstmal alles von Hand testen.

**Anleitung**
```bash
sudo apt update
sudo apt upgrade
sudo apt install apache2
sudo apt install mariadb-server
sudo apt install php php-mysql
mysql -u root -p
CREATE DATABASE wordpress_db;
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL ON wordpress_db.* TO 'wp_user'@'localhost' IDENTIFIED BY 'password';
exit;
cd /tmp && wget https://wordpress.org/latest.tar.gz
tar -xvf latest.tar.gz
sudo cp -R wordpress /var/www/html/
sudo chown -R www-data:www-data /var/www/html/wordpress/
sudo chmod -R 755 /var/www/html/wordpress/
sudo mkdir /var/www/html/wordpress/wp-content/uploads
sudo chown -R www-data:www-data /var/www/html/wordpress/wp-content/uploads/
 ```

## Cloud Init File

#cloud-config
```bash
# Funktion zum Aktualisieren und Installieren von Paketen
package_update: true
packages:
  - mariadb-server
  - apache2
  - php
  - libapache2-mod-php
  - php-mysql

# Funktion zum Schreiben von Dateien
write_files: 
  - content: |
              <VirtualHost *:80>
              ServerAdmin admin@wordpress.com
              DocumentRoot /var/www/html/
              ServerName wordpress.com
              ServerAlias www.wordpress.com

              <Directory /var/www/html/>
                  Options FollowSymLinks
                  AllowOverride All
                  Require all granted
              </Directory>

              ErrorLog ${APACHE_LOG_DIR}/error.log
              CustomLog ${APACHE_LOG_DIR}/access.log combined
              </VirtualHost>

    path: /etc/apache2/sites-available/wordpress.conf
    permissions: "0644"


# Konfiguration für Apache
runcmd: 
    - sudo cp wordpress.conf /etc/apache2/sites-available/wordpress.conf
    - sudo a2ensite wordpress.conf
    - sudo systemctl reload apache2

# Herunterladen von Wordpress und Konfiguration
    - wget https://wordpress.org/latest.tar.gz
    - tar -xzvf latest.tar.gz
    - sudo cp -r wordpress/* /var/www/html/
    - sudo chown -R www-data:www-data /var/www/html/
    - sudo chmod -R 755 /var/www/html/

# Erstellen einer Datenbank und eines Benutzers für Wordpress
    - sudo mysql -u root -p -e "CREATE DATABASE wordpress;"
    - sudo mysql -u root -p -e "CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'password';"
    - sudo mysql -u root -p -e "GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';"
    - sudo mysql -u root -p -e "FLUSH PRIVILEGES;"
```

**Nun im multipass erstellen:**
`multipass launch --cloud-init ./cloudinit.yml -n wordpress`

**IP Auslesen**
`multipass shell wordpress`
`ip a show`

**Im Browser testen**
172.26.158.165/index.php


