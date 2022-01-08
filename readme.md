# Motivation

I decided, that at home, Linux is better environment for my daily work, although I still use Windows 10 for gaming. As with any OS setup, it takes time to configure everything. Ansible can greatly simplify the whole configuration process as well as to document everything, compared to shell scripts.

In the past I used Fedora, Ubuntu and Manjaro, however after few issues with Manjaro a decided to go back to Fedora. Over the years when I used mainly Windows, KDE looked like obvious alternative, but after short proof of concept with Ansible playbook I decided to use Gnome instead due to dconf utility.

This repository contains copy of configuration that I'm using for my personal setup of my workstation (locally).

While you can run it by yourself, I encourage you to inspect and modify roles before first usage.

## Pre-Setup

At home I have several computers. From Ubuntu based HTPC in living room I want to share some disks using NFS.

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

    # or run just specific tag
    ansible-playbook -t [tag] all.yml
    ```
