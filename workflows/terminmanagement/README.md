# Terminmanagement mit KI

## Problem
Kundenanfragen kommen über WhatsApp, E-Mail und Telefon – Termine gehen verloren, Doppelbuchungen passieren.

## Lösung
Zentraler n8n-Workflow:
1. Multi-Channel-Inbox (WhatsApp, E-Mail, Webformular)
2. KI-Vorsortierung (Dringlichkeit, Kategorie, Kunde)
3. Automatische Kalender-Prüfung und Terminvorschlag
4. Bestätigungs-E-Mail + Kalender-Einladung
5. Erinnerung 24h vor Termin

## Ergebnis
- ❌ Keine verpassten Termine
- 🔄 Einheitlicher Kundenkommunikations-Flow
- ⏱️ 3–4 Std./Woche weniger Koordinationsaufwand

## Technologie
- n8n (Webhook + Schedule-Trigger)
- WhatsApp Business API (oder alternativ: E-Mail-zu-SMS)
- Google Calendar API
- Ollama/KI für Anfragen-Klassifizierung

## Status
📝 In Planung
