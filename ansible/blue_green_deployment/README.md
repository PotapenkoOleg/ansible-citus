Microsoft recomends Blue-Green deployment for [Big Database Migration](https://learn.microsoft.com/en-us/postgresql/citus/migrate/migration-data-big?view=citus-14)

Steps:
1. Build a new cluster side-by-side with the existing one
2. Add HAProxy config for new cluster
3. Take schema only backup from old cluster `pg_dump --username {{ POSTGRES_SUPERUSER_USERNAME }} -dbname {{ CLUSTER_NAME }} --file {{ CLUSTER_NAME }}.dump --format t --schema-only --jobs=10 -Z`
4. Restore schema only backup on new cluster `pg_restore --username {{ POSTGRES_SUPERUSER_USERNAME }} --dbname {{ CLUSTER_NAME }} --file {{ CLUSTER_NAME }}.dump --format t --schema-only --clean --if-exists`
5. Restore Citus shard information using https://github.com/PotapenkoOleg/citus_shard_export
6. Restore functions/stored procedures from old cluster 
7. Restore pg_cron jobs from old cluster
8. Enable logical replication
9. When data is fully copied, stop replication and 
10. Switch HAProxy to a new cluster
11. Remove the old cluster. Optionally, leave it to switch back HAProxy in case of any issues

NOTE: You can use install scripts to spin a new cluster, just update config eg ports to avoid conflicts 