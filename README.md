openldap
========

This role installs and configures openldap server for the central authentication.
It also configures the client servers and connnect them to the ldap server.



Role variables
--------------

Available variables are listed below, along with default values (see defaults/main.yml):

	openldap_packages : the required packages to setup openldap server.
	olc_rootDN: ldap admin user account.
	domain: domain name for this openldap server is being setup.
	domain_suffix: domain's suffix (com, net, org, etc...)
	slapd_path: the slapd.d directory path, by default /etc/openldap/slapd.d
	ldap_log_path: openldap log location
	ldap_log_file: name of the openldap log file
	openldap_client_pckgs: list of packages to install on the client servers that will be conenction to openldap server
	ldap_server: ip of the openldap server
	ldap_users: users to create on the ldap server
	
Tags
-----

	ldap_client: to setup client host to connect with the openldap server
	add_users: to create new users to create in the ldap server
	deactivate_user: to deactivate user/s in the ldap server


Example Playbook
----------------

	- hosts: all
      roles:
         - { role: openldap, tags: "openldap" }
      become: true

For the direct one line command installation on localhost use :

	ansible-playbook --connection=local --inventory 127.0.0.1, openldap.yaml

Setup client host :

	ansible-playbook --connection=local --inventory 127.0.0.1, openldap.yaml --tags ldap_client

Create users :
	
	ansible-playbook --inventory 192.168.1.10, openldap.yaml --tags add_users

Deactivate users :
	
	ansible-playbook -i hosts openldap.yaml --tags deactivate_user


Tested on
---------

	- CentOS Linux release 7.8.2003 (Core)


Requirements
------------

	- ansible 2.7.7


Author Information
------------------

	Raman Deep
	18 May 2020
	deep.raman85@gmail.com
