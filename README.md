# Overview

This script automates the process of setting an image or color in GNOME Display Manager 3 background
which comes by default with Ubuntu based distros from the 20.04 onwards.

## Warning

This script wont work with any older version of Ubuntu or Pop OS because they have a different
way of dealing with gdm settings.

It also won't work if your system is set to a custom gdm3 theme. You will have to reset to the
default configuration of gdm3 before using the script.

This tool was made specifically to work with Ubuntu or Pop OS 20.04, 20.10 and 21.04 as it now
bundles all configuration files inside a .gresource file.

If you are going to set an image file that has spaces in its file name or folders, remember to
scape them with backslashes.

## GUI version

I have created a GUI program to make this task much easier and simple with just a few clicks
on the mouse.

The instructions to download it or compile it yourself can be accessed in
https://github.com/thiggy01/gdm-background.
It works either in Ubuntu or Pop OS 20.04 or 20.10 too.

## Installation

First, you will need to install libglib2.0-dev-bin with `sudo apt install libglib2.0-dev-bin`
Then, you can download the script with the command below:
```
wget github.com/thiggy01/change-gdm-background/raw/master/change-gdm-background
```
And set it as an executable with `chmod +x change-gdm-background`

## Usage

Run the script with root privileges such as `sudo ./change-gdm-background /path/to/image`.

If you see a message `login image sucessfully changed`, then, when you restart gdm or reboot your
computer, your gdm background should be covered with the image you selected.

You can restore your original gdm theme any time with `sudo ./change-gdm-background
--restore`.

### Change Color

Now you can change that annoying purple color to any color you like. Just type `sudo
./change-gdm-background \#yourhexcode` and voilá, you changed it. Your color hex format should
be of six characters like \\#407294 or three characters like \\#6ac.

### Multi-screen support

if you use two or more monitors you may see a streched image through the displays as if they were
    one screen. This is the default behavior of GDM3 when dealing with multiple displays.

I found a way to configure GDM to work in other modes like mirror or even single display
[here](https://github.com/thiggy01/change-gdm-background/issues/15), avoiding the joining of them.

## Donation

If you feel this tool was useful and want to show some appreciation, you can donate via
https://ko-fi.com/thiggy01.

