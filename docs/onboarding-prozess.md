# Onboarding-Prozess: Vom Erstgespräch zum laufenden Workflow

Dieses Dokument beschreibt den standardisierten Ablauf eines Kundenprojekts.

---

## Phase 0: Akquise & Erstkontakt

**Dauer:** 1–3 Tage
**Status:** 🟢 Beim Kunden

1. Kunde meldet sich (E-Mail, LinkedIn, Empfehlung)
2. Termin für kostenloses Erstgespräch (90 Min.) vereinbaren
3. **Checkliste für Erstgespräch vorbereiten:**
   - [ ] Welche Prozesse sind zeitaufwändig?
   - [ ] Welche Tools/Software wird aktuell genutzt?
   - [ ] Wo liegen die Daten? (Excel, Cloud, Papier?)
   - [ ] Budget-Vorstellung erfragen
   - [ ] Datenschutz-Bedürfnis klären (Cloud vs. lokal)
   - [ ] Entscheidungsweg: Wer entscheidet?

---

## Phase 1: Analyse & Angebot

**Dauer:** 2–5 Tage
**Status:** 🟡 In Arbeit

1. Prozessanalyse durchführen (persönlich oder remote)
2. Automatisierungspotenzial dokumentieren
3. Festpreis-Angebot erstellen (Vorlage: `templates/angebotsvorlage.md`)
4. Hosting-Option vorschlagen (siehe `hosting-konzept.md`)
5. AV-Vertrag (DSGVO) bei Bedarf beilegen

---

## Phase 2: Entwicklung

**Dauer:** 3–10 Tage (je nach Komplexität)
**Status:** 🔵 In Entwicklung

1. Workflow-Design dokumentieren (Flowchart)
2. Entwicklung in Testumgebung
3. Kunde erhält Zwischenstand (Screenshot/Video)
4. Gemeinsame Testphase (Kunde gibt Beispiel-Daten)
5. Feintuning nach Feedback

---

## Phase 3: Go-Live

**Dauer:** 1–2 Tage
**Status:** 🟢 Live

1. Workflow in Produktion überführen
2. Abschlusstest mit Kundendaten
3. Mitarbeiter-Schulung (30–60 Min.)
4. Dokumentation übergeben
5. Optional: Wartungsvertrag abschließen

---

## Phase 4: Betrieb

**Dauer:** Laufend
**Status:** 🔄 Aktiv

1. Monatlicher Health-Check
2. Bei Wartungsvertrag: monatliches Status-Update
3. Bei Störung: SLA-gerechte Reaktion
4. Jährliches Optimierungs-Review

---

## Vorlagen für Kundenkommunikation

```markdown
Betreff: Dein Projekt-Status – [Projektname]
Hallo [Kunde],

hier der aktuelle Stand:
✅ Phase 1 abgeschlossen (Analyse)
🔄 Phase 2 läuft (Entwicklung)
  - Workflow-Grundgerüst steht
  - Nächster Schritt: API-Anbindung testen
⏳ Nächste Woche: Gemeinsamer Testtermin

Fragen? Einfach antworten.
Beste Grüße, Benjamin
```
