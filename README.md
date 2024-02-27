# Einführung

Infrastructure as Code steuert virtualisierte Ressourcen durch Konfigurationsdateien, um die Infrastruktur auf kodifizierte und wiederholbare Weise zu verwalten. IaC hat zwei Ansätze: deklarativ und imperativ.​ IaC nutzt Softwaretechnik, um Infrastruktur zu verwalten und wurde von Unternehmen wie Netflix, Facebook und Etsy vorangetrieben. IaC behandelt Infrastrukturkonfiguration wie Softwarecode und nutzt Praktiken wie Versionskontrolle, Test Driven Development und Continuous Integration.

Konfigurationsmanagement-Tools: CFEngine, Puppet Community Edition etc.
Funktionen: Automatisierung und Verwaltung von Infrastrukturkomponenten Configs wie Server und Netzwerke

OS-Verfügbarkeit: In der Regel für mehrere Betriebssysteme verfügbar, um die Configs über verschiedene Plattformen hinweg zu verwalten.

Die Konfiguration der Cloud umgebungen sollten in version control systems wie as Git, Subversion, or Perforce ablegbar sein. Die Konfiguration soll vielseitig einsetzbar sein; (Vendor Lock vermeiden, wie gestern von Marcel erwähnt). Eine Versionierung der Konfiguration ist zwingen nötig im Falle eines Rollbacks Eine Continuous Delivery pipeline bauen.  -> Vereinfacht zudem die Integration in die Agile Arbeit.

## Container
Virtualisierung auf Anwendungsebene
*LXC (Linuxcontainer) ist ein Verfahren zur Containervirtualisierung auf Betriebssystemebene, das mehrere voneinander isoliert laufende Linux-Systeme auf einem einzigen Host ermöglicht.

## Orchestrierungslösungen
Bereitstellen von Container-Umgebungen: Docker-Compose, Docker-Swarm (2013)
Kubernetes (2014)
Automatisierung von Deployments, Skalierung und Verwaltung von Containern.
Diese Tools lösen das Problem der ineffizienten Verwaltung und Bereitstellung von Containern in grossen Umgebungen. 
Funktionen wie Lastenausgleich, automatische Wiederherstellung und Ressourcenoptimierung.

### Kann man IaC-Tools Konfigurationen nach der Installationen anpassen?​
Ja die meisten. Ausnahme: Cloud-Init, AWS CloudFormation mit 'Stack Policies'​

### Gibt es Tools die nur für das einmalige ausführen gedacht sind?
Ja! -> CloudFormation (AWS)​
Google Cloud Deployment Manager (GCP)​
Azure Resource Manager (ARM) Templates (Microsoft Azure)​
Bash-Skripte oder PowerShell-Skripte​

### Was könnte das mit Idempotenz zu tun?
Beschreibt der Endzustand; 
Die Idempotenz ist ein wichtiges Konzept in der Welt der Infrastrukturautomatisierung und des IaC. Eine idempotente Operation ist eine, die das gleiche Ergebnis erzeugt, unabhängig davon, wie oft sie ausgeführt wird oder in welchem Zustand sich das System befindet. In Bezug auf IaC bedeutet Idempotenz, dass die Ausführung der Konfigurationsanweisungen das System in den gewünschten Zustand versetzt, unabhängig davon, ob es sich um die erste Bereitstellung oder um eine Aktualisierung handelt.​


### Es gibt den push und pull Ansatz. Was versteht man unter diesen?
Beim Push-Ansatz initiieren Benutzer oder Administratoren den Prozess der Konfigurationsanwendung, indem sie explizit Anweisungen an die Zielsysteme senden.​
​Im Pull-Ansatz überwachen die Zielsysteme aktiv einen zentralen Konfigurations- oder Versionskontrollspeicher und ziehen die Konfigurationen von dort, wenn Änderungen erkannt werden.​

### Wie kommunizieren Menschen im Alltag?​
Im Allgemeinen kommunizieren Menschen häufiger deklarativ

### Gibt es Programmiersprachen welche sowohl deklarativ wie auch imperativ gebraucht werden können?
    • SQL​
    • Prolog​
    • Haskell​
    • Javascript (JSX)​
    • Python
    • Powershell

### Kann in BASH deklarativ programmiert werden?
Viele Funktionen verwenden, welche den Status eines Zustands abfragen und darauf reagieren. Vorinstallierte Programme wie `grep`, `sed` verwenden. Pipes verwenden. Viele Conditionals verwenden (if, else, elif, case). Konventionen für Variabeln verwenden.​


### Welcher Teil von SQL ist eine imperative Sprache?
SQL ist im Allgemeinen eine deklarative Sprache, da Abfragen beschreiben, welche Daten abgerufen oder manipuliert werden sollen, ohne explizit anzugeben, wie dies geschehen soll. Prozedurale Erweiterungen wie PL/SQL können jedoch imperative Konstrukte für spezielle Aktionen in SQL integrieren.

### Warum werden einige Sprachen als imperativ und andere als deklarativ bezeichnet?
Programmiersprachen werden als imperativ bezeichnet, wenn sie explizite Anweisungen zur Steuerung des Programmflusses und zur Zustandsveränderung enthalten, während deklarative Sprachen sich eher auf die Beschreibung des gewünschten Ergebnisses oder der Datenbeziehungen konzentrieren, ohne explizite Anweisungen zur Steuerung des Programmflusses zu geben.​

### Was sind die Hauptunterschiede zwischen deklartivem und imperativen programmieren?
Deklarative Programmierung legt den Fokus darauf, was erreicht werden soll, ohne den genauen Ablauf anzugeben, während imperative Programmierung explizit angibt, wie eine Aufgabe schrittweise ausgeführt werden soll, wodurch eine niedrigere Abstraktionsebene und oft detailliertere, aber potenziell weniger wartbare Codestrukturen entstehen.


**Deklarativ** -> endzustand beschreiben
**Imperativ** -> den weg zum endzustand beschreiben


## Multicloud

### Vorteile:
    • avoiding vendor-locked​
    • meeting compliance requirements​
    • improving flexibility and scaleability

### Nachteile
    • growing cloud costs​
    • data-privacy and protection​
    • specialist management expertise

## Singlecloud

### Vorteile:
    • privacy and control​
    • faster workload​
    • datakonsistenz

### Nachteile:
    • Man ist abhängig von 1nem Provider

## MultiOS

### Vorteile:
    • More choices​
    • Flexible​
    • More requirements achieved​

### Nachteile:
    • Heavier workload​
    • Horrific monitoring​
    • Disastrous patch cycling management

## Single OS

### Vorteile
    • No choices​
    • Not Flexible​

### Nachteile
    • easier workload​
    • simple monitoring​
    • patch cycling management​


## Was passiert wenn man das OS anpassen muss:
Persistent data storage / database either stay or need to be migrated​
The services with the old OS will be deleted and recreated with a new OS​


• What does proprietary mean? Manufactur driven​
• Is proprietary really the opposite of open source? No​
• Compare community-driven with the commons. What do you notice? Society driven with a common goal​
• Is Terraform proprietary or community-driven? Yes it’s both​
• Is open source the same as "free"? Nope (exp. Redhat)​
• What are the advantages of a community-driven tool? Innovative development, catching errors before they spread, support​
• What are the disadvantages of a community-driven tool? Dependend on individuals, community follows trends​
• What other examples of open-source but not "free" software are there besides Threema? Redhat​
• Are there products that are open-source and community-driven but still proprietary? Terraform​