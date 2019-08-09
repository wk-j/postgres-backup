## Backup

*Start*

```bash
mkdir {z-joget,z-tomcat,z-postgres}

docker compose up
open http://localhost:8080/jw
```

*Backup*

```bash
rm *.sql
docker exec -t postgresbackup_postgres_1 pg_dumpall --help

docker exec -t postgresbackup_postgres_1 pg_dumpall -c -U postgres -l jwdb > dump-(date +%d-%m-%Y"_"%H_%M_%S).sql
cat dump*.sql | docker exec -i postgresbackup_postgres_1 psql -U postgres
```