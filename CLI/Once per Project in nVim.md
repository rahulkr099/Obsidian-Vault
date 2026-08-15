Here are the complete steps, covering both `.jsx` and `.tsx` projects:

---

### Step 1 — Install eslint plugins (once per project)

**For `.jsx` projects (React + JS):**

```bash
npm install -D eslint-plugin-react globals
```

**For `.tsx` projects (React + TS):**

```bash
npm install -D eslint-plugin-react globals @typescript-eslint/parser @typescript-eslint/eslint-plugin
```

---

### Step 2 — eslint.config.js

**For `.jsx` projects:**

```jsx
import js from "@eslint/js";
import globals from "globals";
import reactHooks from "eslint-plugin-react-hooks";
import reactRefresh from "eslint-plugin-react-refresh";
import react from "eslint-plugin-react";

export default [
  { ignores: ["dist"] },
  {
    files: ["**/*.{js,jsx}"],
    plugins: {
      react,
      "react-hooks": reactHooks,
      "react-refresh": reactRefresh,
    },
    languageOptions: {
      ecmaVersion: "latest",
      sourceType: "module",
      globals: globals.browser,
      parserOptions: {
        ecmaFeatures: { jsx: true },
      },
    },
    settings: {
      react: { version: "detect" },
    },
    rules: {
      ...js.configs.recommended.rules,
      ...reactHooks.configs.recommended.rules,
      "react-refresh/only-export-components": ["warn", { allowConstantExport: true }],
      "react/jsx-uses-react": "error",
      "react/jsx-uses-vars": "error",
    },
  },
];
```

**For `.tsx` projects:**

```jsx
import js from "@eslint/js";
import globals from "globals";
import reactHooks from "eslint-plugin-react-hooks";
import reactRefresh from "eslint-plugin-react-refresh";
import react from "eslint-plugin-react";
import tseslint from "@typescript-eslint/eslint-plugin";
import tsparser from "@typescript-eslint/parser";

export default [
  { ignores: ["dist"] },
  {
    files: ["**/*.{ts,tsx}"],
    plugins: {
      react,
      "react-hooks": reactHooks,
      "react-refresh": reactRefresh,
      "@typescript-eslint": tseslint,
    },
    languageOptions: {
      ecmaVersion: "latest",
      sourceType: "module",
      globals: globals.browser,
      parser: tsparser,         // ← TypeScript parser handles TSX automatically
      parserOptions: {
        ecmaFeatures: { jsx: true },
        project: "./tsconfig.json",
      },
    },
    settings: {
      react: { version: "detect" },
    },
    rules: {
      ...js.configs.recommended.rules,
      ...tseslint.configs.recommended.rules,
      ...reactHooks.configs.recommended.rules,
      "react-refresh/only-export-components": ["warn", { allowConstantExport: true }],
      "react/jsx-uses-react": "error",
      "react/jsx-uses-vars": "error",
    },
  },
];
```

---

### Step 3 — Save as a template so you never repeat this

```bash
# create a templates folder
mkdir -p ~/templates/eslint

# save both configs
cp eslint.config.js ~/templates/eslint/eslint.jsx.config.js
cp eslint.config.js ~/templates/eslint/eslint.tsx.config.js
```

Every new project, just copy the right one:

```bash
# for JSX project
cp ~/templates/eslint/eslint.jsx.config.js ./eslint.config.js

# for TSX project
cp ~/templates/eslint/eslint.tsx.config.js ./eslint.config.js
```

---

### Summary

|Project type|Extra install needed|Parser|
|---|---|---|
|`.jsx`|`eslint-plugin-react globals`|default|
|`.tsx`|above + `@typescript-eslint/parser @typescript-eslint/eslint-plugin`|`@typescript-eslint/parser`|

The only difference between JSX and TSX config is the TypeScript parser — everything else is the same. Save them as templates and you'll never set this up from scratch again.

**Yes, fully.** VS Code reads the exact same `eslint.config.js` file.

---

### How it works in VS Code

Just install the **ESLint extension** in VS Code:

```
Ext ID: dbaeumer.vscode-eslint
```

That's it. VS Code will automatically pick up your `eslint.config.js` and show the same errors/warnings as Neovim.

---

### One thing to check

Make sure your VS Code `settings.json` has ESLint enabled for JSX/TSX files:

```json
{
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "typescript",
    "typescriptreact"
  ],
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  }
}
```

---

### Bottom line

|Tool|Config file it reads|
|---|---|
|Neovim (eslint LSP)|`eslint.config.js` ✓|
|VS Code (ESLint ext)|`eslint.config.js` ✓|
|Terminal (`npx eslint .`)|`eslint.config.js` ✓|

Your `eslint.config.js` is not Neovim-specific — it's a standard ESLint config that works everywhere. Write it once, works in all tools.