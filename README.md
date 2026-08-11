# Portfolio-Priorisierung (Prototyp)

Klick-Prototyp für die Portfolio-Priorisierung einer Abteilung: sechs Fragen pro Vorhaben, transparente Wenn-dann-Regeln, abgeleitetes Portfolio. Eine HTML-Datei, keine Libraries, speichert nur lokal im Browser (localStorage).

Live: https://julelabs.github.io/portfolio-priorisierung/

Aufbau: `index.html` ist die Landingpage, `werkzeug.html` das Werkzeug. `landing.html` ist nur noch eine Weiterleitung auf die Startseite (alter geteilter Link).

## Deploy

Quelle der Wahrheit sind die Dateien in `../mock/` im Projektordner, nicht die Dateien hier.

Werkzeug aktualisieren (aus `../mock/portfolio-v3.html`):

```bash
sed "s|\.\./\.\./Wirkungswerkstatt/site/assets/fonts/|assets/fonts/|g" ../mock/portfolio-v3.html > werkzeug.html
```

Landingpage aktualisieren (aus `../mock/landing.html`):

```bash
sed -e "s|\.\./\.\./Wirkungswerkstatt/site/assets/fonts/|assets/fonts/|g" \
    -e "s|hero-entwuerfe/|assets/|g" \
    -e "s|portfolio-v3.html|werkzeug.html|g" \
    -e 's|href="landing.html"|href="./"|g' \
    ../mock/landing.html > index.html
```

Bilder, die die Landingpage aus `../mock/hero-entwuerfe/` referenziert, unter gleichem Dateinamen nach `assets/` kopieren. Danach:

```bash
git add -A && git commit -m "Stand aktualisiert" && git push
```

Vor einem Werkzeug-Deploy müssen beide Testsuiten grün sein (siehe `../tests/README.md`).
