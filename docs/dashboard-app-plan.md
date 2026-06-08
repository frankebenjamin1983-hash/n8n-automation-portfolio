# Agentur-Dashboard Android App – Plan

## Aktuelles Dashboard
- `EvelastAgenticcoding/dashboard.py` – Python-HTTP-Server, HTML/CSS, Auto-Refresh
- Zeigt: Server-Status (UpCloud), n8n/Ollama/Docker, 12 Agenten, Budget, Aktivitäten
- Läuft auf Port 8765 (lokal/Windows)

## Ziel
Dashboard als **Android App** realisieren, ggf. mit Google AI Studio (Gemini).

## Architektur-Vorschlag

### Phase 1: API-Refactoring (Backend)
**Wer:** Jason Lindt
- Dashboard.py in API + Frontend trennen
- REST-API-Endpunkte für: Serverstatus, Agenten, Aktivitäten, Budget
- Flask/FastAPI auf UpCloud (oder bestehenden n8n-Server nutzen)
- JSON-Output statt HTML

### Phase 2: Flutter App (Android)
**Wer:** Tim Spiegelhalter + Dr. Frank Fleck
- Flutter (Google's Cross-Platform-Framework)
- Verbindet zur REST-API
- Features: Live-Status, Push-Benachrichtigungen, Agenten-Übersicht
- Gemini-Integration für: Smart Analytics, Aktivitäten-Zusammenfassung

### Phase 3: PWA als Zwischenschritt
**Wer:** Tim Spiegelhalter
- Bestehendes HTML-Dashboard als PWA wrappen
- Service Worker für Offline-Fähigkeit
- Manifest für "Zum Homescreen hinzufügen"
- Schnellster Weg zur Android-Nutzung

## Beteiligte Agenten

| Agent | Aufgabe | Priorität |
|-------|---------|-----------|
| **Dr. Frank Fleck** | Architektur-Review + Flutter-Plan | 🔴 Hoch |
| **Tim Spiegelhalter** | Dashboard verbessern + PWA/Flutter | 🔴 Hoch |
| **Jason Lindt** | REST-API für Dashboard-Daten | 🟡 Mittel |
| **Mara Zweig** | Marketing-Materialien finalisieren | 🟢 Bereit |
| **Chelsea Painter** | LinkedIn-Content post-bereit machen | 🟢 Bereit |
