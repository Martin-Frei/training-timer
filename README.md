# 🏋️ Training Timer

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![PWA](https://img.shields.io/badge/PWA-5A0FC8?logo=pwa&logoColor=white)
[![Live Demo](https://img.shields.io/badge/demo-live-success)](https://martin-frei.github.io/training-timer/)

> **Ein konfigurierbarer Timer für Intervall-Training mit Musik-Unterstützung.**

## 🚀 Live Demo

**[Timer öffnen](https://martin-frei.github.io/training-timer/)**

## 📋 Features

- **Konfigurierbare Einstellungen**: Alle Zeiten und Wiederholungen frei einstellbar
- **Musik-Integration**: MP3, WAV, M4A und OGG Dateien unterstützt
- **Automatische Lautstärke-Anpassung**: Musik wird während Pausen leiser
- **Visuelle Anzeige**: Klare Unterscheidung zwischen Training und Pause
- **Tastatur-Shortcuts**: Schnelle Bedienung per Tastatur
- **Responsive Design**: Funktioniert auf Desktop und Mobile

## 🎯 Verwendung

### 1. Setup
1. Alle Dateien in einem Ordner ablegen
2. `index.html` in einem Webbrowser öffnen
3. MP3-Datei auswählen

### 2. Konfiguration
- Klick auf "⚙️ Einstellungen" zum Anpassen der Parameter
- Alle Einstellungen werden automatisch beim Training-Start übernommen

### 3. Training starten
- "Start Training" klicken
- Timer beginnt mit konfigurierbarem Countdown
- Musik startet automatisch bei Trainingsbeginn

## ⚙️ Einstellungen

| Parameter | Beschreibung | Bereich |
|-----------|-------------|---------|
| Countdown Start | Vorbereitungszeit in Sekunden | 1-60 |
| Anzahl Blöcke | Anzahl der Trainingsblöcke | 1-10 |
| Runden pro Block | Runden in jedem Block | 1-10 |
| Trainingszeit | Dauer jeder Trainingsphase | 10-300 |
| Kurze Pause | Pause zwischen Runden | 5-120 |
| Lange Pause | Pause zwischen Blöcken | 10-300 |

## ⌨️ Tastatur-Shortcuts

- **Leertaste**: Training starten/pausieren
- **Escape**: Training stoppen
- **S**: Einstellungen ein-/ausblenden

## 📁 Datei-Struktur

```
training-timer/
├── index.html          # Haupt-HTML-Datei
├── style.css           # Styling und Layout
├── settings.js         # Einstellungen-Management
├── timer.js            # Timer-Logik
├── app.js              # Hauptfunktionen und Event-Handler
├── manifest.json       # Web-App-Manifest (PWA)
├── icon/               # Favicons und App-Icons
├── docs/LOGIC.md       # Ausführliche Logik-Dokumentation
└── README.md           # Diese Datei
```

Die Timer-Logik ist Schritt für Schritt in [docs/LOGIC.md](docs/LOGIC.md) beschrieben.

## 🔧 Technische Details

### JavaScript-Module

**settings.js**
- Verwaltet alle konfigurierbaren Parameter
- Validierung der Eingaben
- Event-Listener für Einstellungsänderungen

**timer.js**
- Kern-Timer-Logik
- Phasen-Management (Countdown, Training, Pause)
- Display-Updates

**app.js**
- Hauptfunktionen (Start, Pause, Stop)
- Musik-Management
- Tastatur-Shortcuts
- Fehlerbehandlung

### CSS-Features
- Glasmorphismus-Design
- Animationen und Übergänge
- Responsive Layout
- Gradient-Hintergrund

## 🎵 Unterstützte Audio-Formate

- MP3 (empfohlen)
- WAV
- M4A
- OGG

## 📱 Browser-Kompatibilität

- Chrome 60+
- Firefox 55+
- Safari 11+
- Edge 79+

## 🚀 Erweiterungsmöglichkeiten

- **Service Worker**: Offline-Funktionalität
- **Statistiken**: Training-Sessions speichern
- **Benachrichtigungen**: Browser-Notifications
- **Themes**: Verschiedene Farbschemas
- **Presets**: Vordefinierte Training-Programme

## 🐛 Bekannte Probleme

- Auf iOS Safari kann Autoplay blockiert werden
- Sehr große Audio-Dateien können Performance beeinträchtigen

## 📝 Änderungsprotokoll

### Version 1.1
- Vollständige Modularisierung in separate JS-Dateien
- Erweiterte Einstellungsmöglichkeiten
- Tastatur-Shortcuts hinzugefügt
- Responsive Design verbessert
- Konfigurierbare Timer

## 🤝 Beitragen

Verbesserungen und Erweiterungen sind willkommen! Bitte:

1. Fork erstellen
2. Feature-Branch erstellen
3. Änderungen committen
4. Pull Request erstellen

## 📃 Lizenz

Dieses Projekt ist **frei nutzbar für Lern- und Demonstrationszwecke**. Kommerzielle Nutzung nach Rücksprache.

---

## 👤 Autor

Martin Freimuth  
📧 mat.frei@gmx.de  
📍 83135 Schechen  
📆 Erstellt: Juni 2025 