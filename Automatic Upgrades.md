# Automatic Upgrades

## Ubuntu Unattended Upgrades

Run this to configure security updates to be automatically installed:

```console
sudo dpkg-reconfigure --priority=low unattended-upgrades
```
Press **Enter**.

###Add *geth* to the list of packages to automatically upgrade

```console
sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```

Add ```"LP-PPA-ethereum:ethereum";``` on the line below ```"${distro_id}ESM:${distro_codename}-infra-security";``` and save the file.