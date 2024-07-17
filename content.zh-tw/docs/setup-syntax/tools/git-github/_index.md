---
title: Git/GitHub
type: docs
---

# Git/GitHub

## Git

### User Configuration

1. Set your identity
   ```sh
   git config --global user.name "your_name"
   git config --global user.email your_email@users.noreply.github.com
   ```
2. Set default commit branch
   ```sh
   git config --global init.defaultBranch main
   ```
3. Check your settings
   ```sh
   git config --list
   ```

### Branch Operations

1. Switch to an existing branch
   ```sh
   git checkout <branch-name>
   ```
2. Create a new branch and switch to it
   ```sh
   git checkout -b <new-branch-name>
   ```

### Submodule Management

1. Add a new submodule to the repository
   ```sh
   git submodule add <repository-url> <path>
   ```
2. Initialize, fetch and checkout the submodule
   ```sh
   git submodule update --init --recursive
   ```

### Commit Reversion

> &#x26a0;&#xfe0f;WARNING: Reverting commits can potentially lead to loss of work. Ensure you have backups or have communicated with your team before performing these actions.

1. Identify the Commit
   ```sh
   git log
   ```
2. Reset to the Previous Commit
   ```sh
   git reset --hard HEAD~1
   # or
   git reset --hard <commit-hash>
   ```
   > This will discard all changes after the specified commit.
3. Force Push the Changes
   ```sh
   git push --force
   ```
   > This can overwrite changes in the remote repository.

### Conflict Resolution

1. Identify the conflict
   ```sh
   git status
   # or
   git diff
   ```
2. Open the conflicting file
   ```txt
   <<<<<<< HEAD
   Your changes
   =======
   Changes from the branch you are merging
   >>>>>>> branch-name
   ```
   > Remove the conflict markers and decide what the final content should be.
3. Add the resolved file to the staging area
   ```sh
   git add <file-name>
   ```
4. Commit the resolved changes

   ```sh
   git commit
   ```

5. Continue with your merge or rebase

   ```sh
   git merge --continue
   # or
   git rebase --continue
   ```

## GitHub

### SSH Key Setup

1. Generate a new SSH key
   ```sh
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
2. Copy the SSH public key to your clipboard

   ```sh
   cat ~/.ssh/id_ed25519.pub
   ```

   > Then select and copy the contents of the `id_ed25519.pub` file displayed in the terminal to your clipboard.

3. Add a new SSH authentication key to your account

### GPG Key Setup

1. Download and install the [GPG command line tool](https://www.gnupg.org/download/)
2. Generate a GPG key pair
   ```sh
   gpg --full-generate-key
   ```
3. Enter your user ID information
   > When asked to enter your email address, ensure that you enter the verified email address for your GitHub account. To keep your email address private, use your GitHub-provided `no-reply` email address.
4. List the long form of the GPG keys
   ```sh
   gpg --list-secret-keys --keyid-format=long
   ```
   > Some GPG installations on Linux may require you to use `gpg2 --list-keys --keyid-format LONG` to view a list of your existing keys instead. In this case you will also need to configure Git to use `gpg2` by running `git config --global gpg.program gpg2`.
5. Copy the long form of the GPG key ID you'd like to use
   ```sh
   $ gpg --list-secret-keys --keyid-format=long
   /Users/hubot/.gnupg/secring.gpg
   ------------------------------------
   sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
   uid                          Hubot <hubot@example.com>
   ssb   4096R/4BB6D45482678BE3 2016-03-10
   ```
   > In this example, the GPG key ID is `3AA5C34371567BD2`.
6. Paste the text below, substituting in the GPG key ID you'd like to use
   ```sh
   gpg --armor --export 3AA5C34371567BD2
   # Prints the GPG key ID, in ASCII armor format
   ```
   > Copy your GPG key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----`.
7. Add a new GPG key to your account
8. Set your primary GPG signing key in Git
   ```sh
   git config --global user.signingkey 3AA5C34371567BD2
   ```
9. Configure Git to sign all commits by default
   ```sh
   git config --global commit.gpgsign true
   ```
