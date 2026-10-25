# BSH_Deutsche_Bucht_Kueste_Harmonics_2026 (IDX/TCD)

Warum:
Copernicus Marine Data kann in Küstennähe keine genauen Daten liefern. Deshalb habe ich die gesamte deutsche Bucht komplett neu abgebildet mit Daten vom BSH.

1. Die Datenquelle
Quelle ist das BSH-HBMnoku-Modell, auch HIROMB-BOOS-Modell genannt. Verwendet wurde das 900-m-Küstengitter für Deutsche Bucht 
https://gdi.bsh.de/de/feed/Modelled-currents-of-the-operational-circulation-model-of-BSH-in-the-German-Bight-and-the-western-Baltic-Sea-horizontal-resolution-ca-900-m-2025-series.xml

Es sind archivierte operationelle Modellvorhersagen, keine flächendeckenden Strömungsmessungen. Das Modell berücksichtigt unter anderem Gezeiten, DWD-Wettervorhersagen und Flussabflüsse.
https://data.bsh.de/OpenData/OperationalModel/c_file_fine_2016/FactSheet_HBMnoku_deutsch.pdf

2. Welche Originaldateien
Die Originaldateien enthalten:
- Strömung alle 15 Minuten;
- horizontale Ost-West- und Nord-Süd-Komponenten;
- vertikale Strömung;
- bis zu 25 Modellschichten.
Ich habe ausschließlich die oberste Modellschicht und die beiden horizontalen Komponenten behalten.

Die Geschwindigkeiten liegen im Original an unterschiedlichen Seiten der Modellzellen. Deshalb habe ich die benachbarten Komponenten jeweils auf den gemeinsamen Zellmittelpunkt gemittelt. Erst dort bilden Ost- und Nordkomponente einen zusammengehörigen Vektor.

3. Was jetzt in der Jahresdatei steht
Sie enthält 8.760 Stundenkoordinaten, vom 1. Januar 2025 um 01:00 UTC bis zum 1. Januar 2026 um 00:00 UTC. Davon sind 8.742 Stunden mit Daten vorhanden.

4. Wie daraus die Harmonik entsteht
Für den tatsächlichen TCD-Export bestimmen wir je geeigneter Wasserzelle zunächst eine lokale Hauptströmungsachse. Darauf werden die Ost-/Nord-Vektoren projiziert. Das ergibt einen vorzeichenbehafteten Strom entlang dieser Achse.
An diese Zeitreihe passen wir mit UTide und gewöhnlicher kleinster Quadrate 21 astronomische Gezeitenkomponenten an:
M2, S2, N2, K2, K1, O1, P1, Q1, M4, MS4, MN4, 2N2, L2, MU2, NU2, 2SM2, M6, 2MN6, 2MS6, MSN6, M8
Für jede Komponente werden Amplitude und Phase berechnet. Die zusätzlichen Flachwasserkomponenten verbesserten den geprüften Elbe-Test gegenüber den ursprünglichen elf Komponenten.
Die Rechnung verwendet Greenwich-Phasen und astronomische Nodalkorrekturen. Ein linearer Trend wird nicht fortgeschrieben.

Gespeichert werden unter anderem:
- quadratischer Vorhersagefehler in Knoten;
- erklärte Schwankung, also R²;
- Querströmungsanteil;
- Nullwerte und zusätzliche Datenlücken;
- Unterschiede zwischen UTide-Rechnung und tatsächlichem Exportformat.
Für die endgültigen Konstanten wird anschließend mit der gesamten verfügbaren Jahresreihe neu gerechnet.

<img width="1238" height="948" alt="Screenshot 2026-10-25 144323" src="https://github.com/user-attachments/assets/5a58d6a9-1330-4329-9349-9390c8652dc2" />
<img width="1458" height="948" alt="Screenshot 2026-10-25 144843" src="https://github.com/user-attachments/assets/65221d89-73d7-47b5-8b5b-de2448156fb7" />


cheers/C
