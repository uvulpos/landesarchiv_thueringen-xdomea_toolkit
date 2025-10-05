# 🧰 xdomea-Toolkit zur Erzeugung von Test-Aussonderungsnachrichten

> ⚠️ **Wichtiger Hinweis:**  
> Dies ist **nicht** das Repository für den [xdomea Aussonderungsmanager (x-man)](https://github.com/Landesarchiv-Thueringen/x-man).
--- 

## 📖 Überblick

Das **Landesarchiv Thüringen** benötigte für Funktionsprüfungen seiner Software zur elektronischen Langzeitarchivierung **Test-Aussonderungsnachrichten** nach dem Datenaustauschstandard **xdomea**. Mit dem **xdomea-Toolkit** können beliebig komplexe Testnachrichten generiert werden – perfekt geeignet, um die massenhafte Anbietung und Abgabe elektronischer Akten zu testen.

### 🧩 Bestandteile des Toolkits

Das Toolkit umfasst folgende Skripte:

- 📨 **Nachrichtengenerierung** – erstellt Test-Aussonderungsnachrichten der Typen **0501**, **0502** und **0503**  
- 🔁 **Austausch der Prozess-ID** – ersetzt Prozess-IDs in bestehenden Testnachrichten  
- 🧾 **Hilfsskript (Metadaten)** – überträgt Metadaten aus Testdateien in xdomea-Nachrichten  
- ⏱️ **Hilfsskript (Zeitstempel)** – überträgt NTFS-Zeitstempel aus Testdateien in das xdomea-Paket  

### 💡 Die Nachnutzung und Weiterentwicklung des Toolkits ist **ausdrücklich erwünscht!**

--- 

## 📨 Nachrichtengenerierung

### ⚙️ Funktionsweise

Das Skript erzeugt automatisch:

- 🗂️ **Anbietung** (`0501`)
- 🧮 **Bewertung** (`0502`)
- 📦 **Abgabe** (`0503`)

Die Metadaten werden über **Musterdateien** gesteuert, die pro xdomea-Version hinterlegt sind.  
Generische Musterdateien sind im Projekt enthalten.

Das Skript:

- erzeugt komplexe Nachrichtenstrukturen (auch mit hunderten Akten 🏗️)
- wahrt automatisch die logische Integrität der Metadaten
- kann zufällig gewählte Muster verwenden
- wählt automatisch **Primärdateien** anhand von Endungen oder erkannter Formate
- generiert Bewertungen anhand konfigurierbarer Strategien

---

### 🧱 Nachrichtenmuster

Mitgeliefert werden generische Musterdateien für:

- **xdomea 2.3.0**
- **xdomea 2.4.0**
- **xdomea 3.0.0**

💡 **Tipp:**  
Erstelle eigene Muster auf Basis der generischen Vorlagen, um realistische Testfälle zu erzeugen.

Vor der Generierung werden alle Muster automatisch gegen das Schema validiert ✅.

---

### 🧩 Platzhalter in Mustern

In Musterdateien können Platzhalter verwendet werden, um dynamische Inhalte zu erzeugen (z. B. Kennzeichen oder Nummern).  

| Platzhalter | Verwendbar in | Ersetzt durch |
|--------------|----------------|----------------|
| `{AP}` | Akte | Kennzeichen der Aktenplaneinheit |
| `{Ax}` | Akte | Aktennummer |
| `{Vx}` | Vorgang | Vorgangsnummer |
| `{Dx}` | Dokument | Dokumentnummer |

---

### 🧪 Testdaten

Das Projekt enthält generische Testdaten für die `0503`-Nachricht.  
Diese können beliebig ergänzt oder ausgetauscht werden.

⚠️ **Wichtig:**  
Dateinamen dürfen **keine Leer- oder Sonderzeichen** enthalten.  
Verwende stattdessen Unterstriche (`_`).  
Beispiel: `Dokument_001.pdf`

---

### 💻 Verwendung

Das Skript funktioniert standardmäßig in der vorgegebenen Projektstruktur.  
Alle Pfade (Schemadateien, Muster, Testdateien) sind über die **Konfiguration** anpassbar.

#### 🪟 Windows

Im Ordner [`message_generation`](message_generation) befindet sich eine **EXE-Datei**, die direkt ausführbar ist – ohne zusätzliche Installation.  
Alternativ kann das Skript mit dem Python-Interpreter ausgeführt werden.

#### 🐧 Linux / 🍎 macOS

1. Installiere [Python](https://www.python.org/downloads/) (aktuelle Version empfohlen)  
2. Installiere die Abhängigkeiten:

   ```bash
   pip install lxml python-magic
   ```
3. Starte das Programm:
   ```bash
   python message_generation/message_generator.py
   ```

## ⚙️ Konfiguration
....

---

## ⚖️ Lizenz

Dieses Projekt steht unter der [MIT-Lizenz](./license.md).

Lizenziert sind ausschließlich die selbst erstellten **Python-Skripte** für:

- die [Nachrichtengenerierung](./message_generation/message_generator.py)
- den [Wechsel der Prozess-ID](./randomize_process_id/randomize_process_id.py)
- sowie die zugehörigen [Hilfsskripte](./message_generation/lib/util)

📦 Mitgeliefert werden außerdem die **xdomea-Schemadateien**, die **nicht** unter die MIT-Lizenz fallen.  
Laut **Koordinierungsstelle für IT-Standards (KoSIT)** sind diese frei von Rechten Dritter und dürfen uneingeschränkt verwendet werden.  
Auch alle mitgelieferten Muster- und Testdateien können frei genutzt werden.
