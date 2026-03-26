# Micha Spesen Web-App

Das Paket ist so vorbereitet, dass Micha dieselben Daten auf Handy und PC sehen kann.

## Was schon drin ist
- Anmeldung per E-Mail + Passwort
- Synchronisierte Fahrten über Firebase
- Bearbeiten und Löschen
- Monatsübersicht, Summe, CSV, PDF
- Web-App mit Icon über "Zum Startbildschirm hinzufügen"

## Was du jetzt machen musst

### 1) Firebase-Projekt anlegen
1. In der Firebase Console ein neues Projekt anlegen.
2. In **Build → Authentication** die Anmeldung **E-Mail/Passwort** aktivieren.
3. In **Build → Firestore Database** eine Datenbank anlegen.
   - zum Start ruhig **Test Mode**
4. In **Projekteinstellungen → Allgemein** eine **Web-App** registrieren.
5. Die Firebase-Konfigurationswerte kopieren.

### 2) Firebase-Werte eintragen
In `index.html` diesen Block ausfüllen:

```js
const firebaseConfig = {
  apiKey: "HIER_API_KEY",
  authDomain: "HIER_AUTH_DOMAIN",
  projectId: "HIER_PROJECT_ID",
  storageBucket: "HIER_STORAGE_BUCKET",
  messagingSenderId: "HIER_MESSAGING_SENDER_ID",
  appId: "HIER_APP_ID"
};
```

### 3) Auf GitHub Pages hochladen
1. Neues GitHub-Repository anlegen
2. Diese Dateien hochladen
3. In GitHub: **Settings → Pages**
4. Source auf **Deploy from a branch**
5. Branch: **main** / Root
6. Danach entsteht ein Link wie:
   `https://DEINNAME.github.io/REPO-NAME/`

### 4) Micha benutzen lassen
- Auf Handy Link öffnen
- Registrieren
- App auf Startbildschirm legen
- Mit denselben Zugangsdaten am PC anmelden

## Spätere Sicherheit
Nach dem Test sollte Firestore nicht dauerhaft im Testmodus bleiben.
Dann Regeln so umstellen, dass jeder nur seine eigenen Daten lesen und schreiben darf.

Beispiel-Regeln:

```txt
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/trips/{tripId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

## Wichtig
Ohne eingetragene Firebase-Daten synchronisiert die App nicht.
