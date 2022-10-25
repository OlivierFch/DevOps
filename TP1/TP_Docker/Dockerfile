FROM postgres:14.1-alpine

ENV POSTGRES_DB=db \
   POSTGRES_USER=usr \
   POSTGRES_PASSWORD=pwd

COPY ./sql/CreateScheme.sql /docker-entrypoint-initdb.d
COPY ./sql/InsertData.sql /docker-entrypoint-initdb.d