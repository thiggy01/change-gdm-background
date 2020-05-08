#!/usr/bin/env bash
# Autor: Thiago Silva
# Contact: thiagos.dasilva@gmail.com
# URL: https://github.com/thiggy01/ubuntu-20.04-change-gdm-background
# =================================================================== #

# Check if script is run by root.
if [ "$(id -u)" -ne 0 ] ; then
    echo 'This script must be run as root.'
    exit 1
fi

# Check if glib 2.0 development libraries are installed.
if [ ! $(dpkg -s libglib2.0-dev-bin | grep Status | cut -d ' ' -f 4) \
    == installed ]; then
    echo 'Additional glib 2.0 libraries need to be installed.'
    read -p 'Type y or Y to proceed. Any other key to exit: ' -n 1
    if [[ "$REPLY" =~ ^[yY]$ ]]; then
	apt install libglib2.0-dev-bin
    else
	echo
	exit 1
    fi
fi

# Assign the default gdm theme file path.
gdm3Resource=/usr/share/gnome-shell/gdm3-theme.gresource

# Create a backup file of the original theme if there isn't one.
[ ! -f "$gdm3Resource"~ ] && cp "$gdm3Resource" "$gdm3Resource~"

# Restore backup function.
restore () {
mv "$gdm3Resource~" "$gdm3Resource"
if [ "$?" -eq 0 ]; then
    chmod 644 "$gdm3Resource"
    echo 'GDM background sucessfully restored.'
    echo 'Restart GDM service to apply change.'
    exit 0
fi
}

# Restore the original gdm3 theme.
[ "$1" == "--restore" ] && restore

# Test if argument is an image file.
if [[ $(file --mime-type -b "$1") == image/*g ]]; then

    # Define more variables.
    gdm3xml=$(basename "$gdm3Resource").xml
    workDir="/tmp/gdm3-theme"
    gdmBgImg=$(realpath "$1")
    imgFile=$(basename "$gdmBgImg")

    # Create directories from resource list.
    for resource in `gresource list "$gdm3Resource~"`; do
	resource="${resource#\/org\/gnome\/shell/}"
	if [ ! -d "$workDir"/"${resource%/*}" ]; then
	  mkdir -p "$workDir"/"${resource%/*}"
	fi
    done

    # Extract resources from binary file.
    for resource in `gresource list "$gdm3Resource~"`; do
	gresource extract "$gdm3Resource~" "$resource" > \
	"$workDir"/"${resource#\/org\/gnome\/shell/}"
    done

    # Copy selected image to the resources directory.
    cp "$gdmBgImg" "$workDir"/theme

    # Change gdm background to the image you submited.
    oldImg="#lockDialogGroup \{.*?\}"
    newImg="#lockDialogGroup {
	background: url('resource:\/\/\/org\/gnome\/shell\/theme\/$imgFile');
	background-size: cover; }"
    perl -i -0777 -pe "s/$oldImg/$newImg/s" "$workDir"/theme/gdm3.css

    # Generate gresource xml file.
    echo '<?xml version="1.0" encoding="UTF-8"?>
<gresources>
    <gresource prefix="/org/gnome/shell/theme">' > "$workDir"/theme/"$gdm3xml"
    for file in `gresource list "$gdm3Resource~"`; do
	echo "        <file>${file#\/org\/gnome/shell\/theme\/}</file>" \
	>> "$workDir"/theme/"$gdm3xml"
    done
    echo "        <file>$imgFile</file>" >> "$workDir"/theme/"$gdm3xml"
    echo '    </gresource>
</gresources>' >> "$workDir"/theme/"$gdm3xml"

    # Compile resources into a gresource binary file.
    cd "$workDir"/theme
    glib-compile-resources "$gdm3xml"

    # Move the generated binary file to the gnome-shell folder.
    mv gdm3-theme.gresource /usr/share/gnome-shell/

    # Check if gresource was sucessfuly moved to its default folder.
    if [ "$?" -eq 0 ]; then
    # Solve a permission change issue (thanks to @huepf from github).
	chmod 644 "$gdm3Resource"
	echo 'GDM background sucessfuly changed.'
	echo 'Do you want to restart gdm to apply change?'
	read -p '(y - yes, other keys - no): ' -n 1
	if [ "$REPLY" == y ]; then
	    service gdm restart
	fi
    else
	echo 'something went wrong.'
	restore
	echo 'No changes were applied.'
    fi

    # Remove temporary directories and files.
    rm -r "$workDir"

else

    # If no file was submited or file submited isn't an image,
    # show this message.
    echo 'Image file not foud.'
    echo 'Please, submit a .jpg or .png image file.'
    echo 'Usage: sudo ./ubuntu-20.04-change-gdm-background /path/to/image.*g'

fi
