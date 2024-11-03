# Models

### Wie erstelle ich ein Model?
```
<?php

namespace Model;

use Core\Model;

class TestModel extends Model {

    public function SQL() {
        $sql = "INSERT INTO `ticket` (`title`, `content`, `userId`, `tickettypeId`) VALUES (?, ?, ?, ?)";
        $this->exec($sql, "ssii", $title, $content, $userId, $tickettypeId);
    }
}
```
Ein Model benötigt **immer** den `namespace` "Model". Kurzgefasst sorgt das dafür, dass das Model für die Website "sichtbar" gemacht wird. So ermöglichen wir es dem Hauptprogramm dass er dieses Model mit `Model/TestModel` finden kann.

Ebenso müssen wir **immer** `use Core/Model` benutzen. Das Importiert das Main-Model den wir benötigen, damit unser Model funktioniert.

Danach müssen wir eine Klasse-Definieren mit dem **selben** Namen wie die File. Heißt die File also `TestModel.php`, musst die Klasse `TestModel` heißen. Danach `extenden` (= Vererben) wir das Main-Model um seine Funktionen nutzen zu können.


### SQL-Befehl ausführen in einem Models
Mit einem Model lässt sich vereinfacht eine SQL-Request aufbauen.  
Mit dem Befehl `$this->exec($SqlQuery, $ParameterTypes, $ParameterValues)` baust du direkt eine Verbindung zu der Datenbank auf und führt `$SqlQuery` als Query (z.b. "SELECT") aus.  
Um eine Sicherheit gegenüber SQL-Injections zu gewährleisten, verwenden wir `PreparedStatements`. Diese erreichen wir indem wir bei `$ParameterTypes` die jeweiligen Typen, welche wir übergeben wollen, definieren (z.b. Integer [I], ...) und bei `$ParameterValues` den eingesetzten Wert. Wichtig dabei wird, dass bei der `$SqlQuery` jegliche übergebene Variable vorerst als `?` gekennzeichnet wird.  
Beispiel bei einer Search-Funktion:  
  
Ohne `PreparedStatements`:  
`$this->exec("SELECT * FROM products WHERE name LIKE '%Orangensaft%'")`  
  
Mit `PreparedStatements`:  
`$this->exec("SELECT * FROM products WHERE name LIKE '%?%'", "s", "Orangensaft")`  
  
### Prepared Types
| Type     | Beschreibung |
|----------|----------|
| i        | Integer |
| s        | Strings, Doubles, Objects |
| b        | Boolean |


### Weitere SQL Features
Nachdem ein SQL-Befehl abgeschickt wurde, kann man ebenso direkt die Response verarbeiten. So kannst du z.b.:
- `$this->exec($SqlQuery)->resultToLine()` um eine einzelne Antwort zu verarbeiten
- `$this->exec($SqlQuery)->resultToArray()` um mehrere Antworten zu verarbeiten
- `$this->exec($SqlQuery)->countResults()` um die Anzahl der Antworten zu bekommen
- `$this->exec($SqlQuery)->last_id` um die letzte InsertedID zu bekommen