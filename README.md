# infinispan-with-postgres
infinispan(use postgres)

## quickstart

### jdbc persistence
```console
docker network create insp-jdbc
docker run -dP  --net insp-jdbc --name postgres -e POSTGRES_DB=insp \
  -e POSTGRES_USER=admin \
  -e POSTGRES_PASSWORD=password \
  -e POSTGRES_ROOT_PASSWORD=password \
  -e POSTGRES_HOST_AUTH_METHOD=trust \
  postgres
docker run -v $(pwd)/conf:/user-config -itP --rm --name insp-srv --net insp-jdbc -e SERVER_LIBS="org.postgresql:postgresql:42.1.3" -e USER="admin" -e PASS="password" infinispan/server:13.0 -c "/user-config/infinispan-jdbc-config.xml.13.0"
```
