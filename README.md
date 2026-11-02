# GitBasics

A small practice repository for learning core Git concepts: committing, branching, merging, and resolving merge conflicts. The Python scripts are just simple content to experiment with. The commit history is the real learning material.

## Repository contents

| File | Description |
|---|---|
| `fun.py` | Main practice script. Its lines were edited on several branches to produce merge conflicts. |
| `fun_2.py` | Second script, used for a branch and merge exercise (`feature/Number2`). |
| `fun_3.py` | Third script, added on a separate branch. |
| `Git_Revision_Notes.pdf` | Short revision notes on Git, made for interview prep. |

## What this repo demonstrates

- **Basic commits**: creating files and committing changes.
- **Feature branches**: for example `feature/Number2` and `feature/merge-conflict`.
- **Clean merges**: branches that touched different files merged without issues.
- **Merge conflicts**: branches that changed the same lines of `fun.py`, which had to be resolved by hand.
- **Conflict resolution strategies**: for example, keeping the current branch's logic (see commit `dad5a69`).

Run `git log --oneline --graph --all` to see the branching and merging history.

## Getting started

```bash
git clone <your-repo-url>
cd GitBasics
python fun.py
```

Requires Python 3 and Git.

## Practice: create your own merge conflict

```bash
# 1. Create a branch and change line 2 of fun.py
git checkout -b feature/conflict-test
# edit line 2, then:
git commit -am "Change line 2 on feature branch"

# 2. Go back to main and change the SAME line differently
git checkout main
# edit line 2 differently, then:
git commit -am "Change line 2 on main"

# 3. Merge. This triggers a conflict.
git merge feature/conflict-test
```

Git will mark the conflict in the file:

```
<<<<<<< HEAD
your current branch's version
=======
the incoming branch's version
>>>>>>> feature/conflict-test
```

To resolve it:

1. Edit the file to the final version you want and delete the marker lines.
2. Run `git add <file>`.
3. Run `git commit` to complete the merge.

To cancel the merge instead, run `git merge --abort`.

## Quick reference

| Situation | Result |
|---|---|
| Fast-forward merge | No new commit. The branch pointer just moves forward. |
| Clean merge of diverged branches | Git creates a merge commit automatically. |
| Merge with conflicts | You resolve the conflicts, then commit the merge yourself. |

Useful commands:

```bash
git status                       # see conflicted files (marked UU)
git log --oneline --graph --all  # visualize history
git merge --no-ff <branch>       # force a merge commit
git merge --abort                # cancel a merge in progress
```

## Notes

See `Git_Revision_Notes.pdf` for a condensed revision sheet.
