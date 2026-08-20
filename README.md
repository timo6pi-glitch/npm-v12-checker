# npm v12 Install-Script Checker

A free, client-side tool: paste your `package.json`, find out which of your dependencies are known to rely on an npm install script — before npm v12 silently skips it on you.

**Live demo: https://timo6pi-glitch.github.io/npm-v12-checker/**

## What changed

npm v12 (shipped 2026-07-08) disables `preinstall`/`install`/`postinstall` scripts by default, as a response to real supply-chain attacks that abused them. The part that's easy to miss: `npm ci` does not fail when a script is blocked — it silently skips it and exits 0. If a dependency needs its install script to actually work (compiling a native addon, downloading a prebuilt binary), your CI can stay green while that dependency is quietly broken.

## Why it matters

Packages like `sharp`, `bcrypt`, `canvas`, `sqlite3`, `esbuild`, `node-sass`, `puppeteer`, `playwright`, `cypress`, and `husky` (among others) commonly rely on install scripts. If your project depends on one of these — directly or as a dev dependency — it's worth checking before you upgrade to npm v12.

## How to use it

Open the live demo, paste or upload your `package.json`, and click Analyze. You'll get a list of dependencies known to rely on an install script, each marked `NEEDS_VERIFICATION` with the specific reason.

## Privacy

Everything runs in your browser. Your `package.json` is never uploaded or sent anywhere — this page makes no network requests. You can verify this yourself: view source, it's a single unminified HTML file.

## Limitations

- It only checks against a curated list of commonly-affected packages — not your transitive dependencies, and not every package that could be affected.
- A package **not** on the list is not proof your project is safe under npm v12 — only that this tool has no evidence either way.
- Always verify with a real npm v12 environment (`npm ci`) before shipping.

This is a small, free tool, not a company and not a funded product yet — see the in-page note about a possible future CI-integration tier, which does not exist yet.

## Source / reference

- [npm v12 changelog](https://docs.npmjs.com/cli/v12/using-npm/changelog/)

## Live demo

https://timo6pi-glitch.github.io/npm-v12-checker/
