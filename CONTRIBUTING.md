# Contributing

Org-wide conventions for Internetworkexpert repositories. INE staff can find the full
standard and the developer cheat sheet in Confluence; questions go to `#all-developers`
on Slack.

## Branch model

Repositories that deploy per environment (services and environment-deployed lambdas) use
three long-lived branches:

```
develop → staging → production   (default branch: production)
```

- Day-to-day work branches off `develop` and PRs back into `develop` (squash merge).
- Promotion between environments is a PR (`develop → staging`, `staging → production`) and
  is **merge-commit only** — never squash or rebase a promotion.
- Emergency fixes: `hotfix/*` from `production`, PR into `production`, then back-merge.
- Libraries, packages, tooling, IaC, and other non-deployed repos use a single `main` branch.

## Short-lived branches

Format: `type/[TICKET-]short-description` — kebab-case description, uppercase Jira key.

Allowed types: `feature`, `fix`, `hotfix`, `chore`, `refactor`, `docs`, `test`.

Examples: `feature/DEV-123-add-dark-mode`, `fix/DEV-456-login-redirect`.

## Commits and PR titles

PRs into `develop` are squash-merged and the PR title becomes the commit message, so titles
must follow [Conventional Commits](https://www.conventionalcommits.org/):

```
type(scope): description [TICKET]
```

Example: `fix(auth): refresh expired OAuth tokens before retry [DEV-1234]`. Use
`[NO-TICKET]` when no Jira ticket exists.
