# Learn Git & GitHub by Building Your Website

Eleven short lessons. Each one teaches one Git/GitHub idea by doing something real to your website.
Every step shows two ways to do it:

- 💻 **Terminal** – the real `git` commands (type them in the Terminal app)
- 🖱️ **GitHub Desktop** – the point-and-click equivalent

Pick one per lesson, or do it with one and peek at the other. They do exactly the same thing, so you can switch any time.

---

## The big picture (read this first)

```
 your folder          staging area           your local history          GitHub
 (files you edit) ──► (changes you picked) ──► (commits on your Mac) ──► (commits online)
                git add              git commit                 git push
                                                  ◄──────────────────────
                                                         git pull
```

| Word | Plain-English meaning |
|------|-----------------------|
| **Repository (repo)** | A project folder that Git is tracking. |
| **Commit** | A saved snapshot of your files, with a message saying what changed. |
| **Staging** | Choosing which changes go into the next commit. |
| **Branch** | A parallel line of work. `main` is the official one; you make side branches to try things safely. |
| **Merge** | Bringing a branch's commits back into another branch. |
| **Remote / origin** | The copy of your repo on GitHub. `origin` is its nickname. |
| **Push / Pull** | Send your commits up to GitHub / bring new commits down from GitHub. |
| **Pull request (PR)** | A GitHub page that says "please merge my branch", where changes can be reviewed first. |
| **Issue** | A to-do item or bug report on GitHub. |

**Git** is the tool on your computer. **GitHub** is the website that hosts your repos online.

---

## Lesson 0 – Set up (about 15 minutes, once)

