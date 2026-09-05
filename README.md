# Rezepte-App

Dunkle Web-App (PWA) für den Rezept-Log, im selben Stil wie die REWE-/Gassi-App.
Die Seite ist **statisch gebaut**: `index.html` + PWA-Assets werden lokal aus den
`rezepte/*.md` im Vault erzeugt (`../rezepte_app.py`) und hierher gepusht. Der
Workflow `.github/workflows/deploy.yml` veröffentlicht bei jedem Push auf
GitHub Pages.

> Achtung: öffentlich erreichbar (nur nicht in Suchmaschinen, `robots.txt`
> Disallow). Enthält persönliche Bewertungen und Notizen.

## Einmalig einrichten

1. Öffentliches Repo anlegen: <https://github.com/new> → Name **`Rezepte-App`**,
   **Public**, ohne README/Lizenz/gitignore.
2. Dieses Verzeichnis pushen (Remote ist bereits gesetzt):
   ```bash
   git push -u origin main
   ```
3. Auf GitHub: **Settings → Pages → Build and deployment → Source: „GitHub Actions"**.
   Danach läuft der Deploy-Workflow; die Seite liegt unter
   `https://hannibal2404.github.io/Rezepte-App/`.

## Aktualisieren (neues/geändertes Rezept)

Aus `Documents/Tools/Rezepte/`:
```bash
python rezepte_app.py --out Rezepte-App
cd Rezepte-App && git add -A && git commit -m "Rezepte aktualisiert" && git push
```
Der Push löst das Pages-Deployment automatisch aus.

## Später: vollautomatisch wie REWE/Gassi

Für Auto-Rebuild bei jeder Vault-Änderung müsste ein Workflow im privaten
`Obsidian`-Repo (dort liegen die `rezepte/*.md`) die Seite bauen und per PAT
hierher pushen — dasselbe Zwei-Repo-Muster wie `Rewe` → `Rewe-App`. Aktuell
bewusst der einfache lokale Build-und-Push-Weg.
