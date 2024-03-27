## Cloud Init disabeln

Es gibt zwei Optionen die man im Cloud-Init File einfügen kann:

1. Option
```bash
runcmd:
 - touch /etc/cloud/cloud-init.disabled
 ```

2. Option
```bash
runcmd:
- sudo systemctl disable cloud-init
- sudo systemctl disable cloud-init-local
- sudo systemctl disable cloud-config
- sudo systemctl disable cloud-final
```

Zur kontrolle kann man folgenden Befehl benutzen:
`systemctl status cloud-init`

**Es kann sein das es noch einen kurzen reboot benötigt**

## Erstellen von Gitlab Credentials

Zuerst im Github in den Settings ein Token erstellen und diesen dann kopieren und im Skript einfügen

```bash
#!/bin/bash

# Schritt 1: Generiere ein SSH-Schlüsselpaar
ssh-keygen -t rsa -b 4096 -C "laura.dubach@edu.tbz.ch" -f zerotrust -N ""

# Schritt 2: Extrahiere den öffentlichen SSH-Schlüssel
public_key=$(cat zerotrust.pub)


echo '{ "title": "cloudinit", "usage_type": "auth", "expires_at": "'$EXPIRY_TSTAMP'",' > /tmp/json
echo '"key": "'$(cat zerotrust.pub)'" }' >> /tmp/json

# Schritt 3: Hinzufügen des öffentlichen SSH-Schlüssels per REST-API
curl -X POST -H "Authorization: Bearer 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" -H "Accept: application/vnd.github+json" --data @/tmp/json https://api.github.com/user/keys

# Ausgabe für die Benutzer
echo "SSH key generated and added to your account!"
```

Rest-API angaben für GitHub: https://docs.github.com/de/rest/users/keys?apiVersion=2022-11-28