1. **Make a GitHub account** at github.com. Your username becomes part of your website address, so pick one you like.
2. **Install a code editor.** [VS Code](https://code.visualstudio.com) is free and shows Git changes nicely. (Avoid TextEdit; it can quietly turn code into rich text.)
3. **Put the project somewhere sensible.** Unzip `my-website` and move the folder into your home folder or `Documents`.

💻 **Terminal**

4. Open **Terminal** (Cmd+Space, type "Terminal"). Check Git is installed:
   ```bash
   git --version
   ```
   If a box pops up offering to install "command line developer tools", click **Install**, wait, then run it again.
5. Tell Git who you are (this name and email appear on every commit):
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   git config --global init.defaultBranch main
   ```
   Use the same email as your GitHub account.
6. Let your Terminal log in to GitHub: install the **GitHub CLI** from [cli.github.com](https://cli.github.com) (download the macOS installer), then run:
   ```bash
   gh auth login
   ```
   Choose **GitHub.com → HTTPS → Yes (authenticate Git) → Login with a web browser**, and follow along.

🖱️ **GitHub Desktop**

4. Download it from [desktop.github.com](https://desktop.github.com), open it, and **Sign in to GitHub.com**.
5. In **GitHub Desktop → Settings → Git**, check your name and email are right.

> If you're doing both, do both sets of steps.

---

## Lesson 1 – Turn the folder into a repository and make your first commit

**Idea:** a repo is just a folder Git watches. A commit is a snapshot.

💻 **Terminal**
```bash
cd ~/Documents/my-website      # go into the folder (adjust the path to where you put it)
git init                       # start tracking this folder; creates a hidden .git folder
git status                     # see what Git notices: everything is "untracked"
git add .                      # stage every file ("." means "this whole folder")
git status                     # now they're green: staged and ready
git commit -m "First commit: starter website"
git log                        # see your commit (press q to quit)
```

🖱️ **GitHub Desktop**
1. **File → Add Local Repository…**, choose the `my-website` folder.
2. It says this isn't a Git repository yet. Click **create a repository**, then **Create Repository**.
3. Desktop makes your first commit for you ("Initial commit"). Look at the **History** tab to see it.

✅ **Check:** you have exactly one commit.

> 💡 You'll notice a `.gitignore` file in the folder (it may be hidden in Finder). It tells Git which files to ignore. Ours ignores `.DS_Store`, a junk file macOS creates in every folder. More in Lesson 9.

---

## Lesson 2 – Put your repo on GitHub

**Idea:** your commits so far only exist on your Mac. Pushing copies them to GitHub.

💻 **Terminal**
1. On github.com click **+ → New repository**. Name it `my-website`, set it to **Public**, and **don't** tick "Add a README" (you already have one). Click **Create repository**.
2. GitHub shows a page of commands. You need the "push an existing repository" part:
   ```bash
   git remote add origin https://github.com/YOUR-USERNAME/my-website.git
   git branch -M main
   git push -u origin main
   ```
   `remote add origin` = "here's where GitHub keeps my repo".
   `-u` = "remember this, so next time `git push` is enough".

🖱️ **GitHub Desktop**
1. Click **Publish repository** at the top.
2. **Untick "Keep this code private"** (free GitHub Pages sites need a public repo), then **Publish Repository**.

✅ **Check:** refresh `github.com/YOUR-USERNAME/my-website`. Your files are there, and the README shows below them.

---

## Lesson 3 – Publish the website with GitHub Pages

**Idea:** GitHub can turn a repo into a live website, free.

1. On your repo's GitHub page: **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Branch: **main**, folder: **/ (root)**. Click **Save**.
4. Wait a minute or two, refresh, and a link appears at the top: `https://YOUR-USERNAME.github.io/my-website/`

✅ **Check:** your site is live. From now on, **every time you push to `main`, the site updates automatically** (give it a minute).

---

## Lesson 4 – The everyday loop: edit → stage → commit → push

**Idea:** this is 90% of using Git. Make a change, look at it, commit it with a clear message, push.

Open the folder in VS Code. In `index.html`, replace **Your Name** (it appears 3 times) with your real name. Save. Open `index.html` in your browser to look at it (double-click it in Finder).

💻 **Terminal**
```bash
git status                 # index.html is "modified"
git diff                   # exactly what changed: red = removed, green = added (q to quit)
git add index.html
git commit -m "Add my name to the home page"
git push
git log --oneline          # short history: one line per commit
```

🖱️ **GitHub Desktop**
1. The **Changes** tab lists `index.html`; click it to see the diff.
2. Bottom left: type a summary, `Add my name to the home page`, click **Commit to main**.
3. Click **Push origin** at the top.

**Now do the loop 2 or 3 more times**, one small change per commit, for example:
- Change `--accent` in `style.css` to a colour you like (try `#c2410c` or `#4f46e5`). Commit: `Change accent colour`.
- Rewrite the "What I'm working on" list. Commit: `Update what I'm working on`.

> 💡 **Good commit messages** say *what* changed in a few words, like an instruction: "Add about page", "Fix typo in footer". Small, frequent commits are easier to understand and undo than one giant one.

✅ **Check:** `git log --oneline` (or the History tab) shows several commits, and your live site shows your name.

---

## Lesson 5 – Branches and your first pull request

**Idea:** never experiment on `main`. Make a branch, do the work, then merge it with a pull request.

💻 **Terminal**
```bash
git switch -c add-about-page          # create a new branch AND switch to it
cp starter-pieces/about.html .        # copy the ready-made About page into the main folder
```
In `index.html`, replace the `<!-- LESSON 5 ... -->` comment with:
```html
<a href="about.html">About</a>
```
Edit `about.html` to say something about you (and put your name in it). Then:
```bash
git add .
git commit -m "Add about page"
git push -u origin add-about-page     # first push of a new branch needs -u origin <name>
```

🖱️ **GitHub Desktop**
1. **Current Branch → New Branch**, name it `add-about-page`, **Create Branch**.
2. Copy `starter-pieces/about.html` into the main `my-website` folder (Finder: copy and paste). Make the same `index.html` edit as above, and personalise `about.html`.
3. Commit with `Add about page`, then click **Publish branch**.

**Open the pull request (same for both):**
1. Go to your repo on GitHub. A yellow banner says **add-about-page had recent pushes → Compare & pull request**. Click it.
   (In Desktop: **Branch → Create Pull Request** takes you to the same page.)
2. Write a short description, click **Create pull request**.
3. Look around: the **Files changed** tab shows the diff. On a team, this is where people review your work.
4. Click **Merge pull request → Confirm merge**, then **Delete branch** (it's done its job).

**Bring the merge back to your Mac:**

💻 **Terminal**
```bash
git switch main
git pull                          # download the merge from GitHub
git branch -d add-about-page      # delete your local copy of the branch
```
🖱️ **GitHub Desktop:** switch **Current Branch** to `main`, click **Fetch origin**, then **Pull origin**.

✅ **Check:** your live site has an About link that works.

> 💡 While on `add-about-page`, try `git switch main` and look at the folder: `about.html` disappears! Switch back and it reappears. Branches really are parallel versions of your folder.

---

## Lesson 6 – Issues: plan work, then close it with a PR

**Idea:** issues are GitHub's to-do list. Linking a PR to an issue closes it automatically when merged.

1. On GitHub, open the **Issues** tab → **New issue**. Title: `Add a Projects section`. Click **Create**.
2. Note its number at the top, probably **#2** (issues and pull requests share the same numbering, and your PR was #1).
3. Make a branch called `add-projects` (Terminal: `git switch -c add-projects`; Desktop: **New Branch**).
4. Open `starter-pieces/projects-section.html`, copy the `<section>` block, and paste it into `index.html` where the `<!-- LESSON 6 ... -->` comment is. Fill in your own projects.
5. Commit (`Add projects section`) and push the branch (Terminal: `git push -u origin add-projects`; Desktop: **Publish branch**).
6. Open a pull request. In the description, write: **`Closes #2`** (use your issue's number).
7. Merge it, delete the branch, then switch to `main` and pull, as in Lesson 5.

✅ **Check:** the issue is now marked **Closed**, with a link to your PR.

---

## Lesson 7 – Cause (and fix) a merge conflict on purpose

**Idea:** if two branches change *the same line* differently, Git can't guess which you want. That's a conflict. They're normal and not scary.

💻 **Terminal**
```bash
git switch main
git switch -c tagline-a
```
In `index.html`, change the tagline line to: `I make websites and I'm getting better at Git.` Save, then:
```bash
git commit -am "Tagline version A"     # -a stages changed files for you (not new files)
git switch main
git switch -c tagline-b
```
Change the **same** tagline line to something different: `Curious about everything, especially code.` Save, then:
```bash
git commit -am "Tagline version B"
git switch main
git merge tagline-a        # works fine
git merge tagline-b        # CONFLICT!
```

🖱️ **GitHub Desktop**
1. From `main`, create branch `tagline-a`, change the tagline, commit.
2. Switch to `main`, create branch `tagline-b`, change the same line differently, commit.
3. Switch to `main`. **Branch → Merge into current branch…**, pick `tagline-a`, merge.
4. Do it again with `tagline-b`. Desktop warns about a conflict; go ahead.

**Resolve it (same for both).** Open `index.html`. Git has written both versions into the file:
```
<<<<<<< HEAD
      <p class="tagline">I make websites and I'm getting better at Git.</p>
=======
      <p class="tagline">Curious about everything, especially code.</p>
>>>>>>> tagline-b
```
- Top half (`HEAD`) = what's on `main` now. Bottom half = the branch you're merging in.
- Edit it to what you actually want (one version, the other, or a mix) and **delete the three marker lines**. VS Code also offers "Accept Current / Accept Incoming / Accept Both" buttons.
- Save.

Then finish the merge:

💻 `git add index.html`, then `git commit -m "Merge tagline-b, keep combined tagline"`, then `git push`
🖱️ Desktop shows the file as resolved; click **Continue merge**, then **Push origin**.

Tidy up: `git branch -d tagline-a tagline-b` (Desktop: right-click each branch in the branch list → Delete).

✅ **Check:** `git log --oneline --graph` draws your branches splitting and joining. Try it!

---

## Lesson 8 – Undoing things

**Idea:** Git is a safety net. Here are the three undos you'll use most.

**a) "I messed up a file and haven't committed. Put it back."**
Break something in `style.css` on purpose and save. Then:
- 💻 `git restore style.css`
- 🖱️ Changes tab → right-click the file → **Discard changes…**

**b) "I just committed with a typo in the message." (only before pushing)**
Make a small change, commit it with a bad message like `fixd stuff`. Then:
- 💻 `git commit --amend -m "Fix spacing in footer"`
- 🖱️ History tab → right-click the latest commit → **Amend commit…**

> ⚠️ Don't amend commits you've already pushed; it rewrites history that GitHub already has.

**c) "I pushed a commit and want to undo it."**
Make a change you'll regret, commit, push. Then undo it *with a new commit* (this is the safe way, because history is kept):
- 💻 `git log --oneline` to find its short ID (like `a1b2c3d`), then `git revert a1b2c3d`, save the message that opens (in the default editor, type `:wq` and press Enter), then `git push`.
- 🖱️ History tab → right-click the commit → **Revert Changes in Commit**, then **Push origin**.

