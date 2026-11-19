# Git Cheat Sheet

Commands from the SYPPRE lesson/exercise. Examples from this repo
(`nnimmervoll/norbert-nimmervoll-personal-info`).

## git clone

Makes a local copy of an existing remote repo, with full history and the `origin` link.
Done once, before anything else works.

```powershell
git clone https://github.com/nnimmervoll/norbert-nimmervoll-personal-info
```

Creates the folder + `.git`, so `git status` already knows `main` and `origin/main`.

## git status

Shows untracked / modified / staged files and how local branch compares to the remote.
Only looks at tracked files — a new never-added file is not checked for changes and can't be
committed or pushed yet.

```powershell
git status
```

After `git add .\index.html`:

```
Changes to be committed:
        new file:   index.html
```

Newly staged, and obviously not listed under "Untracked files" anymore. Run it after every
step — it says what to do next.

## git add

Starts tracking a file / puts its current content in the staging area so it's part of the
next commit. Nothing is written to the repo yet.

```powershell
git add .\index.html   # one file
git add .              # everything in this folder that isn't ignored
```

First only `index.html`, to see untracked vs staged; then `git add .` for `style.css`,
images and the `status*.txt` docs.

## git commit

Writes the staged content into the repo as a snapshot with a message. Says *what* changed
and *why*.

```powershell
git commit -m "Adding first iteration of index.html"
git commit -am "Fixing the header spacing in style.css"   # -a stages tracked, modified files first
```

Output: `[main d8d9a76] Adding first iteration of index.html` / `1 file changed, 25 insertions(+)` —
`d8d9a76` is the commit hash.

## git push

Sends local commits to the remote so they're on GitHub. Commits only — never untracked or
merely staged files, which is why files can still show as untracked after a successful push.

```powershell
git push
```

`Your branch is ahead of 'origin/main' by 1 commit.` becomes `Your branch is up to date with
'origin/main'.`

## git pull

Fetches remote commits and merges them into the local branch, so local and GitHub don't drift
apart. Run before starting work, especially with more than one machine.

```powershell
git pull
```

Brings someone else's `README.md` change into local `main` before my own commits, so the push
isn't rejected.

## git log

Lists commits on the current branch, newest first: hash, author, date, message.

```powershell
git log              # full history, pager (q to quit)
git log --oneline -5 # one compact line per commit, 5 most recent
```

`git log --oneline -2`:

```
8ce995f Committing all the other files relevant for correctly displaying index.html; ...
d8d9a76 Adding first iteration of index.html
```

## Order of the workflow

`clone` (once) → `pull` → edit → `status` → `add` → `commit` → `push`