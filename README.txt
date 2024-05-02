Multi-Client PXE Network Boot

From: https://forums.raspberrypi.com/viewtopic.php?t=315172
Originally by user RonR


The attached scripts are an effort to automate the process of creating and maintaining a multi-client PXE network boot server.  Multiple Raspberry Pi clients can be served from a single Raspberry Pi server.  The PXE network boot server can be installed on any model Raspberry Pi.  Suitable PXE network boot clients are:

Raspberry Pi 5
Raspberry Pi 400
Raspberry Pi 4B
Raspberry Pi 3B+
Raspberry Pi 3B (with OTP bit 17 set)
Raspberry Pi 2B (rev 1.2)
Raspberry Pi    (any model 1B/2B/3B with an SD card containing only bootcode.bin)

pxe-install is executed on the server and creates the base BOOT (/pxe-boot) and ROOT (/pxe-root) directories, installs and configures dnsmasq and nfs-kernel-server, and enables rpcbind and systemd-networkd.  A reboot is required before the PXE network boot server can be used.

pxe-add adds an image file to the PXE network boot server.  The serial number of the Raspberry Pi client that is to be used with this image file must be specified followed by the image file name.  Optionally, a single client IP address IP address or a range of IP addresses denoted by CIDR (192.168.1.0/24) or netmask (192.168.1.0/255.255.255.0) may also be specified.  If no client IP address is specified, access will be granted to all clients.

pxe-del deletes a Raspberry Pi client serial number and its associated image file from the PXE network boot server.

pxe-chroot performs a linux 'chroot' to the image file associated with the specified Raspberry Pi client serial number.  The current user will be 'root' and the current directory will be '/'.  The host's root filesystem will be available at /host-root-fs.  Use exit or ^D to terminate chroot.  Make sure the Raspberry Pi associated with the specified serial number is not running.

pxe-serial can be run on a Raspberry Pi client to obtain its serial number and to verify it's a suitable model.

image-backup can be used to create an image file of an SD card or USB based system that can then be added to the PXE network boot server.
