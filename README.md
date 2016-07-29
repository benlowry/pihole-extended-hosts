# pihole-extended-hosts
[Pi-hole](https://pi-hole.net) (or [@pi-hole/pi-hole](https://github.com/pi-hole/pi-hole)) supplemented by [@StevenBlack/hosts](https://github.com/StevenBlack/hosts) for privacy, security and malware.

The `custom.hosts` allows you to map your own domains to your private network.

A vagrantfile for VirtualBox, but I don't think it's dependant on anything and it started on a Raspberry Pi 2 so it should still be compatible.

**This project is public domain and may be used or modified unconditionally.**

## Deploying

    1.  First copy the repo, go into the folder and `vagrant up` 
    2.  After the machine boots `curl -L https://install.pi-hole.net/ | bash`
    3.  run 'host-update.sh' to update blocklists and put them into Pihole
