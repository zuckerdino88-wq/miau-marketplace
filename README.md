# M.I.A.U. Marktplatz

Kostenlose Pakete für die M.I.A.U.-App (Celestial Lion). Ein Paket bündelt:

- **Skills**: Anleitungen im offenen `SKILL.md`-Format (Kopf mit `name` und `description`, darunter die Anleitung)
- **MCP über das Netz**: HTTPS-Adressen von MCP-Servern. Sie laufen am Handy und am PC.
- **Lokale MCP-Server**: Befehle wie `npx -y …`. Sie laufen nur in einer Laufzeit, die Programme ausführen darf: am PC über OpenCode, am Handy über die eingebaute Linux-Laufzeit.
- **Hooks**: Pfade, die nie geändert werden dürfen, und Befehle, die nach jeder Code-Änderung laufen (`.miau/hooks.json` im Projekt).

Die App liest `index.json`. Vor jeder Installation zeigt sie eine Karte mit allem, was ein Paket darf, und installiert erst nach „Erlauben“. Lokale Server und Hooks führen Code aus und sind deshalb rot markiert.

## Paketformat `miau-paket-v1`

```json
{
  "format": "miau-paket-v1",
  "id": "doku-suche",
  "name": "Doku-Suche",
  "version": "1.0.0",
  "beschreibung": "…",
  "skills": ["skills/doku-zuerst/SKILL.md"],
  "mcp": [{"id": "deepwiki", "name": "DeepWiki", "url": "https://mcp.deepwiki.com/mcp"}],
  "mcpLokal": [{"id": "memory", "name": "Gedächtnis", "befehl": ["npx", "-y", "@modelcontextprotocol/server-memory"]}],
  "hooks": {"schuetzen": [".env"], "danach": ["npm test"]}
}
```

- `id`: 1–20 Zeichen, nur `a-z`, `0-9`, `-`. `version`: `x.y.z`.
- `skills`: Pfade relativ zum Paketordner, höchstens 10.
- `mcp`: nur `https://`, ohne Zugangsdaten in der Adresse, höchstens 10.
- `mcpLokal`: `befehl` als Liste, das erste Wort muss `npx`, `uvx`, `node`, `python` oder `python3` sein, höchstens 5.
- `hooks.schuetzen`: Pfadmuster (`*` im Ordner, `**` beliebig tief), höchstens 20.
- `hooks.danach`: Befehle als Text, das erste Wort muss `python`, `node`, `npm` oder `cargo` sein (wie im Code-Agenten der App), höchstens 5. Jeder Befehl braucht beim Ausführen weiter deine Freigabe.

## Neues Paket

Ordner unter `pakete/<id>/` mit `paket.json`, Skills daneben, und einen Eintrag in `index.json`.
