# Projektarbeit 2 - Niklas Diehm

### Title: OpenRewrite

### Abgabedatum: XX.XX.2024

### Betreuer: Prof. Dr. Holger Vogelsang

# ====================

## Installationsanleitung

Um das Demo-Projekt, welches OpenRewrite enthält, zu starten, müssen Java sowie Maven installiert sein.

Die Demoanwendung enthält keine Logik. Stattdessen können die OpenRewrite-Recipes ausgeführt werden. Dazu muss folgender Befehl ausgeführt werden:

```bash
mvn rewrite:run
```

Dies führt alle Recipes aus. Der Status der Recipes kann in der Kommandozeile eingesehen werden.

## Erklärung der Recipes

Alle Recipes sind in der pom.xml-Datei innerhalb der plugins-Sektion definiert. Einige Recipes müssen zusätzlich konfiguiert werden. Hierfür gibt es die Datei "rewrite.yml".
Recipes:

- com.hka.niklasdiehm.UpdateMavenDependencyVersion: Aktualisiert die Dependency-Version von "spring-boot-starter-web". Die neue Version wird in der rewrite.yml-Datei definiert.
- com.openrewrite.java.RemoveUnusedImports: Entfernt alle nicht verwendeten Imports.
- org.openrewrite.java.OrderImports: Sortiert die Imports alphabetisch.
- org.openrewrite.java.migrate.UpgradeToJava21: Aktualisiert die Java-Version auf 21.
- org.openrewrite.java.migrate.JavaVersion21: Setzt die Java-Version auf 21 bei maven.compile.source und maven.compile.target.
- com.hka.niklasdiehm.ReplaceStringLiteralValue: ersetzt den String "Hello World" durch "Hello World!". Für Unternehmen oder bei großen Projekten kann dies genutzt werden, wenn sich z.B. der Applikationsname ändert und dieser an vielen Stellen im Code definiert und verwendet wird.

## Gegenüberstellung mit DependencyTrack

DependencyTrack ist ein Tool, um die Versionen von Abhängigkeiten zu verwalten. Die Abbildung von den Abhängigkeiten bzw. Paketen wird in der Software Bill of Material (SBOM) verwaltet. Diese XML-Datei kann erstellt werden mit **einem** der beiden Befehle:

```bash
mvn org.cyclonedx:cyclonedx-maven-plugin:makeAggregateBom
mvn package
```

Die SBOM-Datei befindet sich unter "target/bom.xml" und kann in DependencyTrack eingelesen werden. Um DependencyTrack zu starten, muss Docker installiert sein. Anschließend kann folgender Befehl ausgeführt werden:

```bash
docker-compose up
```

Damit wird DependencyTrack unter http://localhost:8080 gestartet. Die Anmeldedaten sind admin/admin.  
Wichtig: Die Konfiguration ist nicht auf einen Produktivbetrieb ausgelegt, sondern nur für die Demo gedacht.

## Fazit

Um automatisiert Versionen von Paketen zu verwalten, bietet sich OpenRewrite an. Es können Recipes erstellt werden, die die Versionen von Paketen aktualisieren. Dies kann z.B. bei Sicherheitslücken oder veralteten Versionen genutzt werden.  
Um hingegen eine visuelle Oberfläche zu haben, die die Versionen von Paketen verwaltet, bietet sich DependencyTrack an. Hier können die Versionen von Paketen manuell aktualisiert werden. Außerdem können die Abhängigkeiten von Paketen eingesehen werden.
