# Ansible Role: Left 4 Dead 2

An Ansible role that installs and configures a Left 4 Dead 2 dedicated server.

The game server is downloaded thought Steam and exposed as a systemd service for easier management.
Using this role it is possible to publish a minimalist server.

Automatic testing is disabled for this project as it is too long and expensive.

## Requirements

An ansible role dedicated to the installation of SteamCMD such as [ansible-steamcmd](https://github.com/tleguern/ansible-steamcmd).

## Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `steamcmd_user` | User name for steamcmd | `steam` |
| `steamcmd_bin` | Path to the steamcmd executable | `/usr/games/steamcmd` |
| `left4dead2_motd` | HTML text for the server's MOTD | See below |
| `left4dead2_server_cfg` | Server configuration | See below |
| `left4dead2_port` | Network port | `27015` |
| `left4dead2_ip` | IP address to listen on | `0.0.0.0` |
| `left4dead2_host` | HTTP link to a display banner | none |

### `left4dead2_motd`

The MOTD is a welcome text displayed by the server during the first connexion of a player.
It is formatted in HTML.

Default value:

```html
  <html>
  <head>
    <title>Left 4 Dead 2</title>
  </head>
  <body scroll="no">
    <pre>Welcome.</pre>
  </body>
  </html>
```

### `left4dead2_server_cfg`

The server.cfg file is the main configuration file for the server.
It holds the server name, the administrator password as well as various rules.

There is no default value.

Example:

```
hostname "My Left 4 Dead 2 server"
rcon_password mypassword
motd_enabled 1
...
```
## Dependencies

The `acl` package should be installed on the server.

## Example Playbook

```yaml
- hosts: game
  vars:
    left4dead2_server_cfg: |
      hostname "My Server"
      sv_password password
      rcon_password rconpassword
  pre_tasks:
    - package:
        name: acl
        state: present
  roles:
    - role: ansible-steamcmd
    - role: ansible-role-left4dead2
```

## License

ISC

## Contributing

Either send [send GitHub pull requests](https://github.com/tleguern/ansible-role-left4dead2) or [send patches on SourceHut](https://lists.sr.ht/~tleguern/misc).

## Author Information

Tristan Le Guern <tleguern@bouledef.eu>
