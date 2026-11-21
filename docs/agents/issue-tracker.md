# GitHub issue tracker

Issues and specs live in GitHub Issues for `RafyTime/onyx`. Run `gh` from this checkout or pass `--repo RafyTime/onyx`.

- Publish work with `gh issue create --title "..." --body-file <file>`.
- Fetch a ticket with `gh issue view <number> --json number,title,body,labels,comments`.
- List tickets with `gh issue list` and use `--state` and `--label` as needed.
- Comment with `gh issue comment <number> --body-file <file>`.
- Apply or remove a label with `gh issue edit <number> --add-label <label>` or `--remove-label <label>`. See `triage-labels.md` for triage roles.
- Close a ticket with `gh issue close <number> --comment "..."`.

**PRs as a request surface: no.**

## Wayfinding

- Create the map as an issue labeled `wayfinder:map`. Keep its Notes, Decisions-so-far, and Fog in the issue body.
- Create child tickets with `gh issue create --parent <map>` or link existing tickets with `gh issue edit <map> --add-sub-issue <child>`. Label each child `wayfinder:<type>` using `research`, `prototype`, `grilling`, or `task`. If sub-issues are unavailable, add a child to the map's task list and start the child body with `Part of #<map>`.
- Record blockers with `gh api --method POST repos/RafyTime/onyx/issues/<child>/dependencies/blocked_by -F issue_id=<blocker-id>`. Fetch the blocker's database ID with `gh api repos/RafyTime/onyx/issues/<blocker> --jq .id`. If dependencies are unavailable, list blockers near the top of the child body as `Blocked by: #<number>, #<number>`.
- Select the first open, unassigned child in map order whose blockers are all closed. Claim it with `gh issue edit <number> --add-assignee @me` before starting work.
- Resolve the child by posting the answer and closing the issue. Add a short summary and link to the map's Decisions-so-far.
