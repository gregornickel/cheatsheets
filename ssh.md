# SSH


Establish a ssh connection:
```shell
ssh username@address
```

Exit a ssh connection with `exit` or `ctrl+d`


## Check existing SSH keys
```shell
ls -al ~/.ssh
```

## Generate an SSH key pair

For ED25519:
```shell
ssh-keygen -t ed25519 -C "<comment>"
```

For 2048-bit RSA:
```shell
ssh-keygen -t rsa -b 2048 -C "<comment>"
```

### Change passphrase of an SSH key

To change the passphrase on your default key:

```shell
ssh-keygen -p
```

If you need to specify a key, pass the `-f` option:

```shell
ssh-keygen -p -f ~/.ssh/id_dsa
```

## Config file

The ssh config file is stored at `~/.ssh`. You can edit the configuration with `vim config`. 

```
Host github
  User git
  HostName github.com
  IdentityFile ~/.ssh/id_ed25519
```

After configuring username, hostname and identyfile you can ssh login with e.g. ssh github without typing your password (with your private key having no passphrase and your public key containing the server password). 

## Register SSH Key in GitHub account

```shell
$ pbcopy < ~/.ssh/id_ed25519.pub
```

Upload the public key [here](https://github.com/settings/keys).

### Check

```shell
ssh -T git@github.com
```
