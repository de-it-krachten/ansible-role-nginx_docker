[![CI](https://github.com/de-it-krachten/ansible-role-nginx_docker/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-nginx_docker/actions?query=workflow%3ACI)


# ansible-role-nginx_docker

Manage nginx instance in Docker 



## Dependencies

#### Roles
- deitkrachten.openssl

#### Collections
- community.docker

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- RockyLinux 8<sup>1</sup>
- RockyLinux 9<sup>1</sup>
- OracleLinux 8<sup>1</sup>
- OracleLinux 9<sup>1</sup>
- AlmaLinux 8<sup>1</sup>
- AlmaLinux 9<sup>1</sup>
- SUSE Linux Enterprise 15<sup>1</sup>
- openSUSE Leap 15<sup>1</sup>
- Debian 10 (Buster)<sup>1</sup>
- Debian 11 (Bullseye)<sup>1</sup>
- Debian 12 (Bookworm)<sup>1</sup>
- Ubuntu 18.04 LTS<sup>1</sup>
- Ubuntu 20.04 LTS<sup>1</sup>
- Ubuntu 22.04 LTS<sup>1</sup>
- Ubuntu 24.04 LTS<sup>1</sup>
- Fedora 39<sup>1</sup>
- Fedora 40<sup>1</sup>
- Alpine 3<sup>1</sup>
- Docker dind (CI only)

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# nginx root
nginx_root_path: /export/docker/nginx

# Docker image to use
nginx_docker_image: nginx

nginx_docker_ssl: true

# Volume list
nginx_docker_volumes:
  - "{{ nginx_confd_path }}:/etc/nginx/conf.d"
  - "{{ nginx_certs_path }}:/etc/nginx/certs"
  - "{{ nginx_html_path }}:/usr/share/nginx/html"
  - "{{ nginx_log_path }}:/var/log/nginx"

# nginx config path (drop-in)
nginx_confd_path: "{{ nginx_root_path }}/conf.d"

# nginx certificate location
nginx_certs_path: "{{ nginx_root_path }}/certs"

# nginx HTML location
nginx_html_path: "{{ nginx_root_path }}/html"

# nginx log location
nginx_log_path: "{{ nginx_root_path }}/logs"

# nginx webroot
nginx_server_root: /usr/share/nginx/html

# FQDN of the web server
nginx_fqdn: www.example.com

nginx_vhosts:
  - fqdn: "{{ nginx_fqdn }}"
    root: "{{ nginx_server_root }}"

# SSL/TLS type
nginx_cert_type: 'self-signed'

# Ports
nginx_docker_ports:
  - "443:443"

nginx_docker_expose: []
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'nginx_docker'
  hosts: all
  become: 'yes'
  vars:
    nginx_docker_environment: []
    nginx_docker_networks: []
  tasks:
    - name: Include role 'nginx_docker'
      ansible.builtin.include_role:
        name: nginx_docker
</pre></code>
