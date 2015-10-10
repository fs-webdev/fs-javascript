# Linters [draft]

ESLint is our current favored JS linter. We may post recent "best-practice" JSHint configs here, if we get to it.

To use ESLint in your project:
From your project root dir:
```
npm install --save-dev \
eslint \
babel-eslint \
fs-webdev/fs-javascript && \
cp ./node_modules/fs-javascript/linters/eslint-default.txt .eslintrc && \
cp ./node_modules/fs-javascript/linters/.eslintignore .eslintignore

```
**Note:** *Installs eslint, babel-eslint engine for ES6 parse ability, installs the FS eslint repo, copies the default FS .eslintrc config and .eslintignore into your project's root dir*

Then:
- [Set up an ESLint plugin for your code editor](http://eslint.org/docs/user-guide/integrations#editors)
- Additionally, you can run ESLint across your project's .js and .es6 files from CLI using something like:
```
node_modules/.bin/eslint ** --ext .js,es6
```
(be sure you have the .eslintignore set to properly ignore `node_modules` if you'd like to avoid pain)
- You can use many other integrations and tools for ESLint, such as [gulp-eslint](https://www.npmjs.com/package/gulp-eslint),  [eslint-watch](https://www.npmjs.com/package/eslint-watch), or
[mocha-eslint](https://www.npmjs.com/package/mocha-eslint)

You may also want to use separate .eslintrc files for your client-side and nodejs code, since their environments and constraints are very different.
