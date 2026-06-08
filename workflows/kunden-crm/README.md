# Kunden-CRM light

## Problem
Kundendaten liegen in Excel-Tabellen, Rechnungsverfolgung ist manuell, kein System für Wiedervorlage.

## Lösung
n8n-Workflow mit Google Sheets als Daten-Backend:
1. Neukunden-Erfassung (manuell oder per Webformular)
2. Automatische Rechnungserstellung + Versand
3. Fälligkeits-Erinnerung nach 14/30/60 Tagen
4. Mahnstufen bei Nichtzahlung (freundlich → deutlich → letzte Mahnung)
5. Monatliche Kunden-Zusammenfassung als PDF

## Ergebnis
- 📈 100 €/Monat weniger Ausfallrisiko
- 🕊️ Keine manuellen Mahnungen mehr
- 📊 Jederzeit aktueller Überblick über offene Posten

## Technologie
- n8n (Schedule + E-Mail-Trigger)
- Google Sheets (Datenhaltung)
- PDF-Generator (Angebot/Rechnung)
- E-Mail (Sendgrid/Gmail)

## Status
🚧 In Entwicklung
