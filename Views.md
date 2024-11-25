# Views
Eine View enthält das HTML, das der Benutzer sehen soll. Alle zusätzlichen Ressourcen wie CSS, Bilder oder JavaScript werden ebenfalls von der View geladen.
Views enthalten normalerweise keinen Footer, keine Navigation, keinen Header oder andere Elemente, die zum allgemeinen Layout der Seite gehören. 
Dafür sollten Layouts verwendet werden, da eine View ohne ein Layout nicht gerendert werden kann.

Datenbankzugriffe und umfangreiche Logik sollten nicht in der View verwendet werden, da sie in andere Teile der Anwendung gehören.

## Struktur
Eine View sollte sich im Verzeichnis `views` des Projekts befinden, da sie andernfalls nicht gefunden wird, wenn die render-Methode aufgerufen wird.

Es handelt sich um eine PHP-Datei, die ein Array mit bis zu drei Attributen zurückgibt. 
head und body sind Funktionen, die im Layout an den entsprechenden Stellen ausgeführt werden.

head und body sollten einen Parameter namens $opt akzeptieren. Dieser enthält Daten, die über den $opt-Parameter der render-Methode übergeben wurden. 
Damit die View mit einem Controller kommunizieren kann, müssen asynchrone Methoden verwendet werden.

## Einfaches Beispiel
```
<?php return [ "head" => function($opt) { ?>
  <title>Title der Webseite</title>
<?php }, "body" => function($opt) { ?> 
  <h2>Hallo</h2>
<?php }]; ?>
```
