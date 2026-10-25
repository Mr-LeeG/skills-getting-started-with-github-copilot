# Setting Up a GitHub Skills Lab in Local VS Code (macOS)

A repeatable guide for copying a GitHub Skills exercise to your own account, cloning it, and working on it in local VS Code instead of a Codespace.

**Example used in this guide:** *Getting Started with GitHub Copilot*
**GitHub username:** `Mr-LeeG` (replace with your own if different)

---

## Prerequisites

Check that these are in place before you start.

| Requirement | How to check |
|---|---|
| Git installed | Run `git --version` in a terminal |
| VS Code installed | Open it from Applications |
| Signed in to GitHub in VS Code | Accounts icon (bottom-left of VS Code) |
| GitHub Copilot enabled (for Copilot labs) | Copilot icon in the VS Code status bar |
| `code` shell command (optional) | Run `code --version`; see Step 6 if it's missing |

---

## Step 1: Find the official exercise, not someone else's copy

GitHub Skills exercises live under the **`skills`** organization:

```
https://github.com/skills/<exercise-name>
```

Example: `https://github.com/skills/getting-started-with-github-copilot`

> ⚠️ **Don't clone someone else's copy** (for example, `github.com/petender/skills-...`). You can't push to it, so the exercise checks won't run for you. If the README says *"Hey <someone-else>!"*, you're on another person's copy.

---

## Step 2: Copy the exercise to your account

1. On the official exercise page, right-click **Copy Exercise** and open it in a new tab. (On older exercises the button may say **Use this template → Create a new repository**.)
2. Fill in the form:
   - **Owner:** your personal account (`Mr-LeeG`)
   - **Repository name:** leave the default (for example, `skills-getting-started-with-github-copilot`)
   - **Visibility:** **Public**, because private repos use your GitHub Actions minutes
3. Click **Create repository**.

> 💡 Use **Copy Exercise** or the template, not **Fork**. Forks have GitHub Actions turned off by default, so the exercise won't advance.

---

## Step 3: Wait for the exercise to be prepared

1. Wait about **20 seconds**, then refresh your new repo's page.
2. Confirm it's ready:
   - The README greets you by name (*"Hey Mr-LeeG!"*), **or**
   - An issue appears under the **Issues** tab with the step-by-step instructions.

---

## Step 4: Copy your repo's clone URL

On **your** repo page, click **Code → HTTPS** and copy the URL. It should look like this:

```
https://github.com/Mr-LeeG/skills-getting-started-with-github-copilot.git
```

> ⚠️ Don't use a browser URL that contains `/tree/main`. Use the clone URL from the **Code** button.

---

## Step 5: Clone the repo

### Option A: From the VS Code UI
1. Press `Cmd+Shift+P` and run **Git: Clone**.
2. Paste your clone URL and press Enter.
3. Choose a parent folder (for example, `~/Documents/VS Code`).
4. Click **Open** when prompted.

### Option B: From the terminal
```bash
cd ~/Documents/"VS Code"
git clone https://github.com/Mr-LeeG/skills-getting-started-with-github-copilot.git
cd skills-getting-started-with-github-copilot
```

---

## Step 6: Open the repo folder itself in VS Code

Open **only the repo folder**, not its parent folder, so the terminal, Source Control, and Copilot all work against the right repo.

- **From the menu:** **File → Open Folder…** → select `skills-getting-started-with-github-copilot` → **Open**
- **From the terminal (inside the repo):**
  ```bash
  code .
  ```

**If you see `zsh: command not found: code`:**
1. In VS Code, press `Cmd+Shift+P`.
2. Run **Shell Command: Install 'code' command in PATH**.
3. Close and reopen the terminal.
4. Until then, you can use `open -a "Visual Studio Code" .`

**How to tell it worked:** the Explorer shows the repo's files (`.github`, `src`, `README.md` …) at the top level, not nested under another folder.

---

## Step 7: Verify the remote points to your repo

In the VS Code terminal (`` Ctrl+` ``), run:

```bash
git remote -v
```

You should see **your** username:

```
origin  https://github.com/Mr-LeeG/skills-getting-started-with-github-copilot.git (fetch)
origin  https://github.com/Mr-LeeG/skills-getting-started-with-github-copilot.git (push)
```

**If you see `fatal: not a git repository`:** the terminal is in the parent folder. `cd` into the repo folder and try again.

**If you see someone else's username:** you cloned the wrong repo. Delete that folder and go back to Step 2.

---

## Step 8: Set up Python (Python-based labs only)

If the repo has `requirements.txt`, create a virtual environment and install the dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

---

## Step 9: Work through the exercise

1. Open your repo on GitHub and read the instructions in the **Issues** tab or the README.
2. When a step says **"launch a Codespace,"** do that work locally in VS Code instead.
3. After each step, commit and push:
   ```bash
   git add .
   git commit -m "Complete step X"
   git push
   ```
   You can also use the **Source Control** panel: commit, then **Sync Changes**.
4. Wait about 20 seconds and refresh GitHub. The next step appears once the check passes.
5. Watch the **Actions** tab on your repo if a step doesn't advance.

---

## Troubleshooting Quick Reference

| Symptom | Cause | Fix |
|---|---|---|
| No **Use this template** / **Copy Exercise** button | You're on someone else's copy | Go to `github.com/skills/<exercise-name>` |
| README greets someone else | Wrong repo | Copy the exercise to your own account (Step 2) |
| `git push` is rejected (permission denied) | Remote points to someone else's repo | Run `git remote -v`; re-clone your own copy |
| `zsh: command not found: code` | VS Code shell command not installed | `Cmd+Shift+P` → **Install 'code' command in PATH** |
| `fatal: not a git repository` | Terminal is outside the repo folder | `cd` into the repo folder |
| Repo appears nested in the Explorer | You opened the parent folder | **File → Open Folder…** and pick the repo folder |
| Exercise doesn't advance after a push | Actions disabled, or the check failed | Check the **Actions** tab; don't use a fork |

> 📝 **Don't use `git remote set-url` to repoint a clone of someone else's copy to your new repo.** A repo made from a template or Copy Exercise starts with fresh history, so the push will be rejected. Always do a fresh clone of your own copy.
