# simple-gluster-ansible

An Ansible playbook to install GlusterFS with TLS encryption configured and enabled out-of-the-box, designed to be as simple as possible.

To use it, create an inventory file that has all of the hosts you need in the `gluster` group (an example file can be found [here](inventory.ini)), and just run `ansible-playbook site.yml` - yes, that's really it!

It has been tested on Raspbian (now called Raspberry Pi OS) Buster on a combination of Raspberry Pi 4's and Raspberry Pi 3's, but should work just fine on anything else running 64-bit Debian or Ubuntu with systemd.

## Notes

- The brick path is set to `/data/gluster` (can be changed under `external_vars.yml` if desired).

- The gluster volume is automatically mounted under `/gluster` every reboot (which can also be changed under `external_vars.yml`).

- The following volume settings are applied:

    - performance.cache-size: 128MB
    - write-behind: off
    - performance.write-behind-window-size: 0B
    - quick-read: on
    - auth.allow and auth.ssl-allow is set to only allow the nodes that are configured in the inventory
    - ssl.cipher-list: 'HIGH:!SSLv2:!SSLv3'
    - nfs.disable: on
    - performance.flush-behind: off
    - cluster.data-self-heal-algorithm: full
    - client.ssl: on
    - server.ssl: on
