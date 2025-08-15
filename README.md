# INIZIO – Ansible Server Provisioning

This project is part of the INIZIO technical entrance test. It uses **Ansible** to configure a Linux server with a static NGINX website, SSH hardening, firewall, security updates, and brute-force protection.

## Goal

Use Ansible to configure a virtual server, deploy a simple service (web server), and ensure a secure operational setup.


##  What the Playbook Does

###  Core Tasks:
- Installs NGINX with custom configuration (no default site).
- Generates `index.html` via Jinja2 template.
- Creates system user `wwwebapp` and sets up SSH key login.
- Enables **UFW** with ports **22** and **80** allowed.
- Disables SSH password login and root login.
- Installs **fail2ban** with WSL-safe config.
- Enables **unattended-upgrades** for automatic security patches.
- Performs HTTP check for expected response.

##  How to Run It

1. Install Ansible (on WSL Ubuntu 22.04+):

sudo apt update && sudo apt install -y ansible

2. Run the Playbook:

ansible-playbook playbooks/site.yml

 Assumes you're working on **localhost** with `ansible_connection: local`.

##  Validation

The final role (`test`) performs an HTTP request to `http://localhost` and verifies that the response contains:

<h1>Hello from Ansible NGINX!</h1>

## Notes

- Designed for WSL – does **not require systemd**.
- Compatible with Ubuntu 22.04.
- All roles are **idempotent** and safe to re-run.
- Fail2ban jail is disabled for `sshd` in WSL due to missing log files.
- SSH key authentication used instead of passwords.
- Custom NGINX configuration, no default site.
- Fail2ban is adapted for WSL environment using a custom jail.local.

## Author

This repository was created as part of the entrance assignment for **INIZIO Internet Media s.r.o.**  
Candidate: Arsenii Iatskevich 
Email: <yatskevich.arseniy@gmail.com>
