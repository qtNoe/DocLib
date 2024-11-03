# Models, Views und Controllers (Struktur)
Ein Model-View-Controller (MVC) ist ein Entwurfsmuster, das die Logik einer Anwendung in getrennte Bereiche aufteilt, von denen jeder eine bestimmte Aufgabe erfüllt.



### Was ist ein **Model**?
Ein Model ist für die Interaktion mit deiner Daten-Struktur zuständig. Im Normalfall ist das eine Datenbank. Das Model ist dafür da um die Daten zu Bekommen (`SELECT`), Updaten (`UPDATE`), Entfernen (`REMOVE`) oder Hinzuzufügen (`INSERT`)



### Was ist ein **Controller**?
Ein Controller ist für die komplette Logic zuständig. Primär übernimmt er das Routing, aber ist ebenso für Sicherheitsaspekte, Permissionchecks, usw zuständig



### Was ist eine **View**?
Eine View beinhaltet den HTML-Code den der Benutzer sieht. Alle weiteren Ressourcen wie CSS, Bilder oder JavaScript werden ebenso in Views geladen.