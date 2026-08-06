# Portfolio-Priorisierung (Prototyp)

Klick-Prototyp für die Portfolio-Priorisierung einer Abteilung: sechs Fragen pro Vorhaben, transparente Wenn-dann-Regeln, abgeleitetes Portfolio. Eine HTML-Datei, keine Libraries, speichert nur lokal im Browser (localStorage).

Live: https://julelabs.github.io/portfolio-priorisierung/

## Deploy

Quelle der Wahrheit ist `../mock/portfolio-v3.html` im Projektordner, nicht diese Datei hier. Zum Aktualisieren:

```bash
sed "s|\.\./\.\./Wirkungswerkstatt/site/assets/fonts/|assets/fonts/|g" ../mock/portfolio-v3.html > index.html
git add -A && git commit -m "Stand aktualisiert" && git push
```

Vorher müssen beide Testsuiten grün sein (siehe `../tests/README.md`).
