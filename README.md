Ansible Role: bind(src)
================================================================================
Build and install ISC-BIND 9 from a source code at CentOS 7

- Build BIND from a source code at /usr/local/src
- Install BIND into /opt/named
- Deploy files for systemd into /usr/lib/systemd
- Open tcp/53 and udp/53

Requirements
--------------------------------------------------------------------------------
- OpenSSL
  - package: `yum install openssl openssl-devel`
  - source built: [ar-openssl-src](https://github.com/azumakuniyuki/ar-openssl-src)

Role Variables
--------------------------------------------------------------------------------
The following variables are defined in defaults/main.yml file.

```yaml
bind:
  started: true
  rebuild: false
  version: "9.10.4-P8"
  updateonly: false
  changeroot: "/opt/named"
  serverroot: "/opt/named"
  openssldir: "/opt/openssl"
  workingdir: "/usr/local/src"
  initscript: "bind"
  user:
    username: "named"
    uid: 953
    gid: 953
    group: "named"
    shell: "/sbin/nolgin"
    comment: "'DNS BIND9'"
  zones:
    master:
      - "l/localhost.zone"
      - "1/127.in-addr.arpa.rev"
      - "y/your.domain.example.jp"
    slave:
      - "s/some.domain.example.org"

```

Dependencies
--------------------------------------------------------------------------------
If you don't use the following role, install openssl and openssl-devel package.
- [ar-openssl-src](https://github.com/azumakuniyuki/ar-openssl-src)

Example Playbook
--------------------------------------------------------------------------------
```yaml
- hosts: all
  roles:
    - { role: azumakuniyuki.ar-bind-src, bind.version: "9.10.4-P9", bind.rebuild: true }
```

License
--------------------------------------------------------------------------------
BSD

Author Information
--------------------------------------------------------------------------------
[azumakuniyuki](http://nyaan.jp/)

