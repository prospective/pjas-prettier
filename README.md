# @prospective/pjas-prettier

Shared [Prettier](https://prettier.io) config for `pjas-lead`, `pjas-frontend`, and `pjas-bannersandbox`.

## Usage

This package is published to GitHub Packages, so each consuming repo needs an `.npmrc` pointing the `@prospective` scope at that registry:

```
@prospective:registry=https://npm.pkg.github.com
```

Install the package in the dependecies, instead of devDependencies, so that you can use it in the CI as well. Otherwise, use `--save-dev` to omit it on production
```
npm install --save prettier @prospective/pjas-prettier
```

In `package.json`:

```json
{
  "prettier": "@prospective/pjas-prettier"
}
```

No `.prettierrc` needed — Prettier resolves the config via the `prettier` field automatically.

## Formatting

Each consuming repo should expose:

```json
{
  "scripts": {
    "format": "prettier --write .",
    "format:check": "prettier --check ."
  }
}
```

Run `npm run format:check` before pushing. VS Code users get this automatically via each repo's committed `.vscode/settings.json` (Prettier extension `esbenp.prettier-vscode` as default formatter, format-on-save enabled).

## Changing the config

Edit `index.js` and merge to `master`. The [Publish workflow](.github/workflows/publish.yml) runs on every push to `master` and publishes automatically — it resolves the patch number from the version already in the registry, so there is nothing to bump by hand for a normal change. The `version` in `package.json` is only read for its major and minor.

For a breaking or feature-level release, bump the major or minor in `package.json` yourself; the workflow then publishes that line starting at patch `.0`.

Afterwards, bump the version in each consuming repo's `package.json` and re-run `prettier --write .` there.
