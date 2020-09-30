# React Avançado - Landing Page API

This is the API to create the [React Avançado Landing Page](https://reactavancado.com.br/).

## Requirements

This project uses [PostgreSQL](https://www.postgresql.org/), so, in order to make it working, install in your local machine or use Docker.

The configuration to the Database can be found on [config/database.js](config/database.js)

## Development

After cloning this project, install the dependencies:

```
yarn install
```

And run using:

```
yarn develop
```

The urls to access are:

- `http://localhost:1337/admin` - The Dashboard to create and populate data
- `http://localhost:1337/graphql` - GraphQL Playground to test your queries

The first time to access the Admin you'll need to create an user.

## Dump data

This project uses `Postgres` and if you want all the data previously, unzip the [data.zip](data.zip), copy the `uploads` folder to [public/uploads](public/uploads) and restore the data from the `local.dump` file inside the zip.

brew install postgresql

- Start Server:
pg_ctl -D /usr/local/var/postgres start

- enter postgresql
psql postgres

- cria o usuario pro banco
postgres=# CREATE ROLE strapi WITH LOGIN PASSWORD 'strapi';
postgres=# ALTER ROLE strapi WITH PASSWORD 'strapi123'; 
or
postgres=# ALTER user strapi with encrypted password 'strapi123';


- lista usuários
postgres=# \du
- superuser: paulajbastos

- add permission to create DB
postgres=# ALTER ROLE strapi CREATEDB;

- logar com o novo usuário
psql postgres -U strapi

- cria o banco
CREATE DATABASE strapi;

- deleta banco
DROP DATABASE IF EXISTS strapi;

GRANT ALL PRIVILEGES ON DATABASE strapi TO strapi;

- ReStart Server:
pg_ctl -D /usr/local/var/postgres stop
pg_ctl -D /usr/local/var/postgres start

- Copiar o banco de dados de guia para o strapi via postgres
➜ ~ psql -h 127.0.0.1 -U strapi -d strapi -W < strapi_dump.sql


- Logar no painel do Strapi
Strapi Login: paulajbastos@gmail.com
Strapi Senha: Admin123


Prod:

--- heroku config

postgres://username:password@host:port/dbname

heroku config:set DATABASE_USERNAME=username
heroku config:set DATABASE_PASSWORD=password
heroku config:set DATABASE_HOST=host
heroku config:set DATABASE_PORT=port
heroku config:set DATABASE_NAME=dbname