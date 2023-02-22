# Project setup

This repo includes dev dependencies to make coding more pro. The standard config app is a symple TS app with ESLint, Prettier, CommitLint and Husky.

## Installation
Initiliazing git.
```bash
git init
```
Starting TypeScript.
We can add paths in tsconfig.
```bash
npm install -D ts-node typescript @types/node
npx tsc --init
```
Set `"rootDir": "./src"` and `"outDir": "dist"` in tsconfig.

In package.json, set the start script as `"start": "tsc && node ./dist/index.js"`

Let's install CommitLint:
```bash
npm i -D @commitlint/config-conventional @commitlint/cli
```
Create `.commitlintrc` file and include as follows:
```javascript
{
    "extends": ["@commitlint/config-conventional"]
}
```
Now, Husky:
```bash
npm i husky --save-dev
npx husky install
```
In package.json, set the prepare script: `"prepare": "husky install"`. Now let's configure the git hooks.
```bash
npx husky add .husky/commit-msg 'npx --no -- commitlint --edit ${1}'
```
Let's create `.gitignore` and add node_modules.

Now, ESLint:
```bash
npm init @eslint/config
```
Follow the instructions and then rename the file to `.eslintrc`.

Now, Prettier:
```bash
npm i --save-dev --save-exact prettier
```
Let's create `.prettierrc` and `.prettierignore` and include `dist` and `coverage` in the last one.

Now, we need to install some packages to avoid conflicts between them.

```bash
npm i --save-dev eslint-config-prettier eslint-plugin-prettier@latest
```
We need to remove some packages automatically installed by ESLint. You can check the package.json in this file to compare with yours.

Now, add this in `.eslintrc`:
```javascript
{
  "root": true,
  "extends": ["eslint:recommended", "plugin:@typescript-eslint/recommended", "prettier"],
  "parser": "@typescript-eslint/parser",
  "parserOptions": { "project": ["./tsconfig.json"] },
  "plugins": ["@typescript-eslint", "prettier"],
  "rules": {}
}
```
and this in `.prettierrc`:
```javascript
{
    "arrowParens": "always",
    "bracketSpacing": true,
    "printWidth": 100,
    "semi": true,
    "singleAttributePerLine": true,
    "singleQuote": false,
    "tabWidth": 2,
    "trailingComma": "es5",
    "useTabs": false
  }
```
Finally, let's add some scripts in package.json to use this.
```javascript
    "lint": "eslint ./",
    "lint:fix": "eslint ./ --fix"
```
## Usage
It's pretty important to install dependencies and configure them first before using them.

Then, we need to run `npm prepare` to load husky and use its `commit-msg` file already added and included in this repo.

Finally, we code, format documment with your snippet and then run the lint scripts.