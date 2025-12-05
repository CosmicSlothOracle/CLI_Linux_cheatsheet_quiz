# Masterfragen für Badge-System

Diese Datei definiert die Masterfragen für jedes der 6 Badge-Segmente. Jede Masterfrage ist ein realistisches, kombinatorisches Szenario, das mehrere Commands des jeweiligen Segments kombiniert.

---

## Segment 1: Navigation & Grundlagen (Commands 1-10)

**Quiz-IDs**: `pwd`, `cd`, `cd_parent`, `ls`, `ls_a`, `ls_la`, `mkdir`, `mkdir_p`, `mv`, `cp`

### Masterfrage

**Szenario**: Du bist Systemadministrator und musst ein Backup-System für tägliche Dokumente einrichten. Das Backup-Verzeichnis soll mit dem aktuellen Datum benannt werden, und alle wichtigen Dateien sollen automatisch gesichert werden.

**Aufgabe**: Erstelle ein Verzeichnis namens `backups/2025-01-15` (nutze Variablen für das Datum, z.B. `$(date +%Y-%m-%d)`), kopiere alle `.txt`-Dateien aus dem aktuellen Verzeichnis dorthin, und benenne sie so um, dass sie das Datum im Namen tragen (z.B. `notes.txt` → `notes_2025-01-15.txt`). Zeige anschließend mit `pwd` an, wo du dich befindest, und liste den Inhalt des Backup-Verzeichnisses mit `ls -la` auf, um zu prüfen, ob alles korrekt kopiert wurde.

**Korrekte Lösung** (Mehrteilig):
1. `BACKUP_DIR="backups/$(date +%Y-%m-%d)"`
2. `mkdir -p "$BACKUP_DIR"`
3. `cp *.txt "$BACKUP_DIR/"`
4. `cd "$BACKUP_DIR"`
5. `for file in *.txt; do mv "$file" "${file%.txt}_$(date +%Y-%m-%d).txt"; done`
6. `pwd`
7. `ls -la`

**Alternativ (vereinfacht)**:
```
mkdir -p backups/$(date +%Y-%m-%d)
cp *.txt backups/$(date +%Y-%m-%d)/
cd backups/$(date +%Y-%m-%d)
pwd
ls -la
```

**Quiz-Frage** (Multiple Choice):

Du musst ein tägliches Backup-System erstellen. Welche Befehlssequenz erstellt ein Backup-Verzeichnis mit dem aktuellen Datum, kopiert alle `.txt`-Dateien dorthin, wechselt in das Backup-Verzeichnis und zeigt den aktuellen Pfad an?

**Optionen**:
1. `mkdir backups/$(date +%Y-%m-%d) && cp *.txt backups/$(date +%Y-%m-%d)/ && cd backups/$(date +%Y-%m-%d) && pwd`
2. `cd backups && mkdir $(date +%Y-%m-%d) && cp *.txt`
3. `mkdir -p backups && cp *.txt backups/ && pwd`
4. `ls -la backups/$(date +%Y-%m-%d)`

**Korrekte Antwort**: Option 1

**Erklärung**: Die Sequenz nutzt `mkdir` für das Verzeichnis (mit Datum), kopiert alle `.txt`-Dateien, wechselt ins Backup-Verzeichnis und zeigt den Pfad mit `pwd`. Die Kombination aus `mkdir`, `cp`, `cd` und `pwd` ist essentiell.

---

## Segment 2: Dateioperationen & Suche (Commands 11-20)

**Quiz-IDs**: `cp_r`, `rm`, `rm_r`, `cat`, `grep`, `sort`, `sort_n`, `uniq`, `find_name`, `find_maxdepth`

### Masterfrage

**Szenario**: Du musst eine Log-Analyse durchführen: Finde alle `.log`-Dateien im aktuellen Verzeichnisbaum, filtere nach Fehler-Einträgen, entferne Duplikate und erstelle eine sortierte Zusammenfassung.

**Aufgabe**: Finde alle `.log`-Dateien rekursiv, durchsuche sie nach dem Wort "ERROR" (großgeschrieben), sortiere die Ergebnisse alphabetisch, entferne doppelte Zeilen, und speichere das Ergebnis in einer Datei `errors_summary.txt`. Zähle anschließend, wie viele eindeutige Fehler gefunden wurden.

