# 🗂️ Express-Aufgabenverwaltung

## 📝 Aufgabe

In dieser Aufgabe entwickeln Sie eine Express-Anwendung zur Verwaltung von Aufgaben (Tasks). Die Anwendung implementiert eine einfache REST-basierend API zuvor mit transienter und in weiterer Folge mit persistenter Datenhaltung. Bitte führen Sie nach jeder abgeschlossenen Teilaufgabe einen Commit durch, um Ihre Arbeitsfortschritte nachvollziehbar zu dokumentieren.

---

## 📦 Hinweise

- Jede Aufgabe sollte eine eindeutige ID enthalten (z. B. via Zähler oder `uuid`).
- Nutzen Sie `express.json()` zum Parsen eingehender JSON-Daten.
- Achten Sie auf sinnvolle Statuscodes, Fehlerbehandlung und konsistente API-Rückgaben.
- Verwenden Sie zum Speichern und Laden von Dateien das Node.js-`fs`-Modul oder `fs/promises`.

---

## 🧪 Testhinweise

Sie können Ihre API mit Tools wie [Postman](https://www.postman.com/) oder direkt in VS Code mit der Erweiterung [Rest Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) testen:

## 📬 Abgabe

Bitte stellen Sie sicher, dass Ihr Repository Folgendes enthält:

- Nachvollziehbare Commits nach jedem Arbeitsschritt bzw. Arbeitsaufgabe
- Kommentieren Sie Ihre Entscheidungen. Beispielsweise, warum Sie bestimmte Validierungen gewählt haben, welche Methode Sie verwenden, um IDs zu generieren, oder wie Sie die Persistenz implementiert haben.
- Eine lauffähige Express-Anwendung, welche mit Befehl `npm start` gestartet werden kann
- Die Datei `package.json` mit allen Abhängigkeiten und `.gitignore`, um das `node_modules`-Verzeichnis auszuschließen
- Die geforderte Ordnerstruktur und Anforderungen erfüllt
- Die Datei `tasks.json` mit gespeicherten Aufgaben


## 🔧 Anforderungen

### ✅ 1. GET `/tasks`

- Implementieren Sie eine Route `/tasks`, die eine **Liste von Aufgaben** als JSON zurückgibt.
- Die Aufgaben bestehen aus:
  - `id` (eindeutig)
  - `title`
  - `description`
  - `dueDate`
  - `done` (Boolean)
- Die Liste soll zunächst **transient** (nicht persistent) sein.

📌 **Commit:** `feat: add GET /tasks route with in-memory task list`

---

### ✅ 2. POST `/tasks`

- Fügen Sie eine POST-Route `/tasks` hinzu.
- Erwartet mindestens:
  - `title`
  - `dueDate`
- Falls `description` nicht angegeben ist, soll diese leer bleiben.
- Falls `done` nicht angegeben ist, dann verwenden Sie den Standardwert `false`.
- Bedenken Sie eine eindeutige ID für jede Aufgabe zu generieren.
- Validieren Sie die Eingabedaten:
  - **400 – Bad Request**, wenn Felder fehlen oder die Eingabedaten (z.B. kein Titel angegeben, kein gültiges in der Zukunft liegendes Datum) ungültig sind.
  - **409 – Conflict**, wenn z. B. eine Aufgabe mit gleichem Titel bereits existiert.
- Neue Aufgaben werden zur bestehenden Liste hinzugefügt.

📌 **Commit:** `feat: add POST /tasks with validation and error handling`

---

### ✅ 3. Persistenz (tasks.json)

- Speichern Sie die Aufgabenliste in einer Datei `tasks.json`.
- Beim Start der Anwendung sollen die Aufgaben aus der Datei geladen werden.
- Änderungen an der Liste (z. B. durch POST) müssen in die Datei geschrieben werden.

📌 **Commit:** `feat: implement persistent storage in tasks.json`

---

### ✅ 4. GET `/tasks/:id`

- Gibt die Aufgabe mit der angegebenen ID zurück.
- Fehlerbehandlung:
  - **404 – Not Found**, wenn Aufgabe nicht existiert.

📌 **Commit:** `feat: implement GET /tasks/:id`

---

### ✅ 5. DELETE `/tasks/:id`

- Löschen Sie die Aufgabe mit der angegebenen ID.
- Fehlerbehandlung bei nicht vorhandener ID.

📌 **Commit:** `feat: implement DELETE /tasks/:id`

---

## 🧩 Erweiterte Aufgaben (zur Vertiefung ohne Bepunktung)

### ✅ 6. PUT `/tasks/:id`

- Ersetzen Sie eine vollständige Aufgabe mit der angegebenen ID.
- Auch hier gilt: `title` und `dueDate` **müssen gesetzt** sein.
- Fehlerbehandlung:
  - **400 – Bad Request**, wenn Felder fehlen.
  - **404 – Not Found**, wenn keine Aufgabe mit der ID existiert.

📌 **Commit:** `feat: add PUT /tasks/:id for full task replacement`

---

### ✅ 7. PATCH `/tasks/:id`

- Markieren Sie eine Aufgabe als erledigt (`done = true`).
- Nur Teilaktualisierung – kein vollständiges Objekt notwendig.

📌 **Commit:** `feat: add PATCH /tasks/:id to mark as done`
