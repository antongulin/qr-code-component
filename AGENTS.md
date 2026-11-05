# AGENTS.md - qr-code-component

Repository contract for any AI coding agent working here. Read this file, and the shared
workflow it links, before editing.

This file adapts the DOX framework from `agent0ai/dox` at revision
`765ae4ac02cc884eefcd41a3d0f71941721adb89` (retrieved 2026-11-05). The upstream MIT notice is
kept verbatim in `docs/dox-LICENSE.txt`.

## Purpose

A single-page QR code generator built with Create React App. `src/App.js` renders a `react-qr-code`
value from user input and offers copy-to-clipboard and PNG download through `html2canvas`, with
`react-toastify` feedback. This is a small public portfolio app, not a library anyone installs.

The built site is published from the `gh-pages` branch to
`https://antongulin.github.io/qr-code-component/` (GitHub Pages, project path `/qr-code-component/`).
`package.json` `homepage` is what sets that base path.

The repository is normally **archived** on GitHub. For an authorized publication, temporarily
unarchive it only when necessary, and restore and verify the original archive state afterward.
Reuse existing task authorization; preserve archive state during local-only work.

## Ownership

Maintained by Anton Gulin (`i@anton.qa`, https://anton.qa). Follow Anton's task scope and standing
publication and merge authority in the shared workflow. The public identity in metadata, README, and
attribution strings is **Anton Gulin**; preserve historical Git authorship.

## Local Contracts

Small, flat tree. The files that carry the contracts:

- `AGENTS.md` - this contract.
- `docs/dox-LICENSE.txt` - verbatim MIT notice for the DOX framework text adapted here.
- `package.json` - npm metadata, the `homepage` deploy base path, and the four CRA scripts
  (`start`, `build`, `test`, `eject`). Dependencies are React 18, `react-scripts` 5.0.1,
  `react-qr-code`, `html2canvas`, `react-toastify`, Testing Library packages, and `web-vitals`.
- `package-lock.json` - committed, lockfile version 3. It must stay in sync with `package.json`;
  dependency changes need explicit authorization.
- `src/App.js` - the app: generate, copy as image, download as PNG, clear, and theme handling.
- `src/index.js`, `src/reportWebVitals.js`, `src/setupTests.js` - CRA entry point and scaffolding.
- `public/index.html` - page template. Asset references use `%PUBLIC_URL%`, which the build fills
  from the deploy base path.
- `.github/workflows/build-deploy.yml` - builds with `npm ci` and `npm run build`, uploads `./build`,
  then publishes it to `gh-pages`.
- `.github/workflows/code-review.yml` - calls the shared Robin review workflow
  (`antongulin/robin/.github/workflows/review.yml@main`).
- `.gitignore` - ignores `node_modules/`, `build/`, `coverage/`, and local env files.
- `README.md` - human setup instructions and the live demo link.

Configuration and side effects:

- `homepage` is a URL, but Create React App uses only its pathname when `PUBLIC_URL` is unset.
  Changing the host therefore does not change the built asset base path as long as the
  `/qr-code-component/` path stays the same. A supplied `PUBLIC_URL` overrides `homepage` entirely.
- `npm run build` writes to `build/`, which is gitignored. No environment file is required, and the
  deploy job uses only `GITHUB_TOKEN`. Never commit secrets or print them into prompts or logs.

## Work Guidance

- Inspect the real files before changing them. Most tasks here change one URL, one scalar, or one
  workflow input; keep the diff that small.
- Keep dependency and lockfile bytes untouched unless the task is explicitly about dependencies.
  Release engineering, upgrades, and installs are separate work.
- GitHub Actions: new or changed jobs use the standard Ubicloud runner, `runs-on:
  ubicloud-standard-2`. The existing build-and-deploy workflow still uses `ubuntu-latest` with the
  retired `actions/upload-artifact@v3` and `actions/download-artifact@v2` actions; migrating it is
  separate, separately authorized work, not a side effect.
- The Robin `review` job takes a `runner` input. Its contract is a JSON-encoded string, so the label
  is written as `'"ubicloud-standard-2"'` (quoted inside quoted), not as a bare label.
- The Robin caller requires `actions: read`, `contents: read`, and `pull-requests: write`.
  Keep these permissions aligned with the reusable workflow.
- Merge strategy: squash by default for one cohesive PR. Verify permitted merge methods and
  effective branch gates before merging; preserve repository settings and protections.
- Shared workflow rules are not duplicated here. Read `~/.agents/instructions/WORKFLOW.md`, or
  https://github.com/antongulin/baseline/blob/main/baseline/02-agents.md when that file is absent.

## Verification

Run only what the change can break.

- `npm start` - development server on http://localhost:3000. It needs an install first; a fresh
  checkout has no `node_modules`. `homepage` still sets the `%PUBLIC_URL%` base path in
  development.
- `npm run build` - production build into `build/`. Confirms the manifest, the homepage base path,
  and the source still compile.
- `npm test` - starts the CRA Jest runner. The repository ships no test files yet, so it does not
  currently exercise app behavior.
- `python3 -c "import json; json.load(open('package.json'))"` - confirms the manifest still parses
  after a metadata edit.
- `git diff --check` - catches whitespace damage.
- CI: `Build & deploy` runs on push and pull request to `main`. Its Build job depends on the retired
  `upload-artifact@v3`, so a failing run may reflect the workflow, not the app. Verify current run
  results before claiming success, and verify the live demo URL rather than assuming a deploy.

## DOX discipline

- `AGENTS.md` files are binding contracts for their subtrees. Before editing, read this root and
  every applicable child contract; the nearest contract adds local details without weakening DOX.
- After meaningful changes, reconcile affected contracts, file indexes and human documentation.
  Keep stable rules here and execution evidence in task records; remove stale instructions.
- Add a child only for a durable ownership boundary. Its sections are Purpose, Ownership, Local
  Contracts, Work Guidance, Verification, and Child DOX Index; the parent indexes each direct child.
- Before closeout, recheck the changed paths and affected parent/child indexes, run relevant existing
  checks, and report documents left unchanged with the reason.

## Child DOX Index

None. The tree is flat enough that this root file is the whole contract.
