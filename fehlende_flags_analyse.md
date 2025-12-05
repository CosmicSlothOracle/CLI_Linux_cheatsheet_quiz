# Analyse: Fehlende Flag-Informationen in Command-Modals

## Übersicht

Diese Analyse identifiziert alle Kacheln (command-cards), die Flags verwenden, aber keine Flag-Informationen in `commandMeta` haben.

---

## 1. Kacheln mit Flags im Command-Namen (data-command)

### 1.1 `ls -a` (quiz-id: `ls_a`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-a`: zeigt versteckte Dateien und ./.

### 1.2 `ls -la` (quiz-id: `ls_la`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-l`: lange Ausgabe mit Rechten und Besitzer
- `-a`: zeigt versteckte Dateien und ./.

### 1.3 `ls -R` (quiz-id: `ls_R`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-R`: rekursives Auflisten aller Unterverzeichnisse

### 1.4 `ls -aR` (quiz-id: `ls_aR`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-a`: zeigt versteckte Dateien und ./.
- `-R`: rekursives Auflisten aller Unterverzeichnisse

### 1.5 `mkdir -p` (quiz-id: `mkdir_p`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-p`: erstellt fehlende Zwischenverzeichnisse (parents)

### 1.6 `cp -r` (quiz-id: `cp_r`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-r` / `-R`: rekursives Kopieren von Verzeichnissen
- `-a`: archiv-Modus (kopiert Rechte, Links, etc.)

### 1.7 `rm -r` (quiz-id: `rm_r`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-r` / `-R`: rekursives Löschen von Verzeichnissen
- `-f`: force (ohne Nachfrage)
- `-i`: interaktiv (mit Nachfrage)

### 1.8 `sort -n` (quiz-id: `sort_n`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-n`: numerisches Sortieren
- `-r`: reverse (absteigend)
- `-k`: Sortierung nach Spalte

### 1.9 `tree -d` (quiz-id: `tree_d`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-d`: zeigt nur Verzeichnisse (directories)

### 1.10 `tree -L` (quiz-id: `tree_L`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-L`: begrenzt die Tiefe (Level)

### 1.11 `wc -w` (quiz-id: `wc_w`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-w`: zählt Wörter
- `-l`: zählt Zeilen
- `-c`: zählt Zeichen

### 1.12 `wc -l` (quiz-id: `wc_l`)

**Status:** ⚠️ HAT commandMeta, aber `-l` fehlt in flags!
**Aktuell in commandMeta:** nur `--files0-from`
**Fehlende Flags:**

- `-l`: zählt Zeilen (wird im Command-Namen verwendet!)
- `-w`: zählt Wörter
- `-c`: zählt Zeichen

---

## 2. Basis-Commands ohne Flags im Namen, aber die Flags verwenden

### 2.1 `mkdir` (quiz-id: `mkdir`)

**Status:** ❌ KEINE commandMeta
**Verwendet Flags in:** `mkdir_p`
**Fehlende Flags:**

- `-p`: erstellt fehlende Zwischenverzeichnisse (parents)
- `-v`: verbose (zeigt erstellte Verzeichnisse)

### 2.2 `cp` (quiz-id: `cp`)

**Status:** ❌ KEINE commandMeta
**Verwendet Flags in:** `cp_r`
**Fehlende Flags:**

- `-r` / `-R`: rekursives Kopieren von Verzeichnissen
- `-a`: archiv-Modus (kopiert Rechte, Links, etc.)
- `-i`: interaktiv (mit Nachfrage bei Überschreiben)
- `-u`: update (nur wenn Quelle neuer ist)

### 2.3 `rm` (quiz-id: `rm`)

**Status:** ❌ KEINE commandMeta
**Verwendet Flags in:** `rm_r`
**Fehlende Flags:**

- `-r` / `-R`: rekursives Löschen von Verzeichnissen
- `-f`: force (ohne Nachfrage)
- `-i`: interaktiv (mit Nachfrage)

### 2.4 `sort` (quiz-id: `sort`)

**Status:** ❌ KEINE commandMeta
**Verwendet Flags in:** `sort_n`
**Fehlende Flags:**

