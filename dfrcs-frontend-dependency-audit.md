## Table 1 — Runtime environment

| Setting | Current | Target | Note |
|---|---|---|---|
| `Dockerfile` base image | `node:25.5.0-slim` | `node:24-slim` (24.21.0) | Node 25 is the odd/Current line and is EOL; 24 is Active LTS |
| `engines.node` | `20.19.2` | `>=24 <25` | Node 20 reached EOL April 2026 |
| `engines.npm` | `10.2.4` | `>=11` | Ships with Node 24 |

The image and `engines` currently disagree. `npm ci` does not enforce `engines` without `engine-strict`, so the mismatch is silent.

---

## Table 2 — Upgrade: dependencies

| Package                   | Current | Target  | Major |
| ------------------------- | ------- | ------- | ----- |
| `@mui/material`           | 5.13.7  | 9.4.0   | yes   |
| `@emotion/react`          | 11.11.1 | 11.14.0 | no    |
| `@emotion/styled`         | 11.11.0 | 11.14.1 | no    |
| `react`                   | 18.2.0  | 19.3.0  | yes   |
| `react-dom`               | 18.2.0  | 19.3.0  | yes   |
| `react-router-dom`        | 6.30.3  | 7.18.4  | yes   |
| `react-select`            | 5.7.3   | 5.10.2  | no    |
| `react-paginate`          | 8.1.3   | 8.3.0   | no    |
| `react-modal`             | 3.16.1  | 3.16.3  | no    |
| `react-collapse`          | 5.1.0   | 5.1.1   | no    |
| `react-day-picker`        | 9.7.0   | 10.0.1  | yes   |
| `react-dropdown`          | 1.11.0  | 2.0.0   | yes   |
| `lodash`                  | 4.17.23 | 4.18.1  | no    |
| `moment`                  | 2.30.1  | 2.31.0  | no    |
| `prop-types`              | 15.7.2  | 15.8.1  | no    |
| `superagent`              | 10.2.3  | 10.3.0  | no    |
| `file-saver`              | 1.3.8   | 2.0.5   | yes   |
| `normalize.css`           | 4.2.0   | 8.0.1   | yes   |
| `ipaddr.js`               | 2.2.0   | 2.5.0   | no    |
| `fs-extra`                | 5.0.0   | 11.4.0  | yes   |
| `rimraf`                  | 2.7.1   | 6.1.3   | yes   |
| `debug`                   | 2.6.9   | 4.4.3   | yes   |
| `yargs`                   | 18.0.0  | 18.2.0  | no    |
| `html-webpack-plugin`     | 5.5.0   | 5.6.8   | no    |
| `mini-css-extract-plugin` | 2.7.6   | 2.10.2  | no    |
| `@babel/runtime`          | 7.27.6  | 8.0.5   | yes   |

`@babel/runtime` alternative: 7.29.9 to remain on Babel 7. It must match the `@babel/*` line chosen in Table 3.

`rc-input-number` (9.5.0) is already current — no change.

---

## Table 3 — Upgrade: devDependencies (build toolchain)

| Package                           | Current | Target  | Major |
| --------------------------------- | ------- | ------- | ----- |
| `webpack`                         | 5.105.0 | 5.111.1 | no    |
| `webpack-cli`                     | 6.0.1   | 7.2.3   | yes   |
| `webpack-dev-server`              | 5.2.2   | 6.0.0   | yes   |
| `webpack-dev-middleware`          | 5.3.4   | 8.3.0   | yes   |
| `babel-loader`                    | 9.2.1   | 10.1.1  | yes   |
| `css-loader`                      | 6.11.0  | 7.1.5   | yes   |
| `style-loader`                    | 3.3.4   | 4.0.0   | yes   |
| `sass`                            | 1.89.2  | 1.104.1 | no    |
| `sass-loader`                     | 16.0.5  | 17.0.1  | yes   |
| `postcss`                         | 8.5.6   | 8.5.28  | no    |
| `postcss-loader`                  | 8.2.0   | 8.2.1   | no    |
| `babel-plugin-module-resolver`    | 4.1.0   | 5.0.3   | yes   |
| `@babel/core`                     | 7.27.4  | 8.0.6   | yes   |
| `@babel/preset-env`               | 7.27.2  | 8.0.6   | yes   |
| `@babel/preset-react`             | 7.27.1  | 8.0.1   | yes   |
| `@babel/plugin-transform-runtime` | 7.27.4  | 8.0.6   | yes   |
| `express`                         | 4.21.2  | 5.2.1   | yes   |
| `connect-history-api-fallback`    | 1.3.0   | 2.0.0   | yes   |
| `nodemon`                         | 3.1.10  | 3.1.14  | no    |

