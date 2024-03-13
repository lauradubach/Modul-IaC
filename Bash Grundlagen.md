# Bash

Bash -> Born again shell

Bash is a command language interpreter. It is widely available on various operating systems and is a default command interpreter on most GNU/Linux systems. The name is an acronym for the ‘Bourne-Again SHell’.

## Shell
Shell is a macro processor which allows for an interactive or non-interactive command execution.

## Scripting
Scripting allows for an automatic commands execution that would otherwise be executed interactively one-by-one.

## Basics
| Befehl | Funktion |
| ---- | ---- |
| `echo $SHELL` | Mit welchem sprach interpreter man arbeitet |
| `echo` | schreiben |
| `man` beliebiger Befehl (zb:`$man ls`) | Zeigt das manual vom Befehl an |
| `>` | estellen oder überschreiben |
| `>>` | erstellen oder hinzufügen |
| `basename $0` | nimmt den Pfad weg und gibt nur den namen des Files aus |
| `$*` | gibt aus was in der variabel steht (eigentlich wie echo) |


## Tools
| Befehl | Funktion |
| ---- | ---- |
| `cat` | File lesen und Ausgeben |
| `head/tail` | nur die ersten oder letzten x Zeilen von File ausgeben |
| `sort` | File sortieren nach verschiedenen Kriterien | 
| `grep` | File filtern nach pattern | 
| `cut` | Einzelne “Spalten” aus File rauslesen |


## File names and permissions
| Befehl | Funktion |
| ---- | ---- |
| `chmod +x FILENAME` | File ausführbar machen |
| `file FILENAME` | er zeigt was für ein File es ist |
| `./FILENAME.sh` | ausführen |
| `$ls -al` | Details zum Inhalt mit Berechtigungen |
| `tar -czf` | (create Zip File) Erstellt ein archiv vom angegebenen Directory Beispiel: echo 'tar -czf /tmp/myhome_directory.tar.gz /home/linuxconfig/' >> backup.sh |

Beispiel:  `echo 'tar -czf /tmp/myhome_directory.tar.gz /home/linuxconfig/' >> backup.sh`
Probably the best analogy to explain a relative vs. absolute file path is to visualise GNU/Linux filesystem as a multiple storey building. The root directory (building’s entrance door) indicated by / provides the entry to the entire filesystem (building), hence giving access to all directories (levels/rooms) and files (people).


## Variables
| Befehl | Funktion |
| ---- | ---- |
| `$` | Ruft eine Variabel auf | 
| `{}` | wenn man eine Variabel angiebt aber danach noch mehr schreibt setzt man die Variabel in {} damit der rest nicht als variabel zählt | 


## Input, Output and error redirections
| Befehl | Funktion |
| ---- | ---- |
| `>` stdout | Output File |
| `2>` stderr | Error File |
| `&>` both stdout & stderr | Beide Files |
| `>/dev/null` | etwas unterdrücken, es passiert nichts |
| `<` stdin | Input File ZB: cat < test.sh / gibt aus was im test.sh steht |
| `[]` | um einen test zu machen |
| `wc -l` | word count, zählt wie viele linien es gibt | 

