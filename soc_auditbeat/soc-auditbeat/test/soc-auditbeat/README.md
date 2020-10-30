SOC Auditbeat
=========

This role installs auditbeat and centralize auditd and system module logs in SOC ELK:

| Module  | Description                                |
|---------|--------------------------------------------|
| auditd  | admin actions                              |
| host    | General host information, e.g. uptime, IPs |
| login   | User logins, logouts, and system boots.    |
| package | Installed, updated, and removed packages   |
| process | Started and stopped processes              |
| user    | User information                           |

HOWTO
------------
Add this role to your roles/requirements.yml:

```
---
- src: git@git.vptech.eu:veepee/security/security-galaxy/soc-auditbeat.git
  scm: git
  version: "master"
  name: "soc-auditbeat"
```

Create a directory named imported-roles and add it in your current project ansible.cfg:
```
[defaults]
roles_path = imported-roles:roles
```

Import the hardening-linux role in your project:
```
ansible-galaxy install -f -r roles/requirements.yml
```

Exclude imported-roles in .gitignore:
```
imported-roles/*
```

Role Variables
--------------

| Variable    | Description                                                |
|-------------|------------------------------------------------------------|
| auditbeat_ownership   | Tribe or corporate department ownership of the server      |

Example Playbook
----------------

Create a playbook named soc-auditbeat.yml:

    - name: Install auditbeat from SOC
      hosts: all
      become: yes
      roles:
        - role: soc-auditbeat
      vars:
        auditbeat_ownership: tribe_name or corp_dep_name


Deploy the playbook with:

```
ansible-playbook -i inventories/hosts soc-auditbeat.yml
```
