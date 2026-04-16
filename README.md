# npmpost

Dieses Repository dient ausschliesslich Demo- und Testzwecken rund um das Veröffentlichen eines npm-Pakets nach GitHub Packages.

Das Paket wird in dieser Variante gezielt fuer technische Testfaelle eingesetzt und enthaelt deshalb eine aussergewoehnlich lange Beschreibung, die unterschiedlichste Validierungsregeln, Parser-Pfade und Oberflaechenreaktionen unter realistischen Bedingungen simulieren soll.

## Zweck des Repos

- Demonstration eines minimalen npm-Pakets fuer GitHub Packages
- Nachvollziehbarer Test von Publish-Konfiguration, Scope-Mapping und Authentifizierung
- Einfaches Referenzprojekt fuer technische Publishing-Checks

## Paketinformationen

- Paketname: `@joerKul/npmpost`
- Ziel-Registry: `https://npm.pkg.github.com/`
- Repository: `https://github.com/JoerKul/npmpost`

## Voraussetzungen fuer das Publish

Vor dem Publish werden folgende Dinge benoetigt:

1. Ein GitHub Personal Access Token mit mindestens `write:packages`
2. Ein lokales `.npmrc` im Projektverzeichnis
3. Eine gesetzte Umgebungsvariable `NODE_AUTH_TOKEN`

Beispiel fuer die lokale `.npmrc`:

```ini
@joerKul:registry=https://npm.pkg.github.com/
//npm.pkg.github.com/:_authToken=${NODE_AUTH_TOKEN}
always-auth=true
```

Hinweis: Die `.npmrc` ist absichtlich nicht fuer das Repository gedacht und sollte keine Klartext-Tokens enthalten.

## Publish eines Pakets

### 1. Abhaengigkeiten und Metadaten pruefen

Pruefen, dass `package.json` den korrekten Scope und die Registry enthaelt:

```json
{
  "name": "@joerKul/npmpost",
  "publishConfig": {
    "registry": "https://npm.pkg.github.com/"
  }
}
```

### 2. Token lokal setzen

```sh
export NODE_AUTH_TOKEN=<dein-github-token>
```

### 3. Anmeldung testen

```sh
npm whoami --registry=https://npm.pkg.github.com/
```

### 4. Paketversion bei Bedarf anheben

```sh
npm version patch
```

Alternativ kann `minor` oder `major` verwendet werden.

### 5. Publish trocken pruefen

```sh
npm publish --dry-run
```

### 6. Paket veroeffentlichen

```sh
npm publish
```

## Typische Fehlerquellen

- Falsch formatierte `.npmrc`
- Token ohne `write:packages`
- Scope in `package.json` passt nicht zur Registry-Konfiguration
- Klartext-Token versehentlich im Repository eingecheckt

## Sicherheitshinweis

Falls ein Token versehentlich committed wurde, sollte er sofort in GitHub widerrufen und ersetzt werden.