# Contributing

This repository is a derivative of [renatoworks/3dsvg](https://github.com/renatoworks/3dsvg). Keep the upstream attribution and MIT license in place, and distinguish changes made here from features already present upstream.

## Local setup

Use Node.js 20.9 or newer. The automated checks use Node.js 24.

```bash
npm ci --ignore-scripts
npm run check
```

`npm run check` builds the engine before checking the web workspace. To work on the editor, run `npm run dev:web` after that build. If you change engine code, rebuild it with `npm run build:engine` or run `npm run dev:engine` in a separate terminal.

## Proposing a change

- Describe the problem and how to reproduce it.
- Keep the change focused, and include the output of `npm run check`.
- For editor changes, test the affected interaction or export in a browser and describe the result. Compilation alone does not establish visual correctness.
- Do not include credentials, environment files, or private client assets.

The GitHub Actions workflow checks the engine build and web types on Linux and Windows. It does not publish packages or deploy the application.
