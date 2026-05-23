Microsoft recomends Blue-Green deployment for [Big Database Migration](https://learn.microsoft.com/en-us/postgresql/citus/migrate/migration-data-big?view=citus-14)

Steps:
1. Build a new cluster side-by-side with the existing one
2. Restore schema only backup `pg_dump --schema-only`
3. Enable logical replication
4. When data is fully copied, stop replication and switch HAProxy to a new cluster
5. Remove the old cluster. Optionally, leave it to switch back in case of any issues