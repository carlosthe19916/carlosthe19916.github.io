---
sidebar_position: 2
---

# How to Setup SSH keys

- https://docs.gitlab.com/ee/user/ssh.html

## Generate an SSH key pair

- First, generate a GPG key pair. Your GPG key must use RSA with a key size of 4096 bits.

```shell
ssh-keygen -t rsa -b 4096 -C "Github - Thinkpad P16v"
```

When the terminal asks for where to store the file we can type:

```shell
/home/cferiavi/.ssh/id_rsa_github
```

As we are generating a different SSH key for each provider Github|Gitlab we need to create the file `~/.ssh/config`

```shell
vi ~/.ssh/config
```

And insert something like:

```toml
# Github.com
Host github.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_github

# GitLab.com
Host gitlab.com
  PreferredAuthentications publickey
  IdentityFile ~/.ssh/id_rsa_gitlab
```

## Add an SSH key to your account

### Github

- Copy your public key:

```shell
xclip -sel clip < ~/.ssh/id_rsa_github.pub
```

- Add your keys at https://github.com/settings/keys
- Click on `New SSH Key`
- On `Key type` select `Authentication`
- Verify that you can connect:

```shell
ssh -T git@github.com
```

### Gitlab

- Copy your public key:

```shell
xclip -sel clip < ~/.ssh/id_rsa_gitlab.pub
```

- Add your keys at https://gitlab.com/-/user_settings/ssh_keys
- Verify that you can connect:

```shell
ssh -T git@gitlab.com
```
