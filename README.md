# .github

Shared defaults and standards for my repositories.

- `.github/`: default PR and issue templates, used by any repo without its own, plus the
  reusable `pr-title` workflow.
- `standards/`: the files every repo gets. `ruleset-main.json` can also be imported by hand in
  **Settings → Rules → Rulesets → New ruleset → Import a ruleset**.
- `apply-standards.sh` (kept outside this repo): applies `standards/repo-settings.json` and
  `standards/ruleset-main.json` to one repo.

## Add a repo

1. On a branch, copy `standards/pr-title-caller.yml` to `.github/workflows/pr-title.yml` and
   `standards/dependabot.yml` to `.github/dependabot.yml`. Open a PR titled
   `chore: add repo standards`.
2. Once the `pr-title / lint` check has run on that PR, run
   `./apply-standards.sh <repo>` (needs `gh` and `jq`), or import `standards/ruleset-main.json`
   by hand.
3. Squash-merge the PR.
4. In **Settings → Advanced Security**, turn on Dependabot alerts and security updates.

## Change a rule

Edit `standards/`, then re-run the script for each repo. Changes made in a repo's Settings page
are overwritten on the next run.

When someone else joins a repo, set `required_approving_review_count` to `1`.

## Keep Actions minutes low

Run checks on `pull_request` only. Set `concurrency` with `cancel-in-progress` and
`timeout-minutes`. Use `paths-ignore` for docs-only changes, cache dependencies, and use Linux
runners.
