
# VM 449: Using Virtual Machines for CS 449

This course assumes that you have access to an [x86-64](https://en.wikipedia.org/wiki/X86-64) based [Linux](https://en.wikipedia.org/wiki/Linux) machine, and all code (including handouts and assignments) are designed to be run on a Linux host. However, in case you do not have such a machine handy, students who are enrolled in this course are automatically granted access to a special department server called `thoth.cs.pitt.edu` (which can also be accessed via its alias `cs449.cs.pitt.edu`) which runs [Ubuntu Linux 22.04.1 LTS](https://wiki.ubuntu.com/JammyJellyfish). While working and viewing code for this course on another Linux/macOS/Windows system is possible, for assignments, you must ensure that your code runs on the departmental server to receive credit. Hence, we encourage you to develop/work/test your programs on `thoth.cs.pitt.edu`.

However, in case you have trouble developing on the server (due to a maintenance request, busy server, poor internet connection, etc.), we are providing instructions on how to download and set up a **virtual machine** that can approximate the computing experience of an instructional Linux box at school that you can run on your desktop or laptop wherever you are. This document explains how this works, and what you need to do in order to use this software.

## What is a VM?
[Virtual machines](https://en.wikipedia.org/wiki/Virtual_machine) are emulated computer instances running inside a special program you install on your desktop or laptop computer. The virtual machine can run a completely different operating system than its host. For example, you could run a Linux or a Windows 10 virtual machine on your Macintosh laptop, or a Linux virtual machine on your Windows machine.

**Although VMs can approximate `thoth.cs.pitt.edu` very well, you must still ensure that your code compiles and runs on the server before submission.**

### Installing the Virtual Machine Host
Virtual machines run inside some other program, which runs on the host computer (your laptop or desktop). There are many programs such as [Virtual Box](https://www.virtualbox.org/) or [VM Ware](https://www.vmware.com/) that can be used to create virtual machines. This document, however, will use [QEMU](https://www.qemu.org/), which is a free and open-source software since it is compatible with most systems regardless of the underlying hardware and OS.

#### For Everyone
1. Move into the directory where you want to store the VM and clone this directory. You can clone this directory by running the following command:
	```sh
	git clone https://github.com/shinwookim/VM449
	```
2. Download the '**server install image**' for Ubuntu 22.04.2 LTS (Jammy Jellyfish) at https://mirror.cs.pitt.edu/ubuntu/releases/22.04/ and store it in the VM directory (created in step 1).
3. Install QEMU by following the steps below

##### On Windows
4. Install QEMU by visiting https://www.qemu.org/download/#windows and downloading an installer. Alternatively, you can use a package manager such as [Chocolatey](https://chocolatey.org/install).
5. After installing QEMU, add the QEMU path into the **Environment Variables**
	- Open **File Explorer**, go to the QEMU installation location, and then copy the path (E.g., `C:\Program Files\qemu`).
	- Right-click  **This PC**  /  **Computer**, choose  **Properties**, and then click  **Advanced system settings**.
	- Under the  **Advanced**  tab, click  **Environment Variables**.
	- In the  **User variables**  box, double-click the  **Path**  variable, click  **New**, and then paste the QEMU path.
	- Click the  **OK**  button to save changes, and then click the  **OK**  button again to save and exit the  **Environment Variables**
6. Double-click the `start.bat` file in the folder to launch QEMU
##### On MacOS
4. Install QEMU through [Homebrew](https://brew.sh/).
	1. If you do not have Homebrew already, you can install it by opening the terminal and running:
	```sh
	/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
	```
	2. Go through the installation steps. With Homebrew installed, you can now install QEMU by typing:
	```sh
	brew install qemu
	```
5. Once the installation finishes, you can start your VM by moving to where you cloned this repository (using `cd`) and typing:
	```sh
	./start.sh
	```
##### On Linux
Using your appropriate package manager, install your distro’s QEMU package. If you are unsure, please check [here](https://www.qemu.org/download/#linux). With QEMU installed, start the VM by running `start.sh` inside this repository.

#### Troubleshooting (MacOS/Linux)
If you are getting errors when running `start.sh` (such as Permission Denied), you may need to change permissions for the shell script via running:
```sh
chmod +x start.sh
```
