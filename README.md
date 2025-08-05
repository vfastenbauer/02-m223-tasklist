# 🗂️ REST-basierender Service Verwaltung von Aufgaben

## 📝 Aufgabe

In dieser Aufgabe entwickeln Sie eine Express-Anwendung zur Verwaltung von Aufgaben (Tasks). Die Anwendung implementiert eine einfache REST-basierend API zuvor mit transienter Datenhaltung. Bitte führen Sie nach jeder abgeschlossenen Teilaufgabe einen Commit durch, um Ihre Arbeitsfortschritte nachvollziehbar zu dokumentieren.

## 📦 Hinweise

- Jede Aufgabe sollte eine eindeutige ID enthalten (z. B. via eigenem Zähler oder `uuid`).
- Nutzen Sie `express.json()` zum Parsen eingehender JSON-Daten.
- Achten Sie auf sinnvolle Statuscodes, Fehlerbehandlung und konsistente API-Rückgaben.

## 📬 Abgabe

Bitte stellen Sie sicher, dass Ihr Repository Folgendes enthält:

- Eine lauffähige Express-Anwendung, welche mit Befehl `npm start` gestartet werden kann --> sonst erhalten Sie keine Punkte.
- (1) Die Datei `package.json` mit allen Abhängigkeiten und `.gitignore`, um das `node_modules`-Verzeichnis auszuschließen
- (6) Nachvollziehbare Commits nach jedem Arbeitsschritt bzw. Arbeitsaufgabe
- (3) Dokumentieren Sie Ihre Arbeitsschritte fortlaufen, d.h. mit jedem Commit erweitert sich diese Datei, in einer `documentation.md`-Datei:
  - Beschreiben Sie, wie Sie die API entwickelt haben. Dazu zählen die Befehle, welche Sie in der Kommandozeile genutzt, welche Links oder Ressourcen Sie verwendet haben.
  - Erläutern Sie Ihre Entscheidungen und Implementierungsdetails. Beispielsweise, warum Sie bestimmte Validierungen gewählt haben, oder welche Methode Sie verwenden, um IDs zu generieren, oder wie Sie die Fehlerbehandlung umgesetzt haben.
  - Beschreiben Sie, wie Sie die API getestet haben. Geben Sie ggf. Testfiles in einem Ordner `tests` ab: Postman-Collections oder VS Code Rest Client Dateien.
  - Ergänzen Sie, welche Schritte notwendig sind, um die Anwendung zu installieren und zu starten (vgl. klassische Readme-Datei).

## 🧪 Testhinweise

Sie können Ihre API mit Tools wie [Postman](https://www.postman.com/) oder direkt in VS Code mit der Erweiterung [Rest Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) testen.

## 🔧 Anforderungen

### ✅ 1. GET `/tasks`

- Implementieren Sie eine Route `/tasks`, die eine **Liste von Aufgaben** als JSON zurückgibt.
- Die Aufgaben bestehen aus:
  - `id` (eindeutig)
  - `title`
  - `description`
  - `dueDate`
  - `done` (Boolean)
- Die Liste soll **transient** (nicht persistent) sein.

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

### ✅ 3. GET `/tasks/:id`

- Gibt die Aufgabe mit der angegebenen ID zurück.
- Fehlerbehandlung:
  - **404 – Not Found**, wenn Aufgabe nicht existiert.

📌 **Commit:** `feat: implement GET /tasks/:id`

---

### ✅ 4. DELETE `/tasks/:id`

- Löschen Sie die Aufgabe mit der angegebenen ID. Statuscode: **204 – No Content** bei erfolgreicher Löschung.
- Entsprechende Fehlerbehandlung bei nicht vorhandener ID.

📌 **Commit:** `feat: implement DELETE /tasks/:id`

---

### ✅ 5. PUT `/tasks/:id`

- Ersetzen Sie eine vollständige Aufgabe mit der angegebenen ID.
- Auch hier gilt: `title` und `dueDate` **müssen gesetzt** sein.
- Fehlerbehandlung:
  - **400 – Bad Request**, wenn Felder fehlen.
  - **404 – Not Found**, wenn keine Aufgabe mit der ID existiert.

📌 **Commit:** `feat: add PUT /tasks/:id for full task replacement`

---

### ✅ 6. PATCH `/tasks/:id`

- Markieren Sie eine Aufgabe als erledigt (`done = true`).
- Nur Teilaktualisierung – kein vollständiges Objekt notwendig.

📌 **Commit:** `feat: add PATCH /tasks/:id to mark as done`
