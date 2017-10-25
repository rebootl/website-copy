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

- ssh access on the remote host(s)
  (incl. read permission for website files)
  atm. the user calling the script is used
  to simplify logins ssh keys could be used,
  this is set-up independently from this script

- sudo local for writing website files with
  configured user

- mysql access must be configured using ~/.my.cnf files
  on the local and the remote host
  ~/.my.cnf format:
  [mysqldump]
  user=mysqluser
  password=mysecretsqlpassword

using rsync, ssh, gzip
mysqldump, mysql/mysqladmin (?)

cem, 2016-09-01

2017-10-09, updated
