mysql-backup
============

[![Build Status](https://travis-ci.org/infOpen/ansible-role-mysql-backup.svg?branch=master)](https://travis-ci.org/infOpen/ansible-role-mysql-backup)

Install locales package.

Requirements
------------

This role requires Ansible 1.4 or higher, and platform requirements are listed
in the metadata file.

Role Variables
--------------

Default role variables

    # Defaults file for mysql-backup

    # Directories
    mysqlbackup_backupdir_dump     : /srv/backup/mysql-dump
    mysqlbackup_backupdir_full     : /srv/backup/mysql-full
    mysqlbackup_backupdir_inc      : /srv/backup/mysql-inc
    mysqlbackup_crontab_script_dir : /root/crontab-scripts
    mysqlbackup_logdir             : /var/log/mysql

    mysqlbackup_backupdir_owner      : root
    mysqlbackup_backupdir_group      : root
    mysqlbackup_backupdir_permission : "0700"

    mysqlbackup_crontab_script_dir_owner      : root
    mysqlbackup_crontab_script_dir_group      : root
    mysqlbackup_crontab_script_dir_permission : "0700"

    mysqlbackup_crontab_script_files_owner      : root
    mysqlbackup_crontab_script_files_group      : root
    mysqlbackup_crontab_script_files_permission : "0700"

    mysqlbackup_credentials_file : /root/.my_backup.cnf

    mysqlbackup_mysqldump_secure_repo : "https://github.com/cytopia/mysqldump-secure.git"


    # Crontab configuration
    mysql_backup_cron_xtrabackup_full_file      : mysql-backup-xtra
    mysql_backup_cron_xtrabackup_full_user      : root
    mysql_backup_cron_xtrabackup_full_minute    : 5
    mysql_backup_cron_xtrabackup_full_hour      : "*"
    mysql_backup_cron_xtrabackup_full_month_day : "*"
    mysql_backup_cron_xtrabackup_full_month     : "*"
    mysql_backup_cron_xtrabackup_full_week_day  : "*"

    mysql_backup_cron_mysqldump_file      : mysql-backup-mysqldump
    mysql_backup_cron_mysqldump_user      : root
    mysql_backup_cron_mysqldump_minute    : 50
    mysql_backup_cron_mysqldump_hour      : "*"
    mysql_backup_cron_mysqldump_month_day : "*"
    mysql_backup_cron_mysqldump_month     : "*"
    mysql_backup_cron_mysqldump_week_day  : "*"


    # Settings for mysqldump backup
    mysqlbackup_mysqldump_prefix           : "$(date '+%Y-%m-%d')_$(date '+%H-%M')__"
    mysqlbackup_mysqldump_target_dir_mode  : "700"
    mysqlbackup_mysqldump_target_file_mode : "400"
    mysqlbackup_mysqldump_mysql_opts       :
      - "--events"
      - "--triggers"
      - "--routines"
      - "--single-transaction"
      - "--opt"
    mysqlbackup_mysqldump_needed_db :
      - mysql
    mysqlbackup_mysqldump_ignore_db :
      - information_schema
      - performance_schema

    mysqlbackup_mysqldump_logging_active   : 1

    mysqlbackup_mysqldump_compress_active  : 1

    mysqlbackup_mysqldump_encrypt_active   : 0
    mysqlbackup_mysqldump_encrypt_pub_key  : ""
    mysqlbackup_mysqldump_encrypt_algo     : "-aes256"

    mysqlbackup_mysqldump_delete_active    : 0
    mysqlbackup_mysqldump_delete_method    : tmpwatch
    mysqlbackup_mysqldump_delete_force     : 0
    mysqlbackup_mysqldump_delete_max_hours : 720

    mysqlbackup_mysqldump_nagios_active    : 1



# Default Debian vars

    mysqlbackup_packages :
      - percona-xtrabackup

    mysqlbackup_percona_key       : "1C4CBDCDCD2EFD2A"
    mysqlbackup_percona_keyserver : "keys.gnupg.net"
    mysqlbackup_percona_repo      : "deb http://repo.percona.com/apt {{ ansible_distribution_release }} main"



Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
        - { role: achaussier.mysql-backup }

License
-------

MIT

Author Information
------------------

Alexandre Chaussier (for Infopen company)
- http://www.infopen.pro
- a.chaussier [at] infopen.pro
