
# Local Virtual Machine Setup

## Create your own VM

For parts  of this class, we will be making use a Kali VM. In a departure from what may be the usual approach, each of you will be creating your own VM.

Here is a high level overview of the process (some or all of which you may already have done):

1. Using the COE's software install pageLinks to an external site., install one of
    - VMWare Fusion (for macOS)
    - VMWare Workstation (for Windows)
1. Download an appropriate image from the Kali downloads page (Links to an external site.)
    - You really should get a 64-bit version
    - I use the 2020.2 installer, then install Cinnamon desktop.
    - There are pre-built VM appliances available for VMWare, VirtualBox, and Hyper-V, if you would prefer to go that route
1. Create a new VM, point it to your downloaded ISO file, and run through the install process
    - If you run into errors about virtualization extensions needing to be enabled, you'll need to do this in the BIOS. 
      This is OEM/model specific, and you'll have to figure this one out. Searching your model name plus VTx or virtualization is 
      typically a good starting point.
    - I would recommend at least 4GB of RAM -- 8GB would be better
    - I would also suggest at least 2 CPU cores
    - I would suggest at least a 60GB hard drive -- it uses on-demand allocation, so it won't use all 60GB at once.
1. Make sure to create your user account, rather than running as root (kali has changed a bit)
1. Please run this script to install all necessary packages and files for the course (you'll need to create the file on your VM).
     
```bash
    #!/bin/bash

    sudo apt update
    sudo apt upgrade

    #install necessary tools
    sudo apt install zsh tmux emacs cinnamon kali-defaults kali-root-login desktop-base gdb python3-pip cmake gdb-peda gnome-terminal cowsay figlet filters fortunes bsdgames bsdgames-nonfree dos2unix asciinema python3-pyx squashfs-tools squashfs-tools-ng zlib1g-dev liblzma-dev liblzo2-dev docker.io containerd xfsprogs 

    #optional, uncomment if you want a "full" kali install -- is a large download, so it's commented by default
    #just remove the # character
    #sudo apt install kali-tools-gpu kali-tools-hardware kali-tools-fuzzing kali-tools-sdr kali-tools-rfid kali-tools-information-gathering kali-tools-vulnerability kali-tools-passwords kali-tools-wireless kali-tools-reverse-engineering kali-tools-exploitation kali-tools-forensics cmake libboost-all-dev texlive-full emacs auctex fontforge doxygen python3-scipy python3-numpy graphviz radare2-cutter

    #install gef
    wget -q -O- https://github.com/hugsy/gef/raw/master/scripts/gef.sh | sh
    sudo -H pip3 install keystone-engine ropper capstone unicorn requests

    #environment setup
    wget -q -O setup-373.tar.bz2 https://web.engr.oregonstate.edu/~dmcgrath/setup-373.tar.bz2
    tar xjvf setup-373.tar.bz2 -C ~/
    chsh --shell /bin/zsh
```
- this will install a decent amount of packages, as well as update things to the most recent -- fairly large download!
- this pulls down an archive file with all the necessary files for environment I'd recommend you use, as well as labs and homeworks for which you'll be using this VM.
- You will be instructed later if you will need to modify this VM or create additional, smaller VMs.

Some important notes regarding the terminal environment I had you pull down:

- It switches your shell to zsh rather than bash -- this isn't required, though is recommended, and will be assumed if you ask me for help with something related to the VM.
- Every shell you open exists within a tmux session. This means it is
    - recoverable
    - splittable
    - configurable
    - informative
- Ctrl-T is the chord key -- Ctrl-T, a means hit control-t, release it, then hit a
- Within tmux, you can split your window into panes with Ctrl-T, \ for a side by side split, and Ctrl-T, - for a top/bottom split.
- You can create new windows with Ctrl-T, c and rotate between them with Ctrl-T, n and Ctrl-T, p
- Copy and paste is a little more complicated than you may be used to
    - to copy text within a terminal session, highlight it
    - to paste that text, hit Ctrl-T, ]
    - to paste text copied into the system clipboard (from outside the terminal), hold shift and middle click your mouse
    - to copy terminal text into the system clipboard, hold shift while you highlight it
- Scrolling doesn't use the scroll bar, but rather, uses the mouse. Just scroll up or down as you desire with your mouse.

