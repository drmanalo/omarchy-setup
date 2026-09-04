# Omarchy Applications Setup using Ansible

Playbook for minimum software and tools required for a software developer.

![Omarchy desktop](omarchy.png)

## Dependencies

- **[Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)**: `sudo pacman -S ansible`
- **Ansible community.general collection**: `ansible-galaxy collection install -r requirements.yml`
- **yay**: ships with Omarchy by default

## How to run

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

## Windows dual-boot

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

## Customisation

**for iframe issues**

```
❯ cat ~/.config/google-chrome-flags.conf 
--disable-features=WaylandLinuxDrmSyncobj
```

**input.lua**

`ctrl:swap_lalt_lctl:` left Alt (Cmd position) becomes Ctrl and left Ctrl becomes Alt, for Mac-style Cmd shortcuts across all apps.

```
hl.config({
    input = {
    kb_layout = "us,eu",
    kb_options = "compose:caps,shift:both_capslock_cancel,grp:alts_toggle,ctrl:swap_lalt_lctl",
    natural_scroll = true,
    numlock_by_default = true,
    repeat_rate = 40,
    repeat_delay = 250,
    sensitivity = 0.35,
    scroll_factor = 1.5,

    touchpad = {
      clickfinger_behavior = true,
      disable_while_typing = true,
      natural_scroll = true,
      scroll_factor = 0.9,
    },
  },
})
```

**monitors.lua**


```
hl.monitor({ output = "DP-3", mode = "3840x1600", position = "0x0", scale = omarchy_monitor_scale })
hl.monitor({ output = "eDP-2", mode = "2560x1600", position = "3840x0", scale = omarchy_monitor_scale })
```
