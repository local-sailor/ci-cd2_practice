# FizzBuzz Terminal

A tiny terminal-style FizzBuzz in the browser, written in TypeScript. Black background, white text. Type a number and press Enter. Enter `0` to quit, then press **Run** to start again.

## Run it

Requires Node.js.

```bash
npm install
npm start
```

It prints the link when it's ready: http://localhost:8000/src/index.html (opening `http://localhost:8000/` redirects there). To use another port, run `PORT=3000 npm start`.

## Scripts

| Command | What it does |
|---|---|
| `npm start` | Build once, then serve on port 8000 |
| `npm run build` | Compile `src/*.ts` to `dist/` |
| `npm run watch` | Recompile whenever a `.ts` file changes |
| `npm run serve` | Serve without building |
| `npm run typecheck` | Type-check `src/` and `tests/` without building |
| `npm run lint` | Lint and format-check with Biome |
| `npm run lint:fix` | Apply Biome's safe fixes |
| `npm test` | Build, then run the Vitest suite |
| `npm run test:watch` | Re-run tests as you edit |
| `npm run ci` | Everything CI runs: typecheck, lint, test |

## CI

`.github/workflows/ci.yaml` runs on every push and pull request: `npm ci`, then `typecheck`, `lint`, and `test`, cheapest check first. Run `npm run ci` before pushing to see what GitHub will see.

For live editing, run `npm run watch` and `npm run serve` in two terminal tabs, then refresh the page after each save.

## Layout

```
src/
  index.html     the page
  styles.css     the page's stylesheet (black background, white text)
  404.html       shown for pages that don't exist (its CSS is inline on purpose, see the comment in the file)
  main.ts        terminal behavior: input, output, Run button
  fizzbuzz.ts    the FizzBuzz logic, no browser code
dist/            compiled JavaScript (generated, git-ignored)
tests/           Vitest tests (logic, terminal behavior, dev server)
scripts/
  serve.mjs      dev server: folders serve their index.html, missing pages show src/404.html, only src/ and dist/ are served
.github/workflows/ci.yaml   the CI pipeline
biome.json       linter and formatter settings
package.json     scripts and dependencies
tsconfig.json    TypeScript compiler settings (tests/tsconfig.json for type-checking tests)
```

The page has to be served over http. Opening `index.html` directly as a file won't work, because browsers block module scripts on `file://`.
