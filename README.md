# Configure Environment for ESLINT 9+ with Prettier
After ESLINT 9.0 the configuration file changed to flat format, which changed they way to
set up the file. This guide shows the template for setting it up.

## Setup
1. Add Prettier ESLINT config to `settings.json`
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

2. Install dependencies inside your project's folder:
```
npm i eslint eslint-config-prettier eslint-plugin-prettier eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-react-refresh @typescript-eslint/eslint-plugin @typescript-eslint/parser typescript-eslint globals -D
```

3. configure `eslint.config.js`
```
import js from '@eslint/js'
import globals from 'globals'
import react from 'eslint-plugin-react'
import reactHooks from 'eslint-plugin-react-hooks'
import reactRefresh from 'eslint-plugin-react-refresh'
import tseslint from '@typescript-eslint/eslint-plugin'
import tsParser from '@typescript-eslint/parser'
import prettierPlugin from 'eslint-plugin-prettier'

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
                    jsx: true,
                },
            },
        },
        plugins: {
            react,
            'react-hooks': reactHooks,
            'react-refresh': reactRefresh,
            '@typescript-eslint': tseslint,
            prettier: prettierPlugin,
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
            'no-unused-vars': 'off',
            '@typescript-eslint/no-unused-vars': ['warn', { 
                vars: 'all', 
                args: 'after-used', 
                ignoreRestSiblings: true 
            }],
            '@typescript-eslint/no-explicit-any': 'warn',
        },
        settings: {
            react: {
                version: 'detect',
            },
        },
    },
]
```

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
Install dependencies:
```
npm i @rocketseat/eslint-config
```
inside `eslint.config.js`
```
import rocketseatLint from '@rocketseat/eslint-config/react.js';
export default [
  {
    plugins: {
      rocketseatLint
    }
  }
]
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
