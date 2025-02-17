# Configure Environment for EsLint 9+ with Prettier ESLINT
After ESLINT 9.0 the configuration file changed to flat format, which changed they way to
set up the file. This guide shows how to set up EsLint with Prettier

## Setup

### React (with Next.js)

Install dependencies:
```
npm i -D eslint @rocketseat/eslint-config
```
Inside `.eslintrc.json`
```
{
  "extends": [
    "@rocketseat/eslint-config/next", 
    "next/core-web-vitals"
  ]
}
```

### React (without Next.js)

# Configure Environment for EsLint 9+ with Prettier ESLINT
After ESLINT 9.0 the configuration file changed to flat format, which changed they way to
set up the file. This guide shows how to set up EsLint with Prettier

1. Add Prettier ESLINT config to settings.json
```
// Prettier ESLINT  
"editor.defaultFormatter": "rvest.vs-code-prettier-eslint",
"editor.formatOnPaste": false, 
"editor.formatOnType": false, 
"editor.formatOnSave": true, 
"eslint.format.enable": true, 
"editor.formatOnSaveMode": "file", // optional but recommended
"editor.codeActionsOnSave": {
    "source.fixAll": "explicit"
},
```

2. Download the config dependencie
```
npm i @rocketseat/eslint-config/react.js
```

3. Set up eslint.config.js
```
import js from '@eslint/js'
import globals from 'globals'
import react from 'eslint-plugin-react'
import reactHooks from 'eslint-plugin-react-hooks'
import reactRefresh from 'eslint-plugin-react-refresh'
import tseslint from '@typescript-eslint/eslint-plugin'
import tsParser from '@typescript-eslint/parser'
import prettierPlugin from 'eslint-plugin-prettier'

// import the dependencie with the code pattern configuration and add it to Plugins{}
import rocketseatLint from '@rocketseat/eslint-config/react.js';
 
export default [
    {
        ignores: ['dist', 'node_modules'],
    },
    {
        files: ['**/*.{ts,tsx}'],
        languageOptions: {
            parser: tsParser,
            ecmaVersion: 2021,
            sourceType: 'module',
            globals: globals.browser,
            parserOptions: {
                ecmaFeatures: {
                    jsx: true, // Suporte a JSX
                },
            },
        },
        plugins: {
            react,
            'react-hooks': reactHooks,
            'react-refresh': reactRefresh,
            '@typescript-eslint': tseslint,
            prettier: prettierPlugin,
            rocketseatLint,
        },
        rules: {
            'prettier/prettier': [
                'error',
                {
                    printWidth: 80,
                    tabWidth: 2,
                    singleQuote: true,
                    trailingComma: 'all',
                    arrowParens: 'always',
                    semi: false,
                    endOfLine: 'auto',
                },
            ],
            'react/no-unknown-property': 'error',
            ...reactHooks.configs.recommended.rules,
            ...tseslint.configs.recommended.rules,
            ...js.configs.recommended.rules,
            'react/self-closing-comp': 'error',
            '@typescript-eslint/no-empty-object-type': 'off',
            'react/react-in-jsx-scope': 'off',
            'react/prop-types': 'off',
        },
        settings: {
            react: {
                version: 'detect',
            },
        },
    },
]
```

4. Install the dependencies
```
npm i eslint eslint-config-prettier eslint-plugin-prettier eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-react-refresh @typescript-eslint/eslint-plugin @typescript-eslint/parser typescript-eslint globals -D
```

5. Run EsLint -> npx eslint (folderpath)
```
npx eslint .
```

### Node.js

Install dependencies:
```
npm i -D eslint @rocketseat/eslint-config
```
Inside `eslint.config.js`
```
import rocketseatLint from '@rocketseat/eslint-config/node.js';

export default [
  {
    plugins: {
            rocketseatLint,
        },
  }
]
```
