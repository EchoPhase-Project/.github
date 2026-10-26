# Contributing to EchoPhase

Thank you for your help with EchoPhase. This guide contains the rules that
apply to all repositories of the project. Each repository also has its own
guide for its code:

| Repository | Contents | Guide |
|---|---|---|
| [server](https://github.com/EchoPhase-Project/server) | API, realtime gateway, workflows (.NET) | [CONTRIBUTING](https://github.com/EchoPhase-Project/server/blob/main/CONTRIBUTING.md) |
| [webapp](https://github.com/EchoPhase-Project/webapp) | The web client (SolidJS) | [CONTRIBUTING](https://github.com/EchoPhase-Project/webapp/blob/main/CONTRIBUTING.md) |
| [charts](https://github.com/EchoPhase-Project/charts) | Helm chart and Docker Compose | [CONTRIBUTING](https://github.com/EchoPhase-Project/charts/blob/main/CONTRIBUTING.md) |
| [deploy](https://github.com/EchoPhase-Project/deploy) | The EchoPhase instance of the project (Flux) | [CONTRIBUTING](https://github.com/EchoPhase-Project/deploy/blob/main/CONTRIBUTING.md) |

When you contribute, you agree that the project releases your contributions
under its [BSD 3-Clause License](https://github.com/EchoPhase-Project/server/blob/main/LICENSE).

## How you can help

- **Report a bug.** Open an issue in the applicable repository. Tell what you
  did, what you expected, and what occurred. Versions (server, webapp, chart)
  and logs help. If you do not know the applicable repository, use
  [server](https://github.com/EchoPhase-Project/server/issues).
- **Suggest a feature.** Open an issue before you write code. Then we can
  agree on the method.
- **Repair or make something.** For a small fix, you can open a pull request
  immediately. For a larger change, write a comment on the issue first.
- **Translate** the web client. English is the source language. Translators
  write the other languages in Weblate. Refer to the guide of the webapp.
- **Report a security problem** privately. Do not report it in a public
  issue. Refer to [SECURITY.md](SECURITY.md).

## Preparation

The project pins the tool versions with [mise](https://mise.jdx.dev). Thus,
your computer, CI, and the release pipelines use the same versions.

```sh
mise install --locked     # install the tools of mise.lock
mise tasks                # show the tasks that you can run
```

The guide of each repository tells which checks to run before a pull request.
CI runs the same checks on the pull request.

## How to make a change

1. Fork the repository. Make a branch from `main`.
2. Make your change. Add tests for the behaviour that you add or repair.
3. Run the checks of the repository.
4. Open a pull request against `main`. Complete the template.

Make only one change in each pull request. It is easier to examine and to
revert unrelated fixes when they are in separate pull requests.

### Commit messages

Commit messages follow [Conventional Commits](https://www.conventionalcommits.org).
CI examines them with [cocogitto](https://docs.cocogitto.io). The versions and
the release notes come from the commit messages, thus the type is important:

```text
feat(cli): user lock with an expiry
fix: sessions list shows the device for Edge
refactor(api): one mapping from error codes to HTTP statuses
docs: how to run the dev server against a local API
```

- Use `feat` for a new capability and `fix` for a bug fix. Use `perf`,
  `refactor`, or `revert` for other code changes. Use `docs`, `test`, `ci`,
  `build`, `chore`, or `style` for all other changes.
- The subject tells what changes. Write it in lower case, without a full stop.
  If necessary, write a body that tells why.
- If a change is incompatible for users or API clients, add `!` (`feat!: …`).
  Alternatively, add a `BREAKING CHANGE:` footer that tells how to adapt.

### Releases

The maintainers release each repository with a tag `vX.Y.Z`. The tag
publishes the images, the API contract, or the chart to
`ghcr.io/echophase-project`, and makes a GitHub release. The `appVersion` of
the chart tells which release of server and webapp the chart runs.

## Code of conduct

All persons who take part in EchoPhase must obey the
[Code of Conduct](CODE_OF_CONDUCT.md) (Contributor Covenant 2.1). To report
unacceptable behaviour, do the steps in that document.

## Questions

Open an issue in the repository that your question is about.
