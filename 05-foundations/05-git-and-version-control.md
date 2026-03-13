# Git & Version Control

> **18 questions** — 10 theory, 6 practical, 2 experience

- Git internals: three-tree architecture, branches as pointers, commits as a DAG, SHA-1 hashing
- Rebase vs merge: history readability, conflict effort, bisect usability, shared branch safety
- Interactive rebase: squash, reword, reorder, edit, drop commits
- Cherry-picking: moving commits between branches, ranges, -x flag, risks of duplicate commits
- Bisect: finding regressions via binary search, manual and automated workflows
- Reflog: recovering from reset --hard, failed rebase, dropped stashes, expiry
- Branching models: trunk-based development, GitFlow, GitHub Flow — team size, CI maturity, tagging and release workflows
- PR merge strategies: squash-merge vs merge-commit vs rebase-merge tradeoffs
- Force-push: dangers on shared branches, --force-with-lease, branch protection
- Merge conflict resolution: conflict markers, --ours/--theirs, rerere, minimizing conflicts with small PRs and frequent rebasing
- Monorepo workflows: sparse checkout, shallow/partial clone, CODEOWNERS, path-based CI filtering — and why submodules are rarely the answer

---

## Foundational

<details>
<summary>1. How does Git store data internally — what is the three-tree architecture (working directory, staging area, repository), how are commits structured as a directed acyclic graph, what does it mean that branches are just pointers to commits, and why does Git use SHA-1 hashing for content addressing?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>2. Why would you choose rebase over merge (or vice versa) — how does each strategy affect history readability, conflict resolution effort, the usefulness of git bisect, and what are the dangers of rebasing commits that have already been pushed to a shared branch?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>3. Why do different teams need different branching models — compare trunk-based development, GitFlow, and GitHub Flow in terms of team size, CI maturity, release cadence, and risk tolerance, and explain what signals tell you a team has outgrown its current model?</summary>

<!-- Answer will be added later -->

</details>

## Conceptual Depth

<details>
<summary>4. When and why would you cherry-pick commits instead of merging a branch — what problems does cherry-picking solve, what does the -x flag do and why should you use it, how do you cherry-pick a range of commits, and what are the risks of duplicate commits appearing in your history?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>5. How does git bisect find regressions using binary search — why is this approach faster than scanning commits linearly, what makes a codebase bisect-friendly (and what breaks it), and when would you use manual bisect vs automated bisect with a test script?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>6. What does the reflog track that the regular commit log doesn't — what types of operations does it record, why is it your safety net for recovering from destructive operations like reset --hard and failed rebases, and when does the reflog expire so you can no longer recover?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>7. What are the tradeoffs between squash-merge, merge-commit, and rebase-merge as PR merge strategies — how does each affect commit history cleanliness, blame/bisect accuracy, the ability to revert a PR as a unit, and what strategy works best for different team sizes and workflows?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>8. Why is force-pushing dangerous on shared branches — what exactly happens to other developers' work when you force-push, how does --force-with-lease protect against overwriting someone else's commits, and what branch protection rules should you configure to prevent accidental force-pushes to main?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>9. What are the key challenges of working in a monorepo with Git — why do large repositories cause performance problems, and how do sparse checkout, shallow clone, and partial clone each address different aspects of this problem? When would you use each one, and why are Git submodules rarely the right answer for monorepo workflows?</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>10. How do you approach merge conflict resolution beyond just picking sides — explain what the conflict markers mean (including the base version in diff3 mode), when --ours and --theirs are appropriate, what rerere does and when to enable it, and what practices (small PRs, frequent rebasing) minimize conflicts in the first place?</summary>

<!-- Answer will be added later -->

</details>

## Practical — Daily Git Operations

<details>
<summary>11. Walk through an interactive rebase workflow — show the exact commands to squash the last 5 commits into 2 meaningful ones, reword a commit message, reorder commits, edit a commit to split it into two, and drop a commit entirely. Explain what happens if a conflict arises mid-rebase and how you resolve it or abort.</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>12. Show how to use the reflog to recover from three common disasters — recovering commits after a reset --hard, recovering your branch after a failed interactive rebase, and recovering a dropped stash. Show the exact commands for each scenario and explain how you identify the right reflog entry.</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>13. Walk through resolving a merge conflict step by step — show what the conflict markers look like (including diff3 format), demonstrate resolving with --ours and --theirs for specific files, configure and use rerere to auto-resolve recurring conflicts, and show the commands to complete the merge after resolution.</summary>

<!-- Answer will be added later -->

</details>

## Practical — Repository & Workflow Configuration

<details>
<summary>14. Set up a monorepo for efficient development — show how to configure sparse checkout so a developer only clones the packages they work on, write a CODEOWNERS file that assigns different teams to different directories, and demonstrate path-based CI filtering (only run backend tests when backend/ changes). Show the exact commands and config files.</summary>

<!-- Answer will be added later -->

</details>

## Practical — History & Search

<details>
<summary>15. Show how to force-push safely and configure branch protection — demonstrate the difference between --force and --force-with-lease (and when --force-with-lease can still fail), show how to configure branch protection rules on GitHub/GitLab (required reviews, status checks, no force-push), and what to do when you need to force-push to a shared branch as a last resort.</summary>

<!-- Answer will be added later -->

</details>

<details>
<summary>16. Configure PR merge strategy settings on a repository — show how to set up squash-merge as the default on GitHub/GitLab, configure the default squash commit message template, explain when you'd override the default for specific PRs (e.g., merge-commit for a long-lived feature branch), and how to enforce a consistent strategy across a team.</summary>

<!-- Answer will be added later -->

</details>

---

## Experience-Based Questions

These questions test real-world experience. Prepare by mapping them to your own projects and situations.

<details>
<summary>17. Tell me about a time you recovered from a Git disaster in a team setting — what happened (reset --hard, bad rebase, lost commits, force-push to main), how did you diagnose and fix it, and what safeguards did you put in place afterward?</summary>

<!-- Answer framework will be added later -->

</details>

<details>
<summary>18. Describe a time you set up or changed a team's branching strategy — what was the previous workflow, what problems drove the change, how did you get the team to adopt it, and what was the outcome?</summary>

<!-- Answer framework will be added later -->

</details>