The four `@babel/*` entries move together with `@babel/runtime` or not at all.

`express` and `connect-history-api-fallback` are used only by `bin/server.js` (the `npm run dev` path).

---

## Table 4 — Delete: unused, no code change

Zero references across `src/`, `bin/`, `build/`, `config/`, `server/`.

| Package | Type | Note |
|---|---|---|
| `history` | dependency | |
| `react-height` | dependency | |
| `webpack-sources` | dependency | |
| `json-loader` | dependency | |
| `imports-loader` | dependency | |
| `file-loader` | dependency | superseded by webpack 5 asset modules, already in use |
| `url-loader` | dependency | superseded by webpack 5 asset modules, already in use |
| `cssnano` | dependency | not referenced by any postcss config |
| `react-error-overlay` | devDependency | |
| `cheerio` | devDependency | |

---
## Sequencing constraints

1. `@mui/material` must reach v6 or later before `react` moves to 19. MUI 5 does not declare React 19 support.
2. Every other React consumer in the tree (`react-day-picker`, `react-select`, `react-paginate`, `react-modal`, `react-collapse`, `rc-input-number`, `react-dropdown@2`) already declares React 19 in its peer range.
3. `react-router-dom@7` requires Node >= 20, satisfied by the Node 24 target.
4. Table 4 and Table 5 can be applied independently of any upgrade.

---

## Why the MUI and router jumps are cheap

- MUI surface is four components — `CircularProgress`, `FormControlLabel`, `Snackbar`, `Switch` — plus `createTheme()` called with no arguments. No `makeStyles`, no `withStyles`, no `@mui/styles`, no theme customization.
- Router surface is the classic v6 component API only: `BrowserRouter`, `Routes`, `Route`, `Navigate`, `Outlet`, `Link`, `NavLink`, `useRoutes`, `useNavigate`, `useLocation`. All unchanged in v7.
- The app entry already uses `createRoot` (`src/main.js:2`). All 48 class components keep `defaultProps` and `propTypes` under React 19; no function component uses `defaultProps`.

---

## Security context

`npm audit` reports 36 advisories: 2 critical, 14 high, 14 moderate, 6 low.

Reaching shipped code: `react-router-dom` (open redirect leading to XSS), `lodash` (prototype pollution, `_.template` injection), `postcss`, `svgo`, `brace-expansion`, `undici`. The Table 2 and Table 3 targets clear these.

The remainder sit in the dev and test trees (`shell-quote`, `websocket-driver`, `ws`, `js-yaml`).

The 13-entry `overrides` block in `package.json` is compensating for these transitive pins. Most entries become unnecessary once the direct dependencies move; the `ajv: ^8.18.0` entry in particular is incompatible with the currently installed ESLint 7 tree.

---

## Out of scope

Lint and test tooling is left at current versions and not removed: `eslint` and its config/plugin stack, `karma*`, `mocha`, `chai`, `chai-as-promised`, `sinon`, `sinon-chai`, `babel-plugin-istanbul`, `codecov`, `@testing-library/*`, `husky`, `better-npm-run`.
