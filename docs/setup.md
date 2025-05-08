---
title: Setting Up
layout: default
nav_order: 2
---

# BSL Server

## Connecting to the Server

By this point, you should have received your account information (consisting of `username` and `password`) required to connect to the Berkeley Seismology Lab servers.

If not done so already, [install Visual Studio Code](https://code.visualstudio.com/download). Then, install an extension named `Remote - SSH` developed by Microsoft.

Show all commands using `Shift + Command + P` (or `Shift + Control + P`) to run the command `Remote - SSH: Connect to Host`.

Select `Add New SSH Host`, and connect to `<username>@range.geo.berkeley.edu`, replacing `<username>` with the username you have received. Enter password when prompted.

You should be able to connect to the server at this point!

## Changing the Password

If you wish to change the password required to remote SSH into the BSL server, simply execute the command `passwd` in the remote terminal.

## Workspace Directory

The path in the server you are given access to should look like the following: `/home/gcl/TT/<username>`. It is recommended that you create a workspace folder within this path (`mkdir /home/gcl/TT/<username>/workspace`) and reserve that space for all code, since the parent directory may also be used for package managers.

# Package Manager

While working in the BSL, you will often modify multiple python files with varying version of library imports. In order to simplify this process, we will be using [miniconda](https://docs.anaconda.com/miniconda/) to manage our Python packages. 

## Before installing Miniconda

Before installing Miniconda, we must first unload the Python module that the server makes us use by default. With the terminal open inside the remote SSH, enter `module unload python`. Then, execute `vim ~/.bashrc`. This opens the configuration file, which contains commands that execute every single time you open a new terminal. Press the down arrow key and go all the way to the bottom of the bashrc file, press `i` to go into insert mode (which allows you to modify the file), and write down `module unload python` at the bottom of the file.

## Installing Miniconda

Inside `/home/gcl/TT/<username>`, follow the instructions present in [this link](https://docs.anaconda.com/miniconda/install/#quick-command-line-install) to download the package manager. Make sure that you are installing the `Linux` version of Miniconda.

IMPORTANT: we will be installing version `Miniconda3-py311_23.10.0-1-Linux-x86_64.sh`. Please follow the instructions under `download an older version`.

Congratulations! You are now fully set up for BSL work.