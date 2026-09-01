# Omarchy Applications Setup using Ansible

Playbook for minimum software and tools required for a software developer.

![Omarchy desktop](omarchy.png)



### Dependencies

- **[Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)**: `sudo pacman -S ansible`
- **Ansible community.general collection**: `ansible-galaxy collection install -r requirements.yml`
- **yay**: ships with Omarchy by default

### How to run

```bash
❯ ansible-playbook -K developer.yml
BECOME password:

PLAY [AWS CLI] ****************************************************************

TASK [Gathering Facts] ********************************************************
ok: [localhost]

TASK [Install aws-cli-v2] ******************************************************
ok: [localhost]

PLAY RECAP *********************************************************************
localhost   : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

### Windows dual-boot (Limine)

Added manually via `limine-entry-tool`, not automatic. A Windows Boot Manager on a separate disk, will never appear on `limine` by default so it has to be manually added.

```
❯ limine-scan
Available EFI Boot Entries:
#  │ Name                                            │ EFI Path                        
───┼─────────────────────────────────────────────────┼──────────────────────────────────────
1  │ UEFI RST PVC10 SK hynix 1024GB MF2N000210702704 │ /EFI/Boot/BootX64.efi           
2  │ UEFI RST WD_BLACK SN850X 1000GB 23433M800574    │ /EFI/Boot/BootX64.efi           
3  │ Zorin OS                                        │ /EFI/ubuntu/shimx64.efi         
4  │ Windows Boot Manager                            │ /EFI/Microsoft/Boot/bootmgfw.efi
5  │ Limine                                          │ /EFI/limine/limine_x64.efi      

 [↑/↓] select | type [1-5] | [c] cancel
```

This lists every EFI boot entry it can find across all disks and lets you pick which ones to register in `/boot/limine.conf`. Pick the **Windows Boot Manager** entry to add.

Verify it was written before doing a `reboot`.

```
❯ grep -A2 -i "windows boot manager" /boot/limine.conf
```
