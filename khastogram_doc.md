# Quicknotes - Khasbulatov Yusup | Rails Application | Instagram
## Inhaltsverzeichnis
1. [Ruby on Rails](#ruby-on-rails)
2. [ORM](#orm)
3. [Namenskonventionen in Ruby On Rails](#namenskonventionen-in-ruby-on-rails)  
    4. [Allgemeine Regeln](#allgemeine-regeln)  
    5. [Datenbank](#Datenbank)  
    6. [Model (Klassen)](#Model-(Klassen))  
    7. [Beziehungen in Modellen](#Beziehungen-in-Modellen)  
    8. [Controller](#Controller)  
    9. [Routen](#Routen)  
    10. [Views](#Views)

--- 

Um das Wissen über die Arbeit mit Datenbanken durch Webanwendungen zu verbessern, haben wir das Ruby On Rails-Framework wegen seiner Relevanz und Flexibilität verwendet. Vor allem aber wegen der Möglichkeit, in kürzester Zeit ein einsatzbereites Produkt zu erstellen. Ruby On Rails unterstützt Datenbankoperationen out of the box, man muss nichts zusätzlich installieren. Auch das integrierte Webstyle-Framework Bootstrap mit seinen Utility-First css-Klassen macht die Entwicklung von Webinterfaces sehr kostengünstig.

## Ruby on Rails
Rails ist in erster Linie eine Entwicklungsumgebung, die sich hervorragend für die Erstellung jeder Art von Webanwendungen eignet: Website-Management-Systeme und E-Commerce-Plattformen, Webdienste für Zusammenarbeit und Kommunikation, Buchhaltungs- und ERP-Systeme, statistische und analytische Systeme.

Ruby on Rails (RoR oder Rails) ist ein mehrschichtiges MVC-Framework zum Erstellen von Webanwendungen, die relationale und NoSQL-Datenbanken (wie MySQL, MariaDB, PostgeSQL, MongoDB) verwenden. Das Framework ist in der Programmiersprache Ruby geschrieben. Rails eignet sich sowohl für die Entwicklung normaler Websites, die wirklich schnell, fehlertolerant und unter hoher Last arbeiten müssen, als auch für Webanwendungen mit komplexer Geschäftslogik und dynamischen Web-Schnittstellen. Ruby on Rails ist Open Source und steht unter der MIT-Lizenz.  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)

## ORM
Ein integraler Bestandteil jedes interaktiven Programms ist das Speichern, Anzeigen und Bearbeiten von Daten. ORM steht für Object-Relational-Mapping. Im Wesentlichen bedeutet dies, dass Active Record Daten abruft, die in einer Datenbanktabelle mit Zeilen und Spalten gespeichert sind, die durch das Schreiben von SQL-Abfragen geändert oder abgerufen werden müssen (wenn man eine SQL-Datenbank verwendet), und ermöglicht somit die Interaktion mit diesen Daten, wie man es mit einem normalen Ruby-Objekt tun würde.

Beispiel: Angenommen, man möchte ein Array aller Benutzer abrufen. Anstatt Code zu schreiben, um sich mit der Datenbank zu verbinden und dann eine SQL-Abfrage wie SELECT * FROM users zu schreiben und das Ergebnis in ein Array zu konvertieren, kann man einfach User.all eingeben, und Active Record gibt ein Array mit User-Objekten aus, mit denen man beliebig spielen kann.

Es spielt eigentlich keine Rolle, welche Art von Datenbank man verwendet. Active Record gleicht alle Unterschiede zwischen diesen Datenbanken aus, so dass man nicht darüber nachdenken muss. Dabei konzentriert man sich auf das Schreiben des Codes für die Anwendung und Active Record kümmert sich um die Feinheiten der Verbindung zur Datenbank. Das bedeutet auch, dass man beim Wechsel von einer Datenbank zu einer anderen nicht wirklich den zugrunde liegenden Anwendungscode ändern muss, sondern nur einige der Konfigurationsdateien.  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)

## Namenskonventionen in Ruby On Rails

In Ruby on Rails gilt oft die Regel "Konvention vor Konfiguration" - anstatt explizit festzulegen, was mit was zusammenhängt und wie es funktioniert, einigen sich die Entwickler einfach auf einige Regeln für die Benennung von Entitäten und halten sich daran, um ihr Leben zu vereinfachen und die Menge des benötigten Codes zu reduzieren.
Alle Regeln aufzulisten würde viel Platz und Zeit in Anspruch nehmen, aber hier sind einige von denen, die bei der Entwicklung einer Instagram-App wichtig zu wissen sind.  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)

##### Allgemeine Regeln
- Bei der Benennung von Klassen verwenden wir `CamelCase`.
- Bei der Benennung von Methoden und Variablen verwenden wir `snake_case`.
- Methoden mit `?` geben einen booleschen Wert zurück.
- Methoden mit `!` bedeuten eines von zwei Dingen: entweder sie modifizieren das Objekt, auf das sie angewendet werden; oder sie lösen eine Exception aus, anstatt das Programm zum Absturz zu bringen (wie z.B. in `#save!` vs. `#save`-Methoden).
- In der Dokumentation bezieht sich `::method_name` auf die Klassenmethode, wobei `#method_name` auf die Instanzmethode verweist.  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)

##### Datenbank
- Bei der Benennung von Datenbanktabellen wird `snake_case` verwendet. Die Namen selbst stehen im **Plural**.
- Bei Spaltennamen wird `snake_case` verwendet, diese werden in **Singular** geschrieben.  Beispiel:
```
    +--------------------------+        +------------------------------+
    | firmas                   |        | angestelltes                 |
    +------------+-------------+        +---------------------+--------+
    | id         | ID          |        | id             | ID          |
    | name       | STRING      |        | name           | STRING      |
    | addresse   | STRING      |        | ferien         | INT         |
    +------------+-------------+        | firma_id       | FOREIGN KEY |
                                        | addresse       | STRING      |
                                        +---------------------+--------+
```  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)

##### Model (Klassen)
- In Modellklassennamen wird `CamelCase` verwendet und sie werden in **Singular** geschrieben. Diese werden automatisch auf die Namen der Datenbanktabellen abgebildet.
- Bei der Benennung von Attributen und Methoden in Modellen wird `snake_case` verwendet. Diese werden auf die Spaltennamen der Datenbanktabelle abgebildet.
- Die Modelldateien befinden sich unter `app/models/#{singular_model_name}.rb...`. Beispiel:
```
# app/models/firma.rb
class Firma < ActiveRecord::Base
  # Diese Klasse wird die folgenden Attribute haben: id, name, addresse
end
```
```
# app/models/angestellte.rb
class Angestellte < ActiveRecord::Base
  # Methoden folgen den gleichen Konventionen wie Attribute
  def hat_ferien?
    ferien < 25
  end
end
```  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)

##### Beziehungen in Modellen
- `snake_case` wird zur Kennzeichnung von Beziehungen verwendet. Sie hängen von der Art der Verknüpfung ab: `has_one` und `belongs_to` sind **Singular**, `has_many` ist **Plural**.
- Bei externen Schlüsseln in der Datenbank wird angenommen, dass sie ein `_id`-Suffix haben - sie werden automatisch mit Beziehungen abgeglichen, wenn die Namen übereinstimmen. Beispiel:
```
# app/models/firma.rb
class Firma < ActiveRecord::Base
  has_many :angestellte
end
```
```
# app/models/angestellte.rb
class Angestellte < ActiveRecord::Base
  belongs_to :firma
end
```  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)

##### Controller
- Bei Klassennamen in Controllern wird `CamelCase` verwendet, sie müssen ein Suffix `Controller` haben. Dieses Suffix steht immer im **Singular**. Der Quellenname steht in der Regel im **Plural**. Beispiel:
```
# app/controllers/angestellten_controller.rb
class AngestelltenController < ApplicationController
    def index
        # ...
    end
end
```
- Bei der Benennung von Controller-Aktionen wird `snake_case` verwendet, sie werden üblicherweise auf Standard-Rails-Pfadnamen (`index`, `show`, `new`, `create`, `edit`, `update`, `delete`) abgebildet.
- Controller befinden sich unter `app/controllers/#{resource_name}_controller.rb...`  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)

##### Routen
- Pfadnamen (routen) werden mit `snake_case` geschrieben, sie passen in der Regel zu den entsprechenden Controllern. In den meisten Fällen werden die Pfade in **Plural** geschrieben.
- Singuläre Routen sind ein Sonderfall. Diese verwenden die singuläre Quelle und einen singulären Quellennamen. Sie mappen aber trotzdem standardmässig auf einen Plural-Controller! Beispiel:
```
resources :firmas
# Benutzer können nur ihre eigenen Profile sehen, daher verwenden wir `/profile`.
# anstatt die ID zur URL hinzuzufügen.
resource :profile
```  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)

##### Views
- Standardmässig werden die Namen von Views den Controllern und Aktionen abgebildet, auf die sie zugeordnet sind.
- Die Views sind unter `app/views/#{resource_name}/#{action_name}.html.erb...`. Beispiel:
```
app/views/angestellten/index.html.erb
app/views/firmas/index.html.erb
```























