
# db

## Delete all tables and data 

```bash
DROP SCHEMA public CASCADE;
CREATE SCHEMA public;
```

# New Backupp

```bash
sudo -u postgres pg_dump -d database --no-owner --no-acl > backup.sql
```

# Copy

```bash
psql "postgresql://ne......."  < backup.sql
```
