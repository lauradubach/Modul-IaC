## Beschreibung Ansible

### Control Node:
Der Hauptcomputer, von dem aus Ansible gesteuert wird. Kann auf verschiedenen Geräten ausgeführt werden, einschließlich Laptops, Desktops und Servern.

### Managed Nodes:
Die Ziele, die mit Ansible verwaltet werden sollen, wie Server oder Netzwerkgeräte.

### Inventory:
Eine Liste von verwalteten Nodes mit spezifischen Informationen wie IP-Adressen und Gruppenzuweisungen.

### Playbooks:
Dateien in YAML, die Aktionen für Ansible definieren und einfach zu lesen und zu teilen sind.

### Roles:
Wiederverwendbare Ansible-Inhalte für Plays.

### Tasks:
Aktionen, die auf verwalteten Hosts ausgeführt werden sollen.

### Handlers:
Spezielle Aktionen, die nur bei bestimmten Ereignissen ausgeführt werden.

### Modules:
Code, der auf verwalteten Nodes ausgeführt wird, um bestimmte Aufgaben zu erledigen.

### Plugins:
Erweiterungen für die Kernfähigkeiten von Ansible.

### Collections:
Verteilte Ansible-Inhalte, die Playbooks, Rollen, Module und Plugins enthalten können und über Ansible Galaxy installiert werden können.


## Ansible VM erstellen

Yaml File:
```bash
#cloud-config

ssh_authorized_keys:
  - 

write_files:
  - path: /tmp/zerotrust
    permissions: '0600'
    content: |
    SSH KEY PLACE

runcmd:
  - apt update -y
  - apt install -y python3-pip
  - apt install -y python-is-python3
  - python -m pip install --upgrade pip
  - pip install ansible
  - export GIT_SSH_COMMAND="ssh -i /tmp/zerotrust -o StrictHostKeyChecking=no"
  - git clone git@github.com:lauradubach/ansible.git /opt/ansible_playbooks
  - git clone git@github.com:lauradubach/ansible2.git /opt/ansible_inventory
  - touch /etc/cloud/cloud-init.disabled
```

## Inventory erstellen

Auf der ansible VM ein inventory.ini erstellen und folgendes reinschreiben:
```bash
[myhosts]
IP1
IP2
IP3
```
Nun den Private key auf die VM transferieren:
`multipass transfer iackey ansible:`

Dann auf der VM die Rechte anpassen
`chmod 600 filename`

Nun das ini file ausführen:
`ansible --private-key ~/iackey -i inventory.ini -m ping myhosts`

Als nächstes müssen wir das 3 mal ausführen, damit es die IP`s übernimmt.
Um dies zu umgehen kann man wie folgt vorgehen:

```bash
export ANSIBLE_HOST_KEY_CHECKING=False
ansible -m ping -i inventory.ini hostgroup
unset ANSIBLE_HOST_KEY_CHECKING
```

## Playbook erstellen

Nun erstellen wir ein Playbook:

Zuerst ein playbook.ini File erstellen mit folgendem Input:
```bash
- name: My first play
  hosts: myhosts
  tasks:
   - name: Create file /laura
     ansible.builtin.file:
       path: /laura
       state: touch
```

Nun das Playbook ausführen:
`ansible-playbook --private-key iackey -b  -i inventory.ini playbook.ini`