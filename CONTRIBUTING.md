# Contributing to EchoPhase

Thank you for helping with EchoPhase. This guide covers every repository of
the project; each repository's README has its own setup and commands.

By contributing, you agree that your contributions are released under the
project's [BSD 3-Clause License](https://github.com/EchoPhase-Project/server/blob/main/LICENSE).

## Ways to help

- **Report a bug.** Open an issue in the repository it is about, with what you
  did, what you expected and what happened instead. Versions (server, webapp,
  chart) and logs help. Not sure where it belongs? Use
  [server](https://github.com/EchoPhase-Project/server/issues).
- **Suggest a feature.** Open an issue first, before writing code, so we can
  agree on the approach.
- **Fix or build something.** Small fixes can go straight to a pull request;
  for anything larger, comment on the issue first.
- **Translate.** The web client is in English, Russian and Romanian; see
  [Translations](#translations).
- **Report a security problem** privately, never in a public issue: see
  [SECURITY.md](SECURITY.md).

## Repositories

| Repository | What | Stack |
|---|---|---|
| [server](https://github.com/EchoPhase-Project/server) | API, realtime gateway, workflows | .NET 10, PostgreSQL, ScyllaDB, Valkey |
| [webapp](https://github.com/EchoPhase-Project/webapp) | The web client | SolidJS, Vite, TypeScript |
| [charts](https://github.com/EchoPhase-Project/charts) | Helm chart and Docker Compose | Helm |
| [deploy](https://github.com/EchoPhase-Project/deploy) | The project's own instance | Flux, SOPS |

## Getting set up

Tools are pinned with [mise](https://mise.jdx.dev): the same versions on your
machine, in CI and in the release pipelines.

```sh
mise install --locked     # the tools of mise.lock
mise tasks                # what you can run
```

Then follow the README of the repository:

- **server:** `mise run test`, `mise run lint` (`mise run format` fixes
  style), `mise run openapi:check` when you change the API,
  `mise run migrations:add <name>` when you change the database model.
- **webapp:** `mise run install`, then `mise run dev` (it proxies `/api` to a
  server at `API_TARGET`, by default `http://localhost:8080`). Before a pull
  request, `mise run check`: contract types, type check, lint, formatting,
  tests and build.
- **charts:** `helm lint charts/echophase` and `helm template` with the
  required secrets set (see the README).

## Making a change

1. Fork the repository and create a branch from `main`.
2. Make your change, with tests for behaviour you add or fix.
3. Run the checks of that repository (above). CI runs the same ones on your
   pull request.
4. Open a pull request against `main` and fill in the template.

Keep a pull request to one change: unrelated fixes are easier to review and
to revert as separate pull requests.

### Commit messages

Commits follow [Conventional Commits](https://www.conventionalcommits.org),
checked in CI by [cocogitto](https://docs.cocogitto.io). Versions and release
notes are made from them, so the type matters:

```text
feat(cli): user lock with an expiry
fix: sessions list shows the device for Edge
refactor(api): one mapping from error codes to HTTP statuses
docs: how to run the dev server against a local API
```

- `feat` a new capability, `fix` a bug fix; `perf`, `refactor`, `revert` other
  code changes; `docs`, `test`, `ci`, `build`, `chore`, `style` the rest.
- The subject says what changes, in lower case, without a full stop. The body,
  when needed, says why.
- A change that breaks users or API clients gets a `!` (`feat!: …`) or a
  `BREAKING CHANGE:` footer explaining how to adapt.

To check messages as you commit, install [cocogitto](https://docs.cocogitto.io)
and run `cog verify "<message>"`; in server, `cog install-hook commit-msg`
installs a hook that does it for every commit.

### API changes (server)

The API contract (`openapi.json`) may not break clients within a release
series: before 1.0, a minor version (`0.2.x`). `mise run openapi:check`
compares your change with the latest release of its series. Breaking it on
purpose is described in the server README, under "Breaking API changes".

When the contract changes, the webapp regenerates its types from it
(`mise run gen:api`) in a pull request of its own.

### Database changes (server)

Change the model, then add a migration: `mise run migrations:add <name>`.
`mise run migrations:check` fails when the model has changes no migration
covers. Never edit a migration that has been released; add a new one.

## Web client guidelines

### Accessibility

The web client should work with a keyboard, a screen reader and at any zoom.
For changes to the interface:

- every interactive element is reachable and usable with the keyboard, with a
  visible focus;
- form fields have labels, and errors are tied to their field;
- colour is never the only signal (state, errors, links);
- colours come from the theme tokens (`src/shared/styles/tokens.scss`), whose
  contrast `palette.test.ts` checks in both themes;
- animations respect `prefers-reduced-motion`;
- native elements (`button`, `a`, `dialog`) before custom ones; ARIA only
  where HTML has nothing.

Check new or changed screens in both themes, light and dark.

### Translations

Every string the user sees goes through the translation files in
`src/static/locales/`: `<lang>.json` for the whole site, `<page>.<lang>.json`
for one page. English is the source.

When you add or change a string, add it to the file of every language.
`locales.test.ts` fails when a language lacks a key the English file has. If
you do not speak a language, copy the English text there and say so in the
pull request; translators replace it.

## Code of conduct

Be respectful and constructive. Critique the code, not the person; assume good
intent; help newcomers. Harassment or abuse of any kind is not tolerated, and
maintainers may remove comments, close issues or block accounts that cross
that line.

## Questions

Open an issue in the repository your question is about.
