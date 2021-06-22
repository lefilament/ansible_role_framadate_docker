docker_framadate
================

This role deploys Framadate in a Docker. This role is based on [Le Filament Framadate Docker](https://hub.docker.com/repository/docker/lefilament/framadate) which is also described on corresponding [Le Filament GitHub page](https://github.com/lefilament/docker_framadate), and is collecting code directly from [Framasoft Framapad git repository](https://framagit.org/framasoft/framadate/framadate).
The main repo for this role is on [Le Filament GitLab](https://sources.le-filament.com/lefilament/ansible-roles/docker_framadate.git)

Requirements
------------

None

Role Variables
--------------

Variables from default directory :
* date_url: URL on which Framadate will be listening
* date_db_root: Database root password
* date_db_user: Database user
* date_db_pass: Database password
* date_admin_user: Framadate Admin user
* date_admin_pass: Framadate Admin password
* default_maintenance_email: Framadate Admin e-mail

* Mail configuration (optional, if set, a postfix proxy will be deployed, otherwise a mailhog instance will be deployed for blocking e-mails)
  * mailname: domain to which the users belong to
  * mailserver: SMTP server to use for sending e-mails (defaults to smtp.{{ domain }})
  * smtpport: SMTP server port (defaults to 465)
  * smtpuser: SMTP username (defaults to smtpuser)
  * smtppass: SMTP user password (defaults to veryUnsecurePassToBeModified)
* Backups (for backups to be deployed, host needs to be in maintenance_contract group)
  * swift parameters for 2 object storage instances where backups should be pushed daily
  * date_backup_pass : Passphrase for encryption of backups

Dependencies
------------

This role requires the following Ansible collection :
* community.docker

This Docker role supposes that Traefik is deployed as an inverseproxy in front of the deployed Dockers.
The following role is used by Le Filament for deploying Traefik : docker_server (https://sources.le-filament.com/lefilament/ansible-roles/docker_server)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: docker_framadate }
      vars:
         - { date_url: "date.example.org" }
         - { date_db_root: "veryUnsecureRootPassToBeModified" }
         - { date_db_user: "framadate" }
         - { date_db_pass: "veryUnsecurePassToBeModified" }
         - { date_admin_user: "admin" }
         - { date_admin_pass: "veryUnsecureAdminPassToBeModified" }
         - { default_maintenance_email: "maintenance@example.org" }

License
-------

AGPL-3

Author Information
------------------

Le Filament (https://le-filament.com)
