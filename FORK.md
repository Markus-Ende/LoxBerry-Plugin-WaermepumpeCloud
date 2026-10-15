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

Fork-Fassungen hängen eine vierte Stelle an die Fassung des Originals, auf
der sie aufbauen: `0.9.31.1`, `0.9.31.2`, … — Tag `v0.9.31.1`.

- Das Original vergibt nur dreiteilige Tags; Fork-Tags überschreiben also nie
  eines davon, und `release.yml` reagiert nur auf vierteilige.
- LoxBerry vergleicht so: 0.9.31 < 0.9.31.1 < 0.9.32
  (`LoxBerry::System::plugin_version_compare`, Rückfall auf `version.pm`).
- Kein `+fork.1`: Build-Metadaten ignoriert LoxBerry beim Vergleich, ein
  Update würde nie angeboten.

## Release

1. Auf einem Zweig `release/<Fassung>`: `VERSION` in `plugin.cfg`,
   `release.cfg` und `prerelease.cfg`, `ARCHIVEURL` und `INFOURL` in den
   beiden cfg auf den neuen Tag. `ARCHIVEURL` ist
   `https://github.com/Markus-Ende/LoxBerry-Plugin-WaermepumpeCloud/releases/download/v<Fassung>/waermepumpe-<Fassung>.zip`.
2. PR nach `master`, mergen.
3. `git tag v<Fassung> && git push origin v<Fassung>` — `release.yml` prüft
   Fassungen und Adressen, baut das ZIP und legt das Release an.

## Original nachziehen

    git fetch upstream
    git merge upstream/master

Konflikte entstehen dabei nur in den drei cfg-Dateien; dort gelten die
Adressen dieses Forks und die höhere Fassung.
