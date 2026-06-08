# Hosting-Konzept für Kunden-Workflows

## Ausgangslage

Benjamin Franke hostet seine eigene n8n-Infrastruktur auf UpCloud Frankfurt:
- Server: 4 vCPU, 15 GB RAM, 50 GB SSD
- n8n läuft in Docker
- Ollama (lokale KI-Modelle) läuft ebenfalls dort
- Standort: Frankfurt, Deutschland (DSGVO-konform)
- Kosten: ~12–15 €/Monat (Festpreis)

## Modell: Drei Optionen für Kunden

### Option A: Kunde hostet selbst (Empfohlen für Datenschutz-sensible Betriebe)
**Beschreibung:**
- Workflow wird auf Kundensystem installiert (eigener Server, NAS, oder VPS)
- Benjamin hat nur temporären Zugriff für Entwicklung & Wartung
- Kunde behält volle Datenkontrolle

**Vorteile:**
- ✅ Maximale DSGVO-Konformität
- ✅ Keine Abhängigkeit von Benjamin
- ✅ Kunde kann später selbst erweitern

**Nachteile:**
- ❌ Kunde braucht eigene Infrastruktur (oder kauft sie auf Empfehlung)
- ❌ Einrichtung aufwändiger

**Preis:** normaler Entwicklungspreis + ggf. Einrichtungs-Assistent (50–100 €)

---

### Option B: Shared Hosting auf Benjamins UpCloud (Start-up-freundlich)

**Beschreibung:**
- Ein dedizierter n8n-Workflow läuft in Benjamins Docker-Infrastruktur
- Isolierte Umgebung pro Kunde (eigener n8n-Space oder separater Container)
- Benjamin überwacht & wartet

**Vorteile:**
- ✅ Keine eigene Infrastruktur nötig
- ✅ Schnellste Inbetriebnahme
- ✅ Inkl. Monitoring & Wartung
- ✅ Günstig für Kunden

**Nachteile:**
- ❌ Daten liegen in Benjamins Infrastruktur (AV-Vertrag nötig)
- ❌ Abhängigkeit von Benjamins Server-Verfügbarkeit
- ❌ Skalierungsgrenze (UpCloud hat nur 15 GB RAM)

**Preis:** 15–25 €/Monat zzgl. zum Wartungsvertrag (oder im Wartungsvertrag enthalten)

---

### Option C: VPS beim Kunden (Empfohlen ab 3+ Workflows)

**Beschreibung:**
- Benjamin richtet einen günstigen Hetzner/Netcup-VPS (~5–8 €/Monat) für den Kunden ein
- n8n läuft dort exklusiv für diesen Kunden
- Benjamin hat SSH-Zugriff für Wartung

**Vorteile:**
- ✅ Volle Isolierung
- ✅ Datenhoheit beim Kunden (VPS und dessen Vertrag)
- ✅ Skalierbar

**Nachteile:**
- ❌ Zusätzliche Kosten für Kunden (5–10 €/Monat)
- ❌ Einmaliger Einrichtungsaufwand

**Preis:** VPS-Kosten trägt Kunde (~5–10 €/Monat) + Einrichtung (50 € einmalig)

---

## Empfehlung nach Kundentyp

| Kundentyp | Empfohlenes Modell | Begründung |
|-----------|-------------------|------------|
| 1 Workflow, datenschutz-unktritisch | Option B (Shared) | Günstig, schnell |
| 1 Workflow, datenschutz-sensibel | Option A (Self-Hosted) | DSGVO-konform |
| 2–3 Workflows | Option C (VPS) | Isoliert & skalierbar |
| 4+ Workflows | Option C (VPS) | Eigene Infrastruktur lohnt sich |

## Technische Umsetzung (für Benjamin)

### Option B (Shared Hosting)
```yaml
# docker-compose.override.yml für getrennte n8n-Instanzen
services:
  n8n-kunde-a:
    image: n8nio/n8n
    ports:
      - "5679:5678"    # separater Port
    volumes:
      - n8n-kunde-a-data:/home/node/.n8n
    environment:
      - N8N_PORT=5678
      - N8N_METRICS=false

volumes:
  n8n-kunde-a-data:
```

### Option C (VPS)
- Hetzner CX22 (2 vCPU, 4 GB RAM) reicht für 1–3 Workflows (~7 €/Monat)
- Einrichtung via Docker + Cloudflare Tunnel für SSL
- Automatische Backups via Cron

## Hosting-Hinweise für Angebotstexte

> *„Ihre Workflows laufen auf Ihrem System, auf einem eigenen VPS oder in meiner verwalteten Infrastruktur – Sie entscheiden. In jedem Fall gilt: Ihre Daten bleiben in Deutschland und unter Ihrer Kontrolle."*
