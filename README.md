# prettier-config-pjas

Shared [Prettier](https://prettier.io) config for `pjas-lead`, `pjas-frontend`, and `pjas-bannersandbox`.

## Usage
Install the package in the dependecies, instead of devDependencies, so that you can use it in the CI as well. Otherwise, use `--save-dev` to omit it on production
```
npm install --save prettier prettier-config-pjas
```

In `package.json`:

```json
{
  "prettier": "prettier-config-pjas"
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

Bump the version in `package.json`, publish (`npm publish`), then bump the version in each consuming repo's `package.json` and re-run `prettier --write .` there.
