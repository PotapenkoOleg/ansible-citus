Microsoft recomends Blue-Green deployment for [Big Database Migration](https://learn.microsoft.com/en-us/postgresql/citus/migrate/migration-data-big?view=citus-14)

Steps:
1. Build a new cluster side-by-side with the existing one
2. Take schema only backup from old cluster `pg_dump --username {{ POSTGRES_SUPERUSER_USERNAME }} -dbname {{ CLUSTER_NAME }} --file {{ CLUSTER_NAME }}.dump --format t --schema-only --jobs=10 -Z`
3. Restore schema only backup on new cluster `pg_restore --username {{ POSTGRES_SUPERUSER_USERNAME }} --dbname {{ CLUSTER_NAME }} --file {{ CLUSTER_NAME }}.dump --format t --schema-only --clean --if-exists`
4. Restore Citus shard information using https://github.com/PotapenkoOleg/citus_shard_export
5. Restore functions/stored procedures from old cluster 
6. Restore pg_cron jobs from old cluster
3. Enable logical replication
4. When data is fully copied, stop replication and switch HAProxy to a new cluster
5. Remove the old cluster. Optionally, leave it to switch back in case of any issues

NOTE: You can use install scripts to spin a new cluster, just update config eg ports to avoid conflicts 