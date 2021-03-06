# zprint action

## Validations on Push

This actions will check the formatting of the project, using
[boot-fmt](https://github.com/pesterhazy/boot-fmt).

The container configures [zprint](https://github.com/kkinnear/zprint) to search
for configuration files in the current project, allowing you to commit the
formatting rules as part of the project.

For more configuration details, check upstream
[documentation](https://github.com/kkinnear/zprint#how-to-configure-zprint)

Alternatively, there is also [cljfmt](../cljfmt) action available.

## Fixes on Pull Request review

This action provides automated fixes using Pull Request review comments.

If the comment starts with `fix $action_name` or `fix zprint`, a new commit will
be added to the branch with the automated fixes applied.

**Supports**: autofix on push

## Example workflow

```hcl
workflow "on push" {
  on = "push"
  resolves = ["zprint"]
}

# Used for fix on review
# Don't enable if you plan using autofix on push
# Or there might be race conditions
workflow "on review" {
  resolves = ["zprint"]
  on = "pull_request_review"
}

action "zprint" {
  uses = "bltavares/actions/zprint@master"
  # Enable autofix on push
  # args = ["autofix"]
  # Used for pushing changes for `fix` comments on review
  secrets = ["GITHUB_TOKEN"]
}
```