![Informationskanäle](https://github.com/lauradubach/Modul-IaC/blob/18f7417363d2bf0f90a92d9a6af116e9ce38e35c/Informationskan%C3%A4le.png)

## Numeric and String

| Description | Numeric Comparison | String Comparison | 
| ---- | ---- | ---- |
| less than | -lt | < |
| greater than | -gt | > |
|equal | -eq | = |
| not equal | -ne | != |
| less or equal | -le | N/A |
|greater or equal | -ge | N/A |

## Conditional Statements

`If/then/else`

## Positional Parameters

$1, $2 …. $n

Die Verwendung der -z-Bash-Option in Kombination mit einer bedingten if-Anweisung dient dazu zu überprüfen, ob der positionale Parameter $1 einen Wert enthält. 
-z gibt einfach true zurück, wenn die Länge des Strings, der in unserem Fall die Variable $1 ist, null ist. Ist dies der Fall, setzen wir die Variable $user auf den Namen des aktuellen Benutzers.

## Bash Loops

### For Loop
#### Die For-Loop durchläuft eine Liste von Elementen und führt für jedes Element einen Befehl aus. Dies wird anhand eines Beispiels demonstriert, das die Anzahl der Zeichen in einer Datei zählt.

```bash
for i in 1 2 3; do
echo $i
done
```

### While Loop
#### Die While-Loop führt einen Befehl aus, solange eine Bedingung wahr ist, wie anhand eines Beispiels gezeigt wird, das Zahlen zählt. Die Until-Schleife ist ähnlich der While-Schleife, führt jedoch solange einen Block Code aus, bis eine Bedingung wahr wird.

```bash
while [ $counter -lt 3 ]; do
let counter+=1
echo $counter
done
```

### Until Loop
#### Die "until"-Loop in Bash funktioniert gegenteilig zur "while"-Schleife. Sie führt einen Codeblock solange aus, bis eine Bedingung wahr wird. Der Text liefert ein Beispiel, in dem eine Zählvariable verringert wird, bis sie einen bestimmten Schwellenwert erreicht.

```bash
until [ $counter -lt 3 ]; do
let counter-=1
echo $counter
done
```

## Bash-Arithmetik
1. Arithmetische Expansion: Diese Methode umfasst das Einklammern mathematischer Ausdrücke in doppelte Klammern. Beispiele sind Addition, Subtraktion, Multiplikation und Division.
2. expr-Befehl: Eine weitere Methode ist die Verwendung des expr-Befehls, der arithmetische Operationen ohne Klammern oder Anführungszeichen ermöglicht. Das Multiplikationszeichen muss jedoch zur Vermeidung von Syntaxfehlern maskiert werden.
3. let-Befehl: Ähnlich wie expr bewertet der let-Befehl mathematische Ausdrücke und speichert das Ergebnis in einer Variable. Er unterstützt auch Inkrement- und Exponentenoperationen.
4. bc-Befehl: Für Dezimalberechnungen wird der bc-Befehl verwendet. Er ermöglicht komplexere Operationen und die Kontrolle über die Genauigkeit. Beispiele sind Division, Quadratwurzel und das Festlegen der Genauigkeit mit dem scale-Parameter.

## Klammmern 
| Befehl | Funktion |
| ---- | ---- |
| `()` | Kommandos als subprozess ausführen |
| `${}` | Variablen |
| `` | das gleiche wie: $() |
| `[]` | Array $[name(0)], Tests, Wildcards |
| `$()` | Kommandos ausführen und den Output (stdout) im Skript einfügen |
| `[[]]` | Tests advanced -> manpage bash anschauen |
| `~username` | Pfad von userhome - directory von username |
| `&` | umleiten von Output, Background prozesse |
| `{1..4}` | Aufzählungen |
| `;:` | Trent Kommandos |
| `$(())` | Aritmetische Ops |

## Definition Wildcards
Wildcards sind spezielle Zeichen oder Zeichenfolgen, die in Suchmustern verwendet werden, um flexiblere Suchkriterien festzulegen. Sie ermöglichen es, Teile eines Musters zu ersetzen oder auf beliebige Zeichen zuzugreifen. Wildcards werden häufig beim Durchsuchen von Texten, Dateien und Verzeichnissen sowie beim Schreiben von Skripten oder Programmen verwendet.
In Bash gibt es Wildcards um Files und Directories zu "suchen". Diese sind hier beschrieben. Sie sind komplett verschieden von Wildcards in [regulären Ausdrücken](regular_expression.md).
 
| Wildcard | Description | Example Usage |
| ---- | ---- |
| `*` (asterisk) | Matches any sequence of characters (including none). | `ls *.txt` |
| `?` (question mark) | Matches any single character. | `ls file?.txt`|
| `[ ]` | Matches any character within the brackets. | `ls file[123].txt` |
| `[ - ]` | Matches any character within the specified range. | `ls file[1-3].txt` |
| `{ }` | Matches any of the comma-separated patterns inside. | `mv file{1,2}.txt directory/` |

## Sed
1. Was ist Sed?
Sed steht für Stream Editor und ermöglicht das Bearbeiten von Texten aus der Befehlszeile.

2. Grundfunktionen
Sed bearbeitet Texte zeilenweise und auf nicht-interaktive Weise. Alle Bearbeitungsentscheidungen werden beim Aufrufen des Befehls getroffen, und Sed führt die Anweisungen automatisch aus.

3. Verwendung
Sed ist besonders nützlich für das schnelle und effektive Transformieren von Texten, insbesondere in Skripten oder automatisierten Workflows.

4. Unterschiedliche Versionen
Es gibt sowohl eine GNU-Version als auch eine BSD-Version von Sed, die auf verschiedenen Betriebssystemen verwendet werden.

5. Grundlegende Operationen
Das Tutorial sollte grundlegende Operationen mit Sed abdecken, wie das Drucken von Zeilen, das Löschen von Text, das Ersetzen von Text und das Arbeiten mit Adressbereichen.

6. Beispielanwendungen
Es sollte Beispiele dafür geben, wie Sed verwendet wird, um verschiedene Textbearbeitungsaufgaben zu erledigen.

7. Fortgeschrittene Funktionen
Es kann erwähnt werden, dass Sed auch fortgeschrittenere Funktionen bietet, die in einem späteren Artikel behandelt werden können.

8. Vorsichtsmaßnahmen
Es ist wichtig zu betonen, dass Sed die Originaldatei standardmäßig nicht bearbeitet, es sei denn, der Befehl wird mit der Option "-i" verwendet, die Änderungen direkt in der Datei vornimmt.

Indem diese Punkte in der Dokumentation behandelt werden, erhalten die Leser eine solide Einführung in die Verwendung von Sed und können verschiedene Textbearbeitungsaufgaben effektiv damit erledigen.