- `-n`: numerisches Sortieren
- `-r`: reverse (absteigend)
- `-k`: Sortierung nach Spalte
- `-u`: unique (entfernt Duplikate)

### 2.5 `tree` (quiz-id: `tree`)

**Status:** ❌ KEINE commandMeta
**Verwendet Flags in:** `tree_d`, `tree_L`
**Fehlende Flags:**

- `-d`: zeigt nur Verzeichnisse
- `-L`: begrenzt die Tiefe (Level)
- `-a`: zeigt auch versteckte Dateien

### 2.6 `wc` (quiz-id: existiert nicht, aber `wc_l` und `wc_w` existieren)

**Status:** ❌ KEINE commandMeta für Basis-Command
**Fehlende Flags:**

- `-l`: zählt Zeilen
- `-w`: zählt Wörter
- `-c`: zählt Zeichen

### 2.7 `mv` (quiz-id: `mv`)

**Status:** ❌ KEINE commandMeta
**Erwähnt in:** `beginnerMistakes` mit `-i` Flag
**Fehlende Flags:**

- `-i`: interaktiv (mit Nachfrage bei Überschreiben)
- `-v`: verbose (zeigt verschobene Dateien)
- `-n`: no-clobber (überschreibt nicht)

### 2.8 `chgrp` (quiz-id: `chgrp`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-R`: rekursiv auf Unterordner anwenden
- `-v`: verbose (zeigt Änderungen)

### 2.9 `cat` (quiz-id: `cat`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-n`: zeigt Zeilennummern
- `-b`: zeigt Zeilennummern (nur nicht-leere Zeilen)

### 2.10 `uniq` (quiz-id: `uniq`)

**Status:** ❌ KEINE commandMeta
**Fehlende Flags:**

- `-c`: zählt Vorkommen
- `-d`: zeigt nur Duplikate
- `-u`: zeigt nur eindeutige Zeilen

---

## 3. Zusammenfassung

### Commands mit Flags im Namen, aber KEINE commandMeta:

1. `ls_a` → Flag: `-a`
2. `ls_la` → Flags: `-l`, `-a`
3. `ls_R` → Flag: `-R`
4. `ls_aR` → Flags: `-a`, `-R`
5. `mkdir_p` → Flag: `-p`
6. `cp_r` → Flags: `-r`, `-a`
7. `rm_r` → Flags: `-r`, `-f`, `-i`
8. `sort_n` → Flags: `-n`, `-r`, `-k`
9. `tree_d` → Flag: `-d`
10. `tree_L` → Flag: `-L`
11. `wc_w` → Flags: `-w`, `-l`, `-c`

### Commands mit commandMeta, aber unvollständigen Flags:

1. `wc_l` → hat commandMeta, aber `-l` fehlt in flags (nur `--files0-from` vorhanden)

### Basis-Commands ohne commandMeta, die Flags verwenden:

1. `mkdir` → `-p`, `-v`
2. `cp` → `-r`, `-a`, `-i`, `-u`
3. `rm` → `-r`, `-f`, `-i`
4. `sort` → `-n`, `-r`, `-k`, `-u`
5. `tree` → `-d`, `-L`, `-a`
6. `mv` → `-i`, `-v`, `-n`
7. `chgrp` → `-R`, `-v`
8. `cat` → `-n`, `-b`
9. `uniq` → `-c`, `-d`, `-u`

---

## 4. Empfehlungen

1. **Für Commands mit Flags im Namen:** Erstelle separate `commandMeta` Einträge für jede Variante (z.B. `ls_a`, `ls_la`, etc.) oder erweitere die Basis-Command-Meta um alle Flags.

2. **Für Basis-Commands:** Füge `commandMeta` Einträge hinzu, die alle relevanten Flags dokumentieren.

3. **Für `wc_l`:** Füge `-l` Flag zur bestehenden commandMeta hinzu.

4. **Priorität:** Beginne mit den am häufigsten verwendeten Commands:
   - `ls` Varianten (`ls_a`, `ls_la`, `ls_R`, `ls_aR`)
   - `mkdir -p`
   - `cp -r`
   - `rm -r`
   - `sort -n`
   - `wc` Varianten
