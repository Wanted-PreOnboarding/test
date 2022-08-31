# init setting

prettier

```js
module.exports = {
  arrowParens: 'avoid',
  parser: 'typescript',
  singleQuote: true,
  semi: true,
  printWidth: 100,
  tabWidth: 2,
};
```

eslint

```json
{
  // "extends": ["react-app", "eslint:recommended"],
  "env": {
    "browser": true,
    "node": true,
    "es6": true
  },
  "rules": {
    "no-var": "error",
    "no-multiple-empty-lines": "error",
    "no-console": ["warn", { "allow": ["warn", "error", "info"] }], // error => warn
    "eqeqeq": "error",
    "dot-notation": "error",
    "no-unused-vars": "error",
    /// 추가 rules
    "camelcase": "error",
    "prefer-const": "error",
    "no-new-object": "error",
    "array-bracket-newline": "error",
    "array-element-newline": "error",
    "object-property-newline": "error",
    "object-shorthand": "error",
    "lines-between-class-members": "error",
    "no-new-func": "error",
    "prefer-arrow-callback": "error",
    "arrow-parens": "error",
    "prefer-destructuring": "error",
    "prefer-template": "error",
    "brace-style": "error",
    "curly": "error",
    "keyword-spacing": "error",
    "padding-line-between-statements": "error"
    ///
  }
}
```
