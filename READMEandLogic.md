# Training Timer App - README und Logik-Dokumentation

## Übersicht

Diese Web-App ist ein vollständig funktionsfähiger Trainings-Timer, der speziell für Intervalltraining entwickelt wurde. Die App unterstützt mehrere Trainingsblöcke mit konfigurierbaren Runden, Pausen und Musik-Wiedergabe.

## Dateistruktur

```
training-timer/
├── index.html          # Haupt-HTML-Datei
├── styles.css          # Styling und Animationen
├── settings.js         # Einstellungsmanagement
├── timer.js            # Timer-Logik und Phasen-Management
├── app.js              # Hauptfunktionen und Event-Handler
└── README.md           # Diese Dokumentation
```

## JavaScript-Module im Detail

### 1. settings.js - Einstellungsmanagement

**Zweck**: Verwaltet alle konfigurierbaren Parameter des Trainings-Timers.

#### Kernfunktionen:

- **`settings`-Objekt**: Zentrale Konfiguration mit Standardwerten
  - `countdownTime`: Vorbereitungszeit (10s)
  - `totalSets`: Anzahl Trainingsblöcke (3)
  - `roundsPerSet`: Runden pro Block (3)
  - `trainingTime`: Aktive Trainingszeit (45s)
  - `shortBreakTime`: Kurze Pause zwischen Runden (15s)
  - `longBreakTime`: Lange Pause zwischen Blöcken (60s)

- **`loadSettings()`**: Lädt Werte aus HTML-Inputs in das settings-Objekt
- **`validateSettings()`**: Überprüft Eingaben auf Gültigkeit (Min/Max-Werte)
- **`toggleSettings()`**: Blendet Einstellungspanel ein/aus
- **`initializeSettingsListeners()`**: Registriert Event-Listener für Live-Updates

#### Besonderheiten:
- Automatische Validierung verhindert ungültige Eingaben
- Responsive Updates bei Änderungen
- Benutzerfreundliche Fehlermeldungen

### 2. timer.js - Timer-Logik und Phasen-Management

**Zweck**: Verwaltet den Trainingsablauf und die verschiedenen Phasen.

#### Globale Variablen:
```javascript
let isRunning = false;          // Timer aktiv?
let isPaused = false;           // Timer pausiert?
let currentTimer = null;        // Referenz auf setInterval
let currentRound = 1;           // Aktuelle Runde
let currentSet = 1;             // Aktueller Block
let timeLeft = 45;              // Verbleibende Zeit
let isTrainingPhase = true;     // Trainings- oder Pausenphase?
let isCountdownPhase = false;   // Countdown-Phase?
```

#### Kernfunktionen:

- **`updateDisplay()`**: Aktualisiert UI-Elemente basierend auf aktuellem Status
  - Zeigt formatierte Zeit an
  - Wechselt Status-Emojis und Farben
  - Passt Lautstärke der Musik an (0.7 für Training, 0.2 für Pause)

- **`startTimer()`**: Startet den 1-Sekunden-Interval
  - Dekrementiert `timeLeft`
  - Ruft `updateDisplay()` auf
  - Wechselt zu `nextPhase()` bei Zeitablauf

- **`nextPhase()`**: Komplexe Logik für Phasenwechsel
  - Training → Pause (kurz/lang je nach Runde)
  - Pause → Training (nächste Runde oder Block)
  - Erkennt Trainingsende automatisch

- **`completeTraining()`**: Beendet das Training ordnungsgemäß
- **`resetTimer()`**: Setzt alle Variablen zurück

#### Phasen-Logik:
1. **Countdown-Phase**: Vorbereitung vor erstem Training
2. **Training-Phase**: Aktives Training mit Musik
3. **Pause-Phase**: Kurze Pause (zwischen Runden) oder lange Pause (zwischen Blöcken)

### 3. app.js - Hauptfunktionen und Event-Handler

**Zweck**: Verbindet UI mit Timer-Logik und verwaltet Audio-Funktionalität.

#### Kernfunktionen:

- **Musik-Datei laden**:
  ```javascript
  musicFile.addEventListener('change', function(e) {
      const file = e.target.files[0];
      if (file) {
          const url = URL.createObjectURL(file);
          audioPlayer.src = url;
          audioPlayer.volume = 0.7;
          // Dateityp-Validierung
      }
  });
  ```

- **`startTraining()`**: Hauptfunktion zum Starten
  - Validiert Einstellungen
  - Initialisiert Timer-Variablen
  - Startet Countdown-Phase
  - Aktiviert/deaktiviert Buttons

- **`pauseTraining()`**: Pausiert/Fortsetzt Training
  - Stoppt/startet Timer
  - Pausiert/spielt Musik
  - Wechselt Button-Text

