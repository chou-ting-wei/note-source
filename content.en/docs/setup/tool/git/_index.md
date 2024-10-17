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
   git config --global user.email "your_email@example.com"
   ```
   > To keep your email address private, use your GitHub-provided `no-reply` email address.
2. Set default commit branch
   ```sh
   git config --global init.defaultBranch main
   ```
3. Check your settings
   ```sh
   git config --list
   ```

### Basic Operations

1. Clone a repository
   ```sh
   git clone <repository_url>
   ```
2. Pull changes from the remote repository
   ```sh
   git pull
   ```
3. Stage files in the current directory

   ```sh
   # stage a specific file
   git add <file_name>

   # stage multiple specific files
   git add <file_name1> <file_name2>

   # stage all changes in the current directory
   git add .
   ```

4. Commit your changes
   ```sh
   git commit -m "<commit_message>"
   ```
5. Push changes to the remote repository
   ```sh
   git push
   ```

### Branch Operations

1. Switch to an existing branch
   ```sh
   git checkout <branch_name>
   ```
2. Create a new branch from the current branch and switch to it
   ```sh
   git checkout -b <new_branch_name>
   ```
3. Create a new branch from a specific branch and switch to it
   ```sh
   git checkout -b <new_branch_name> <branch_name>
   ```
4. List all branches
   ```sh
   git branch -a
   ```
5. Rename the current branch
   ```sh
   git branch -m <new_branch_name>
   ```
6. Delete a local branch
   ```sh
   git branch -d <branch_name>
   ```
7. Push a new branch to the remote repository
   ```sh
   git push -u origin <branch_name>
   ```
8. Delete a branch from the remote repository
   ```sh
   git push origin -d <branch_name>
   ```

### Submodule Management

1. Add a new submodule to the repository
   ```sh
   git submodule add <repository_url> <path>
   ```
2. Initialize, fetch and checkout the submodule
   ```sh
   git submodule update --init --recursive
   ```

### Commit Reversion

> &#x26a0;&#xfe0f;**Warning:** Reverting commits can potentially lead to loss of work. Ensure you have backups or have communicated with your team before performing these actions.

1. Identify the Commit
   ```sh
   git log
   ```
2. Reset to the Previous Commit
   ```sh
   git reset --hard HEAD~1
   # or
   git reset --hard <commit_hash>
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
   git add <file_name>
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

### Git Stash for Branch Switching

1. Save your current changes

   ```sh
   git stash
   ```

2. View the stashed changes
   ```sh
   git stash list
   ```
3. Switch to the target branch

   ```sh
   git checkout <target_branch>
   ```

4. Apply and remove the latest stash
   ```sh
   git stash pop
   ```

### Git Large File Storage

1. Install Git LFS
   ```sh
   git lfs install
   ```
2. Use Git LFS to track specific file types. For example, to track all `.psd` files

   ```sh
   git lfs track "*.psd"
   ```

3. After you add files to be tracked by LFS, ensure you add them to the repository by staging the `.gitattributes` file
   ```sh
   git add .gitattributes
   git commit -m "chore(main): add Git LFS tracking for large files"
   ```
4. Git LFS automatically handles large files as you push them to the repository

## GitHub

### SSH Key Setup

1. Generate a new SSH key

   ```sh
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```

   > To keep your email address private, use your GitHub-provided `no-reply` email address.

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

### Initialize a New Git Repository

```sh
echo "# <repository_name>" >> README.md
git init
git add README.md
git commit -m "init(main): create repository and add README.md"
git branch -M main
git remote add origin <repository_url>
git push -u origin main
```

### Common Commit Message

1. `feat(<branch_name>):` – For new features or significant additions.

   - Example: `feat(<branch_name>): add user authentication module`

2. `fix(<branch_name>):` – For bug fixes or resolving issues.

   - Example: `fix(<branch_name>): resolve login error on homepage`

3. `docs(<branch_name>):` – For documentation changes.

   - Example: `docs(<branch_name>): update README with setup instructions`

4. `chore(<branch_name>):` – For routine tasks, maintenance, or minor setup changes.

   - Example: `chore(<branch_name>): set up project structure`

5. `refactor(<branch_name>):` – For refactoring code without changing its functionality.

   - Example: `refactor(<branch_name>): optimize data processing logic`

6. `style(<branch_name>):` – For formatting changes that do not affect the code’s functionality (e.g., fixing indentation).

   - Example: `style(<branch_name>): apply consistent code formatting`

7. `test(<branch_name>):` – For adding or updating tests.

   - Example: `test(<branch_name>): add unit tests for authentication service`

8. `perf(<branch_name>):` – For performance improvements.

   - Example: `perf(<branch_name>): enhance database query efficiency`

9. `build(<branch_name>):` – For changes that affect the build system or dependencies.

   - Example: `build(<branch_name>): update webpack configuration`

10. `ci(<branch_name>):` – For CI/CD pipeline changes.
    - Example: `ci(<branch_name>): update GitHub Actions workflow`
