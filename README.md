Infrastructure as a service

Infrastructure as Code steuert virtualisierte Ressourcen durch Konfigurationsdateien, um die Infrastruktur auf kodifizierte und wiederholbare Weise zu verwalten. IaC hat zwei Ansätze: deklarativ und imperativ.​

IaC nutzt Softwaretechnik, um Infrastruktur zu verwalten und wurde von Unternehmen wie Netflix, Facebook und Etsy vorangetrieben.

IaC behandelt Infrastrukturkonfiguration wie Softwarecode und nutzt Praktiken wie Versionskontrolle, Test Driven Development und Continuous Integration.

Automatisierungstool (Windows AIK, Solaris Jumpstart, Redhat Kickstart)

Konfigurationsmanagement-Tools: CFEngine, Puppet Community Edition etc.
Funktionen: Automatisierung und Verwaltung von Infrastrukturkomponenten Configs wie Server und Netzwerke

OS-Verfügbarkeit: In der Regel für mehrere Betriebssysteme verfügbar, um die Configs über verschiedene Plattformen hinweg zu verwalten.

Die Konfiguration der Cloud umgebungen sollten in version control systems wie as Git, Subversion, or Perforce ablegbar sein. Die Konfiguration soll vielseitig einsetzbar sein; (Vendor Lock vermeiden, wie gestern von Marcel erwähnt). Eine Versionierung der Konfiguration ist zwingen nötig im Falle eines Rollbacks Eine Continuous Delivery pipeline bauen.  -> Vereinfacht zudem die Integration in die Agile Arbeit.


Container:
Virtualisierung auf Anwendungsebene
*LXC (Linuxcontainer) ist ein Verfahren zur Containervirtualisierung auf Betriebssystemebene, das mehrere voneinander isoliert laufende Linux-Systeme auf einem einzigen Host ermöglicht.

Orchestrierungslösungen:
Bereitstellen von Container-Umgebungen: Docker-Compose, Docker-Swarm (2013)
Kubernetes (2014)
Automatisierung von Deployments, Skalierung und Verwaltung von Containern.
Diese Tools lösen das Problem der ineffizienten Verwaltung und Bereitstellung von Containern in grossen Umgebungen. 
Funktionen wie Lastenausgleich, automatische Wiederherstellung und Ressourcenoptimierung.