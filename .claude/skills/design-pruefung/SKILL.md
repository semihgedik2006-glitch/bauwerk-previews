---
name: design-pruefung
description: Pflicht vor jedem PR, der an einer Bauwerk-Fassung etwas Sichtbares ändert. Screenshots in allen Breiten, Messung von Kontrast, Trefferflächen, Überlappung, Barrierefreiheit und kaputten Links. Auslöser: Design, Layout, CSS, Knopf, Farbe, Abstand, „sieht komisch aus“.
---

# Design-Prüfung

1. Kein Server nötig, das Skript liefert den Ordner selbst aus.
2. Vorher: `node tools/design-pruefung.mjs <Fassung>/index.html --basis /bauwerk-previews --ruhig --breiten 320,390,820,1280,1440,1920 --aus /tmp/dp-vorher --nur-bericht`
3. Ändern.
4. Nachher: `node tools/design-pruefung.mjs <Fassung>/index.html --basis /bauwerk-previews --ruhig --breiten 320,390,820,1280,1440,1920 --aus /tmp/dp` (Exit-Code 1 heißt Fehler). Jede geänderte Unterseite einzeln.
5. Screenshots selbst ansehen (mindestens 390 und 1440): Hierarchie, Ausrichtung, gleiche Ecken und Abstände je Ebene, Zustände (Hover, Fokus, leer, Fehler, Laden).
6. Tabelle aus `bericht.md` und je Breite ein Satz zu den Screenshots in die PR-Beschreibung. Neue Fehler gegenüber vorher: nicht mergen.

Gemessen: waagerechter Überlauf, Trefferflächen (Handy und Tablet 44 × 44 px, Rechner 24 × 24 px, Mitte nicht verdeckt), Kontrast 4,5 : 1 (große Schrift 3 : 1, auf Bild und Verlauf an Bildpunkten), Text ragt aus Knopf oder Kasten, lang, Zoom, Namen, Labels, alt, Überschriften, Fokus-Stil, Konsolenfehler, 4xx/5xx, Abstände außerhalb des 2-px-Rasters.

`--ruhig` scrollt einmal durch die Seite und wartet, bis die Scroll-Animationen (GSAP, Lenis) stillstehen. Leere Flächen im Vollbild-Screenshot dann im echten Fenster nachsehen.

Externe Dienste (Karten, Schriften) fallen in dieser Umgebung oft aus und erscheinen als Warnung, nicht als Fehler. Gewollte Meldungen über `--vorher datei.mjs` mit `export const erlaubt = [/…/]` ausnehmen.

Selbsttest: `node tools/design-pruefung.mjs --selbsttest`.
