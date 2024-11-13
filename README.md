# Testing rules repo

## Branches rules

### Main branch

- Restrict deletions (Only allow users with bypass permissions to delete matching refs.)
- Require linear history (Prevent merge commits from being pushed to matching refs.)
- Require a pull request before merging:
  -- Dismiss stale pull request approvals when new commits are pushed
  -- Required approvals - 1
  -- Require conversation resolution before merging
- Require status checks to pass:
  -- Require branches to be up to date before merging
  -- check-source-branch-for-main (workflow)
- Block force pushes

### Dev branch

- Restrict deletions (Only allow users with bypass permissions to delete matching refs.)
- Require linear history (Prevent merge commits from being pushed to matching refs.)
- Require a pull request before merging:
  -- Dismiss stale pull request approvals when new commits are pushed
  -- Required approvals - 1
  -- Require conversation resolution before merging
- Block force pushes

## Automation Workflows

### branch_rule.enforce-branch-naming.yml

Checks that new branch name created from **main** IS compatible with template `hotfix/**`, new branch created from **dev** IS compatible with template `^(feature|feat|task|issue|fix)/.*$`. If not - delete branch.

### branch_rule_main.restrict-pr.yml

Ensures that PRs to **main** are create only from branches `dev` or `hotfix/**`. If not - dont allow to finish PR.

### branch_rule_main.autorebase-dev.yml

Automatically rebase main onto dev branch after successful merge. Rebase is done by `misto-action-bot` to bypass restriction rules.

### branch_rule_dev.restrict-pr.yml

Ensures that PRs to **dev** are create only from branches which names compatible with template `^(feature|feat|task|issue|fix)/.*$`. If not - dont allow to finish PR.

## Other

Proposal is to use rebase and merge for pull requests to get consistent commit history in fin.
Also we need to determine number of approvals for PRs in main and dev. If i forget something just let me know. In future there will be added other check for success passing PR like deployment, tests, security checks etc.
