- Set up [Algo VPN](https://github.com/trailofbits/algo) (This assumes you'll
  use the submodule in here. Remember to update it first).
- Set up Raspbian with
  [SSH](https://www.raspberrypi.org/documentation/remote-access/ssh/) (default
  creds are "pi"/"raspberry")
- Use `ssh-copy-id` to setup publickey SSH access
- Write inventory.yaml.
- Run `ansible-playbook -i inventory.yaml wireguard-client.yml -e target=pi-vpn` to install wireguard.
- Spend fucking ages figuring out why the fuck the above presumably spat out a
  totally fucking useless error message.
- Curse the Debian maintainers
- Curse the Ansible maintainers
- Curse whoever the fuck invented YAML
