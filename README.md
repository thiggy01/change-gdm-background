# ubuntu-20.04-change-gdm-background

This script automates the process of changing the GNOME Display Manager
background of Ubuntu version 20.04 Focal Fossa.

## Warning

This script wont work with any older version of Ubuntu because they have a different
way of dealing with gdm settings.

This tool was made specifically to work with Ubuntu 20.04 as it now bundles all 
configuration files inside the gdm3-theme.gresource file. 

## Installation

First, you will need to install libglib2.0-dev-bin with `sudo apt install libglib2.0-dev-bin`

Then, you can download the script with the command below:

    curl -L -O github.com/thiggy01/ubuntu-20.04-change-gdm-background/raw/master/ubuntu-20.04-change-gdm-background

And give it execution permition with `chmod +x gdm-change-login-background`

## Usage

Run the script with root privileges such as `sudo ./ubuntu-20.04-change-gdm-background /path/to/image`.

If you see a message `login image sucessfully changed`, then, when you restart gdm or reboot your computer, your gdm background should be covered with the image you selected.

You can restore your original gdm theme any time with sudo `./ubuntu-20.04-change-gdm-background --restore`.

If you feel this tool was useful and want to show some appreciation, you can donate me via https://ko-fi.com/thiggy01.

