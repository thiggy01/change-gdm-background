# ubuntu-20.04-change-gdm-background

This script automates the process of setting an image in the GNOME Display Manager 3 background
which comes by default with Ubuntu version 20.04 Focal Fossa.

## GUI version

If you are an experienced linux user and know how to compile programs, you can build my
new program that can make this task much easier with a just a few clicks with the mouse.

You just need access it's repo at https://github.com/thiggy01/gdm-background and follow the
instructions to have it installed on your system. I even added instructions on how to uninstall it.

## Warning

This script wont work with any older version of Ubuntu because they have a different
way of dealing with gdm settings.

It also won't work if your system is set to a custom gdm3 theme. You will have to reset to the
default configuration of gdm3 before using the script.

This tool was made specifically to work with Ubuntu 20.04 as it now bundles all
configuration files inside a .gresource file.

If you are going to set an image file that has spaces in its file name or folders, remember to
scape them with backslashes.

## Installation

First, you will need to install libglib2.0-dev-bin with `sudo apt install libglib2.0-dev-bin`

Then, you can download the script with the command below:
```
wget github.com/thiggy01/ubuntu-20.04-change-gdm-background/raw/master/ubuntu-20.04-change-gdm-background
```
And set it as an executable with `chmod +x ubuntu-20.04-change-gdm-background`

## Usage

Run the script with root privileges such as `sudo ./ubuntu-20.04-change-gdm-background /path/to/image`.

If you see a message `login image sucessfully changed`, then, when you restart gdm or reboot your
computer, your gdm background should be covered with the image you selected.

You can restore your original gdm theme any time with sudo `./ubuntu-20.04-change-gdm-background
--restore`.

If you feel this tool was useful and want to show some appreciation, you can donate via
https://ko-fi.com/thiggy01.

