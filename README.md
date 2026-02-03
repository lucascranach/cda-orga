# CDA Intern

## JSON-Endpunkte für Posts und News

Dieses Jekyll-Projekt stellt die Inhalte aus `_posts` und `_news` zusätzlich als JSON bereit. Die folgenden Endpunkte werden beim Build generiert:

- `posts.json` – Alle Blog-Posts aus `_posts`
- `news.json` – Alle News-Einträge aus `_news`
- `content.json` – Kombinierte Ausgabe mit den beiden Arrays `posts` und `news`

Wichtig: Der in `_config.yml` gesetzte `baseurl` ist `/intern/blog`. Beim Hosten unter dieser Basis-URL sind die Endpunkte daher unter folgenden Pfaden erreichbar:

- `/intern/blog/posts.json`
- `/intern/blog/news.json`
- `/intern/blog/content.json`

### Felder

Jedes Objekt enthält – soweit vorhanden – folgende Felder:

- `type`: "post" oder "news"
- `id`: interne Kennung (Pfad oder Post-ID)
- `title`: Titel
- `subtitle`: Untertitel (falls gesetzt)
- `date`: ISO-8601-Datum für Posts; bei News aus dem Dateinamen (YYYY-MM-DD) abgeleitet
- `url`: Link zur Seite (bei News derzeit `null`, da die Collection nicht als einzelne Seiten ausgegeben wird)
- `categories`/`tags`: nur bei Posts, falls genutzt
- `excerpt`: Kurzfassung ohne HTML
- `content`: Vollständiger HTML-Inhalt

Hinweis: Die Collection `_news` ist in `_config.yml` mit `output: false` konfiguriert. Dadurch erhalten News-Einträge keine eigene HTML-Seite und das Feld `url` bleibt `null`. Falls gewünscht, kann `output: true` gesetzt werden, um pro News-Eintrag auch eine Seite sowie eine `url` zu erhalten.

### Nutzung extern (CORS)

Die Endpunkte sind statische `.json`-Dateien. Abhängig vom Host (z. B. GitHub Pages oder eigener Server) werden geeignete CORS-Header meist automatisch geliefert. Falls ein externer Client per Browser-Fetch blockiert wird, muss serverseitig `Access-Control-Allow-Origin` konfiguriert oder ein kleiner Proxy genutzt werden.

