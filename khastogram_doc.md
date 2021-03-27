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
    12. [C](#betrachten-wir-diese-funktionen-mit-hilfe-von-beispielen-und-fangen-gleich-mit-c-an)  
    13. [R](#dann-kommt-das-r-von-crud)  
    14. [U](#artikel-update)  
    15. [D](#artikel-delete)  
16. [Modell Assoziationen](#modell-assoziationen)

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

[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)  

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

Es besteht jedoch verschiedene Möglichkeiten, Daten zu validieren, bevor sie in einer Datenbank gespeichert werden:
- Validierungen auf Modell-Ebene (native Datenbankeinschränkungen)
- Clientseitige Validierungen
- Validierungen auf Controller-Ebene

Mit Validierungen wird sichergestellt, dass nur gültige Daten in die Datenbank gespeichert werden. Beispielsweise kann es für eine Anwendung wichtig sein, sicherzustellen, dass jeder Benutzer eine gültige E-Mail-Adresse und eine gültige Postanschrift angibt. Validierungen sind datenbankunabhängig im Sinne, dass Sie auf verschieden Datenbanken anwendbar sind. Validierungen können nicht von Endbenutzern umgangen werden und sind für Entwicklerinnen und Entwickler bequem zu testen und zu warten.

Folgende Methoden machen keine Validierung und speichern Objekte im Modell ohne Prüfung ab. Deshalb muss man diese Methoden mit Vorsicht angewandten:
```
    decrement!
    decrement_counter
    increment!
    increment_counter
    toggle!
    touch
    update_all
    update_attribute
    update_column
    update_columns
    update_counters
```

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
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)  

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
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)  

##### Artikel-Update
Das Aktualisieren einer Ressource ist dem Erstellen einer Ressource sehr ähnlich. Es handelt sich bei beiden um mehrstufige Prozesse. Zunächst fordert der Benutzer ein Formular zum Bearbeiten der Daten an. Dann sendet der Benutzer das Formular ab. Wenn keine Fehler aufgetreten sind, wird die Ressource dann aktualisiert. Andernfalls wird das Formular erneut mit Fehlermeldungen angezeigt und der Vorgang wiederholt sich. Konventionell werden diese Schritte von den `edit`- und `update`-Aktionen des Controllers übernommen. Eine typische Implementierung dieser Aktionen fügen wir in `app/controllers/articles_controller.rb` ein:
```
class ArticlesController < ApplicationController
  def edit
    @article = Article.find(params[:id])
  end

  def update
    @article = Article.find(params[:id])

    if @article.update(article_params)
      redirect_to @article
    else
      render :edit
    end
  end

  private
    def article_params
      params.require(:article).permit(:title, :body)
    end
end
```
Die Methode `"edit"` holt den Artikel aus der Datenbank und speichert ihn in `@article`, so dass er für den Aufbau des Formulars verwendet werden kann. Standardmässig rendert die Methode `"edit"` die Datei `app/views/articles/edit.html.erb`. Die `update`-Methode holt den Artikel (erneut) aus der Datenbank und versucht, ihn mit den in `article_params` gefilterten Daten des übermittelten Formulars zu aktualisieren. Wenn keine Validierung fällt und die Aktualisierung erfolgreich ist, leitet diese Methode den Browser auf die Artikelseite um. Andernfalls wird die Methode das Formular mit Fehlermeldungen erneut anzeigen und `app/views/articles/edit.html.erb` wiedergeben.  
Da das `edit`-Formular genauso aussieht wie das `new`-Formular, sogar der Code wird dank des Rails-Formular-Builders und des Ressourcen-Routings gleich sein, kann man eine gemeinsame View erstellen, die _partiell_ `app/views/articles/_form.html.erb` mit dem folgenden Inhalt heisst:
```
<%= form_with model: article, local: true do |form| %>
  <div>
    <%= form.label :title %><br>
    <%= form.text_field :title %>
    <%= article.errors.full_messages_for(:title).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.label :body %><br>
    <%= form.text_area :body %><br>
    <%= article.errors.full_messages_for(:body).each do |message| %>
      <div><%= message %></div>
    <% end %>
  </div>

  <div>
    <%= form.submit %>
  </div>
<% end %>
```
Der obige Code ist derselbe wie das Formular in `app/views/articles/new.html.erb`, mit der Ausnahme, dass alle Instanzen von `@article` durch `article` ersetzt werden. Da es sich bei Partials um kollaborativen Code handelt, ist es eine gute Praxis, sie nicht von bestimmten Instanzvariablen abhängig zu machen, die von der Controller-Methode gesetzt werden. Stattdessen wird der Artikel als lokale Variable an den Partial übergeben. Dafür muss man den `app/views/articles/new.html.erb` und `app/views/articles/edit.html.erb` aktualisieren damit sie den `render` methode verwenden.
```
# app/views/articles/new.html.erb
<h1>New Article</h1>

<%= render "form", article: @article %>
```
```
# app/views/articles/edit.html.erb
<h1>Edit Article</h1>

<%= render "form", article: @article %>
```
>Der Name der Partialdatei muss mit einem Unterstrich beginnen, also `_form.html.erb`. Beim Rendern verweisen wir aber ohne Unterstrich darauf, also `rendern "form"`.  

[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)  

##### Artikel-Delete
Das Löschen einer Quelle ist ein einfacherer Vorgang als das Erstellen oder Aktualisieren einer Quelle. Es wird nur eine Route und eine Controller-Methode benötigt. Und unser Ressourcen-Routing (`resources :articles`) bietet bereits diese Route, die `DELETE /articles/:id`-Anfragen mit der `destroy`-Methode im `ArticlesController` verknüpft.
```
class ArticlesController < ApplicationController
  def destroy
    @article = Article.find(params[:id])
    @article.destroy

    redirect_to root_path
  end
end
```  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)  

# Modell Assoziationen
Wie wir bereits in Bereich [Beziehungen in Modellen](#Beziehungen-in-Modellen) beschrieben habe werden die Assoziationen  immer im Model beschrieben. Einen neuen Model kann mit folgendes Befehl erstellt werden:
```
$ rails generate model Artikel title:string body:text author:references
```
Dieser Befehl erzeugt vier Dateien:
| Datei | Funktion |
|---|---|
| db/migrate/2021032701010_create_artikels.rb | Migration zum Erstellen einer `artikels`-Tabelle in der Datenbank |
| app/models/artikel.rb | Model Artikel |
| test/models/artikel_test.rb | Gerüst zum Testen des Artikelmodells |
| test/fixtures/artikels.yml | Artikelmuster zur Verwendung in Tests |

Mit Active Record-Beziehungen lassen sich auf einfache Weise Beziehungen zwischen zwei Modellen deklarieren. Im Fall von Artikel und Autor kann man die Beziehung wie folgt beschreiben:
- Jeder Artikel gehört zu einem Autor.
- Ein Autor kann viele Artikel haben.

Und so sieht die Modelle aus:
```
class Author < ApplicationRecord
  has_many :artikels

  validates :name, presence: true
  validates :addresse, presence: true
end
```
Und Artikel Model:
```
class Artikel < ApplicationRecord
  belongs_to :author
  
  validates :title, presence: true
  validates :body, presence: true, length: { minimum: 10 }
end
```
`has_many` symbolisiert der 1-seitige Beziehung, dass dieses Modell viele Assoziationspartner besitzt. Die eindeutige Zuordnung der N-Seite wird dagegen weiterhin durch ein belongs_to angezeigt. Für die Navigation bzw. Zuweisung sind die Veränderungen ebenso einseitig.  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)  

# Rails Instagram
Nun, da wir bereits die Grundlagen über die Datenbank beschrieben haben und sie in Zukunft als Hilfsmittel verwenden können, beginnen wir mit den Notizen über die Rails Instagram-App und gleich mit der Authentifizierung.

##### Basic Authentifikation
Für die Basis-Authentifizierung werden wir eine Authentifizierungskomponente verwenden, nämlich den `device`-Paket. 
>Devise ist eine Full-Stack-Authentifizierungslösung, die alle Model-, View- und Controller-Schichten mit Rails Engines implementiert. Sie befasst sich mit der Kontobestätigung und der Passwort-Wiederherstellung.

Um die neueste Version zu installieren ([_mehr über gem und Gemfile_](#RubyGem)):
```
gem install device
```
Um die ein bestimmte Version zu installieren:
```
gem install device -v 2.1.2
```
Nun müssen wir den gem in unseren [Gemfile](#RubyGem) einfügen:
```
gem 'devise'
```
Nach der Installation von `device` müssen wir die entsprechende Konfiguration anhand der Ausgabeinhalte an der Kommandozeile vornehmen. Zudem generieren wir eine Migrationsdatei für einen User-model und führen schlussendlich die Migrationen ein:
```
rails g devise User
rails db:migrate
```
Nun können wit mithilfe des Device alle view Operationen (CRUD) mit User-modelle machen. Device erstellt für uns auch folgende Routen:
```
$ rails routes
                  Prefix Verb   URI Pattern                         Controller#Action
        new_user_session GET    /users/sign_in(.:format)            devise/sessions#new
            user_session POST   /users/sign_in(.:format)            devise/sessions#create
    destroy_user_session DELETE /users/sign_out(.:format)           devise/sessions#destroy
       new_user_password GET    /users/password/new(.:format)       devise/passwords#new
      edit_user_password GET    /users/password/edit(.:format)      devise/passwords#edit
     user_password PATCH        /users/password(.:format)           devise/passwords#update
                         PUT    /users/password(.:format)           devise/passwords#update
                         POST   /users/password(.:format)           devise/passwords#create
cancel_user_registration GET    /users/cancel(.:format)             devise/registrations#cancel
   new_user_registration GET    /users/sign_up(.:format)            devise/registrations#new
  edit_user_registration GET    /users/edit(.:format)               devise/registrations#edit
       user_registration PATCH  /users(.:format)                    devise/registrations#update
                         PUT    /users(.:format)                    devise/registrations#update
                         DELETE /users(.:format)                    devise/registrations#destroy
                         POST   /users(.:format)                    devise/registrations#create
```
z.B wenn wir auf folgendes URL gehen http://localhost:4000/users/sign_in soltten wir einen Form sehen:
![image](https://user-images.githubusercontent.com/17837758/112711057-c7fed400-8ec5-11eb-9289-653550f6d13b.png)


[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)  

##### RubyGem
**RubyGems** ist ein Framework für die Installation und Paketierung von Ruby-Bibliotheken und -Anwendungen.  
**gem** - Ein Paket (Datei), das eine Bibliothek oder Anwendung enthält. Sie hat ein standardisiertes Aussehen und befindet sich in einem Repository im Netzwerk.  
**gem command tool** - RubyGems bietet ein "gem"-Hilfsprogramm, um gem-Pakete von der Kommandozeile aus zu manipulieren. Es ist in Ruby integriert und erlaubt den Zugriff auf installierte Gems als Bibliotheken.
---
Ruby on Rails hat den **Gemfile** welches eine Liste von Paketen speichert, die man für sein Projekt installieren möchte, mit zusätzlichen Informationen darüber, wo sie zu finden sind und welche Version zu verwenden ist. Wenn keine **Gemfile.lock** vorhanden ist, verwendet Bundler die Informationen aus der Gemfile und findet Pakete und Versionen, die installiert werden können, um alle Abhängigkeiten zu erfüllen. Gemfile.lock wird dann generiert, um die Pakete und ihre Versionen zu speichern, die von Bundle Install verwendet werden (nachdem die Abhängigkeiten aufgelöst wurden). Wenn jemand bundle install erneut aufruft, prüft Bundler, ob Gemfile.lock aktualisiert ist, und wenn ja, verwendet Bundler die Versionen aus Gemfile.lock, um Gems zu installieren.  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)  

##### Bootstrap 4 und jQuery installieren
**Bootstrap** - ist eine offene Schnittstellenplattform für die schnelle und einfache Website-Entwicklung. Bootstrap enthält HTML- und CSS-basierte Designvorlagen für Typografie, Formulare, Schaltflächen, Tabellen, Navigation, Modals, Karussellbilder und vieles mehr sowie zusätzliche JavaScript-Plugins. Bootstrap gibt auch die Möglichkeit, auf einfache Weise adaptive Designs zu erstellen
**jQuery** - ist eine leichtgewichtige, "weniger schreiben, mehr tun" JavaScript-Bibliothek. Der Zweck von jQuery ist es, die Verwendung von JavaScript auf der Website wesentlich zu vereinfachen. jQuery nimmt viele gängige Aufgaben, die viele Zeilen JavaScript-Code zur Ausführung erfordern, und verpackt sie in Methoden, die mit einer einzigen Zeile Code aufgerufen werden können. jQuery vereinfacht auch viele komplexe Dinge von JavaScript, wie AJAX-Aufrufe und DOM-Manipulation.
---
Für den Installation von Bootstrap und jQuery werden wir den Packetenmanager `yarn` verwenden.
>`yarn` ist ein alternativer npm-Client, der als JavaScript-Paketmanager dient und von Facebook, Google, Exponent und Tilde mitentwickelt wurde. Dieser Paketmanager beschleunigt die Paketerstellung und macht sie sicherer.

Das Installation wird mit folgenden Befehl gemacht:
```
yarn add bootstrap jquery popper.js
```
> `popper.js` benötigt Bootstrap für einige interaktive Bootstrap JS-Komponenten.  

Wir müssen nun den [Webpack](#webpack) konfigurieren:
```
// config/webpack/environment.js
const { environment } = require('@rails/webpacker') 
const webpack = require('webpack') 
environment.plugins.append('Provide', 
    new webpack.ProvidePlugin({ 
        $: 'jquery/src/jquery', 
        jQuery: 'jquery/src/jquery', 
        Popper: ['popper.js', 'default']
    })
)
```
Und den Bootstrap in `app/javascript/packs/application.js` importieren:
```
import "bootstrap";
```
Da wir in unserem Projekt [SCSS](#scss) anstelle von CSS verwenden möchten, müssen wir die Datei `application.css` in das Format `*.scss` umbenennen. Und in die umbenannte Datei die Bootsrtap importieren.
```
// app/assets/stylesheets/application.scss
@import "bootstrap/scss/bootstrap";
```  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)  

##### SCSS
SCSS ist ein CSS-Präprozessor, dessen Hauptzweck es ist, die Möglichkeiten zum Schreiben von CSS-Code zu verbessern. Der SCSS-Präprozessor beschleunigt das Schreiben von CSS-Code und macht ihn um ein Vielfaches einfacher zu pflegen. SCSS ist eine programmiersprachenähnliche Sprache, die die CSS-Entwicklung erleichtert und beschleunigt. SCSS ist eine kompilierbare Sprache und wird vom Browser in seiner reinen Form nicht verarbeitet. Die Syntax ist vollständig kompatibel mit CSS, so dass es nicht nötig ist, sie separat zu lernen, es ist einfach CSS mit Zusätzen.  
Die Verwendung von SCSS bietet eine Reihe von Vorteilen, die viel Zeit und Mühe sparen.
- SCSS gibt die Möglichkeit, Variablen zuzuweisen.
- SCSS erlaubt das Verschachteln von CSS-Regeln ineinander.
- Verwenden von Add-ons (imports)  

Es gibt jedoch auch die Nachteile, z.B:
- Wenn man CSS nicht sehr gut kennt, hilft der SCSS nicht weiter.
- Es wird ziemlich viel Zeit in Anspruch nehmen, alle Funktionen von SCSS zu erlernen.
- der eingebaute HTML-Element-Inspektor des Browsers hilft nicht, wenn man SCSS verwendet.  

[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)  

##### Webpack  
In JavaScript geschriebene Anwendungen werden immer komplexer, so dass für das Zusammenstellen von Modulen zunehmend ein spezielles Werkzeug - ein Bundler - eingesetzt wird. Solche Werkzeuge ermöglichen es Entwicklern, alle für ein Projekt benötigten Ressourcen zu paketieren, zu kompilieren und allgemein zu organisieren. Es können nicht nur Fremdbibliotheken, sondern auch eigene Dateien verwendet werden. Ein solches Baukastensystem ermöglicht eine bessere Organisation eines Projekts, da es in kleine Module aufgeteilt wird.

>`webpack` ist ein statischer Modul-Bundler für moderne JavaScript-Anwendungen. Wenn `webpack` die Anwendung verarbeitet, baut es intern einen Abhängigkeitsgraphen auf, der jedes Modul, dass das Projekt benötigt, abbildet und ein oder mehrere Bundles erzeugt.

Webpack ist derzeit einer der leistungsstärksten solchen Bundler, also Modular Builder. Es ist Open-Source und erlaubt die Lösung einer Vielzahl von Aufgaben. Wie andere Entwickler-Tools hat auch Webpack seine Vor- und Nachteile.  
**Vorteile**: Es ist ideal für Single-Page-Anwendungen. Das Webpack kann auch eine erweiterte Codeaufteilung durchführen. Aufgrund dieser und anderer Vorteile ist es derzeit eines der beliebtesten JS-Entwicklungswerkzeuge.  
**Nachteile**: Es ist etwas schwierig herauszufinden, wie es funktioniert, ein Teil der Dokumentation ist aufgrund der vielen Änderungen bei Updates veraltet.  
[Zurück zum Inhaltsverzeichnis](#inhaltsverzeichnis)  























