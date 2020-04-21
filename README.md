# ev-modelling

## Datenaufbereitung

 - Anpassen der NHTS Trip-Daten
	 - Übernehmen relevanter Daten
	 - Reduzieren der Zustände
	 - ...
	 - speichern verarbeiteter Rohdaten

## Datenauswertung

- Auswerten von 
	- Aufenthaltsdauer
	- Initiale Abfahrtszeit
	- Übergangswahrscheinlichkeiten
	- Wegstrecken
- statistische Grundlage der Fahrtensimulation
- aufgeteilt nach Werktag, Samstag, Sonntag
- ablegen der Ergebnisse und Modelle im Subordner "Simulationsdaten"

## EV Klasse

- Blueprint der EV Klasse für Simulation
- in Simulation aktualisiert und ausgebaut

## Fahrtensimulation

- Simulation von Fahrten auf Basis der Ergebnisse der Datenauswertung

## Rohdaten 

- Ablageort des verarbeiteten NHTS Datensatz
- Ablageort der tabellarischen Auflistung von EV-Modellen die in der Simulation zum Einsatz kommen

## Simulationsauswertung

- Auswertung des Simulationsergebnisses 
	- Vorgehen analog zur Datenauswertung
- Vergleich mit Ausgangsdatensatz als Proof of Concept
- Auswertung der Energiebedarfszeitreihe

## Zusätzliche Informationen

**Zu den Density Estimation Modellen der Aufenthaltsdauer:**

Die Modelle lassen sich über die Einstellung der Bandbreite parametrieren. Zunächst hab ich einfach unterschiedliche Werte getestet und den Wert gewählt bei welchem die Verteilungsfunktion die Charakteristik der Histogramme recht gut wiederzugeben scheint. 
Die Parameterauslegung lässt sich numerisch über eine Kreuzvalidierungsverfahren optimieren, worauf ich aber erst einmal verzichtet habe, da ich sowieso noch nicht mit den „richtigen“ Daten arbeite und das Ganze ziemlich rechenintensiv ist.


**Zu den Übergangswahrscheinlichkeiten:**

Hier macht der Mangel an Daten in den frühen Morgenstunden Probleme. An Werktagen sind ausreichend Fahrten zur Verfügung um zu jedem 15-minütigem Zeitschritt eine Übergangswahrscheinlichkeit zu berechnen wobei jedoch einzelne Ausreißer zu sehen sind wo beispielsweise die Wahrscheinlichkeit in einem Intervall zu einem anderen Zustand zu wechseln = 1 ist (da alle Fahrten des Ausgangsdatensatzes die vom Zustand x ausgingen und im Zeitintervall t starteten in den Zustand y übergingen). Das Ganze ist noch extremer an Samstagen/Sonntagen, da hier offensichtlicherweise vergleichsweise noch weniger Daten zur Verfügung stehen, hier lassen sich teils keine Fahrten im Datensatz finden die zu gegebenem Zeitpunkt starten vom spezifischen Zustand starten und deshalb ist auch keine Übergangswahrscheinlichkeit zu berechnen.
 Hier habe ich überlegt bei Unterschreiten einer Mindestmenge an Fahrten, solche aus umliegenden Zeitschritten zusammenzuwerfen und eine gemeinsame Übergangswahrscheinlichkeit für eine größere Zeitperiode zu berechnen