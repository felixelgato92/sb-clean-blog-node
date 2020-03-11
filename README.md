# SB Clean Blog Node

[![Build Status](https://travis-ci.org/StartBootstrap/sb-clean-blog-node.svg?branch=master)](https://travis-ci.org/StartBootstrap/sb-clean-blog-node)

## Prerequisites

Before you begin, make sure your development environment inlcudes the following technologies:

### 1) Node.js

We recommend you use the latest LTS version of node, which is currently 12.x

To get node, go to [nodejs.org](http://nodejs.org)

To check your node version run the following in terminal:

```bash
node --version
```

### 2) Postgres

Our Chosen ORM in Node is TypeORM. [TypeORM suports most major databases](https://typeorm.io/#/connection-options)

We prefer the very popular and open source [postgres](https://www.postgresql.org).

If desiered it should be relatively trivial to switch databases.

_Note: db scripts at `scripts/db/` have not been tested with any other databases besides postgres_

To get postgres, go to [postgresql.org](https://www.postgresql.org/download) or install via [homebrew](https://brew.sh/)

_Note: If you install via homebrew, don't forget to run `brew services start postgresql`_

To check your postgres version run the following in terminal:

```bash
psql --version
```

To set up a new user in postgres type the following in terminal (It will prompt you for a password):

```bash
createuser newuser --pwprompt --createdb # newuser can be any username you choose
```

#### _NOTE: Remember the username password you use here. You will need to add it into `.env`_

Test that you can log in to postgres:

```bash
psql -U newuser template1
```

Common postgres commands can be found in: [NOTES/POSTGRES.md](NOTES/POSTGRES.md)

## Quick Start

### 1) Set up `.env`

```bash
cp .env.sample .env
```

Open `.env` and change the values for:

```bash
DB_ROOT_USER_PASSWORD=CHANGE_ME__STRING # make up a password
TYPE_ORM_USERNAME=CHANGE_ME__STRING # postgres username
TYPE_ORM_PASSWORD=CHANGE_ME__STRING # postgres password
JWT_SECRET=CHANGE_ME__STRING # make up a random string
```

### 2) Install dependencies

```bash
npm install
```

### 3) Reset the database

This command:

- drops the current database
- recreates the databse
- runs all migrations
- creates the root user
- seeds the db with random posts

```bash
npm run db:reset # See the next command if you have issues with this command
```

_Note: If you receive an error `function uuid_generate_v4() does not exist` then run the command:_

```bash
npm run db:uuid
```

This will add the extension `uuid-ossp` to the template1 databse.
You will then need to run `npm run db:reset` again

### 4) Start the server

```bash
npm start
```

You should be able to hit <http://localhost:8200/api/latest/health>

## Tests

Unit Tests are named `*.test.ts` and are located in the same directory as the file they are testing.

### Unit Tests

```bash
npm run test
npm run test:watch
npm run test:watch-all
```

To run a specific test, you can do:

```bash
npm run test:one -- -t=[string]
```

#### View Coverage

```bash
npm run serve:coverage
```

## Migrations

```bash
npm run cli -- -h
npm run db:migration:generate -- -n my-migration
npm run db:migration:run
```

## Style

### Lint Code

```bash
npm run lint
```

### Fix all fixable lint errors

```bash
npm run lint:fix
```

### Check if any tslint rules conflick with prettier

```bash
npm run lint:check
```

## Debug 

### To run in debug mode

```bash
npm run debug
```

### To debug tsonfig

```bash
node_modules/.bin/tsc --showConfig -p ./src/tsconfig.app.json
node_modules/.bin/tsc --showConfig -p ./src/tsconfig.spec.json
```