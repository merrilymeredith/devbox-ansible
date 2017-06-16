

# Devbox playbook

This is a playbook that installs dev tools and DE tools I like to have around 
and sets up some other preferences like repositories, and drops in my dotfiles. 
It's best-tested on Debian, but has some cases for OSX and FreeBSD too.

The `gui_enabled` var controls whether or not to install graphical tools.

# Running

## Push

1. Create inventory file with target host.
2. If we can ssh as root with key, use `-u root`.  If we can sudo, use `-bK`.
3. GUI box? `-e gui_enabled=true`
4. `ansible-playbook -i $inventory $args local.yml`

## Pull

1. Install `ansible`, `git`
2. `echo -e '[localhost]\nlocalhost ansible_connection=local' >> /etc/ansible/hosts`
2. `ansible-pull -U https://github.com/merrilymeredith/devbox-ansible.git`

### cloud-init

```yaml
#cloud-config
packages:
  - ansible
  - git
runcmd:
  - echo -e '[localhost]\nlocalhost ansible_connection=local' >> /etc/ansible/hosts
  - ansible-pull -U https://github.com/merrilymeredith/devbox-ansible.git
```

# TODO

- Make pull config install cron entry?