- **`stopTraining()`**: Beendet Training komplett
  - Stoppt Timer und Musik
  - Setzt alle Variablen zurück
  - Reaktiviert Start-Button

#### Keyboard-Shortcuts:
- **Leertaste**: Start/Pause Toggle
- **Escape**: Training stoppen
- **S**: Einstellungen toggle

#### Audio-Management:
- Automatisches Starten/Stoppen der Musik
- Lautstärke-Anpassung je nach Phase
- Fehlerbehandlung für nicht unterstützte Dateitypen
- Loop-Wiedergabe während Training

#### Zusätzliche Features:
- **Warnung vor Seitenverlassen** während aktivem Training
- **Service Worker** Unterstützung
- **Logging** für Training-Sessions
- **Benachrichtigungen** (erweiterbar)

## HTML-Besonderheiten

### Struktur:
```html
<div class="container">
    <h1>🏋️ Training Timer</h1>
    <button class="toggle-settings">⚙️ Einstellungen</button>
    
    <div class="settings hidden">
        <!-- Einstellungsfelder -->
    </div>
    
    <div class="file-input">
        <!-- Musik-Upload -->
    </div>
    
    <div class="status">Bereit zum Start</div>
    <div class="timer">00:00</div>
    <div class="progress">Wähle eine Musikdatei aus</div>
    <div class="volume-info">Lautstärke: Normal</div>
    
    <div class="controls">
        <!-- Start/Pause/Stop Buttons -->
    </div>
    
    <audio id="audioPlayer" loop></audio>
</div>
```

### Accessibility:
- Semantische HTML-Struktur
- Klare Labels für alle Inputs
- Keyboard-Navigation unterstützt

## CSS-Besonderheiten

### Design-Philosophie:
- **Glassmorphism**: Transparente Elemente mit Blur-Effekt
- **Gradient-Hintergrund**: Dynamischer Farbverlauf
- **Responsive Design**: Mobile-First Ansatz

### Animationen:
```css
@keyframes pulse {
    0% { transform: scale(1); }
    50% { transform: scale(1.05); }
    100% { transform: scale(1); }
}

.training {
    color: #4CAF50;
    animation: pulse 1s infinite;
}
```

### Besondere Klassen:
- `.training`: Grün + Pulsieren für aktives Training
- `.pause`: Orange für Pausen
- `.hidden`: Versteckt Einstellungen
- Responsive Breakpoints für mobile Geräte

### Button-Interaktionen:
- Hover-Effekte mit Transform und Box-Shadow
- Backdrop-Filter für Glaseffekt
- Disabled-State für nicht verfügbare Aktionen

## Trainings-Ablauf

1. **Initialisierung**: Einstellungen laden, Display aktualisieren
2. **Datei laden**: MP3/Audio-Datei auswählen
3. **Einstellungen**: Parameter anpassen (optional)
4. **Start**: 
   - Countdown-Phase (10s Standard)
   - Training-Phase (45s Standard mit Musik)
   - Pause-Phase (15s kurz / 60s lang)
5. **Wiederholung**: Automatischer Wechsel zwischen Phasen
6. **Abschluss**: Alle Blöcke abgeschlossen

## Technische Features

### Fehlerbehandlung:
- Audio-Fehler werden abgefangen
- Dateityp-Validierung
- Eingabe-Validierung für Einstellungen

### Performance:
- Effiziente DOM-Updates
- Memory-Management für Audio-URLs
- Optimierte Timer-Intervalle

### Erweiterbarkeit:
- Modulare Struktur
- Logging-System vorbereitet
- Service Worker ready
- LocalStorage kompatibel

## Browser-Kompatibilität

- **Modern Browsers**: Chrome, Firefox, Safari, Edge
- **Audio-Formate**: MP3, WAV, M4A, OGG
- **Features**: ES6+, CSS3, HTML5 Audio API

## Deployment

1. Alle Dateien in einen Webserver-Ordner kopieren
2. Keine Build-Schritte erforderlich
3. HTTPS empfohlen für Service Worker
4. Keine Backend-Abhängigkeiten

## Troubleshooting

### Häufige Probleme:
1. **Audio spielt nicht**: Dateityp prüfen, Browser-Autoplay-Policy
2. **Timer stoppt**: JavaScript-Fehler in Browser-Konsole prüfen
3. **Einstellungen werden nicht gespeichert**: LocalStorage deaktiviert?

### Debug-Tipps:
- Browser-Konsole für Fehlermeldungen
- Netzwerk-Tab für Audio-Loading
- Performance-Tab für Timer-Performance

## 📃 Lizenz

Dieses Projekt ist **frei nutzbar für Lern- und Demonstrationszwecke**. Kommerzielle Nutzung nach Rücksprache.

---

## 👤 Autor

Martin Freimuth  
📧 mat.frei@gmx.de  
📍 83135 Schechen  
📆 Erstellt: Juni 2025 