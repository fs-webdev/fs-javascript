# Linters

ESLint is our current favored JS linter. We may post recent "best-practice" JSHint configs here, if we get to it.

To use ESLint in your project:
From your project root dir:
```
npm install --save-dev \
eslint \
git+https://github.com/fs-webdev/javascript.git \
babel-eslint
echo "{"extends":"./node_modules/javascript/linters/.eslintrc","rules": {}}" > .eslintrc
```
