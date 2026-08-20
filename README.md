# Portfolio-Priorisierung (Prototyp)

Klick-Prototyp für die Portfolio-Priorisierung einer Abteilung: sechs Fragen pro Vorhaben, transparente Wenn-dann-Regeln, abgeleitetes Portfolio. Eine HTML-Datei, keine Libraries, speichert nur lokal im Browser (localStorage).

Live: https://julelabs.github.io/portfolio-priorisierung/

Aufbau: `index.html` ist die Landingpage, `werkzeug.html` das Werkzeug. `landing.html` ist nur noch eine Weiterleitung auf die Startseite (alter geteilter Link).

## Deploy

Quelle der Wahrheit sind die Dateien im Projektordner, nicht die Dateien hier: das Werkzeug in `../mock/portfolio-v3.html`, Landingpage und FAQ in `../mock/Entwürfe und Tests/`. Seit dem 20.08. liegt auch Julias Hero vom 17.08. in der mock-Quelle (Rückführung, Entscheidung 119); ein Deploy nach dieser Anleitung erhält ihn.

Werkzeug aktualisieren (aus `../mock/portfolio-v3.html`):

```bash
sed "s|\.\./\.\./Wirkungswerkstatt/site/assets/fonts/|assets/fonts/|g" ../mock/portfolio-v3.html > werkzeug.html
```

Landingpage aktualisieren (aus `../mock/Entwürfe und Tests/landing.html`):

```bash
sed -e "s|\.\./\.\./\.\./Wirkungswerkstatt/site/assets/fonts/|assets/fonts/|g" \
    -e 's|href="landing.html"|href="./"|g' \
    -e 's|href="\.\./portfolio-v3\.html|href="werkzeug.html|g' \
    "../mock/Entwürfe und Tests/landing.html" > index.html
```

FAQ aktualisieren (aus `../mock/Entwürfe und Tests/faq.html`):

```bash
sed -e "s|\.\./assets/fonts/|assets/fonts/|g" \
    -e 's|href="landing.html"|href="./"|g' \
    -e 's|href="\.\./portfolio-v3\.html"|href="werkzeug.html"|g' \
    "../mock/Entwürfe und Tests/faq.html" > faq.html
```

Der Hero der Landingpage ist seit 17.08. reines CSS und braucht keine Bilddateien mehr; die zwei alten Bilder in `assets/` (`hero-entscheidungsboard-ausschnitt.jpg`, `08-linsen-papier-menschlicher.jpg`) werden nicht mehr referenziert und bleiben nur als Rest liegen. Danach:

```bash
git add -A && git commit -m "Stand aktualisiert" && git push
```

Vor einem Werkzeug-Deploy müssen die Testsuiten grün sein (siehe `../tests/README.md`).
