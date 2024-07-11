---
layout: page
title: Setup
---

## Ensure you have a working shell

"The shell" is what we call a program that enables us to send commands to the computer and receive output. It is also referred to as the terminal or command line. There are many different programs that can operate as a shell. We will use the `bash` shell (though if you are using a Mac, you may use a shell called `zsh`). 

This shell is what we will be using in the second half of the workshop after lunch!

### The instructions below should get you a working shell running on your own laptop or desktop computer.

> ## Windows users
> Computers running the Microsoft Windows operating systems  do not automatically have a Unix Shell program installed. They have Powershell and the DOS shell instead. 
> 
> However, since the release of Windows 10, Microsoft has provided the Windows Subsystem for Linux (WSL), that allows a complete virtual Linux system hosted on your Windows machine locally. This allows developers to access the power of both Windows and Linux at the same time on a Windows machine. 
>
> While users can install multiple Linux distributions at the same time, I recommed sticking to the default (Ubuntu), especially for beginners.
>
> To install WSL and the default Ubuntu distribution, users can follow the instructions hyperlinked from Microsoft for both [Windows 10 and Windows 11]. But in summary, the steps will look something like this:
> 
> 1. find the PowerShell application and open it _in Administrator mode_ (right click on the application icon to run in Administrator mode)
> 2. From the PowerShell command line, type `wsl --install`. Wait for the command to finish, and then restart the machine.
> 3. Then type `wsl -l -v` to see what Linux distributions have been installed. The default at time of writing is Ubuntu 22.04 under WSL 2.
> 4. From the start menu, type "Linux", or "Ubuntu", and you should have a Linux distribution available to run. The first time you launch it might be a bit slow.
>
> > ## Accessing the Linux File System from Windows File Explorer
> > 
> >To allow ourselves to access the Linux filesystem (mounted as a virtual disk) in the Windows Explorer, follow the steps [here].
> > Alternatively:
> > 1. Open File Explorer
> > 2. Type `\\wsl$` in the address bar, and press `Enter`
> >
> > OR: Enter `\\wsl$` in the run command. i.e.: `[WINDOWS KEY + R] > \\wsl$ > [ENTER]`
> >
> > Our personal Linux files will typically be stored at: `\\wsl$\Ubuntu\home\<yourname>`. Where <yourname> is the username you defined during installation.
> >
> {: .idea}
>
> > ## Removing Ubuntu from WSL2
> >
> > In case the user is interested in removing/resetting their Ubuntu image from WSL2/their laptops after the workshop, they can do so by entering PowerShell in Administrator mode and:
> > 1. Find the Bash shell distro name (likely `Ubuntu` by default) with: `wsl --list`
> > 2. Unregister (removing) the distro with `wsl --unregister Your_Ubuntu_distro`, replacing `Your_Ubuntu_distro` with the distro name you obtained from the step above. 
> >
> > Note that once unregistered, all data, settings, and software associated with that distribution will be permanently lost. Reinstalling by following the steps above (with `wsl --install` ) will install a clean copy of the distribution. For example, wsl --unregister Ubuntu would remove Ubuntu from the distributions available in WSL. Running wsl --list will reveal that it is no longer listed.
> >
> {: .idea}
> 
> Additional references are below.
> #### Reference
> * [Git for Windows](https://git-for-windows.github.io/)
> * [Using the Windows 10 Bash Shell](https://www.howtogeek.com/265900/everything-you-can-do-with-windows-10s-new-bash-shell/)
{: .windows}

> ## Mac OS X users
> For a Mac computer running macOS Mojave or earlier releases, the default Unix Shell is Bash. For a Mac computer running macOS Catalina or later releases, the default Unix Shell is Zsh. Your default shell is available via the Terminal program within your Utilities folder.
>
> To open Terminal, try one or both of the following:
> * Go to your Applications. Within Applications, open the Utilities folder. Locate Terminal in the Utilities folder and open it.
> * Use the Mac ‘Spotlight’ computer search function. Search for: `Terminal` and press <kbd>Return</kbd>.
>
> To check if your machine is set up to use something other than Bash, type echo $SHELL in your terminal window.
> If your machine is set up to use something other than Bash, you can run it by opening a terminal and typing bash.
>  
> > ## Homebrew and iTerm2
> > 
> > - While the MacOSX system comes with a proper shell by default, you will need a package manager to get the most out of it. I recommend installing the Homebrew ([https://brew.sh](https://brew.sh)) package manager on MacOSX. This will help you manage software installation from the command line.
> > - While the default terminal application on MacOSX is pretty good, the [iTerm2](https://www.iterm2.com/) application is an excellent alternative to the standard MacOSX terminal.
> > 
> {: .idea}
> 
> #### Reference 
> For more reading, go to[ How to Use Terminal on a Mac](http://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/)
{: .osx}

> ## Native Linux users
> You should be set to go! :)
> 
> The default Unix Shell for Linux operating systems is usually Bash. On most versions of Linux, it is accessible by running the [(Gnome) Terminal](https://help.gnome.org/users/gnome-terminal/stable/)
> or [(KDE) Konsole](https://konsole.kde.org/)
> or [xterm](https://en.wikipedia.org/wiki/Xterm),
> which can be found via the applications menu or the search bar.
> 
> If your machine is set up to use something other than bash, you can run it by opening a terminal and typing `bash`.
>
{: .linux}


## Some files you will need

*After you have a working shell,* you need to download some files to follow this workshop. These files include Nanopore sequencing data files which we will use during exercises in this workshop, and a .sh shell script which we will need to run on the Shell to install some packages necessary to follow along. These can be installed through the bash command line/terminal with the following line when in the same directory as where the install.sh script is stored:

~~~
sudo bash ./install_poh_lab.sh
~~~
{: .bash}


{% include links.md %}

[Windows 10 and Windows 11]: https://learn.microsoft.com/en-us/windows/wsl/install
[here]: https://devblogs.microsoft.com/commandline/access-linux-filesystems-in-windows-and-wsl-2/

<!-- this is an html comment -->

{% comment %} This is a comment in Liquid {% endcomment %}

<!-- References: https://swcarpentry.github.io/shell-novice/index.html -->
<!-- References: https://gtk-teaching.github.io/Intro-to-bash/setup.html -->
