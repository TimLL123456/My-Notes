## Step 1: Get the latest `main`
1) Go to your project folder:
```bash
cd path/to/your-repo
```

2) Confirm you’re in a Git repo and see what’s happening:
```bash
git status
```
`git status` shows what files changed and which branch you are on.

3) Switch to `main` and update it:
```bash
git switch main
git pull
```
`git pull` fetches changes from the remote and merges them into your current branch.

## Step 2: Create a branch for one feature
1) Create and switch to a new branch (example feature: “Export CSV”):
```bash
git switch -c feature/export-csv
```
GitHub Flow recommends creating a branch for each change so you can work without affecting the default branch.[2][1]

2) (Optional) Verify you’re on the new branch:
```bash
git status
```
This helps beginners avoid accidentally committing to `main`.

## Step 3: Make changes and commit (save progress)
1) Edit code as usual, then check what changed:
```bash
git status
```
This shows what Git sees as modified/untracked.

2) Stage the files you want to include in the next “snapshot”:
```bash
git add .
```
`git add` prepares changes to be included in the next commit.

3) Create a commit with a clear message:
```bash
git commit -m "Add CSV export for expenses"
```
A commit records your staged snapshot into the project history.

4) Repeat steps (edit → add → commit) as you continue, so your feature is built in small checkpoints.

## Step 4: Push your branch to GitHub
1) Push the new branch (first time only, use `-u`):
```bash
git push -u origin feature/export-csv
```
Git’s cheat sheet shows `git push -u origin <name>` for pushing a branch you’ve never pushed before.

2) Next pushes can be just:
```bash
git push
```
Once tracking is set, `git push` pushes the current branch to its tracking branch.

## Step 5: Open a Pull Request (PR)
1) On GitHub, open a PR from `feature/export-csv` into `main`.
2) A PR is how you propose merging a branch into another branch and keep discussion/review attached to the change.

## Step 6: Merge the PR safely
1) After checks/review, merge the PR so your branch changes appear on `main`.
2) GitHub supports multiple merge methods (merge commit / squash / rebase), depending on repo settings and what history style you want.

## Step 7: Sync `main` and clean up
1) Update your local `main` after merge:
```bash
git switch main
git pull
```
This ensures your local `main` matches the merged result on the remote.

2) Delete the local feature branch (only after it’s merged):
```bash
git branch -d feature/export-csv
```
This keeps your local branch list clean.

## Step 8: (Recommended) Tag your demo version
When `main` reaches “demo-ready”, add a tag so you can always return to the exact demo code:
```bash
git tag v0.1.0-demo
git push origin v0.1.0-demo
```
Git can push tags to the remote so teammates/CI can reference the same demo build.