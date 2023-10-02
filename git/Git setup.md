#### Git quick setup

###### Generating SSH key
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```


###### Adding your SSH key to the ssh-agent
Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key.

Start the ssh-agent in the background.
    
```
$ eval "$(ssh-agent -s)"
> Agent pid 59566
```

Depending on your environment, you may need to use a different command. For example, you may need to use root access by running sudo -s -H before starting the ssh-agent, or you may need to use exec ssh-agent bash or exec ssh-agent zsh to run the ssh-agent.

Add your SSH private key to the ssh-agent.

If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_ed25519 in the command with the name of your private key file.

```
ssh-add ~/.ssh/id_ed25519
```

Add the SSH public key to your account on GitHub. For more information, see "Adding a new SSH key to your GitHub account."



###### Git usernames and email
```
git config --global user.name "Mona Lisa"
git config --global user.email "YOUR_EMAIL"
```



###### Signing commit with SSH key
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
signingkey = ssh-ed25519 AA........

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
