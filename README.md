# Devbox playbook

This is a playbook that installs dev tools and DE tools I like to have around 
and sets up some other preferences like repositories, and drops in my dotfiles. 
It's best-tested on Debian, but has some cases for OSX and FreeBSD too.

# Interesting Variables

## `gui_enabled`

Boolean. Install and configure GUI tools, or with vim, choose between `gtk` and
`nox`.

## `disable_stock_users`

Boolean.  Disable stock users like `pi` or `pine64`.

# Running

## Push

1. Create inventory file with target host, maybe extra vars
2. If we can ssh as root with key, use `-u root`.  If we can sudo, use `-bK`.
3. `ansible-playbook -i $inventory $args local.yml`
4. After the first run, `ansible` management user is created.

## Pull

1. Install `ansible`, `git`
2. `echo -e '[localhost]\nlocalhost ansible_connection=local' >> /etc/ansible/hosts`
3. `ansible-pull -U https://github.com/merrilymeredith/devbox-ansible.git`

### cloud-init

```yaml
#cloud-config
packages:
  - ansible
  - git
runcmd:
  - echo '[localhost]\nlocalhost ansible_connection=local' >> /etc/ansible/hosts
  - ansible-pull -U https://github.com/merrilymeredith/devbox-ansible.git
```

# TODO

- Make pull config install cron entry?
