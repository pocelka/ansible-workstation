# Motivation

Lately I decided that Linux is better environment for my daily work, although I still use Windows 10 for gaming. One thing which is always a problem, as with any re-installation is the following setup. I choose Ansible as my go to tool for configuration as it is easier to document and execute compared to shell scripts.

I wanted to use Manjaro as I didn't have issue in the past with it and it has great package manager. However it broke after first update so I decided to use Fedora gnome edition instead. Over the year I used mainly Windows and KDE seemed like better option to not change dramatically my flow, however after short proof of concept for Ansible playbook it looked like it would be nightmare to configure kde with Ansible. So I decided to use gnome instead and so far I like it.

This repository contains copy of configuration that I'm using for my personal setup of my workstation (locally). While you can run it by yourself, I encourage you to inspect and modify roles before first usage.

## Pre-Setup

At home I have several computers. On my Ubuntu based HTPC in living room I want to share some disks using NFS.

To share data over NFS I need to modify `/etc/exports` and add the following lines:

```bash
/home/b0rg/data                 192.168.1.0/24(rw,sync,no_subtree_check)
/home/b0rg/backup_medium        192.168.1.0/24(rw,sync,no_subtree_check)
```

afterwards:

```bash
sudo exportfs -ra
sudo systemctl restart nfs-server
```

## Initial Setup

In order to be able to run Ansible playbooks I need to install few basic things before I can use Ansible.

- Initial setup:

    ```bash
    # Fedora:
    sudo dnf install ansible
    ansible-galaxy collection install community.general
    ```

- Execution

    ```bash
    # clone or download repository
    # make changes to group_vars/workstation
    ansible-playbook all.yml
    ```
