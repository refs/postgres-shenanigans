Once the container is running:

```
> psql postgresql://postgres:mysecretpassword@localhost:5432/postgres
```

```sql
CREATE EXTENSION pgaudit;
ALTER SYSTEM SET pgaudit.log_catalog = off;
ALTER SYSTEM SET pgaudit.log = 'all, -misc'
ALTER SYSTEM SET pgaudit.log_relation = 'on'
ALTER SYSTEM SET pgaudit.log_parameter = 'on'
```

### Observe the audit logs

```
set pgaudit.log = 'read, ddl';

create table account
(
    id int,
    name text,
    password text,
    description text
);

insert into account (id, name, password, description)
             values (1, 'user1', 'HASH1', 'blah, blah');

select *
    from account;
```

_source: https://access.crunchydata.com/documentation/pgaudit/1.2.0/_
