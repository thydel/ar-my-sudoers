# [Install my-sudoers with Ansible](https://github.com/thydel/ar-my-suoders)

- Install an admin sudoers user file in sudoers.d
- Give root power via sudoers on Debian
- Give root power via sudo group on Ubuntu
- Set per user env_keep

## note

- Not designed as a generic role
- Fit my needs
- Starting point, but
  - Easy to extend sudoers user dict
  - Easy to add more template using more sudoers user dict params

## Usage

Install via [Galaxy](https://galaxy.ansibleworks.com/):

```
ansible-galaxy install thydel.my-sudoers
```

## Role Default Variables

```yaml
sudoers_super: True
sudoers_template: default
sudoers_envkeep: []
```

## Role Variables

```yaml
sudoers:
  users:
    - user: someone    # user name
	  super: True      # can sudo root - default to sudoers_super
	  template: simple # template file - default to sudoers_template
	  env_keep: 
		  - HOME       # list of environment variable to keep - default to sudoers_envkeep
    - &thy
      user: thy
      env_keep:
        - HOME
    - &cedric
      user: cedric
  active:
    - *thy
```

## Example Playbook

```yaml
- hosts: all
   roles:
	- thydel.my-sudoers
```

## WARNING

- Maybe using group for Ubuntu was not a goot idea
 - I found no simple way to remove a user from a group using user module
 - If a user.super change from True to False, user keep ability to sudo root
 
