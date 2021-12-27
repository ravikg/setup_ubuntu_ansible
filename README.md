# Steps

Normally `root` user has password based login when we create a new machine, and to work with ansible or in general development work we want to use ssh key instead of password. To do that we can configure ssh key based login using following ways:


### Setup Ansible to use ssh password
Setup `root` user with ssh key based login. To do that we will use this role:

```bash
ansible-galaxy install GROG.authorized-key
```

and install `sshpass` so that we can run ansible command with password

```
brew install hudochenkov/sshpass/sshpass
```

Ref: [how-to-install-sshpass-on-mac](https://stackoverflow.com/questions/32255660/how-to-install-sshpass-on-mac/62623099#62623099)


and then use this playbook to setup root ssh key in server

### Setup ssh key based root login : using Ansible `--ask-pass`

```bash
ansible-playbook -i hosts setup-ssh-root.yml -l server1 -u root --ask-pass
```

### Setup ssh key based root login : using `ssh-copy-id`

For me `sshpass` installation didn't work so wasn't able to use --ask-pass param in ansible command
so used the `ssh-copy-id` command as manual step

```bash
ssh-copy-id -i  ~/.ssh/id_ed25519.pub root@rack
```

Now I can ssh using ssh key

```bash
ssh -i ~/.ssh/id_ed25519  root@rack
```

### Initialize the server : Using Ansible playbook

Once the root ssh key setup is done, we can run the initial server setup plybook

```bash
ansible-playbook -i hosts playbook.yml -l server1 -u root
```

### References
* <https://github.com/do-community/ansible-playbooks.git>
* <https://www.digitalocean.com/community/tutorials/how-to-use-ansible-to-automate-initial-server-setup-on-ubuntu-18-04> 
* <https://rkg.xyz/post-2/>
