# Contributing to EchoPhase

Thank you for helping with EchoPhase. This guide is what every repository of
the project has in common; each repository has its own guide for its code:

| Repository | What | Its guide |
|---|---|---|
| [server](https://github.com/EchoPhase-Project/server) | API, realtime gateway, workflows (.NET) | [CONTRIBUTING](https://github.com/EchoPhase-Project/server/blob/main/CONTRIBUTING.md) |
| [webapp](https://github.com/EchoPhase-Project/webapp) | The web client (SolidJS) | [CONTRIBUTING](https://github.com/EchoPhase-Project/webapp/blob/main/CONTRIBUTING.md) |
| [charts](https://github.com/EchoPhase-Project/charts) | Helm chart and Docker Compose | [CONTRIBUTING](https://github.com/EchoPhase-Project/charts/blob/main/CONTRIBUTING.md) |
| [deploy](https://github.com/EchoPhase-Project/deploy) | The project's own instance (Flux) | [CONTRIBUTING](https://github.com/EchoPhase-Project/deploy/blob/main/CONTRIBUTING.md) |

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
- **Translate** the web client: English is the source, other languages are
  translated in Weblate (see the webapp's guide).
- **Report a security problem** privately, never in a public issue: see
  [SECURITY.md](SECURITY.md).

## Getting set up

Tools are pinned with [mise](https://mise.jdx.dev): the same versions on your
machine, in CI and in the release pipelines.

```sh
mise install --locked     # the tools of mise.lock
mise tasks                # what you can run
```

The repository's guide says what to run before a pull request; CI runs the
same checks on it.

## Making a change

1. Fork the repository and create a branch from `main`.
2. Make your change, with tests for behaviour you add or fix.
3. Run the repository's checks.
4. Open a pull request against `main` and fill in the template.

Keep a pull request to one change: unrelated fixes are easier to review and to
revert as separate pull requests.

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

### Releases

Each repository is released by its maintainers with a tag `vX.Y.Z`: it
publishes the images, the API contract or the chart to
`ghcr.io/echophase-project`, with a GitHub release. The chart's `appVersion`
says which release of server and webapp it runs.

## Code of conduct

Be respectful and constructive. Critique the code, not the person; assume good
intent; help newcomers. Harassment or abuse of any kind is not tolerated, and
maintainers may remove comments, close issues or block accounts that cross
that line.

## Questions

Open an issue in the repository your question is about.
