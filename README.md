# Devbox playbook

This is a playbook that installs dev tools and DE tools I like to have around 
and sets up some other preferences like repositories, and drops in my dotfiles. 
It's best-tested on Debian, but has some cases for OSX and FreeBSD too.

The `gui_enabled` var controls whether or not to install graphical tools.

## TODO

- Adjust to work with ansible-pull via cloud-config userdata like this:

```yaml
#cloud-config
packages:
  - ansible
  - git
runcmd:
  - echo -e "[localhost]\n127.0.0.1 ansible_connection=local" >> /etc/ansible/hosts
  - ssh-keyscan github.com >> /etc/ssh/ssh_known_hosts
  - mkdir /etc/ansible/web
  - ansible-pull -d /etc/ansible/web/ -U <git repo URL>
```

