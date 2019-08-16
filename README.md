# Devbox playbook

This is a playbook that installs dev tools and DE tools I like to have around 
and sets up some other preferences like repositories, and drops in my dotfiles. 
It's best-tested on Debian, but has some cases for OSX and FreeBSD too.

# Interesting Variables

## `gui_enabled`

Install and configure GUI tools, or with vim, choose between `gtk` and
`nox`.

## `disable_stock_users`

Default `true`.  Disable stock users like `pi` or `pine64`.

## `bootstrap_ansible_controller`

Create an `ansible` user for the controller to connect as, with a public 
key set up and sudo permission.

# Running

## Push

1. Create inventory file with target hosts, maybe extra vars
    - For a single host, `-i ${hostname},` works directly.
2. We'll need to be root:
    1. If we can ssh as root with key, use `-u root`.
    2. If we can sudo, use `-bK`.
3. `ansible-playbook -i $inventory $args playbook.yml`
4. After the first run, `ansible` management user is created.

## Pull

1. Install `ansible`, `git`
2. `ansible-pull -i localhost, -c local -U https://github.com/merrilymeredith/devbox-ansible.git`

### cloud-init

```yaml
#cloud-config
packages:
  - ansible
  - git
runcmd:
  - ansible-pull -i localhost, -c local -U https://github.com/merrilymeredith/devbox-ansible.git
```

# TODO

- Make pull config or bootstrap install cron entry?
