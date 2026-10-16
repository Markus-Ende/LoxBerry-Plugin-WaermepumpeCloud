# Fork von timanders22/LoxBerry-Plugin-WaermepumpeCloud

Dieser Fork baut eigene Installationsarchive, solange Korrekturen noch nicht
im Original angekommen sind. Korrekturen gehen als Pull Request ans Original;
was hier nur den Fork betrifft (dieses Dokument, `.github/`, die Adressen in
`plugin.cfg`, `release.cfg`, `prerelease.cfg`), gehört nicht in diese PRs.

## Zweige

- **Korrekturen** zweigen vom `master` des Originals ab und enthalten nur den
  Code. Derselbe Zweig geht erst als PR in diesen Fork, nach dem Test am
  LoxBerry als PR ins Original.
- **Fork-Releases** (`release/<Fassung>`) heben nur Fassung und Adressen an.

## Fassungen und Tags

Fork-Fassungen tragen den SemVer-Postfix `-fork.<n>` auf der **nächsten**
Patch-Fassung des Originals: Aufbauend auf 0.9.31 heißt das erste
Fork-Release `0.9.32-fork.1`, das nächste `0.9.32-fork.2` — Tag
`v0.9.32-fork.1`.

- Das Original vergibt nur Tags ohne Postfix; Fork-Tags überschreiben also
  nie eines davon.
- LoxBerry vergleicht nach SemVer
  (`LoxBerry::System::plugin_version_compare`):
  0.9.31 < 0.9.32-fork.1 < 0.9.32-fork.2 < 0.9.32.
- Warum die nächste Patch-Fassung: Ein Postfix ist eine Vorabfassung und
  damit *kleiner* als dieselbe Fassung ohne — `0.9.31-fork.1` läge unter der
  installierten 0.9.31, und LoxBerry böte kein Update an.
- Erscheint im Original 0.9.32, ist es höher als jedes `0.9.32-fork.<n>`.
  Nach dem Nachziehen heißt das nächste Fork-Release `0.9.33-fork.1`.
- Kein `+fork.1`: Build-Metadaten ignoriert LoxBerry beim Vergleich (SemVer
  §10), ein Update würde nie angeboten.

## Release

Kein eigener Bauschritt: GitHub liefert zu jedem Tag das Quellarchiv als ZIP,
und LoxBerry installiert es so, wie es ist (das Original macht es genauso).
`FORK.md` und `.gitattributes` hält `export-ignore` aus dem Archiv.

1. Auf einem Zweig `release/<Fassung>`: `VERSION` in `plugin.cfg`,
   `release.cfg` und `prerelease.cfg` anheben, `ARCHIVEURL` und `INFOURL` in
   den beiden cfg auf den neuen Tag:

       ARCHIVEURL=https://github.com/Markus-Ende/LoxBerry-Plugin-WaermepumpeCloud/archive/refs/tags/v<Fassung>.zip
       INFOURL=https://github.com/Markus-Ende/LoxBerry-Plugin-WaermepumpeCloud/releases/tag/v<Fassung>

2. PR nach `master`, mergen.
3. `git tag v<Fassung> && git push origin v<Fassung>`

Vor dem Tag von Hand prüfen, dass alle drei `VERSION` gleich sind und beide
Adressen den Tag nennen — sonst zeigt das Auto-Update auf ein Archiv, das es
nicht gibt. Manuell installieren: das ZIP unter `ARCHIVEURL` herunterladen
und in der Plugin-Verwaltung hochladen.

## Original nachziehen

    git fetch upstream
    git merge upstream/master

Konflikte entstehen dabei nur in den drei cfg-Dateien; dort gelten die
Adressen dieses Forks und die höhere Fassung.
