# Development Environment Setup

This guide will outline the minimum steps to get a development environment up and running.

Despite us working in Python, we will be skipping the installation of it as a direct executable for now. We work in virtual environments to get around this. A virtual environment is an excellent way to manage all our libraries and executables so they don't screw with the system. If you want to install things directly, then have a look at the [Python website](https://www.python.org/), but you will need to do some research to support yourself adequately.

## Terminal Setup

The term 'Terminal' refers to a text prompt to enter commands on your system. It is an essential tool when working with the robot. Some basic knowledge is assumed when working through these instructions. If something is unclear, try a quick Google or ask in Slack!

Windows:  Windows has several terminal options by default. We recommended installing [Windows Terminal](https://apps.microsoft.com/detail/9n0dx20hk701?hl=en-us&gl=US). We suggest configuring it to make the default profile Windows PowerShell if it isn't already and making it the default terminal application. Open like any other Windows program or swiftly by pressing the Windows key, typing `wt` and pressing enter. You can also open it directly in a folder by holding down shift, right-clicking the folder and selecting "open in PowerShell".

Mac: Open finder/spotlight and search for terminal to open. We suggest adding a keyboard shortcut for ease of access. Typical Linux usage has ctrl-alt-t, so an easy equivalent here is `command-option-t`.

Linux: use `ctrl-alt-t`.

You should pin the program to your relevant taskbar in all operating systems for easy access.

## Making a Github Account

Github is a code hosting service run by Microsoft. You are here now reading this guide!

Every software section member must create a GitHub account to contribute to our development. Follow the instructions on the [website](https://github.com/signup) to get started! Don't fret if you already have one from previous work or hobbies. You can continue using that same account, but we recommend you register a secondary email within the settings menu for your commit sign-offs and email notifications.

## Installing UV

UV is a Python package manager written in Rust. We use it to automate the installation of all the libraries we need to write code for the robot. It is a helpful tool to limit bugs throughout the season by guaranteeing everyone has identical versions and environments as things get updated. No one wants to hear "But it works on my machine!".

The installation instructions with more context are available on their [website](https://docs.astral.sh/uv/getting-started/installation/). We suggest using the standalone installer for your operating system.

For Windows, it is:

``` bash
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

For Linux and Mac users, it is:

``` bash
wget -qO- https://astral.sh/uv/install.sh | sh
```

## Installing a Text Editor

Any text editor should work. At a minimum, it should offer syntax highlighting (coloured text), linting (automatically flagging errors), and autocomplete. Many team members use Visual Studio Code (Vscode), which can be downloaded [here](https://code.visualstudio.com/Download).

Note for Vscode users:

- Have a look around at the extensions available for themes and other things to make your life easier
- Download the Python extension for Python language support
- Download the Live Share extension to make pair programming with a fellow student or mentor easier

## Installing and Authenticating Git

We use Git to handle all of our version control within the team. It requires some basic authentication setup on every new machine before you can use it to contribute to the code on the team.

Check if you have installed Git by running `git --version` in your terminal. If you already have it, you can skip the first part of this step and generate an ssh key.

Windows: Visit the git website [here](https://git-scm.com/downloads) for the download. There are also some extra steps for installation here

- We suggest making your installed text editor the default editor for Git. It will default to Vim if you skip this, which isn't the most user-friendly thing.
- Install Git from the command line and also from 3rd part software
- Use bundled OpenSSH
- The other install options do not matter as much and can be left with the default selection

macOS: There is a version of Git built into macOS. It gets installed as a prerequisite for Homebrew. However, you can get a more up-to-date version from Homebrew too: `brew install git`

Linux: Install Git using your package manager. For an Ubuntu system, the command is `apt install git`

Next, you will need to generate an SSH key for authentication. Follow the instructions [here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to create the key. We suggest leaving the key with the default name and saving location and then having no password.

You will now need to add the public key to Github. From your terminal, run `cat ~/.ssh/id_rsa.pub` and copy the output, including the header and trailing email address, to a new key within the GitHub settings, `Github->Settings->SSH and GPG Keys->New SSH Key`.

NOTE: Windows users must run an extra step to ensure this authentication is maintained between reboots. Copy the code block here and paste it into your terminal. This assumes you didn't the ssh key when generating it!

``` bash
echo 'env=~/.ssh/agent.env

agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

agent_start () {
    (umask 077; ssh-agent >| "$env")
    . "$env" >| /dev/null ; }

agent_load_env

# agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2=agent not running
agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
    agent_start
    ssh-add
elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
    ssh-add
fi

unset env' >> ~/.bashrc
```

After this, reboot your system for the script to take effect.

At this point, we suggest doing the team [git tutorial](https://github.com/thedropbears/git-tutorial) if you haven't already or are unfamiliar with Git.

## Repo

The final step is to clone down the current git repo for the year. [Check our Github](https://github.com/orgs/thedropbears/repositories?type=source) to see if it has already been created. It will follow the naming standard of `py<GAME NAME>`. Otherwise, stand by because it will be up and running soon! Make sure you know where you are cloning the repo. We suggest you open a terminal in situ on your desktop or in your documents in a folder that you want to save your robotics work in going forward so things don't get lost.
