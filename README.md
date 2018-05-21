Ansible Role: Peertube
=========

Installs [Peertube](https://github.com/Chocobozzz/PeerTube) for Ubuntu.

Requirements
------------

This role only runs on Ubuntu

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):


	peertube_version: v1.0.0-beta.4
	peertube_domain: peertube.example.com
	peertube_admin_email: peertube@example.com
	peertube_database_suffix: _prod
	peertube_database_username: peertube
	peertube_database_password: peertube

	peertube_smtp_hostname: smtp.example.com
	peertube_smtp_port: 465
	peertube_smtp_username: peertube@example.com
	peertube_smtp_password: "eid2wueRudiv3ToX0oLkjnHy5rT("
	peertube_smtp_tls: true
	peertube_smtp_disable_starttls: false
	peertube_smtp_ca_file: null # Used for self signed certificates
	peertube_smtp_from_address: 'peertube@example.com'

	peertube_instance_name: PeerTube
	peertube_instance_short_description: 'PeerTube, a federated (ActivityPub) video streaming platform using P2P (BitTorrent) directly in the web browser with WebTorrent and Angular.'
	peertube_instance_description: ""
	peertube_instance_terms: ""
	peertube_services_twitter_username: '@Chocobozzz'
	peertube_services_twitter_whitelisted: false


Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use the role :

	---
	- hosts: peertube
	  become: true
	  roles:
	    - geerlingguy.postgresql
	    - geerlingguy.nodejs
	    - geerlingguy.nginx
	    - geerlingguy.certbot
	  tasks:

	    - name: Use certbot to test certificate creation
	      command: /usr/bin/certbot certonly --agree-tos --register-unsafely-without-email --test-cert --renew-by-default --webroot -w /var/www/html/ -d {{ peertube_domain }}

	    - name: Use certbot to generate certificate
	      command: /usr/bin/certbot certonly --agree-tos --renew-by-default --register-unsafely-without-email --webroot -w /var/www/html/ -d {{ peertube_domain }}


	- hosts: peertube
	  become: true
	  roles:
	    - wiseflat.peertube


License
-------

license GPLv3

Author Information
------------------

This role was created by [Mathieu Garcia](https://www.github.com/wiseflat)
