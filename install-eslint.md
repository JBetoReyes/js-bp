# How to set eslint with ts in your project

1.- Create a file in your root called ```.editorconfig```

```
root=true
[*.js]
indent_style = space
indent_size = 2
charset = utf-8
```

2.- Install the following dependencies

```json
npm i -D ts-node eslint @types/source-map @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-airbnb-typescript eslint-config-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-prettier eslint-plugin-react prettier typescript
```

3.- Create a new files called ```.eslintrc.js```

```
module.exports = {
  root: true,
  parser: '@typescript-eslint/parser',
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 2018,
    sourceType: 'module',
    project: './tsconfig.json',
  },
  plugins: ['@typescript-eslint', 'prettier'],
  extends: [
    'airbnb-typescript',
    'plugin:prettier/recommended',
    'plugin:@typescript-eslint/eslint-recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  rules: {
    'import/extensions': [
      'error',
      'ignorePackages',
      {
        js: 'never',
        ts: 'never',
      }
    ],
    'prettier/prettier': 'error',
  },
  settings: {
    'import/resolver': {
      node: {
        extensions: ['.js', '.ts']
      }
    }
  }
}
```

4.- Add a configuration for prettier ```.prettierc```
```
{
  "singleQuote": true,
  "trailingComma": "es5"
}
```

5.- Add a tsconfig with the following command
```
npx tsc --init
```