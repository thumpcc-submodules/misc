# Thy's desktop environment

How I configure my desktop environment

## Operating System

I use [Linux Mint 21.1, codename Vera](https://linuxmint.com/rel_vera_cinnamon.php) which is based on [Ubuntu 22.04, codename Jammy Jellyfish](https://wiki.ubuntu.com/JammyJellyfish).

[Cinnamon Desktop Environment](https://en.wikipedia.org/wiki/Cinnamon_(desktop_environment)) derives from [GNOME 3](https://en.wikipedia.org/wiki/GNOME_3) but follows traditional [desktop metaphor](https://en.wikipedia.org/wiki/Desktop_metaphor) conventions.


## Settings

### Update apt's `sources.list`

Change to local mirror, for example http://mirror.0x.sg/ubuntu

```{code-block} shell
sudo sed -i 's!http://archive.ubuntu.com/ubuntu!http://mirror.0x.sg/ubuntu!g' /etc/apt/sources.list
sudo sed -i 's!http://security.ubuntu.com/ubuntu!http://mirror.0x.sg/ubuntu!g' /etc/apt/sources.list
```

Get the URL from https://launchpad.net/ubuntu/+archivemirrors or run

```{code-block} shell
curl mirrors.ubuntu.com/mirrors.txt
```


<!--
### Replicate Windows Shortcuts

I'm a Linux user who are `forced` to use Windows at work. 

Here's how to replicate Windows shortcuts to my Development Machine.

```{admonition} TODO
put the `dconf load` command
```
-->

### Jetbrains PyCharm shortcuts conflict

Some shortcuts conflict with global system actions. To fix these conflicts, I reassign or disable the conflicting shortcut.

Taken from [jetbrains](https://www.jetbrains.com/help/pycharm/configuring-keyboard-and-mouse-shortcuts.html#conflicts), here are a few examples of system shortcut conflicts with the default keymap in PyCharm

| Shortcut            | System action                            | IntelliJ IDEA action            |
|---------------------|------------------------------------------|---------------------------------|
| Ctrl+Alt+S          | Shade window                             | Open the Settings dialog        |
| Ctrl+Alt+L          | Lock screen                              | Reformat Code                   |
| Ctrl+Alt+T          | Launch Terminal                          | Surround With                   |
| Ctrl+Alt+F12        | Open the tty12 virtual console	File path |                                 |
| Ctrl+Alt+Left/Right | Switch between Workspaces                | Undo/redo navigation operations |
| Alt+F7              | Move window                              | Find Usages                     |
 | Alt+F8              | Resize window                            | Evaluate Expression             |


## Applications

### Miniconda 

[Miniconda](https://docs.conda.io/en/latest/miniconda.html) is a free minimal installer for conda. It is a small, bootstrap version of Anaconda that includes only conda, Python, the packages they depend on, and a small number of other useful packages, including pip, zlib and a few others. 

#### Install

Download the installer and verify [SHA256](https://docs.conda.io/en/latest/miniconda.html#latest-miniconda-installer-links) hash

```shell
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
sha256sum ~/miniconda.sh
```

Run `miniconda.sh`

```shell
bash ~/miniconda.sh -b -p $HOME/miniconda
rm -f ~/miniconda.sh
```

Update conda

```shell
. ~/miniconda/etc/profile.d/conda.sh
conda init
conda config --set auto_activate_base false
conda update -yn base -c defaults conda
```

#### Create `thy` environment

If there is an existing `thy` environment, remove it

```shell
conda deactivate
conda env remove -n thy
```

Create `thy` environment

```shell
conda create -n thy --no-default-packages -y python=3.9
conda activate thy
pip install -U pip
```

## Reference

- <https://github.com/webpro/awesome-dotfiles>
