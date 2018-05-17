Stouts.docker-postgres
======================

Ansible role to run Postgres with Docker

#### Variables

```yaml
postgres_enabled: yes

postgres_prefix: /opt/postgres      # Host data directory
postgres_image: postgres:alpine     # Docker Postgres Image
postgres_env: {}                    # ENV variables
postgres_ports: ["5432:5432"]       # Listen ports
postgres_volumes:                   # Container volumes
- "{{postgres_prefix}}/init-db.sh:/docker-entrypoint-initdb.d/init-db.sh:ro"
- "{{postgres_prefix}}/postgres.conf:/etc/postgresql/postgresql.conf"
- "{{postgres_prefix}}/data:/var/lib/postgresql/data"

# Configure postgres (https://www.postgresql.org/docs/current/static/runtime-config.html)
# postgres_options:
#   max_connections: "1000"
#   shared_buffers: "512MB"
postgres_options: {}

# Init databases, roles
# postgresql_databases:
# - name: "db1"
# - name: "db2"
# postgres_users:
# - { name: "user1", pass: "pass1" }
# - { name: "user2", pass: "pass2" }
# postgres_user_privileges:
# - { name: "user1", db: "db1", priv: "ALL" }
# - { name: "user2", db: "db2", priv: "ALL" }
postgres_databases: []
postgres_users: []
postgres_user_privileges: []
```

#### Usage

Add `Stouts.docker-postgres` to your roles and set vars in your playbook file.

Example:

```yaml

- hosts: all

  roles:
    - Stouts.postgres

  vars:
    postgres_databases:
    - name: db1
    postgres_users:
    - name: user1
      pass: pass
    postgres_user_privileges:
    - { name: "user1", db: "db1", priv: "ALL" }
    postgres_options:
        max_connections: "1000"
        max_wal_size: "2GB"
        min_wal_size: "1GB"
        random_page_cost: "1.1"
        shared_buffers: "512MB"
```

#### License

Licensed under the MIT License. See the LICENSE file for details.

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Stouts/Stouts.docker-postgres/issues)!
