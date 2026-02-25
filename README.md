# SSEF
Der SSEF oder Size-to-Sound-Factor ist eine Effizienzkennzahl, die dazu entwickelt wurde, die optimale MP3-Bitrate zur MP3-Kompression via LAME zu bestimmen.


### [Excel-Tabelle mit Ergebnissen & Diagrammen](Ergebnisse/Ergebnisse_SSEF_Berechnung.xlsx)


## Auswertungsskript "answerfinder.py"
Wertet Umfrageergebnisse aus und exportiert sie in die Excel-Vorlage.
### Voraussetzungen
- Python 3
- openpyxl (macht Export in Excel möglich)
- Im gleichen Ordner wie [answerfinder.py](Auswertungsskript/answerfinder.py):
	- [jsonfile.txt](Auswertungsskript/jsonfile.txt) (1:1 Export aus der Datenbank von soundcompare.onrender.com)
	- [Mappe1.xlsx](Auswertungsskript/Mappe1.xlsx) (Vorlage)
- Ausführung in Windows Powershell

### Installation von openpyxl
    python -m pip install openpyxl
### Ausführen Auswertungsskript
    python answerfinder.py


## Code zur Reproduktion in einer Ubuntu-Umgebung
### Den SSEF einer MP3-Datei bestimmen
für maschinelle Berechnung nötig:
- Original-Datei (im .wav-Format muss zu "ref.wav" umbenannt werden
- komprimierte .mp3 (zurück in .wav dekomprimiere) muss zu "test.wav" umbenannt werden

### in Ubuntu-Umgebung folgenden Code ausführen:
	sudo apt install git (falls nicht schon vorhanden)
	pip install git+https://github.com/ashvala/AQUA-tk.git --break-system-packages
	pip install "aquatk[plotting]" --break-system-packages
	python3 -m aquatk.metrics.PEAQ.peaq_basic ref.wav test.wav
(Es wird empfohlen, mehrere Messungen gleichzeitig in verschiedenen Terminals laufen zu lassen, da eine einzelne Messung bis zu 20 min dauern kann.)


## Durchzuführende Rechnungen

Die aus der Rechnung resultierende Objective Difference Grade bzw. ODG in folgende Formel einsetzen:
$O_{obj} = \frac{ODG + 4}{4}$

Die resultierenden $O_{obj}$- & $O_{subj}$-Werte werden in folgende Formel eingesetzt:
$Q_{total} = 0,6 \times Q_{subj} + 0,4 \times Q_{obj}$

Nun wird der Speicheraufwand für diese .mp3-Datei relativ zu allen anderen .mp3-Dateien mit anderen Bitraten normiert:
$\frac{S - S_{min}}{S_{max} - S_{min}}$\\\\
$S = \text{Speicheraufwand dieser .mp3-Datei}$\\\\
$S_{min} = \text{Speicheraufwand der kleinsten .mp3-Datei}$\\\\
$S_{max} = \text{Speicheraufwand der größten .mp3-Datei}$\\\\

Die resultierenden $Q_{total}$-Wert werden in die folgende Formel eingesetzt:
$SSEF = Q_{total} \times (1 - S_norm + 0,05)$

## Alle verwendeten Tools:
- draw.io für Schemata
- TeXstudio für Diagramme
- Audacity für (De)Kompression
