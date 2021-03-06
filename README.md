# pihole-extended-hosts
Network-wide ad and tracker blocking, similar to running Ublock and Ghostery on a computer but for all of your devices if you configure your router to use it as your DNS server.

[Pi-hole](https://pi-hole.net) (or [@pi-hole/pi-hole](https://github.com/pi-hole/pi-hole)) is a DNS server supplemented by [@StevenBlack/hosts](https://github.com/StevenBlack/hosts) for privacy, security and malware.

The `custom.hosts` allows you to map your own domains to your private network.

A vagrantfile for VirtualBox, but I don't think it's dependant on anything more than Ubuntu 14.04,  and it started on a Raspberry Pi 2, the setup (see Vagrantfile) and update scripts should be compatible still.

**This project is public domain and may be used or modified unconditionally.**

## Deploying

    1.  First copy the repo, go into the folder and `vagrant up` 
    2.  After the machine boots `curl -L https://install.pi-hole.net/ | bash`
    3.  run 'host-update.sh' to update blocklists and put them into Pihole
    4.  configure router to point to your VM for DNS resolution
