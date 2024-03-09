# Obsidian Visual Example
>Das folgende Dokument enthält verschiedene Arten der Visualisierung die mit Obsidian möglich sind als auch weitere Funktionen die mit Hilfe von Plugins erreichbar sind.
Der Beispiel Code ist in seiner Funktionweise Dokumentiert und kann für verschiedene Anwendungszwecke umgebaut werden.

# Datenvisualisierung
#### Tabellen

#### Säulen Diagramm
> Säulen Diagramme lassen sich ganz einfach mit <font style="color:#9966FF">Dataview</font> & <font style="color:#9966FF">Chart</font> erstellen.
##### Beispiel Barchart mit manuell eingetragenen Daten
```dataviewjs

const labels = ['One', 'Two', 'Three'];
const data = [1, 2, 3];

const chartData = {  
    type: 'bar',
    data: {
        labels: labels,
        datasets: [{
            label: 'Numbers',
            data: data,
            backgroundColor: 'rgba(153, 102, 255, 0.6)'
        }]
    }
}
this.container.style.width = '600px'
this.container.style.height = '300px'

window.renderChart(chartData, this.container);
```
##### Beispiel Barchart mit geladenen daten

```dataviewjs


```
#### Linien Diagramm
> Linien Diagramme können nur mit Hilfe von den Community Plugins <font style="color:#9966FF">Dataview</font> & <font style="color:#9966FF">Chart</font> erstellt werden.
```dataviewjs
//erstellen der Daten sowie den Labels
const labels = ['Januar', 'Februar', 'März', 'April', 'Mai', 'Juni', 'Juli', 'August', 'September', 'Oktober', 'November', 'Dezember'];
const verkaufszahlen = [100, 120, 110, 130, 140, 125, 135, 150, 145, 160, 155, 170];
const kosten = [80, 90, 85, 95, 100, 88, 92, 98, 97, 105, 102, 110];

// Chart erstellen
const chartData = {
	// Chart Type definieren
	type: 'line',
	// Daten für den Chart definieren
	data: {
		labels: labels,
		// erste linie für die Verkaufzahlen
		datasets: [{
			label: 'Verkaufszahlen im Jahr',
			data: verkaufszahlen,
			borderColor: 'rgba(153, 102, 255, 1)',
			backgroundColor: 'rgba(153, 102, 255, 0.2)',
			borderWidth: 2
			},
			// zweite linie für die Kosten
			{
			label: 'Kosten im Jahr',
			data: kosten,
			borderColor: 'rgba(255, 99, 132, 1)', // Rote Farbe für die Kostenlinie
			backgroundColor: 'rgba(255, 99, 132, 0.2)', // Hintergrundfarbe für den Bereich unterhalb der Linie
			borderWidth: 2 }] } }

this.container.style.width = '600px'
this.container.style.height = '300px'

window.renderChart(chartData, this.container);
```

