## What and why

<!-- What does this change, and why? Link the issue it closes: "Closes #123". -->

## Checklist

- [ ] I followed the [contributing guide](https://github.com/EchoPhase-Project/.github/blob/main/CONTRIBUTING.md).
- [ ] Commit messages follow Conventional Commits; breaking changes are marked (`!` or `BREAKING CHANGE:`).
- [ ] Tests cover what I added or fixed, and the repository's checks pass locally.
- [ ] Docs (README, comments) are updated where behaviour changed.

### Server (skip if not touched)

- [ ] API changes pass `mise run openapi:check`, or the break is intended and explained below.
- [ ] Database model changes come with a migration (`mise run migrations:check` passes).

### Web client (skip if not touched)

- [ ] Works with the keyboard, focus is visible, fields have labels.
- [ ] Checked in the light and the dark theme.
- [ ] New strings are in the English locale files, with an English fallback in the code.
- [ ] Animations respect `prefers-reduced-motion`.

## Notes

<!-- Optional: screenshots, things left for later, anything reviewers should know. -->
