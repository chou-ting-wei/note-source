---
title: Git & GitHub
type: docs
---
# Git & GitHub

## Git
1. 設定識別資料
    ```sh
    git config --global user.name "your_name"
    git config --global user.email your_email@users.noreply.github.com
    ```
2. 檢查設定
    ```sh
    git config --list
    ```

## GitHub
### SSH key
1. 生成 SSH key
    ```sh
    ssh-keygen -t ed25519 -C "your_email@example.com"
    ```
2. 複製 SSH public key
    ```sh
    cat ~/.ssh/id_ed25519.pub
    # Then select and copy the contents of the id_ed25519.pub file
    # displayed in the terminal to your clipboard
    ```
3. 在 GitHub 設定中加入 SSH public key

### GPG key
1. 下載 [GnuPG](https://www.gnupg.org/download/) 並安裝
2. 生成 GPG key
    ```sh
    gpg --full-generate-key
    ```
3. 皆使用默認選擇，並設定識別資料
    > When asked to enter your email address, ensure that you enter the verified email address for your GitHub account. To keep your email address private, use your GitHub-provided `no-reply` email address.
4. 列出所有 GPG key
    ```sh
    gpg --list-secret-keys --keyid-format=long
    ```
    > Some GPG installations on Linux may require you to use `gpg2 --list-keys --keyid-format LONG` to view a list of your existing keys instead. In this case you will also need to configure Git to use `gpg2` by running `git config --global gpg.program gpg2`.
5. 選擇要使用的 GPG key
    ```sh
    $ gpg --list-secret-keys --keyid-format=long
    /Users/hubot/.gnupg/secring.gpg
    ------------------------------------
    sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
    uid                          Hubot <hubot@example.com>
    ssb   4096R/4BB6D45482678BE3 2016-03-10
    ```
    > In this example, the GPG key ID is `3AA5C34371567BD2`.
6. 複製 GPG key
    ```sh
    gpg --armor --export 3AA5C34371567BD2
    # Prints the GPG key ID, in ASCII armor format
    ```
    > Copy your GPG key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----`.
7. 在 GitHub 設定中加入 GPG key
8. 將 GPG key 配置到 git config 中
    ```sh
    git config --global user.signingkey 3AA5C34371567BD2
    git config --global commit.gpgsign true
    ```
