# Portfolio-Priorisierung (Prototyp)

Klick-Prototyp für die Portfolio-Priorisierung einer Abteilung: sechs Fragen pro Vorhaben, transparente Wenn-dann-Regeln, abgeleitetes Portfolio. Eine HTML-Datei, keine Libraries, speichert nur lokal im Browser (localStorage).

Live: https://julelabs.github.io/portfolio-priorisierung/

Aufbau: `index.html` ist die Landingpage, `werkzeug.html` das Werkzeug. `landing.html` ist nur noch eine Weiterleitung auf die Startseite (alter geteilter Link).

## Deploy

Quelle der Wahrheit sind die Dateien im Projektordner, nicht die Dateien hier. Seit dem 22.08. liegen alle drei Seiten zusammen in `../mock/`: das Werkzeug als `portfolio-v3.html`, die Startseite als `landing.html`, die FAQ als `faq.html`. Vorher lagen Startseite und FAQ unter `Entwürfe und Tests/`, was sie wie Entwürfe aussehen ließ und die Verlinkung untereinander lokal kaputt machte. Alle drei benutzen jetzt denselben Schriftpfad, deshalb ist die erste Ersetzung in allen drei Befehlen identisch.

Werkzeug aktualisieren:

```bash
sed "s|\.\./\.\./Wirkungswerkstatt/site/assets/fonts/|assets/fonts/|g" ../mock/portfolio-v3.html > werkzeug.html
```

Landingpage aktualisieren:

```bash
sed -e "s|\.\./\.\./Wirkungswerkstatt/site/assets/fonts/|assets/fonts/|g" \
    -e 's|href="landing.html"|href="./"|g' \
    -e 's|href="portfolio-v3\.html|href="werkzeug.html|g' \
    ../mock/landing.html > index.html
```

FAQ aktualisieren:

```bash
sed -e "s|\.\./\.\./Wirkungswerkstatt/site/assets/fonts/|assets/fonts/|g" \
    -e 's|href="landing.html#|href="./#|g' \
    -e 's|href="landing.html"|href="./"|g' \
    -e 's|href="portfolio-v3\.html"|href="werkzeug.html"|g' \
    ../mock/faq.html > faq.html
```

Die Anker-Regel muss vor der Regel ohne Anker stehen: Seit dem 22.08. trägt die FAQ dasselbe Abschnittsmenü wie die Startseite, und `href="landing.html#danach"` wird von der exakten Regel nicht erfasst.

## Lokale Gesamtdatei

Für den Gesamttest und den Transport auf einen Arbeitsrechner gibt es zusätzlich eine einzelne Datei mit Startseite, FAQ, Werkzeug und eingebetteten Schriften:

```bash
node ../tools/build-gesamtdatei.mjs
node ../tests/test-gesamtdatei.js
```

Das Ergebnis liegt unter `../mock/portfolio-priorisierung-komplett.html`. Es ist ein generiertes Artefakt und wird nicht von Hand bearbeitet. Die drei Dateien in `../mock/` bleiben die Quellen der Wahrheit; die GitHub-Pages-Struktur mit drei Adressen bleibt davon unberührt.

Der Hero der Landingpage ist seit 17.08. reines CSS und braucht keine Bilddateien mehr; die zwei alten Bilder in `assets/` (`hero-entscheidungsboard-ausschnitt.jpg`, `08-linsen-papier-menschlicher.jpg`) werden nicht mehr referenziert und bleiben nur als Rest liegen. Danach:

```bash
git add -A && git commit -m "Stand aktualisiert" && git push
```

Vor einem Werkzeug-Deploy müssen die Testsuiten grün sein (siehe `../tests/README.md`).