**Korrekte Lösung**:
```
find . -name "*.log" -type f -exec grep "ERROR" {} \; | sort | uniq > errors_summary.txt
wc -l errors_summary.txt
```

**Oder mit Pipe**:
```
find . -name "*.log" -type f | xargs grep "ERROR" | sort | uniq > errors_summary.txt
cat errors_summary.txt | wc -l
```

**Quiz-Frage** (Multiple Choice):

Du musst alle Fehlermeldungen aus Log-Dateien extrahieren. Welche Befehlssequenz findet alle `.log`-Dateien, sucht nach "ERROR", sortiert die Ergebnisse, entfernt Duplikate und zählt die eindeutigen Treffer?

**Optionen**:
1. `find . -name "*.log" | grep "ERROR" | sort | uniq | wc -l`
2. `find . -name "*.log" -type f -exec grep "ERROR" {} \; | sort | uniq | wc -l`
3. `grep -r "ERROR" *.log | sort | uniq`
4. `cat *.log | grep "ERROR" | sort`

**Korrekte Antwort**: Option 2

**Erklärung**: `find` sucht rekursiv nach `.log`-Dateien, `-exec grep` durchsucht jede gefundene Datei, `sort` sortiert die Ergebnisse, `uniq` entfernt Duplikate, und `wc -l` zählt die Zeilen. Die Kombination aus `find`, `grep`, `sort` und `uniq` ist typisch für Log-Analysen.

---

## Segment 3: Erweiterte Auflistung & Umleitung (Commands 21-30)

**Quiz-IDs**: `ls_R`, `ls_aR`, `tree`, `tree_d`, `tree_L`, `echo`, `redirect_overwrite`, `redirect_append`, `redirect_stderr`, `pipe`

### Masterfrage

**Szenario**: Du richtest ein Logging-System für eine Anwendung ein. Die Anwendung soll ihre Ausgaben in eine Logdatei schreiben, Fehler sollen separat gespeichert werden, und du musst die Verzeichnisstruktur dokumentieren.

**Aufgabe**: Erstelle ein Verzeichnis `logs/app` mit allen Zwischenordnern, schreibe eine Startnachricht mit Timestamp in `logs/app/application.log`, leite Fehler in `logs/app/errors.log` um, und erstelle eine Übersicht der Verzeichnisstruktur mit begrenzter Tiefe.

**Korrekte Lösung**:
```
mkdir -p logs/app
echo "$(date): Application started" >> logs/app/application.log
tree -L 2 logs/ > logs/app/structure.txt 2> logs/app/errors.log
```

**Oder detaillierter**:
```
mkdir -p logs/app
echo "$(date '+%Y-%m-%d %H:%M:%S'): Application started" >> logs/app/application.log
tree -L 2 logs/ > logs/app/structure.txt 2>> logs/app/errors.log
ls -aR logs/ > logs/app/full_listing.txt
```

**Quiz-Frage** (Multiple Choice):

Du richtest ein Logging-System ein. Welche Befehlssequenz erstellt die Verzeichnisstruktur `logs/app`, schreibt eine Startnachricht mit Datum in die Logdatei, und dokumentiert die Verzeichnisstruktur (Fehler sollen in eine separate Datei)?

**Optionen**:
1. `mkdir logs/app && echo "$(date)" >> logs/app/application.log && tree -L 2 logs/ > structure.txt 2> errors.log`
2. `mkdir -p logs/app && echo "$(date): Started" >> logs/app/application.log && tree -L 2 logs/ > logs/app/structure.txt 2> logs/app/errors.log`
3. `cd logs && mkdir app && echo "Started" > application.log`
4. `tree logs/ > structure.txt && echo "Started" >> application.log`

**Korrekte Antwort**: Option 2

**Erklärung**: `mkdir -p` erstellt die Struktur, `echo` mit `>>` hängt an (ideal für Logs), `tree -L 2` zeigt die Struktur begrenzt, und `2>` leitet Fehler separat um. Die Kombination aus `echo`, `>>`, `2>`, und `tree` ist typisch für Logging-Setups.

---

## Segment 4: System & Rechte (Commands 31-40)

**Quiz-IDs**: `whoami`, `chmod`, `chmod_R`, `chown`, `chgrp`, `touch`, `head`, `tail`, `wc_l`, `wc_w`

### Masterfrage

**Szenario**: Du installierst ein Web-Server-Script und musst sicherstellen, dass es mit den richtigen Berechtigungen läuft. Das Script muss ausführbar sein, und du musst prüfen, wer es ausführt.

