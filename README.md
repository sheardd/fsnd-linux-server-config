README - Item Catalog Project for Udacity
==============================================================================

Quick-Start Guide

------------------------------------------------------------------------------

Server Public IP Address: 54.236.243.62

URL: http://54.236.243.62/

SSH Port: 2200

Private key for ubuntu user 'grader' provided in submission notes.

The password for this private key is 'udacity'.

------------------------------------------------------------------------------

Software Installed

------------------------------------------------------------------------------

Main Software

Ubuntu 16.04 Xenial - Operating System

Apache2 - Server Application

Postgresql - Database Application

Python 2.7 - Required to run Item Catalog app. Ubuntu 16.04 comes with
			 python3 pre-installed; this was left untouched and python 2.7
			 installed in parallel.


Apache2 Modules

mod_wsgi - Because the Item Catalog app uses python, apache2 requires the
		   wsgi module to serve it.


Python Modules

psycopg2 - Not strictly required to run postgresql using sqlalchemy, but
		   recommended by ubuntu package source lists.

requests - required to make API requests in python.

Oauth2client - required for third-party authentication via Facebook and Google
			   using Oauth2.

------------------------------------------------------------------------------

Configuration Notes

------------------------------------------------------------------------------

1) Configured the UFW firewall to only listen for incoming data on ports 80,
   123, and 2200, for http, ntp, and ssh respectively. Copied these settings
   on the AWS Lightsail built-in firewall. The firewall was configured first
   in case it was misconsfigured and the instance needed to be re-created, so
   no other work would be done, only for it to be lost.

2) Configured the server's SSH to listen on port 2200 instead of port 22 using
   the sshd_config file.

3) Updated and upgraded all pre-installed software on the system using apt.

4) Created evaluation user 'grader' in ubuntu. Granted this user sudo
   privileges by copying the existing 90-cloud-init-users file in
   /etc/sudoers.d/, renaming it grader, and changing the username inside the
   file to grader. Created an SSH key pair locally for this user, copied the
   public key into a newly-created /home/grader/.ssh/authorized_keys file

5) Set the local timezone to UTC.

6) Installed Apache2 and mod_wsgi

7) Installed Postgresql and psycopg2, ensuring the remote connections were not
   allowed, and created postgresql user 'catalog'. Because of postgresql's
   'ident sameuser' configuration this involved creating a new catalog ubuntu
   user to match the database user. This user should be secure though, since
   password login is disabled and no key has been added for ubuntu user
   'catalog'. The only permission 'catalog' was granted was permission to
   create databases. As the owner of any databases created, 'catalog' would
   automatically be able to perform required CRUD operations.

8) Installed Git.

9) Cloned Item Catalog app from github, installed python modules as outlined
   above, modified sqlalchemy URLs to use postgresql 'catalog' user, replaced
   filepaths to read JSON client secret files with absolute filepaths for wsgi
   scope reference, created itemcat.wsgi to serve the application and define
   application.secret (which involved temporarily disabling WSGIRestrictStdout
   to debug). Ran database_setup.py and populate.py (which required resetting
   id_seq values on tables afterwards, as postgresql didn't seem to track
   incrementing id values when run through a script for some reason), and
   updated fb_client_secrets.json after updating facebook API URLs.

10) Updated everything one more time using apt, then restarted Apache.

------------------------------------------------------------------------------

Third-Party Resources

------------------------------------------------------------------------------

- All previously mentioned software and modules

- Facebook API

- Google+ API

- Various image files for pre-loaded catalog data, and project's fake logo

- All sample data (compiled and organised myself but is actual information
  pertaining to real artists)

