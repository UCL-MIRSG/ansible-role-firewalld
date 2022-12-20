# Role Name

This role configures firewalld for use in a dual VM deployment (web app VM +
database VM) of XNAT or OMERO.

## Role Variables

See defaults/main.yml for the full list.

- `allow_collaborator_access`: Allow access to IP addresses/ranges listed in
  `collaborator_networks`. Defaults to `false`.
- `allow_public_access`: Allow access from an IP address. Defaults to `false`.
- `collaborator_networks`: A list of IP addresses/ranges of UCL collaborating
  partners. Defaults to `[]`.
- `work_networks`: List of public UCL IP addresses/ranges requiring access to
  the `work` zone. Defaults to `[]`.
- `internal_networks`: List of private internal UCL IP addresses/ranges.
  Defaults to `[]`.
- `internal_port`: A port to open on the internal zone (typically for
  Postgresql). Defaults to `""`.
- `open_internal_zone_to_server_ip`: Add a rich rule to accept traffic on the
  `internal` zone on this IP address (typically for connecting the web
  application to Postgresql). Defaults to `""`.
- `vm_firewall_type`: Used to determine the services required by the VM firewall
  configuration. Valid options are `"web"` or `"db"`. A "web" configuration will
  allow connections via SSH, HTTP and HTTPS for IP address defined in
  `internal_networks`, `work_networks` and `collaborator_networks`. Defaults to
  `"web"`.
- `web_rich_rules`: Any other rich rules to add. Defaults to `[]`.
- `zone_ports`: Additional ports to open for `internal` and `work`
  zones.Defaults to `[]`.

## Installation

Include in a `requirements.yml` file as follows:

```yaml
- src: https://github.com/UCL-MIRSG/ansible-role-dual-vm-firewalld.git
  version: main
  name: mirsg.firewalld
```

## Example Playbook

Including an example of how to use your role (for instance, with variables
passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: mirsg.firewalld, vm_firewall_type: "web" }
