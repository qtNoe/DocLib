# Controller und Actions

### Was ist Routing?
Routing beschreibt die verwaltung der einzelnen Endpunkte.  

Eine URL ist in 4 geteilt:  
| https://localhost/`ROOTNAME`/`Controller`/`Action`/`Parameters`  
- **Rootname**: Der Rootname ist der Standardmäßige Part, der nach dem Host kommt. In Unserem Beispiel ruft man unsere Website mit dem Rootnamen `OS2` oder `Onlineshop` auf.
- **Controller**: Der Name des Controllers
- **Action**: Der Name der Action
- **Parameters**: Zusätzliche Informationen wie z.b. Seitenzahl

`localhost/OS2/Test/Beispiel/15/83/Aktiviert`  
Das würde in dem `TestController` die Action `Beispiel` aufrufen und die Parameter `15`, `83`, `Aktiviert` übergeben.



### Wie erstelle ich einen Controller?
```
<?php

namespace Controller;

use Core\Controller;

class TestController extends Controller {

    public function action_index() {

    }

    public function action_test(...$params) {

    }

}
```
Ein Controller benötigt **immer** den `namespace` "Controller". Kurzgefasst sorgt das dafür, dass der Controller für die Website "sichtbar" gemacht wird. So ermöglichen wir es dem Hauptprogramm dass er diesen Controller mit `Controller/TestController` finden kann.

Ebenso müssen wir **immer** `use Core/Controller` benutzen. Das Importiert den Main-Controller den wir benötigen, damit unser Controller funktioniert.

Danach müssen wir eine Klasse-Definieren mit dem **selben** Namen wie die File. Heißt die File also `TestController.php`, musst die Klasse `TestController` heißen. Danach `extenden` (= Vererben) wir den Main-Controller um seine Funktionen nutzen zu können.

Eine **Action** wird immer mit einer public function beschrieben. Zusätzlich ist es notwendig, dass der Name der function mit `action_` beginnt, danach der Name ist egal.  
Eine Besonderheit ist die `action_index`, diese sorgt dafür dass der "action"-Part der URL wegfällt. Somit wird in diesem Beispiel die `action_index` unter folgender Domain aufgerufen:  
| https://localhost/`ROOTNAME`/`Controller`/  
Der Nachteil daran ist, dass Parameters nicht funktionieren.

### Funktionen in einem Controller
Ein Controller bietet zusätzlich mehrere Funktionen an.
- **Parameters**: Im Controller hast du Zugriff auf die Parameters. Diese kannst du in einer Action aufrufen, indem du `...$params` als Parameter in der Function eingibst. Dieses gibt dir ein Array mit allen Parametern wieder.
- **Render**: Mit dem Befehl `$this->render($view, $data)` kannst du eine View Rendern. Zusätzlich zum Rendern der View, kannst du ebenso mit dem `$data`-Parameter wichtige Informationen mit der View teilen, damit du diese im View wiederfinden kannst.
- **getModel**: Mit dem Befehl `$this->getModel($modelName)` kannst du dir Zugriff zu einem erstellten Model verschaffen. Damit kannst du dann `function`\`s in diesem Model aufrufen.  
| $this->getModel("TestModel")->testFunction()
- **isAction**: Mit dem Befehl `$this->isAction($actionName)` bekommst du ein Boolean zurück, ob per POST-Request eine Action definiert ist. Das ist wichtig um Asynchrone-Requests zu ermöglichen
- **success**: Mit dem Befehl `$this->success($data)` kannst du ein Feedback z.b. an einer Asyncrhonen-Request senden um zu vermitteln dass diese Request einwandfrei durchgekommen ist.
- **error**: Mit dem Befehl `$this->error($data)` kannst du ein Feedback z.b. an einer Asyncrhonen-Request senden um zu vermitteln dass diese Request ein Fehler hat.