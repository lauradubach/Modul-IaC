REGEX -> Regular expressions

Zum Beispiel gängiger Befehl
````
sed -n 's/Server/Host/p' practise.txt
````
Ersetzt im File "practise.txt" alle Wörter "Server" mit "Host"
```
sed -n '/IP/ s/Server/Host/p' practise.txt
```
matcht nur Zeilen in denen "IP" vorhanden ist
 
```
grep "[A-Za-z]*\s[0-9]\sIP:\s" practise.txt
```
  - `[A-Za-z]*`: Beliebige Buchstabenfolge (Groß- und Kleinbuchstaben)
  - `\s`: Leerzeichen
  - `[0-9]`: Eine Ziffer von 0 bis 9
  - `IP:`: Feste Zeichenfolge "IP:"
  - `\s`: Leerzeichen
 
```
awk -F: '$3>400 && $7=="/usr/bin/false"{print $1}' /etc/passwd
```
  - `awk`: Befehl zur Textverarbeitung und Auswertung von Dateien
  - `-F:`: Option, um das Feldtrennzeichen auf den Doppelpunkt zu setzen
  - `'...'`: AWK-Bedingung, die folgende Aktionen ausführt:
    - `$3>400`: Das dritte Feld größer als 400
    - `&&`: Logisches UND
    - `$7=="/usr/bin/false"`: Das siebte Feld entspricht "/usr/bin/false"
    - `{print $1}`: Aktion, die den Wert des ersten Feldes ausgibt
  - `/etc/passwd`: Datei, die von AWK verarbeitet wird (hier: Passwortdatei)
`
 
## Common Use Cases for `awk` Command
 
1. **Data Extraction and Reporting**: Extract specific fields or columns from structured data files and generate reports.
 
2. **Text Processing and Pattern Matching**: Search for patterns or regular expressions within files and perform actions based on matches found.
 
3. **Data Transformation and Manipulation**: Convert data formats, perform calculations on numeric data, or modify text content.
 
4. **Report Formatting**: Format data for presentation in reports or tables by adding headers, footers, etc.
 
5. **Processing Multiple Files**: Perform operations across multiple files simultaneously, such as merging, comparing, or aggregating data.

## Skript

Dies sollte in jedem Skript enthalten sein:

```bash
cwd=`pwd` #current working directory  
BINDIR=$(cd `dirname $0`;`pwd`) #BINDIR: the directory where the script is located
BASENAME=`basename $0` #Set the script name (without path to it)
TMPDIR=/tmp/$BASENAME.$$ #Set a temporary directory if needed with a ending $$ which is the process-ID of the Skript
ETCDIR=$BINDIR/../etc #ETCDIR is the config directory of the script, which is normally located one directory up from the script location and then into etc
```