✅ **Check:** your history shows a "Revert …" commit, and the site is back to how it was.

---

## Lesson 9 – .gitignore: tell Git what not to track

**Idea:** some files shouldn't be in your repo: system junk, private notes, passwords.

1. Create a file called `notes-to-self.txt` with anything in it.
2. Look at `git status` (or Desktop's Changes tab): Git wants to track it.
3. Open `.gitignore` (in VS Code it's visible in the file list) and add a line:
   ```
   notes-to-self.txt
   ```
   (Desktop shortcut: right-click the file in Changes → **Ignore file**.)
4. Check status again: the notes file is gone from the list, and `.gitignore` itself is changed. Commit that: `Ignore my private notes`.

> 💡 Never commit passwords or secret keys. Even if you delete them later, they stay in the history.

---

## Lesson 10 – Pull changes made on GitHub

**Idea:** the copy on GitHub and the copy on your Mac can get out of sync. `pull` catches you up.

1. On github.com, open `README.md` and click the ✏️ pencil icon.
2. Replace `YOUR-USERNAME` in the live site link with your username. Click **Commit changes…** and commit directly to `main`.
3. Your Mac doesn't have that commit yet. Get it:
   - 💻 `git pull`
   - 🖱️ **Fetch origin**, then **Pull origin**

✅ **Check:** the README on your Mac has the new link.

> 💡 Make it a habit: **pull before you start working.** It prevents most conflicts.

---

## Lesson 11 – Tags and releases: mark version 1.0

**Idea:** a tag is a permanent bookmark on a commit. A release is a tag with notes on GitHub.

💻 **Terminal**
```bash
git tag -a v1.0 -m "First finished version of my site"
git push origin v1.0
```
🖱️ **GitHub Desktop:** History tab → right-click the latest commit → **Create Tag…** → `v1.0` → then **Push origin**.

Then on GitHub: **Releases** (right side of the repo page) → **Draft a new release** → choose tag `v1.0` → write a few notes about what's in it → **Publish release**.

🎉 **You're done.** You've used every core part of Git and GitHub.

---

## Cheat sheet

| I want to… | Terminal | GitHub Desktop |
|---|---|---|
| See what's changed | `git status`, `git diff` | Changes tab |
| Stage & commit | `git add .` then `git commit -m "msg"` | Tick files, write summary, **Commit** |
| Send to GitHub | `git push` | **Push origin** |
| Get latest from GitHub | `git pull` | **Fetch origin → Pull origin** |
| See history | `git log --oneline --graph` | History tab |
| New branch | `git switch -c name` | Current Branch → **New Branch** |
| Change branch | `git switch name` | Current Branch → pick one |
| Merge a branch into current | `git merge name` | Branch → **Merge into current branch** |
| Delete a local branch | `git branch -d name` | Right-click branch → Delete |
| Discard uncommitted edits | `git restore file` | Right-click file → Discard changes |
| Undo a pushed commit | `git revert <id>` | History → Revert Changes in Commit |
| Copy someone's repo to your Mac | `git clone <url>` | File → Clone Repository |

## Where to go next
- Add a third page, or a photo (put images in an `images/` folder).
- Try **forking**: copy someone else's public repo to your account, change it, and open a PR to suggest it back.
- Clone your repo into a second folder, make conflicting changes in each, and push both, to see what a "rejected push" looks like and fix it with `git pull`.
