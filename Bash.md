# Einführung

Bash -> Born again shell

## Bash
Bash is a command language interpreter. It is widely available on various operating systems and is a default command interpreter on most GNU/Linux systems. The name is an acronym for the ‘Bourne-Again SHell’.

## Shell
Shell is a macro processor which allows for an interactive or non-interactive command execution.

## Scripting
Scripting allows for an automatic commands execution that would otherwise be executed interactively one-by-one.

| Befehl | Funktion |
| ---- | ---- |
| `echo $SHELL` | Mit welchem sprach interpreter man arbeitet |
| `echo` | schreiben |
| `cat` | Inhalt von einem File wird angezeigt |
| `chmod +x FILENAME` | File ausführbar machen |
| `file FILENAME` | er zeigt was für ein File es ist |
| `./FILENAME.sh` | ausführen |
| `man` beliebiger Befehl (zb:`$man ls`) | Zeigt das manual vom Befehl an |
| `$ls -al` | Details zum Inhalt mit Berechtigungen |
| `>` | estellen oder überschreiben |
| `>>` | erstellen oder hinzufügen |
| `tar -czf` | (create Zip File) Erstellt ein archiv vom angegebenen Directory Beispiel: echo 'tar -czf /tmp/myhome_directory.tar.gz /home/linuxconfig/' >> backup.sh |
| `$` | Ruft eine Variabel auf | 
| `{}` | wenn man eine Variabel angiebt aber danach noch mehr schreibt setzt man die Variabel in {} damit der rest nicht als variabel zählt | 
| `>` stdout | Output File |
| `2>` stderr | Error File |
| `&>` both stdout & stderr | Beide Files |
| `<` stdin | Input File ZB: cat < test.sh / gibt aus was im test.sh steht |

Beispiel:  echo 'tar -czf /tmp/myhome_directory.tar.gz /home/linuxconfig/' >> backup.sh

Probably the best analogy to explain a relative vs. absolute file path is to visualise GNU/Linux filesystem as a multiple storey building. The root directory (building’s entrance door) indicated by / provides the entry to the entire filesystem (building), hence giving access to all directories (levels/rooms) and files (people).