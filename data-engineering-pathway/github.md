# Github

### Git Manual for Data Engineering Learning Journey

This document outlines the lessons learned during the initial setup of this repository's branching strategy and provides a manual for maintaining and expanding the learning journey in the future.

***

#### I. Lessons Learned from Initial Setup

The process of organizing this repository by Git branches highlighted several key principles and common pitfalls:

1. **Clarity of Goal is Paramount:** Initially, the goal was to "change the folder structure to a GitHub branch." However, the _true_ intent was to use _branches as the primary organizational unit for distinct learning topics_. This distinction significantly altered the strategy from folder refactoring on `main` to dedicated topic branches. Always clarify the overarching vision first.
2. **Branches are Powerful Isolation Tools:** Creating dedicated branches (`topic/fundamentals-de`, `topic/sql`, `topic/python`) _before_ cleaning up `main` proved to be the safest and most effective way to manage content. It ensured no data loss and kept each topic's content focused.
3. **Git's History is Persistent:** Even when files are "deleted" on a branch, they remain in the repository's history on previous commits. This is why "deleted" files on `main` could still be leveraged for new topic branches by creating those branches from `main`'s earlier, full state.
4. **`git status` is Your Best Friend:** Regularly running `git status` after _any_ local change (moving files, deleting files, creating new files) is critical. It provides immediate feedback on what Git sees in your working directory and staging area, preventing accidental commits or pushes of unintended changes.
5. **`git add .` vs. `git add <file>`:** While `git add .` is convenient, being explicit with `git add <filename>` (especially for new files or after complex moves/deletions) can help ensure Git stages exactly what you intend, avoiding issues like the `README.md` not being staged after its creation.
6. **`git push` Pushes&#x20;**_**Committed**_**&#x20;Changes:** An accidental `git push` before `git add` and `git commit` doesn't break anything, but it also doesn't push your latest local changes. Always `add` and `commit` _before_ attempting to `push`.
7. **Shell Specifics (e.g., `zsh` and `echo`):** Be aware of your shell's (like `zsh`) interpretation of special characters. Escaping characters (e.g., `\)`) in `echo` commands is sometimes necessary to avoid "event not found" errors.
8. **Visual Confirmation is Key:** After major Git operations (especially `push`), always visit GitHub directly to visually confirm the changes reflect your intentions. This provides immediate feedback and builds confidence.

***

#### II. Future Manual for Repository Management

This section provides a manual for continuing to manage and expand your Data Engineering Learning Journey repository.

**Repository Structure Philosophy:**

* **`main` branch:** This branch serves as the central "Table of Contents" or overview for your entire learning journey. It should primarily contain a single `README.md` file with an introduction to the journey and links to each major learning topic.
* **`topic/<topic-name>` branches:** Each significant learning topic (e.g., `fundamentals-de`, `sql`, `python`, `big-data`) will reside in its own dedicated branch. These branches contain all the files, code, notebooks, and resources related to that specific topic.

***

**1. Starting Work on an Existing Topic**

When you want to continue learning or add content to a topic you've already branched out:

1.  **Switch to the relevant topic branch:**

    Bash

    ```
    git checkout topic/<topic-name>
    ```

    (e.g., `git checkout topic/python`)
2.  **Pull any remote changes (if working from multiple machines or after a long break):**

    Bash

    ```
    git pull origin topic/<topic-name>
    ```
3. **Make your changes:**
   * Add new files/notebooks.
   * Update existing files.
   * Delete obsolete files.
   * _Ensure all content related to this topic stays within the root of this branch._
4.  **Check your status:**

    Bash

    ```
    git status
    ```

    (Verify changes are as expected)
5.  **Stage your changes:**

    Bash

    ```
    git add .
    ```

    (Or `git add <specific-file>` for precision)
6.  **Commit your changes:**

    Bash

    ```
    git commit -m "Descriptive message about what you added/changed in this topic"
    ```
7.  **Push your changes to GitHub:**

    Bash

    ```
    git push origin topic/<topic-name>
    ```

***

**2. Starting a Brand New Learning Topic**

When you're ready to begin a completely new section of your data engineering journey:

1.  **Switch to the `main` branch:**

    Bash

    ```
    git checkout main
    ```
2.  **Ensure your `main` branch is up-to-date:**

    Bash

    ```
    git pull origin main
    ```

    _This is crucial. You want your new topic branch to start from a clean, up-to-date overview._
3.  **Create a new branch for your topic (choose a descriptive name like `topic/new-topic-name`):**

    Bash

    ```
    git checkout -b topic/<new-topic-name>
    ```

    (e.g., `git checkout -b topic/cloud-platforms`)
4. **Add all your new learning content (files, notebooks, subfolders) into the root of this new branch.**
   * Think about the structure _within_ this topic branch. For example, `topic/cloud-platforms` might have `aws/`, `azure/`, `gcp/` subfolders.
5.  **Check your status:**

    Bash

    ```
    git status
    ```
6.  **Stage all new content:**

    Bash

    ```
    git add .
    ```
7.  **Commit your initial topic content:**

    Bash

    ```
    git commit -m "Initial commit for topic: <New Topic Name>"
    ```
8.  **Push your new topic branch to GitHub:**

    Bash

    ```
    git push -u origin topic/<new-topic-name>
    ```

    _The `-u` (or `--set-upstream`) is only needed the first time you push a new branch._
9. **Update the `main` branch's `README.md` to link to your new topic:**
   * **Switch back to `main`:** `git checkout main`
   * **Pull to ensure local `main` is fresh:** `git pull origin main`
   * **Open `README.md` in your editor (e.g., VS Code).**
   *   **Add a new link under "Explore the Journey" section:**&#x4D;arkdown

       ```
       - [**<New Topic Name>** (Branch: `topic/<new-topic-name>`)](https://github.com/mnizhadali-afg/data-engineering-journey/tree/topic/<new-topic-name>)
       ```

       (Remember to replace `<new-topic-name>` and `<New Topic Name>` with your actual branch/topic name, and ensure the URL is correct for your repo.)
   * **Stage the updated `README.md`:** `git add README.md`
   * **Commit the `README.md` update:** `git commit -m "Update README: Add link to new topic: <New Topic Name>"`
   * **Push the updated `main` branch:** `git push origin main`

***

**3. General Git Commands & Tips**

* **`git status`**: Use frequently to understand your current local Git state.
* **`git log`**: View commit history. `git log --oneline --graph` is great for a compact view.
* **`git diff`**: See changes before staging or committing. `git diff` (unstaged), `git diff --staged` (staged).
* **Discarding local changes:**
  * `git restore <file>`: Discard changes in a specific file in your working directory.
  * `git restore .`: Discard all unstaged changes in the current directory.
  * **Caution:** These discard uncommitted work.
* **Deleting a local branch (after it's merged to `main` and/or served its purpose):**
  * `git branch -d <branch-name>` (safe delete, only if merged)
  * `git branch -D <branch-name>` (force delete, use with caution)
* **Deleting a remote branch (after it's no longer needed on GitHub):**
  * `git push origin --delete <branch-name>`

This manual, combined with your practical experience from setting up the repository, will serve as a solid foundation for your ongoing data engineering learning journey!