**Aufgabe**: Erstelle ein Script `deploy.sh`, mache es ausführbar (Besitzer: rwx, Gruppe/Andere: rx), ändere den Besitzer auf `www-data:www-data`, prüfe mit `whoami`, wer es ausführen würde, und überwache die ersten Zeilen der Logdatei nach dem Start.

**Korrekte Lösung**:
```
touch deploy.sh
chmod 755 deploy.sh
sudo chown www-data:www-data deploy.sh
whoami
# Nach Script-Ausführung:
head -n 10 /var/log/deploy.log
```

**Oder rekursiv für ein Verzeichnis**:
```
mkdir -p /var/www/myapp/scripts
touch /var/www/myapp/scripts/deploy.sh
chmod -R 755 /var/www/myapp/scripts
sudo chown -R www-data:www-data /var/www/myapp/scripts
echo "Script runs as: $(whoami)" >> /var/www/myapp/scripts/deploy.log
tail -f /var/www/myapp/scripts/deploy.log
```

**Quiz-Frage** (Multiple Choice):

Du installierst ein Web-Server-Script. Welche Sequenz erstellt das Script, setzt die Rechte auf 755 (Besitzer: rwx, Gruppe/Andere: rx), ändert Besitzer und Gruppe auf www-data, und prüft, wer es ausführen würde?

**Optionen**:
1. `touch deploy.sh && chmod 755 deploy.sh && sudo chown www-data:www-data deploy.sh && whoami`
2. `chmod +x deploy.sh && chown www-data deploy.sh`
3. `touch deploy.sh && chmod 777 deploy.sh && whoami`
4. `mkdir deploy.sh && chmod 755 deploy.sh`

**Korrekte Antwort**: Option 1

**Erklärung**: `touch` erstellt die Datei, `chmod 755` setzt die Standard-Web-Server-Rechte, `chown user:group` ändert Besitzer und Gruppe, und `whoami` prüft den aktuellen Benutzer. Die Kombination aus `touch`, `chmod`, `chown` und `whoami` ist essentiell für sichere Script-Installationen.

---

## Segment 5: Erweiterte Dateioperationen (Commands 41-50)

**Hinweis**: Die genaue Zuordnung der Commands 41-50 hängt von der vollständigen Liste ab. Diese Masterfrage ist ein Platzhalter und sollte angepasst werden, sobald alle 60 Commands bekannt sind.

### Masterfrage (Platzhalter)

**Szenario**: Du musst eine komplexe Dateiverwaltung durchführen, die mehrere erweiterte Operationen kombiniert.

**Aufgabe**: [Wird basierend auf den Commands 41-50 definiert]

**Quiz-Frage**: [Wird ergänzt]

---

## Segment 6: Fortgeschrittene Techniken (Commands 51-60)

**Hinweis**: Die genaue Zuordnung der Commands 51-60 hängt von der vollständigen Liste ab. Diese Masterfrage ist ein Platzhalter und sollte angepasst werden, sobald alle 60 Commands bekannt sind.

### Masterfrage (Platzhalter)

**Szenario**: Du musst eine fortgeschrittene, produktive Workflow-Aufgabe lösen, die mehrere komplexe Commands kombiniert.

**Aufgabe**: [Wird basierend auf den Commands 51-60 definiert]

**Quiz-Frage**: [Wird ergänzt]

---

## Implementierungsnotizen

- **Format**: Jede Masterfrage sollte als Multiple-Choice-Frage mit 4 Optionen implementiert werden
- **Schwierigkeit**: Die Masterfragen sind deutlich schwieriger als die normalen Quiz-Fragen, da sie Kombinationen erfordern
- **Realismus**: Alle Szenarien sind praxisnah und kommen in realen Systemadministrations-Aufgaben vor
- **Feedback**: Nach der Beantwortung sollte eine detaillierte Erklärung zeigen, wie die einzelnen Commands zusammenwirken

## Technische Integration

Die Masterfragen werden im JavaScript als `masterQuizData` Objekt implementiert:

```javascript
const masterQuizData = {
  segment1: {
    title: "Masterquiz: Navigation & Grundlagen",
    scenario: "Du bist Systemadministrator...",
    question: "Du musst ein tägliches Backup-System erstellen...",
    options: [...],
    correctIndex: 0,
    explanation: "..."
  },
  // ...
};
```

