# prettier

- https://prettier.io/

## prettier import sort

- https://github.com/trivago/prettier-plugin-sort-imports

## prettier tailwindcss sort

- https://tailwindcss.com/blog/automatic-class-sorting-with-prettier

# format code before git commit

## Way 1: pre-commit

## Way 2: husky & lint-staged

### Step 1: install and init

```shell
pnpm add -D husky lint-staged
pnpm dlx husky-init  # .husky/
pnpm i
```

### Step 2: config package.json

- Prettier + ESLint

```json
{
  "scripts": {
    "prepare": "husky install"
  },
  "lint-staged": {
    "**/*.{js,ts,jsx,tsx,vue,json,css,md}": ["prettier --write", "eslint --fix"]
  }
}
```

- Biome

```json
{
  "lint-staged": {
    "**/*.{js,ts,jsx,tsx,json,css}": ["biome check --apply"]
  }
}
```

- OXC: Oxlint + Prettier

```json
{
  "lint-staged": {
    "**/*.{js,ts,jsx,tsx}": [
      "oxlint --deny-all --warn-all --fix",
      "prettier --write"
    ]
  }
}
```

### Step 3: config husky

`.husky/pre-commit`

```
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npx lint-staged
```

```shell
git commit -m "feat: bypass" --no-verify
```

`.vscode/settings.json`

```json
{
  "editor.formatOnSave": false,
  "files.autoSave": "off",
  "editor.codeActionsOnSave": {
    "source.fixAll": "never",
    "source.organizeImports": "never",
    "source.fixAll.eslint": "never",
    "source.fixAll.biome": "never",
    "source.stylelint": "never"
  },

  "[typescript]": {
    "editor.formatOnSave": false,
    "editor.defaultFormatter": null
  },
  "[typescriptreact]": {
    "editor.formatOnSave": false,
    "editor.defaultFormatter": null
  },

  "tailwindCSS.classAttributes": ["class", "className", "ngClass"],
  "editor.formatOnType": false
}
```
