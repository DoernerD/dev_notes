## Windows Linux Subsystem Notes

# Mounting network drives

In order to mount network drives on WSL, first make the mount point with

    sudo mkdir /mnt/u

Now 'u' is your mount point in WSL. To mount a drive, execute

    sudo mount -t drvfs <network path to drive> /mnt/u

Now you can 'cd' into '/mnt/u' and have all files from the network drive
available
