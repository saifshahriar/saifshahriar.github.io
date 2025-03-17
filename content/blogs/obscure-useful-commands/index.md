+++
title="Obscure Useful Commands"
author="Saif Shahriar"
date = "2024-06-01"
toc = true
tocBorder = true
categories = ["command", "linux"]
tags = ["software", "linux"]
+++

## Intro
This post I have tried talking about some obscure commands, that can save your
back when you need them. I have tried keeping every section short and concise.
No BS.

## Git
### Edit commit history to prevent private email address from showing up
> **Desc:** Suppose you have accidentally revealed your <private@mail.com> by
commiting and pusing it to github. How do you safely change that email to
<public@mail.com> so that it overwrites your commit history?

Here is what you need to do.

1. Backup the repo your with all the latest changes. In case you make some
   mistake. Also make sure to commit any changes that you might have made to the
   repo but have not pushed yet.
   ```fish
   cp -r /path/to/repo /path/to/repo.bak
   ```

2. Do a fresh commit of the repo and cd inside it:
   ```fish
   git clone git@github.com:user/repo.git
   cd repo
   ```

3. Install [git-filter-repo](https://github.com/newren/git-filter-repo). We are
   going to use this tool to overwrite our commit history.

   **Debian/Ubuntu/Mint**:
   ```fish
   apt install git-filter-repo
   ```
   **Arch Linux:**
   ```fish
   pacman -S git-filter-repo
   ```
   **Void Linux:**
   ```fish
   xbps-install git-filter-repo
   ```
   *Use `sudo` if needed.*

   Others follow the [link](https://github.com/newren/git-filter-repo).

4. Overwrite the repo's commit history:
   ```fish
   git filter-repo --commit-callback '
   if commit.author_email == b"private@mail.com":
   commit.author_email = b"public@mail.com"
   if commit.committer_email == b"private@mail.com":
   commit.committer_email = b"public@mail.com"
   '
   ```
   Change `private@mail.com` with your *unwanted exposed mail address* and
   `public@mail.com` with your new mail address.

5. Now force push all the changes.
   ```fish
   git push --force --all
   ```

   Thats it! You can see if your private email is still showing in the commit
   history by running `git log | grep private@mail.com`.

### Delete Commit History
**Desc:** Commits can be undone, and you can erase the history just like that.
ft. `git reset`.

1. Use `git log` to see your commit history.
2. After identifying which commit to erase, run:
   ```fish
   git reset --hard <commit-hash>
   ```
   Example:
   ```fish
   git reset --hard 0ceef5d2d76a88d07e2e4f8e050cc082ee31b4c4
   ```
   Here, `0ceef5d2d76a88d07e2e4f8e050cc082ee31b4c4` represents unique the hash
   for the commit.

   This command will delete the entire commit history up until the commit:
   `0ceef5d2d76a88d07e2e4f8e050cc082ee31b4c4`.

   You can also do the same using HEAD~n.
   Example:
   ```fish
   git reset --hard HEAD~5
   ```
   This will erase the last 5 commits from your history.
3. Verify that your desired commit is gone forever from the face of the earth.
   ```fish
   git log
   ```
4. Now, **force push** your changes.
   ```fish
   git push --force --all
   ```
