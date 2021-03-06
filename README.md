modular script to create copies of websites including databases (mysql)

- automatic adaption of config files for Joomla websites

usage (always on local server);

    ./website-copy<mod> <config-file>

using one config file per-website
multiple copies of one website can be created under different
names, using separate configs

for the available config options and functions, see the `functions` file

Currently implemented modules include:

__-r-l-rdb-ldb__

where `-r-l` stands for remote-website to local-website
and `-rdb-ldb` for remote-db to local-db

Scenario:

    production site
      - web server (remote)
      - db server (remote)

    test site (copy created by script)
      - web and db server (local)

required permissions (also see notes below):

- local sudo
- ssh access (remote)
- mysql access using .my.cnf

the database is safely transferred using ssh
(encrypted and compressed using gzip)

files are transferred using rsync (--> encrypted ?)

__-l-l-rdb-rdb__

local-website to local-website and remote-db to remote-db

Scenario:

    production site
      - web server (local)
      - db server (remote)

    test site
      - web server (local)
      - db server (remote)

required permissions (also see notes below):

- local sudo
- mysql access using the priviledged user set in config
  (the script will ask for a password)

__in this scenario the database will be transferred unencrypted!__

notes on permissions:

- to simplify login ssh keys could be used,
  this is set-up independently from this script

- local sudo is needed for writing website files with
  configured user

- if needed set up mysql access by .my.cnf files

e.g. ~/.my.cnf:
~~~
[mysqldump]
user=mysqluser
password=mysecretsqlpassword
~~~

using rsync, ssh, gzip
mysqldump, mysql

2016-09-01, initial

2017-10-09, updated
