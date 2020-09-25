# ansible-role-percona

Ansible role to install [Percona](https://www.percona.com/) repo and software for RHEL/CentOS

## Role Variables

### Default role variables

``` yaml
percona_gpg_key: "https://www.percona.com/downloads/RPM-GPG-KEY-percona"
percona_release_rpm: "https://repo.percona.com/yum/percona-release-latest.noarch.rpm"

percona_server_install: yes
# for RHEL/CentOS 6-7: 55 | 56 | 57 | 80
# for RHEL/CentOS 8: 57 | 80
percona_server_version: '57'
percona_server_packages:
  - 'Percona-Server-server-{{ percona_server_version }}'
  - 'Percona-Server-shared-{{ percona_server_version }}'
  - 'Percona-Server-client-{{ percona_server_version }}'
  - 'Percona-Server-shared-compat-{{ percona_server_version }}'
  - percona-toolkit
percona_server_obsoleted_packages:
  - mysql
  - mysql-server
  - mysql-libs
  - mariadb
  - mariadb-server

percona_server_tokudb_install: no
# 56 | 57
percona_server_tokudb_version: "{{ percona_server_version if percona_server_version in [ '56', '57' ] else omit }}"
percona_server_tokudb_packages:
  - 'Percona-Server-tokudb-{{ percona_server_tokudb_version }}'

percona_server_rocksdb_install: no
# 57 only
percona_server_rocksdb_version: "{{ percona_server_version if percona_server_version == '57' else omit }}"
percona_server_rocksdb_packages:
  - 'Percona-Server-rocksdb-{{ percona_server_rocksdb_version }}'

percona_xtrabackup_install: yes
# percona-xtrabackup | percona-xtrabackup-22 | percona-xtrabackup-24 | percona-xtrabackup-80
percona_xtrabackup: "{{ percona-xtrabackup-80 if percona_server_version == '80' else percona-xtrabackup }}"
percona_xtrabackup_packages:
  - '{{ percona_xtrabackup }}'
  - qpress

percona_proxysql_install: no
# proxysql | proxysql2
percona_proxysql: 'proxysql2'

percona_pmm_client_install: no
# pmm-client | pmm2-client
percona_pmm_client: 'pmm2-client'

percona_xtradb_install: no
# for RHEL/CentOS 6-7: 55 | 56 | 57
# for RHEL/CentOS 8: 57
percona_xtradb_version: '57'
percona_xtradb_packages:
  - 'Percona-XtraDB-Cluster-{{ percona_xtradb_version }}'
  - 'Percona-XtraDB-Cluster-client-{{ percona_xtradb_version }}'
  - 'Percona-XtraDB-Cluster-full-{{ percona_xtradb_version }}'
  - 'Percona-XtraDB-Cluster-garbd-{{ percona_xtradb_version }}'
  - 'Percona-XtraDB-Cluster-server-{{ percona_xtradb_version }}'
  - 'Percona-XtraDB-Cluster-shared-{{ percona_xtradb_version }}'

percona_mongodb_install: no
# for RHEL/CentOS 6-7: 32 | 34 | 36
# for RHEL/CentOS 8: 36
percona_mongodb_version: '36'
percona_mongodb_packages:
  - 'Percona-Server-MongoDB-{{ percona_mongodb_version }}'
  - 'Percona-Server-MongoDB-{{ percona_mongodb_version }}-mongos'
  - 'Percona-Server-MongoDB-{{ percona_mongodb_version }}-server'
  - 'Percona-Server-MongoDB-{{ percona_mongodb_version }}-shell'
  - 'Percona-Server-MongoDB-{{ percona_mongodb_version }}-tools'
```

## Ansible Galaxy

ansible-galaxy install me_vlad.percona


## Example Playbook

``` yaml
- hosts: dbs
  roles:
    - me_vlad.percona
```

## License

MIT

## Author Information

Vlad V. Teteria
