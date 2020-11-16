# Ubuntu Instructions

## Installation
Ubuntu 20.04 LTS Server Edition is the standard recommended Linux distro, as it's both very stable and will receive long term support (LTS). 

The Server Edition is recommended over the Desktop edition, as it doesn't contain superflous apps and features that'll needlessly consume resources.

You'll need an USB stick of 8GB or more for the installation, be aware that everything on it will be deleted.

1. Download Ubuntu 20.04 LTS Server Edition [here](https://releases.ubuntu.com/20.04/ubuntu-20.04.1-live-server-amd64.iso).

2. Install [Rufus](https://rufus.ie) on your regular computer and create an USB installation stick with the ISO. It should be pretty self-explanatory, just follow the steps.

3. Disconnect the USB stick from your regular computer and connect it to your staking system. 

4. Make sure the BIOS is set to boot from the USB first, and boot the Ubuntu installer. 

 **Be aware that EVERYTHING on the computer will be deleted by the installer.**

5. Follow the steps, use the keyboard to navigate.


## Extend Partition
For some reason the Ubuntu installer partitioner won't use your full SSD space by default when creating the partitions. Thankfully expanding the partition to use all available space is damn easy and takes seconds.

Do the following the installation of Ubuntu. It also works fine even if you installed Ubuntu a long time ago and have processes running.

1. ```lvextend -l +100%FREE /dev/mapper/ubuntu--vg-ubuntu--lv```
2. ```sudo resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv```

## Firmware and BIOS upgrading
Don't forget to also upgrade your firmware/BIOS to the latest versions at this point, since doing that when you are already staking will involve downtime.

Instructions varies depending on what type of system you have, but instructions for Intel NUC10s can be found [here](https://www.intel.com/content/www/us/en/support/articles/000033291/intel-nuc.html). The F7 method is recommended.