---
layout: post
title: "NTFS-3G: R/w Ntfs in Mac"
date: 2012-01-20 15:33
comments: true
categories:
- Note
---

### Fuse4x + NTFS-3G from MacPorts

    sudo port install ntfs-3g

Backup `mount_ntfs`:
    sudo mv /sbin/mount_ntfs /sbin/mount_ntfs.orig

Create some script for tricking OSX into redirecting the automount procedure for OSX's native NTFS to use NTFS-3G instead:
    sudo touch /sbin/mount_ntfs
    sudo chmod 0755 /sbin/mount_ntfs
    sudo chown 0:0 /sbin/mount_ntfs
    sudo nano /sbin/mount_ntfs

Paste the script in the editor:

{% codeblock lang:bash %}
#!/bin/bash

VOLUME_NAME="${@:$#}"
VOLUME_NAME=${VOLUME_NAME#/Volumes/}
USER_ID=501
GROUP_ID=20
TIMEOUT=20

if [ `/usr/bin/stat -f "%u" /dev/console` -eq 0 ]; then
    USERNAME=`/usr/bin/defaults read /library/preferences/com.apple.loginwindow | /usr/bin/grep autoLoginUser | /usr/bin/awk '{ print $3 }' | /usr/bin/sed 's/;//'`
    if [ "$USERNAME" = "" ]; then
        until [ `stat -f "%u" /dev/console` -ne 0 ] || [ $TIMEOUT -eq 0 ]; do
            sleep 1
            let TIMEOUT--
        done
        if [ $TIMEOUT -ne 0 ]; then
            USER_ID=`/usr/bin/stat -f "%u" /dev/console`
            GROUP_ID=`/usr/bin/stat -f "%g" /dev/console`
        fi
    else
        USER_ID=`/usr/bin/id -u $USERNAME`
        GROUP_ID=`/usr/bin/id -g $USERNAME`
    fi
else
    USER_ID=`/usr/bin/stat -f "%u" /dev/console`
    GROUP_ID=`/usr/bin/stat -f "%g" /dev/console`
fi

/opt/local/bin/ntfs-3g \
    -o volname="${VOLUME_NAME}" \
    -o local \
    -o noappledouble \
    -o negative_vncache \
    -o auto_xattr \
    -o auto_cache \
    -o noatime \
    -o windows_names \
    -o user_xattr \
    -o inherit \
    -o uid=$USER_ID \
    -o gid=$GROUP_ID \
    -o allow_other \
    "$@" &> /var/log/ntfsmnt.log

exit $?;
{% endcodeblock %}

Press `Ctrl`+`X`, say `Y` to save, press Enter to accept the file name.

Now, note the option `-uid` and `-gid`. It teels __ntfs-3g__ which OSX user and group should own the files on the mounted volume. If you don't provide these options, ntfs-3g will default to the root user, which will allow you to do most writing operations on the volume except write/modify to existing files - __to be able modify files, you should then specify the uid and gid for the login you use on your system__. In a standard OSX installation, the `uid 501` and `gid 20` should be the first standard user you provided on OSX install, and the "staff" group, respectively. To make sure these `uid` and `gid` pair match the ones for the user you use on your system, type in the Terminal (make sure you're not on a root ("#") prompt):

    id -u && id -g

This should output two lines:  
- the first containing the id for your user  
- the second the id of the default group for your user

__If they don't match the ones on the script, edit the script again and modify it accordingly.__  
Update: This is needed only in a worst case scenario where you have autologin disabled and you don't login manually within 20 seconds (adjustable in the TIMEOUT variable).


### TIPS:
Command of listing disks in Mac through terminal:

    df [-Th]

It seems `fdisk -l` only works in linux(not sure, but it doesn't work).


### REFERENCES:

- [NTFS WRITE SUPPORT ON OSX LION WITH NTFS-3G](http://fernandoff.posterous.com/ntfs-write-support-on-osx-lion-with-ntfs-3g-f)
- [Install NTFS-3G with read-write on OS X Lion using MacPorts](http://superuser.com/questions/316341/install-ntfs-3g-with-read-write-on-os-x-lion-using-macports)
