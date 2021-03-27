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
11. [CRUD](#CRUD)  
    12. [C](#Betrachten-wir-diese-Funktionen-mit-Hilfe-von-Beispielen-und-fangen-gleich-mit-C-an.)  
    13. [R](Dann-kommt-das-“R”-von-CRUD.)  

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
- Bei externen Schlüsseln in der Datenbank wird angenommen, dass sie ein `_id`-Suffix haben - sie werden automatisch mit Beziehungen abgeglichen, wenn die Namen übereinstimmen. 
- `created_at` Ermittelt automatisch das aktuelle Datum und die Uhrzeit, wann der Datensatz erstellt wurde.
- `updated_at` Bei jeder Aktualisierung des Datensatzes wird automatisch das aktuelle Datum und die aktuelle Uhrzeit eingetragen. Beispiel:
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

## CRUD
CRUD (create, read, update, delete) - vier grundlegende Funktionen, die bei der Arbeit mit Datenbanken und anderen Informationsspeichern verwendet werden:

| Funktion               | SQL-Befehl | HTTP           |
|------------------------|------------|----------------|
| Create (Erstellen)     | INSERT     | POST           |
| Read (Lesen)           | INSERT     | GET            |
| Update (Aktualisieren) | UPDATE     | PUT oder PATCH |
| Delete (Löschen)       | DELETE     | DELETE         |

##### Betrachten wir diese Funktionen mit Hilfe von Beispielen und fangen gleich mit C an.
Normalerweise ist das Erstellen einer neuen Ressource in Webanwendungen ein mehrstufiger Prozess. Zuerst fordert der Benutzer ein Formular zum Ausfüllen an. Dann sendet der Benutzer das Formular ab. Wenn es keine Fehler gibt, wird die Ressource erstellt und eine Bestätigung angezeigt. Andernfalls wird das Formular erneut mit Fehlermeldungen angezeigt, und der Vorgang wird wiederholt.

In einer Rails-Anwendung werden diese Schritte traditionell von den Controller-Aktionen `new` und `create` erledigt. Beispiel von typische Implementierung dieser Aktionen in `app/controllers/articles_controller.rb`:
```
class ArticlesController < ApplicationController
  def new
    @article = Article.new
  end

  def create
    @article = Article.new(title: "...", body: "...")

    if @article.save
      redirect_to @article
    else
      render :new
    end
  end
  
  private
    def article_params
      params.require(:article).permit(:title, :body)
    end
end
```
Aktion `new` initialisiert einen neuen Artikel, speichert ihn aber nicht. Dieser Artikel wird in der Ansicht beim Aufbau des Formulars verwendet. Standardmässig wird die neue Aktion `app/views/articles/new.html.erb` gerendert.
Die Aktion `create` initialisiert einen neuen Artikel mit Werten für `title` und `body` und versucht, ihn zu speichern. Wenn der Artikel erfolgreich gespeichert wurde, leitet die Aktion den Browser auf die Artikelseite `"http://localhost:3000/articles/#{@article.id}"` um. Andernfalls zeigt die Aktion das Formular erneut an, indem sie `app/views/articles/new.html.erb` rendert.
>`redirect_to` veranlasst den Browser, eine neue Anfrage zu stellen, wohingegen `render` die angegebene Ansicht für die aktuelle Anfrage rendert. Es ist wichtig, `redirect_to` nach einer Änderung des Datenbank- oder Anwendungsstatus zu verwenden. Andernfalls, wenn der Benutzer die Seite aktualisiert, wird der Browser die gleiche Anfrage stellen und die Änderung wird wiederholt.

Die übermittelten Formulardaten werden in den `params`-Hash eingebettet, zusammen mit den erfassten Routenparametern. Die `create`-Aktion hat also Zugriff auf den gesendeten Titel als `params[:article][:title]` und auf den gesendeten Inhalt als `params[:article][:body]`. Diese Werte können separat an `Article.new` übergeben werden, aber das kann hässlich und fehleranfällig sein.
Wir übergeben einen einzelnen Hash, der die Werte enthält. Wir müssen jedoch noch festlegen, welche Werte in diesem Hash gültig sind. Andernfalls könnte ein Angreifer möglicherweise zusätzliche Formularfelder senden und sensible Daten überschreiben. Wenn wir nämlich einen ungefilterten `params[:article]`-Hash direkt an `Article.new` übergeben, ruft Rails `ForbiddenAttributesError` auf, um uns auf das Problem hinzuweisen. Daher werden wir eine Rails-Funktion namens **_Strong Parameters_** zum Filtern von Parametern verwenden. Der private Methode am Ende von `app/controllers/articles_controller.rb`, genannt `article_params`, filtert params.

**Form builder**
Mit dem Form Builder kann man mit einem Minimum an Code ein vollständig angepasstes Formular ausgeben, das den Rails-Konventionen folgt. Um aber Fehlermeldungen anzeigen zu können, legen wir in Artikeln einige Validierungen an. Rails bietet eine Validierungsfunktion, die uns hilft, mit falschen Benutzereingaben umzugehen. Validierungen sind Regeln, die vor dem Speichern eines Modellobjekts überprüft werden. Wenn eine der Prüfungen fehlschlägt, wird der Speichervorgang abgebrochen und entsprechende Fehlermeldungen werden dem Attribut `errors` des Modellobjekts hinzugefügt. Validierungen für das Modell in `app/models/article.rb`:
```
class Article < ApplicationRecord
  validates :title, presence: true
  validates :body, presence: true, length: { minimum: 10 }
end
```
Die erste Validierung besagt, dass der `titel`-Wert vorhanden sein muss. Da der Titel eine Zeichenkette ist, bedeutet dies, dass der `titel`-Wert mindestens ein Zeichen ohne Leerzeichen enthalten muss.
Die zweite Validierung besagt, dass der `body`-Wert ebenfalls vorhanden sein muss. Ausserdem wird festgelegt, dass die Länge des `body`-Wertes mindestens 10 Zeichen betragen muss.
>Active Record definiert automatisch Modellattribute für jede Tabellenspalte, so dass es nicht notwendig ist, diese Attribute in der Modelldatei zu deklarieren.

Das Formular erstellen wir in folgendes Datei `app/views/articles/new.html.erb`:
```
<h1>New Article</h1>

<%= form_with model: @article do |form| %>
  <div>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
    <%= @article.errors.full_messages_for(:title).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.label :body %><br>
    <%= form.text_area :body %><br>
    <%= @article.errors.full_messages_for(:body).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```
Die Helper-Methode `form_with` initialisiert den Form Builder. Im `form_with`-Block rufen wir Methoden wie `label` und `text_field` auf dem Form Builder auf, um die entsprechenden Formularelemente auszugeben.
Die resultierende Ausgabe eines Aufrufs von form_with sieht wie folgt aus:
```
<form action="/articles" accept-charset="UTF-8" method="post">
  <input type="hidden" name="authenticity_token" value="...">

  <div>
    <label for="article_title">Titel</label><br>
    <input type="text" name="article[title]" id="article_title">
  </div>

  <div>
    <label for="article_body">Text</label><br>
    <textarea name="article[body]" id="article_body"></textarea>
  </div>

  <div>
    <input type="submit" name="commit" value="Artikel erstellen" data-disable-with="Artikel erstellen">
  </div>
</form>
```

##### Dann kommt das "R" von CRUD.
Standardmäßig werden für "R" die Methoden `index` und `show` verwendet. Unter `index` wird eine Übersicht über alle Elemente des Modells erstellt, und unter `show` werden einzelne Elemente angezeigt. Hier ist ein Beispiel:
```
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end

  def show
    @article = Article.find(params[:id])
  end
end
```
Wie oben erwähnt, benötigen wir auch Routen für die Anzeige einzelner Elemente sowie für die Methode `index`. Auf diese Weise könnten Routen erstellt werden:
```
Rails.application.routes.draw do
  root "articles#index"

  get "/articles", to: "articles#index"
  get "/articles/:id", to: "articles#show"
end
```
Mit dem `root "articles#index` sagen wir, dass unsere erste geladene Seite `"articles#index"` sein wird. Anstatt jede Routen selber zu definieren können wir auch eine Hilfemethode `resources` von Rails verwenden:
```
Rails.application.routes.draw do
  root "articles#index"

  resources :articles
end
```
Mit dem Befehl `rails routes` lässt sich feststellen, welche Routen miteinander verbunden sind:
```
$ rails routes
      Prefix Verb   URI Pattern                  Controller#Action
        root GET    /                            articles#index
    articles GET    /articles(.:format)          articles#index
 new_article GET    /articles/new(.:format)      articles#new
     article GET    /articles/:id(.:format)      articles#show
             POST   /articles(.:format)          articles#create
edit_article GET    /articles/:id/edit(.:format) articles#edit
             PATCH  /articles/:id(.:format)      articles#update
             DELETE /articles/:id(.:format)      articles#destroy
```
Die `resources`-Methode konfiguriert auch Hilfs-URL- und Pfad-Methoden, die verwendet werden können, um zu verhindern, dass unser Code von der Konfiguration einer bestimmten Route abhängt. Die Werte oben in der Spalte **"Präfix"** plus das Suffix `_url` oder `_path` bilden die Namen dieser Hilfsmethoden. Zum Beispiel gibt der Helfer `article_path` `"/articles/#{article.id}"` für einen bestimmten Artikel zurück. Nun erstellen wir die Übersichtsseite `app/views/articles/index.html.erb`:
```
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <a href="<%= article_path(article) %>">
        <%= article.title %>
      </a>
    </li>
  <% end %>
</ul>
```
Oder man könnte auch die Hilfemethode `link_to` zu verwenden. Der `link_to`-Helfer erzeugt einen Link mit dem ersten Argument als Linktext und dem zweiten Argument als Linkadresse. Wenn wir das Modellobjekt als zweites Argument übergeben, ruft `link_to` den entsprechenden Pfadhelfer auf, um das Objekt in einen Pfad zu konvertieren.
```
<h1>Articles</h1>

<ul>
  <% @articles.each do |article| %>
    <li>
      <%= link_to article.title, article %>
    </li>
  <% end %>
</ul>
```

























