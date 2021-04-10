# ioBroker-HomePod
Workaround um über Siri (HomePod) bestimmte Datenpunkte aus dem ioBroker abfragen zu können

## Anleitung

zunächst benötigt man den Adapter: simple RESTful API

<img src="https://user-images.githubusercontent.com/66023319/114274881-b1599080-9a20-11eb-9d5d-3d652f71b881.png" height="200">

Anschließend erzeugt man sich einen Datenpunkt mit dem Text der von Siri wiedergegeben werden soll:

Hier als Beispiel mit dem Tankerkönig Adapter und dem Datenpunkt tanken. 

```
on("tankerkoenig.0.stations.cheapest.e5.feed", function(dp) {
    var tankePreis = getState("tankerkoenig.0.stations.cheapest.e5.feed").val;

    setState("0_userdata.0.Siri.tanken", "Du zahlst " +tankePreis+ " je Liter.");
});
```

Um nun mittels Siri darauf zugreifen zu können erstellen wir auf einem iOS-Gerät ein Kurzbefehl:

### 1. Kurzbefehl umbennen

  * Diesen Namen verwendet man als Sprachbefehl an Siri. 
  
    * (Beispiel: Kurzbefehl Name "tanken"  -> Sprachbefehl: "Hey Siri, tanken")

### 2. Aktion hinzufügen: Inhalte von URL Abrufen

  * http://DEINE-IP:8087/getPlainValue/DATENPUNKT
  
    * DEINE-IP = Die Ip deines ioBrokers mit dem Port 8087 (Beispiel: 192.168.178.3:8087)
  
    * DATENPUNKT = Der Pfad deines Datenpunktes mit dem erstellten Text (Beispiel: 0_userdata.0.Siri.tanken)

### 3. Aktion hinzufügen: Text sprechen

  * Inhalt der URL
  
Das sollte dann so aussehen:

<img src="https://user-images.githubusercontent.com/66023319/114275745-f8955080-9a23-11eb-947b-98bae40c9f7c.png" height="500">


### 4. Bestätigen

    * Nun Bestätigen wir die Einstellungen mit fertig

    * Fragen wir nun: Hey Siri, tanken

        * Kommt als Antwort: Du zahlst 1 Euro 30 je Liter.
