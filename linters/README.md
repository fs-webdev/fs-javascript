# Linters

ESLint is our current favored JS linter. We may post recent "best-practice" JSHint configs here, if we get to it.

To use ESLint in your project:
From your project root dir:
```
npm install --save-dev eslint babel-eslint
npm install --save-dev https://git@github.com/fs-webdev/fs-javascript/tarball/master
echo "{\"extends\":\"./node_modules/fs-javascript/linters/.eslintrc\",\"rules\": {}}" > .eslintrc


```
