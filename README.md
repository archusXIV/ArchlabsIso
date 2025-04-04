# ArchlabsIso

### ChangeLog
- Fixed weird EOF indentation after removing mixed-indent blocks of code.
- Removed virtualbox-guest-dkms package from the installer because it does not exist anymore.
- Fixed /etc/mkinitcpio.conf by changing archiso_kms to kms in the HOOKS array.

### Credits
Thanks to Nate for his great job on ArchLabs and for publishing so we can fork and customize our own iso.

### Building the ISO

The package `archiso` must be installed and it needs to be built on an `Arch x86_64` system.

First clone the repo to your system.

    git clone https://github.com/archusXIV/ArchlabsIso.git


Next make a directory to build the ISO in. It can be anywhere you like, it's just a place to work.

    mkdir ~/build


Now you need to move the contents of the `archlabs` folder into the new directory that you made.
**NOTE: It is very important that you do it as root**. Every file needs to be owned by root.
This can be done by opening a file manager as root, or from a terminal using `su` or `sudo`.

If you cloned the repo and made a directory as shown above, then you can run

    cp -r ~/Downloads/archlabs-iso/archlabs/* ~/build/
	cd ~/build


Before building you will need to clean your pacman cache.

    sudo pacman -Scc


Now just run the build script with `-u` to update the installer, see `./build -h` for more options.

    ./build -u


When finished there will be a directory called `out`, the ISO will be in there.


### Customization

- `profiledef.sh` contains the build setup for archiso and file permissions for certain files on the ISO.
   See: https://gitlab.archlinux.org/archlinux/archiso/-/blob/master/docs/README.profile.rst

- `packages.x86_64` This will be generated when building, to add more packages edit the build script.

- `efiboot` and `syslinux` contain boot configuration files.

- `pacman.conf` is used while building and has entries for the `archlabs` and `archlabs-testing` repos.

- `airootfs` is the live boot file system. This is where to add anything that you want included on the ISO.
Remember, **everything must be done as root**, if you add something, do it with `su`, `sudo`, or `doas`.
Once added update `profiledef.sh` if special permissions are needed *(executable, read-only, etc.)*
Also note that the files included in the iso will **not** be added to installed systems, this must be done
in the archlabs installer.

When finished, run the `build` script in the main directory.
