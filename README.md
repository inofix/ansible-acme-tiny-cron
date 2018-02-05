[![Travis CI](https://img.shields.io/travis/inofix/ansible-acme-tiny-cron.svg?style=flat)](http://travis-ci.org/inofix/ansible-acme-tiny-cron)


Role Name
=========

This is an ansible role for creating cron jobs for the recreation of your cerificates for a certain domain.

The role is meant to be run for a system accessible from the web. It will make the request with "Let's Encrypt" from an existing csr (see inofix.acme-tiny-setup), solve the challenge on the server's well-known webfolder and then put the resulting certificates in the openssl configuration directory.

It takes over the work of inofix.acme-tiny-sign which must be run at least once as it is base on the preparations of that role and only repeats the recreation of the certificate once a month (so no ansible "master" etc. has to be involved later).


Status
------

UNSTABLE! We are just migrating from zwischenloesung.acme-tiny-cron.


Promise
-------

Sure, this role may change in the future, but we will only expand features to not break backwards compatibility.

If radical changes should become necessary, a new role will be created, probably with an 'ng' or version suffix...

Installation
------------

 # ansible-galaxy install inofix.acme-tiny-cron

Requirements
------------

* Ansible >2.0
* On target host
 * Generic UNIX with FHS
 * Python2/3
 * Cron
 * Running webserver with ^/.well-known/acme-challenge/ directory accessible (hardcoded in acme-tiny script..)
 * The webserver must serve HTTP, even for consequent certificates (not just HTTPS; requirement of acme-tiny/let's-encrypt)
 * Resolve all names in the cert to localhost or the local-IP

Role Variables
--------------

* app\_\_acme\_\_tiny\_\_user - optional, default='acme'
* app\_\_acme\_\_tiny\_\_config\_dir - optional, default='/etc/ssl/acme-tiny'
* app\_\_acme\_\_tiny\_\_account\_key - optional, auto
* app\_\_acme\_\_tiny\_\_challenge\_dir - optional, default='/var/www/acme-challenge'
* app\_\_acme\_\_tiny\_\_domain - optional, default='example.com'
* app\_\_acme\_\_tiny\_\_cert\_name - optional, auto
* app\_\_acme\_\_tiny\_\_cert\_dir - optional, auto
* app\_\_acme\_\_tiny\_\_request - optional, auto
* app\_\_acme\_\_tiny\_\_cron\_minute - optional, default='22,44'
* app\_\_acme\_\_tiny\_\_cron\_hour - optional, default='04'
* app\_\_acme\_\_tiny\_\_cron\_day - optional, default='\*'
* app\_\_acme\_\_tiny\_\_cron\_month - optional, default='\*'
* app\_\_acme\_\_tiny\_\_cron\_weekday - optional, default='\*'
* fqdn - optional, default={{ ansible\_fqdn | d(inventory\_hostname ) }}

Dependencies
------------

* 'inofix.acme-tiny-sign' - as a weak dependency, as the role must be run once at least, but the role can also be used later to fix the cronjobs.

Example Playbook
----------------

    - hosts: servers
      roles:
         - inofix.acme-tiny-cron

License
-------

GPLv3

Author Information
------------------

* Michael Lustenberger at [inofix.ch](http://www.inofix.ch)

