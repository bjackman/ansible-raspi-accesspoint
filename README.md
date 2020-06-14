# Set up Pi
- Set up Raspbian with
  [SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/) (default
  creds are "pi"/"raspberry")
- Use `ssh-copy-id` to setup publickey SSH access
- Write inventory.yaml.

# Set up VPN
- Set up [Algo VPN](https://github.com/trailofbits/algo) (This assumes you'll
  use the submodule in here. Remember to update it first).
- Set `vpn_server` and `vpn_user` in `group_vars/all.yml`
- Run `ansible-playbook -i inventory.yaml wireguard-client.yml -e target=pi-vpn`
  to setup wireguard.
- Spend fucking ages figuring out why the fuck the above presumably spat out a
  totally fucking useless error message.
- Curse the Debian maintainers
- Curse the Ansible maintainers
- Curse whoever the fuck invented YAML
- Run curl ipv4.icanhazip.com from the Pi. The result should match what you
  configured for `vpn_server`.

# Set up WiFi AP
- Set up the remaining stuff in group_vars/all.yaml. Make sure that the subnet
  for your Ethernet LAN won't overlap with the WLAN.
- Run `ansible-playbook -i inventory.yaml  -e target=pi-vpn access-point.yml`
- Reboot the Pi (the playbook must be missing a systemd command. Not sure).

I couldn't get 5Ghz (hw_mode=a) to work, I always got "Configured channel (%d)
not found from the channel list of current mode (2) IEEE 802.11a". Haven't
really investigated.

I also couldn't get Automatic Channel Selection (channel=0) to work, hostapd
just shut down without any error message, and return code 0. Haven't really
investigated.
