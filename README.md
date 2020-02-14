# OpenVAS 
Install and configure  [OpenVAS 10](https://github.com/greenbone/openvas) on supported cloud images.
The role uses [Caddy](https://caddyserver.com/) as reverse proxy with automatic HTTPS for OpenVaS.


Supported cloud image is [Debian Buster (10)](https://cdimage.debian.org/cdimage/openstack/current/).
Other distros based on Debian might also work.


## Configuration
The role uses the following variables preset with some meaningful defaults.
You have to overwrite `caddy_domain_name` (required) and openvas_password (required).

```
caddy_version: v1.0.4
caddy_sha256: 9e7f37466cbfad53188f038b84ed4469645d3d0fc91f9206f7a54b36eee4b432
caddy_domain_name: my-domain.com

openvas_local_ip: 127.0.0.1
openvas_local_port: 8080
openvas_local_http_url: http://{{openvas_local_ip}}:{{openvas_local_port}}
openvas_admin: admin
openvas_password: admin
```

## Example playbook
Depending on your cloud image the play (and the hosts file) might look different.

#####hosts
```
[debian]
192.168.0.2 ansible_ssh_user=debian
```

#####site.yml
```
- hosts: debian
  become: 'yes'
  vars:
    caddy_domain_name: openvas.my-domain.de
    openvas_password: SuperSecurePassword
  roles:
  - jkrue.openvas
```