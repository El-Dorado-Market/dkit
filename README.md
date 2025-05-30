# dKiT demo

## Note on dependecies

Pinned dependency versions in `package.json` using [resolutions](https://classic.yarnpkg.com/lang/en/docs/selective-version-resolutions/#toc-how-to-use-it)

```
{
  "resolutions": {
    "@noble/curves": "~1.6.0",
    "@noble/hashes": "~1.5.0"
  }
}
```

Also note [overrides](https://docs.npmjs.com/cli/v9/configuring-npm/package-json#overrides) for other package managers.

## Note on polyfills

In general the Node.js globals `Buffer` and `global` need to be polyfilled. If you're using vite it's as easy as installing and configuring [vite-plugin-node-polyfills](https://npmjs.com/package/vite-plugin-node-polyfills)

## Note on tsconfig.json

The lowest supported `tsconfig.json` target is ES2022 and also requires lib ES2022 to be specified, due to usage of `Error.cause`.

Because of the usage of `enum`s, the [erasableSyntaxOnly](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-5-8.html#the---erasablesyntaxonly-option) `compilerOption` in your `tsconfig.json` has to be turned off.

## React + TypeScript + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend updating the configuration to enable type-aware lint rules:

```js
export default tseslint.config({
  extends: [
    // Remove ...tseslint.configs.recommended and replace with this
    ...tseslint.configs.recommendedTypeChecked,
    // Alternatively, use this for stricter rules
    ...tseslint.configs.strictTypeChecked,
    // Optionally, add this for stylistic rules
    ...tseslint.configs.stylisticTypeChecked,
  ],
  languageOptions: {
    // other options...
    parserOptions: {
      project: ['./tsconfig.node.json', './tsconfig.app.json'],
      tsconfigRootDir: import.meta.dirname,
    },
  },
})
```

You can also install [eslint-plugin-react-x](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-x) and [eslint-plugin-react-dom](https://github.com/Rel1cx/eslint-react/tree/main/packages/plugins/eslint-plugin-react-dom) for React-specific lint rules:

```js
// eslint.config.js
import reactX from 'eslint-plugin-react-x'
import reactDom from 'eslint-plugin-react-dom'

export default tseslint.config({
  plugins: {
    // Add the react-x and react-dom plugins
    'react-x': reactX,
    'react-dom': reactDom,
  },
  rules: {
    // other rules...
    // Enable its recommended typescript rules
    ...reactX.configs['recommended-typescript'].rules,
    ...reactDom.configs.recommended.rules,
  },
})
```
