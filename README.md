
# VM 449: Using Virtual Machines for CS 449

This course assumes that you have access to an [x86-64](https://en.wikipedia.org/wiki/X86-64) based [Linux](https://en.wikipedia.org/wiki/Linux) machine, and all code (including handouts and assignments) are designed to be run on a Linux host. However, in case you do not have such a machine handy, students who are enrolled in this course are automatically granted access to a special department server called `thoth.cs.pitt.edu` (which can also be accessed via its alias `cs449.cs.pitt.edu`) which runs [Ubuntu Linux 22.04.1 LTS](https://wiki.ubuntu.com/JammyJellyfish). While working and viewing code for this course on another Linux/macOS/Windows system is possible, for assignments, you must ensure that your code runs on the departmental server to receive credit. Hence, we encourage you to develop/work/test your programs on `thoth.cs.pitt.edu`.

However, in case you have trouble developing on the server (due to a maintenance request, busy server, poor internet connection, etc.), we are providing instructions on how to download and set up a **virtual machine** that can approximate the computing experience of an instructional Linux box at school that you can run on your desktop or laptop wherever you are. This document explains how this works, and what you need to do in order to use this software.

## What is a VM?
[Virtual machines](https://en.wikipedia.org/wiki/Virtual_machine) are emulated computer instances running inside a special program you install on your desktop or laptop computer. The virtual machine can run a completely different operating system than its host. For example, you could run a Linux or a Windows 10 virtual machine on your Macintosh laptop, or a Linux virtual machine on your Windows machine.

**Although VMs can approximate `thoth.cs.pitt.edu` very well, you must still ensure that your code compiles and runs on the server before submission.**

### Installing QEMU
Virtual machines run inside some other program, which runs on the host computer (your laptop or desktop). There are many programs such as [Virtual Box](https://www.virtualbox.org/) or [VM Ware](https://www.vmware.com/) that can be used to create virtual machines. This document, however, will use [QEMU](https://www.qemu.org/), which is a free and open-source software since it is compatible with most systems regardless of the underlying hardware and OS.

#### For Everyone
1. Move into the directory where you want to store the VM and clone this directory. You can clone this directory by running the following command:
	```sh
	git clone https://github.com/shinwookim/VM449
	```
2. Download the '**server install image**' for Ubuntu 22.04.2 LTS (Jammy Jellyfish) at https://mirror.cs.pitt.edu/ubuntu/releases/22.04/ and store it inside the cloned repository (created in step 1). **DO NOT RENAME THE `.iso` FILE. The file name should be exactly `ubuntu-22.04.2-live-server-amd64.iso`**
3. Install QEMU by following the steps below

##### On Windows
4. Install QEMU by visiting https://www.qemu.org/download/#windows and downloading an installer. Alternatively, you can use a package manager such as [Chocolatey](https://chocolatey.org/install).
5. After installing QEMU, add the QEMU path into the **Environment Variables**
	- Open **File Explorer**, go to the QEMU installation location, and then copy the path (E.g., `C:\Program Files\qemu`).
	- Right-click  **This PC**  /  **Computer**, choose  **Properties**, and then click  **Advanced system settings**.
	- Under the  **Advanced**  tab, click  **Environment Variables**.
	- In the  **User variables**  box, double-click the  **Path**  variable, click  **New**, and then paste the QEMU path.
	- Click the  **OK**  button to save changes, and then click the  **OK**  button again to save and exit the  **Environment Variables**


##### On MacOS
4. Install QEMU through [Homebrew](https://brew.sh/).
	1. If you do not have Homebrew already, you can install it by opening the terminal and running:
	```sh
	/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
	```
	2. Go through the installation steps. Once Homebrew is installed, you can install QEMU by running:
	```sh
	brew install qemu
	```
##### On Linux
Using your appropriate package manager, install your distro’s QEMU package. If you are unsure of the package name, please check [here](https://www.qemu.org/download/#linux).


### Installing the VM
To ensure you've correctly installed QEMU, open your command line/terminal and run:
```sh
qemu-system-x86_64 -- version
```

You should be able to verify that QEMU is installed correctly if the terminal shows something like:
```
QEMU emulator version 7.2.94 (v8.0.0-rc4-12015-g9de3238476-dirty)
Copyright (c) 2003-2022 Fabrice Bellard and the QEMU Project developers
```
Once you've verified QEMU is installed, we can now setup the VM. For your convenience, we've provided several scripts to ease the installation process.
1. Examine and run the `setup.sh` (or `setup-win.bat`) from the terminal.
   - The first command `qemu-img create -f qcow2 VM449.qcow2 40G` creates a new virtual hard drive with a maximum capacity of 40GiB.
   - The second command `qemu-system-x86_64.exe -m 2G -usb -hda VM449.qcow2 -cdrom ubuntu-22.04.2-live-server-amd64.iso` will boot QEMU with the OS image loaded into the virtual CDROM.
2. Running the script above should open QEMU. Follow the steps within the VM to install Ubuntu onto your virtual hard drive.
3. Once installation has finished, you can power down your VM by running `sudo poweroff`.
4. Now, you can open QEMU by running the `run.sh` (or `run-win.bat`) script.

Note that the setup scripts will create a new virtual hard drive with the same name every time it is run. Hence, if you run `setup.sh` again after you've installed the OS, it will essentially *format* the disk and you will need to install the OS again.