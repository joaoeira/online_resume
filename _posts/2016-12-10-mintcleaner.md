---
layout: post
title: How To Keep Your Mint Installation Clean
category: Post
tags: [Tips, Tech]
---

If you are using Mint as your OS and are running low on space in your main drive, or just want to clean it up, you can use this little script I found somewhere online that's been useful to me as I fill my old laptop's 20GB SSD:

1. Create a file in your home directory titled *mintcleaner.sh* with the following code:

```
 #!/bin/bash

OLDCONF=$(dpkg -l|grep "^rc"|awk '{print $2}')
CURKERNEL=$(uname -r|sed 's/-*[a-z]//g'|sed 's/-386//g')
LINUXPKG="linux-(image|headers|ubuntu-modules|restricted-modules)"
METALINUXPKG="linux-(image|headers|restricted-modules)-(generic|i386|server|common|rt|xen)"
OLDKERNELS=$(dpkg -l|awk '{print $2}'|grep -E $LINUXPKG |grep -vE $METALINUXPKG|grep -v $CURKERNEL)
YELLOW="\033[1;33m"
RED="\033[0;31m"
ENDCOLOR="\033[0m"

if [ $USER != root ]; then
  echo -e $RED"Error: must be root"
  echo -e $YELLOW"Exiting..."$ENDCOLOR
  exit 0
fi

echo -e $YELLOW"Cleaning apt cache..."$ENDCOLOR
aptitude clean

echo -e $YELLOW"Removing old config files..."$ENDCOLOR
sudo aptitude purge $OLDCONF

echo -e $YELLOW"Removing old kernels..."$ENDCOLOR
sudo aptitude purge $OLDKERNELS

echo -e $YELLOW"Emptying every trashes..."$ENDCOLOR
rm -rf /home/*/.local/share/Trash/*/** &> /dev/null
rm -rf /root/.local/share/Trash/*/** &> /dev/null

echo -e $YELLOW"Script Finished!"$ENDCOLOR
```

2. Open the terminal in your home directory and write:

```
sudo chmod +x mintcleaner.sh
sudo sh mintcleaner.sh
```
Let the script run and it should reduce the amount of space the OS is taking. 
