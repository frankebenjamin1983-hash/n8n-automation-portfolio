# Angebotserstellung automatisieren

## Problem
Ein Betrieb erhält 15+ Angebotsanfragen pro Woche per E-Mail.  
Bisher: Manuelles Copy & Paste aus Vorlagen → 30 Minuten pro Angebot → ~7,5 Std./Woche.

## Lösung
n8n-Workflow, der:
1. Eingehende E-Mails auf Angebotsanfragen prüft (KI-Klassifizierung)
2. Relevante Daten extrahiert (Kunde, Leistung, Menge, Ort)
3. PDF-Angebot aus Vorlage erstellt
4. Zur Freigabe an den Chef sendet
5. Nach Freigabe automatisch versendet und in CRM vermerkt

## Ergebnis
- ⏱️ **5 Stunden/Woche gespart**
- 📈 Angebote gehen 2× schneller raus
- ❌ Keine vergessenen Nachfassaktionen mehr

## Technologie
- n8n (E-Mail-Trigger + KI-Node + PDF-Generator)
- Ollama (lokale KI für Datenextraktion – datenschutzkonform)
- Google Sheets (einfaches CRM)
- Gmail/IMAP (E-Mail-Eingang)

## Status
🚧 In Entwicklung – Basis-Workflow ist konzipiert.
