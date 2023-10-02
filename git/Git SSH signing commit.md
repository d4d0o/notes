#### Git SSH signing commit

Git config: `~/.gitconfig`

- Set \[`gpg] format` to `ssh`.
- Set \[`user] signingkey` to the public key you chose to sign commits with.
- Set \[`commit] gpgsign` to `true` so you don't need to include the `-S` flag with each commit. *(optional)*
- Set \[`gpg "ssh"]` to the SSH signer binary, so you don't have to set `SSH_AUTH_SOCK` yourself. *(optional)*

###### \~/.gitconfig

```
[user]
name = User Name
email = user@e.mail
signingkey = ssh-ed25519 AAAAC3NzaC1IZDI1NTE5AAAAIFIUXAdv5sWOrfZFEPAW8liKjBW3sFxuaNITBWwtFKO

[commit]
gpgsign = true

[gpg]
format = ssh

[gpg "ssh"]
program = /Applications/binary

[includeIf "gitdir:~/work/acme/"]
path = ~/work/acme/.gitconfig
```

###### \~/work/acme/.gitconfig

```
[user]
email = user.work@acme.com
signingkey = 6A40D13BBB936F443084E8C9292E4F983136B860

[gpg]
format = openpgp
```

<https://developer.1password.com/docs/ssh/git-commit-signing/>

###### Then it needs to add the key as one to be trusted

<https://blog.dbrgn.ch/2021/11/16/git-ssh-signatures/>