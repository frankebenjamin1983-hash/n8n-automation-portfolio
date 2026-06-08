# Dashboard Android App – Architektur-Plan

## Status Quo

Aktuelles Dashboard: `EvelastAgenticcoding/dashboard.py`
- Python-HTTP-Server (Standardbibliothek, keine Dependencies)
- Port 8765, läuft lokal auf Windows
- Daten via SSH auf UpCloud-Server (85.9.202.196)
- HTML/CSS mit Inline-Styling, Dark Theme
- Auto-Refresh alle 30s (Meta-Refresh)
- Zeigt: Serverstatus, n8n, Ollama, Docker, 12 Agenten, Budget, Aktivitäten

**Probleme:**
- Keine API-Trennung (HTML + Daten gemischt)
- Keine mobile Optimierung (nur Media-Query-Breakpoint)
- Keine Push-Benachrichtigungen
- Keine Authentifizierung
- Datenpolling via SSH, kein Event-System

---

## Phase 1: PWA (Progressive Web App) – SOFORT

**Aufwand:** 1 Stunde
**Wirkung:** Dashboard auf Android via "Zum Homescreen hinzufügen"

### Änderungen an dashboard.py
1. **Service Worker** (`sw.js`) – cached HTML + Daten für Offline
2. **Manifest** (`manifest.json`) – App-Name, Icons, Theme-Color
3. **HTTPS-Tunnel** – via Cloudflare Tunnel oder ngrok (für Service Worker nötig)
4. **Mobile UI** – Touch-freundliche Buttons, swipe-freundliche Karten
5. **Meta-Tags** – Apple/Android-spezifische Meta-Tags

### Vorteile PWA
- ✅ Läuft in 30 Minuten
- ✅ Kein App-Store nötig
- ✅ Automatische Updates
- ✅ Offline-Fallback
- ✅ Push-Benachrichtigungen möglich

---

## Phase 2: REST-API (FastAPI/Flask) – IN 1-2 TAGEN

**Ziel:** Daten von Darstellung trennen, API auf UpCloud hosten

### API-Endpunkte

| Endpunkt | Methode | Beschreibung | Response |
|----------|---------|-------------|----------|
| `GET /api/v1/status` | GET | Server-Health | `{ssh, n8n, ollama, docker, uptime}` |
| `GET /api/v1/agents` | GET | Agenten-Team | `[{name, role, status, model}]` |
| `GET /api/v1/activities` | GET | Letzte Aktivitäten | `[{timestamp, text}]` |
| `GET /api/v1/budget` | GET | Budget-Status | `{today, remaining, total}` |
| `GET /api/v1/metrics` | GET | Dashboard-Metriken | aggregierte Daten |
| `POST /api/v1/agents/:id/task` | POST | Task an Agent senden | `{status}` |

### API-Hosting
- **Option A:** FastAPI auf UpCloud (neben n8n/Ollama, neuer Port)
- **Option B:** Bestehenden n8n-Webhook nutzen (kein neuer Service)
- **Empfehlung:** Option A (FastAPI, eigener Docker-Container)

### Authentifizierung
- Einfacher API-Key (statisch, für Startphase)
- Später: JWT mit Login

---

## Phase 3: Flutter-App (Google-Stack) – IN 1-2 WOCHEN

**Warum Flutter:**
- ✅ Cross-Platform (Android + iOS in einem Code)
- ✅ Von Google – enge Gemini-Integration
- ✅ Hot Reload für schnelle Entwicklung
- ✅ Material Design 3 (modernes Android-UI)
- ✅ Große Community + Package-Ökosphäre

### Flutter-App-Struktur

```
dashboard_app/
├── lib/
│   ├── main.dart                    # App-Start + Routing
│   ├── models/                      # Datenmodelle
│   │   ├── server_status.dart
│   │   ├── agent.dart
│   │   └── activity.dart
│   ├── services/                    # API-Services
│   │   ├── api_service.dart         # REST-Client
│   │   └── gemini_service.dart      # KI-Analyse
│   ├── providers/                   # State-Management
│   │   ├── dashboard_provider.dart
│   │   └── agent_provider.dart
│   ├── screens/                     # Bildschirme
│   │   ├── dashboard_screen.dart
│   │   ├── agent_detail_screen.dart
│   │   └── settings_screen.dart
│   └── widgets/                     # Wiederverwendbare Widgets
│       ├── status_card.dart
│       ├── agent_tile.dart
│       └── activity_feed.dart
├── pubspec.yaml
└── assets/
    └── icons/
```

### Gemini-Integration (Google AI Studio)

**Anwendungsfälle für Gemini im Dashboard:**

1. **Smart Analytics** – "Wie war die Server-Auslastung diese Woche?"
   → Gemini analysiert historische Daten → natürliche Zusammenfassung

2. **Aktivitäten-Zusammenfassung** – "Was ist heute passiert?"
   → Gemini fasst Activity-Log in 2-3 Sätzen zusammen

3. **Predictive Insights** – "Ollama zeigt Muster?"
   → Gemini erkennt Anomalien im Server-Verhalten

4. **Agent-Task-Assistent** – "Welcher Agent ist frei für Aufgabe X?"
   → Gemini matched Task mit verfügbaren Agenten

### Architektur (C4-Diagramm, Textform)

```
┌─────────────┐     SSH      ┌──────────────┐
│  UpCloud    │◄────────────►│  FastAPI      │
│  Server     │              │  (Container)  │
│  ┌───────┐  │              │  Port 8000    │
│  │n8n    │  │              └──────┬───────┘
│  │Ollama │  │                     │
│  │Docker │  │                     │ HTTP/JSON
│  └───────┘  │                     │
└─────────────┘              ┌──────▼───────┐
                             │  Flutter App  │
                             │  (Android)    │
                             │  ┌─────────┐  │
                             │  │ Gemini  │  │
                             │  │ (AI)   │  │
                             │  └─────────┘  │
                             └───────────────┘
```

---

## Empfohlene Roadmap

| Phase | Was | Wer | Dauer | Priorität |
|-------|-----|-----|-------|-----------|
| **1** | Dashboard PWA-fähig machen | Tim | ⏱️ 1 Std. | 🔴 SOFORT |
| **2** | FastAPI-Backend auf UpCloud | Jason | 🕐 1 Tag | 🟡 NÄCHSTE WOCHE |
| **3** | Flutter-App bauen | Frank + Tim | 🕐 1-2 Wochen | 🟢 NACH MVP |
| **4** | Gemini-Integration | Frank | 🕐 3-5 Tage | 🟢 OPTIONAL |

---

## Nächste Schritte (heute)

1. ✅ `sw.js` + `manifest.json` für aktuelles Dashboard
2. ✅ Dashboard-HTTPS via Cloudflare Tunnel oder lokalen Reverse-Proxy
3. ✅ API-Entwurf in neuer `api_dashboard.py`
4. 🔲 Flutter-Projekt initialisieren (`flutter create`)
