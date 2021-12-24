# Step 1

Setup `root` user with ssh key based login. To do that we will use this role:

```
ansible-galaxy install GROG.authorized-key
```

and install `sshpass` so that we can run ansible command with password

```
brew install hudochenkov/sshpass/sshpass
```

Ref: [URL](https://stackoverflow.com/questions/32255660/how-to-install-sshpass-on-mac/62623099#62623099)


and then use this playbook to setup root ssh key
---
setup root ssh, using root password

```
ansible-playbook -i hosts setup-ssh-root.yml -l server1 -u root --ask-pass
```

For me `sshpass` installation didn't work so wasn't able to use --ask-pass param in ansible command
so used the `ssh-copy-id` command as manual step

```
ssh-copy-id -i  ~/.ssh/id_ed25519.pub root@rack
```

Now I can ssh using ssh key

```
ssh -i ~/.ssh/id_ed25519  root@rack
```

--
once the root ssh key setup is done, we can run the initial server setup plybook

```

```