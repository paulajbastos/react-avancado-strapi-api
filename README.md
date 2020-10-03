# React Avançado - Landing Page API

This is the API to create the [React Avançado Landing Page](https://paulajbastos-react-avancado-landpage.netlify.app/).

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


# Guides

## Install Postgressql
```
brew install postgresql
```

## Start Server:
```
pg_ctl -D /usr/local/var/postgres start
```

## Enter postgresql
```
psql postgres
```

## Create user for DB
```
postgres=# CREATE ROLE strapi WITH LOGIN PASSWORD 'strapi';
```
```
postgres=# ALTER ROLE strapi WITH PASSWORD 'strapi123'; 
```
or
```
postgres=# ALTER user strapi with encrypted password 'strapi123';
```

## Users List
```
postgres=# \du
```

## DBs List
```
postgres=# \l
```
- superuser: paulajbastos

## Add permission for user to create DB
```
postgres=# ALTER ROLE strapi CREATEDB;
```
## Login as new user
```
psql postgres -U strapi
```
## Create DB
```
CREATE DATABASE strapi;
```
## Delete DB
```
DROP DATABASE IF EXISTS strapi;
```

## Give privileges on DB to user
```
GRANT ALL PRIVILEGES ON DATABASE strapi TO strapi;
```
## Restart Server:
```
brew services restart postgresql
```
or
```
pg_ctl -D /usr/local/var/postgres stop
```
```
pg_ctl -D /usr/local/var/postgres start
```
## Copy localGuideDb to local postgres
```
➜ ~ psql -h 127.0.0.1 -U strapi -d strapi -W < strapi_dump.sql
```

## Login to Local Strapi

Strapi Login: paulajbastos@gmail.com

Strapi Senha: Admin123


## How to generate ADMIN_JWT_SECRET Token:
(https://strapi.io/documentation/v3.x/migration-guide/migration-guide-3.0.x-to-3.1.x.html)
```
node -e "console.log(require('crypto').randomBytes(64).toString('base64'))" # (all users)
```

## Production:

```
heroku config
```

## Config Heroku variables with the infos below

postgres://username:password@host:port/dbname

```python
heroku config:set DATABASE_USERNAME=username
heroku config:set DATABASE_PASSWORD=password
heroku config:set DATABASE_HOST=host
heroku config:set DATABASE_PORT=5432
heroku config:set DATABASE_NAME=dbname
heroku config:set ADMIN_JWT_SECRET=gerarToken
```
## Save DB in Local
```
PGPASSWORD=strapi123 pg_dump -Fc --no-acl --no-owner -h localhost -U strapi strapi > strapi-local.dump
```


##  Import a database saved in any external url to heroku (needs to be an external url, not local)
```
heroku pg:backups:restore 'https://paulajbastosdev.com/strapi-local.dump' DATABASE_URL
```

## Demo:

[https://react-avancado-strapi-api.herokuapp.com/admin/](https://react-avancado-strapi-api.herokuapp.com/admin/)
