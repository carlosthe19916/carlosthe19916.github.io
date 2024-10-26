---
sidebar_position: 1
---

# How to Setup Verified Commits

How to Setup Verified Commits
Quick guide on how to setup git signing. Information is aggregated from following sources:

- https://help.github.com/articles/signing-commits/
- https://help.github.com/articles/telling-git-about-your-signing-key/
- https://help.github.com/articles/generating-a-new-gpg-key/
- https://docs.github.com/en/authentication/managing-commit-signature-verification/adding-a-gpg-key-to-your-github-account

## Creating GPG Keys

- First, generate a GPG key pair. Your GPG key must use RSA with a key size of 4096 bits.

```shell
gpg --full-generate-key
```

- At the prompt, specify the kind of key you want, or press. Enter to accept the default RSA and RSA.
- Enter the desired key size. We recommend the maximum key size of `4096`
- Enter the length of time the key should be valid. Press Enter to specify the default selection, indicating that the key doesn't expire.
- Verify that your selections are correct.
- Enter your user ID information. E.g. `Name Surname`

> When asked to enter your email address, ensure that you enter the verified email address for your GitHub account. To keep your email address private, use your GitHub-provided no-reply email address. You can find your private email at [settings/email](https://github.com/settings/emails)

> When asked for a `Comment` set something like `Github GPG from Thinkpad 123` for better understading of what that key will be used for

- Type a secure passphrase.
- Use the gpg `--list-secret-keys --keyid-format LONG` command to list GPG keys for which you have both a public and private key. A private key is required for signing commits or tags. From the list of GPG keys, copy the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:

```shell
$ gpg --list-secret-keys --keyid-format LONG
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
uid                          Hubot
ssb   4096R/42B317FD4BA89E7A 2016-03-10
```

- Paste the text below, substituting in the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:

```shell
$ gpg --armor --export 3AA5C34371567BD2
# Prints the GPG key ID, in ASCII armor format
```

- Copy your GPG key, beginning with `-----BEGIN PGP PUBLIC KEY BLOCK-----` and ending with `-----END PGP PUBLIC KEY BLOCK-----`.

## Adding a new GPG key to your GitHub account

- In the upper-right corner of any page, click your profile photo, then click Settings.
- In the user settings sidebar, click SSH and GPG keys.
- Click New GPG key.
- In the "Key" field, paste the GPG key you copied when you generated your GPG key.
  Click Add GPG key.
- To confirm the action, enter your GitHub password.

## Getting GPG Keys

- Open Git Bash
- Use the `gpg --list-secret-keys --keyid-format LONG` command to list GPG keys for which you have both a public and private key. A private key is required for signing commits or tags.
- From the list of GPG keys, copy the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:

```shell
$ gpg --list-secret-keys --keyid-format LONG
/Users/hubot/.gnupg/secring.gpg
------------------------------------
sec   4096R/3AA5C34371567BD2 2016-03-10 [expires: 2017-03-10]
uid                          Hubot
ssb   4096R/42B317FD4BA89E7A 2016-03-10
```

## Git Settings

To set your GPG signing key in Git, paste the text below, substituting in the GPG key ID you'd like to use. In this example, the GPG key ID is `3AA5C34371567BD2`:

```shell
$ git config --global user.signingkey 3AA5C34371567BD2
```

To tell git to automatically sign commits you can set:

```shell
$ git config --global commit.gpgsign true
```

Set the global email. Take the private email from [settings/email](https://github.com/settings/emails)

```shell
git config user.email "your_email@abc.example"
```

## Setup permanent auth in git

Install the Github CLI. There are official docs [here](https://github.com/cli/cli/blob/trunk/docs/install_linux.md#fedora-centos-red-hat-enterprise-linux-dnf)

If you are using Fedora you can just execute:

```shell
sudo dnf install gh
```

Then login to Github:

```shell
gh auth login
```

From now on you will be able to use git in your terminal to do pull, push, etc.