#### Kombinierte Diagramme
> Diese können auch nur mit Hilfe der beiden Plugins erstellt werden, da es die Möglichkeiten von Mermaid übersteigt.
```dataviewjs
const labels = ['Januar', 'Februar', 'März', 'April', 'Mai', 'Juni', 'Juli', 'August', 'September', 'Oktober', 'November', 'Dezember'];
const verkaufszahlen = [100, 120, 110, 130, 140, 125, 135, 150, 145, 160, 155, 170];
const kosten = [80, 90, 85, 95, 100, 88, 92, 98, 97, 105, 102, 110];

// Berechnen des Gewinns
const gewinn = verkaufszahlen.map((value, index) => value - kosten[index]);

// Berechnen des kumulierten Gewinns
const kumulierterGewinn = gewinn.reduce((acc, value, index) => {
	if (index === 0) {
	acc.push(value);
	} else {
	acc.push(acc[index - 1] + value);
	}
	return acc;
	}, []);

const chartData = {
	type: 'line',
	data: {
		labels: labels,
		datasets: [
			{
				label: 'Verkaufszahlen im Jahr',
				data: verkaufszahlen,
				borderColor: 'rgba(153, 102, 255, 1)',
				backgroundColor: 'rgba(153, 102, 255, 0.2)',
				borderWidth: 2
			},
			{
				label: 'Kosten im Jahr',
				data: kosten,
				borderColor: 'rgba(255, 99, 132, 1)',
				backgroundColor: 'rgba(255, 99, 132, 0.2)',
				borderWidth: 2
			},
			{
				type: 'bar', // Barchart für den Gewinn
				label: 'Gewinn im Jahr',
				data: gewinn,
				backgroundColor: 'rgba(75, 192, 192, 0.2)', // Hintergrundfarbe für die Balken
				borderColor: 'rgba(75, 192, 192, 1)', // Farbe der Balken
				borderWidth: 1
			},
			{
				label: 'Kummulierter Gewinn',
				data: kumulierterGewinn,
				borderColor: 'rgba(255, 206, 86, 1)', // Gelbe Farbe für den durchschnittlichen Gewinn
				backgroundColor: 'rgba(255, 206, 86, 0.2)', // Hintergrundfarbe für den Bereich unterhalb der Linie
				borderWidth: 2
			}
		]
	}
};

this.container.style.width = '600px'
this.container.style.height = '300px'

window.renderChart(chartData, this.container);
```
#### Pie-Chart
> Grundsätzlich benötigt Obsidian für die Verwendung von Pie-Charts keine weiteren Community Plugins jedoch sehen diese Optisch durch die Verwendung von **<font style="color:#9966FF">Dataview</font>** in Kombination mit <font style="color:#9966FF">Chart</font> deutlich anschaulicher aus.
##### Mermaid Lösung
```mermaid
%%{init: {'theme': 'dark'}}%%
pie 
title Beispiel Studenten des Studiengangs Data Science

"Männlich" : 20
"Weiblich" : 4
"divers" : 2
```
##### Dataviewjs lösung
> Durch das klicken in das Diagramm können Filter aktiviert werden! :)
```dataviewjs
const labels = ['Männlich', 'Weiblich', 'divers'];
const data = [20, 4, 2];

const chartData = {  
    type: 'pie',
    data: {
        labels: labels,
        datasets: [{
            label: 'Numbers',
            data: data,
            backgroundColor: ['rgba(0, 0, 128, 0.8)', 'rgba(153, 102, 255, 0.8)', 'rgba(204, 204, 204, 0.8))']
        }]
    }
}
this.container.style.width = '500px'
this.container.style.height = '500px'


window.renderChart(chartData, this.container);
```
# Andere darstellungs formen
#### Fluss Diagramm
> Flussdiagramme können ohne weitere Obsidian Community Plugins erstellt werden.
##### Mermaid
```mermaid
flowchart TB 
	start((Start)) --> input[Benutzereingabe]
	input --> decision{Eingabe gültig?}
	decision -- Ja --> process1[Aktion 1]
	decision -- Nein --> error((Fehlermeldung))
	process1 --> sub1(Subprozess)
	sub1 --> process2[Aktion 2]
	process2 --> decision2{Bedingung erfüllt?}
	decision2 -- Ja --> end1[Ende 1]
	decision2 -- Nein --> process3[Aktion 3] 
	rocess3 --> end2[Ende 2]
	error --> input
```
#### Sequenzdiagramm
> Sequenzdiagramme können ohne weitere Obsidian Community Plugins erstellt werden.
##### Mermaid
###### Einfaches Beispiel
```mermaid
sequenceDiagram
	participant Client
	participant Server
	
	Client->>Server: Anfrage senden
	activate Server
	Server-->>Client: Bestätigung erhalten
	deactivate Server
	Client->>Server: Daten senden
	activate Server
	Server-->>Client: Daten verarbeiten
	deactivate Server
	Client-->>Server: Ergebnisse abrufen
	activate Server
	Server-->>Client: Ergebnisse senden
	deactivate Server
```
###### Komplexeres Beispiel
```mermaid
sequenceDiagram
	participant Client
	participant Server
	participant Datenbank
	
	Client->>Server: Anfrage senden
	activate Server
	Server->>Datenbank: Anfrage weiterleiten
	activate Datenbank
	Datenbank-->>Server: Datenbankantwort
	deactivate Datenbank
	Server-->>Client: Antwort senden
	alt Erfolgreiche Antwort
		Client->>Server: Bestätigung erhalten
	else Fehlerhafte Antwort
		Client->>Server: Fehlermeldung erhalten
	end
	deactivate Server
	loop 5 times
		Client->>Server: Zusätzliche Anfrage senden
		activate Server
		Server->>Datenbank: Anfrage weiterleiten
		activate Datenbank
		Datenbank-->>Server: Datenbankantwort
		deactivate Datenbank
		Server-->>Client: Antwort senden
		deactivate Server
	end

```

#### Graphen
```mermaid
graph LR
	A((Start)) -- 10 --> B[New York]
	A -- 15 --> C[Los Angeles]
	B -- 5 --> D[Chicago]
	B -- 8 --> E[Miami]
	C -- 12 --> F[San Francisco]
	C -- 9 --> G[Seattle]
	D -- 7 --> H[Dallas]
	D -- 11 --> I[Atlanta]
	E -- 6 --> J[Orlando]
	E -- 13 --> K[Houston]
	F -- 14 --> L[Las Vegas]
	F -- 10 --> M[Denver]
	G -- 9 --> N[Portland]
	G -- 7 --> O[Phoenix]
	H -- 5 --> P[Austin]
	H -- 6 --> Q[New Orleans]
	I -- 8 --> R[Charlotte]
	I -- 9 --> S[Nashville]
	J -- 3 --> T[Tampa]
	J -- 4 --> U[Boston]
	K -- 11 --> V[San Diego]
	K -- 10 --> W[Minneapolis]
```

