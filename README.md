Debian Hyperland
=========

An Ansible playbook that installs Hyprland on Debian 12 machines

Getting Started (Debian Install)
----------------

- Install Debian 12 from netinstall ISO
- Flash ISO onto USB flash disk (rufus, etecher, etc..)
- Insert USB flash disk into the machine you want to install, and reboot
- On reboot, select the USB flash disk to boot
- On Debian launch, select the normal "Graphical Install"
- Install Debian like normal, except when you get to the Install Packages option
- Unselect the following:
  - Debian desktop environment
  - Gnome
- Select the "SSH server"
- Continue install as normal
- Click continue to reboot

Installing Prerequisites
----------------

- Login into the new Debian machine, using the credentials you created during install
- Run `su`

```bash
su
```

- Install `sudo` package

```bash
apt install sudo
```

- Add your useraccount to the `sudo` and `input` groups

```bash
/sbin/usermod -aG sudo,input <username>
```

- Run `visudo` (optional)

```bash
/sbin/visudo
```

- Change the `%sudo` group to not require password (optional)

```bash
    change %sudo   ALL=(ALL:ALL) ALL
    to %sudo   ALL=(ALL) NOPASSWD:ALL
```

- Save and exit `visudo`
- Exit and re-login

```bash
exit
```

- Install the following prerequisites packages

```bash
sudo apt install curl git ansible
```

- Clone the repository from github

```bash
git clone https://github.com/mikepruett3/debian-hyprland.git
```

- Run the `hyprland.yaml` playbook (Its going to take a while...)

```bash
ansible-playbook hyprland.yaml
```

- After the playbook finishes, reboot the machine

```bash
/sbin/reboot
```

Using my dotfiles (Optional)
----------------

I have pretty basic configurations in my dotfiles repo, that manage several Hyprland configurations. Your more than welcome to try them.

I use `chezmoi` to manage my dotfiles, so you will need to install `chezmoi` to get them.

```bash
sh -c "$(curl -fsLS get.chezmoi.io)" -- init --apply mikepruett3
```

My dotfiles also include a bootstrap script to install a bunch of my most-used utilities and apps. One of which is `tailscale`. If you are using `tailscale` like I am, after `chezmoi` does its thing, run the folloing to join your machine to the tailnet...

```bash
sudo tailscale up
```
