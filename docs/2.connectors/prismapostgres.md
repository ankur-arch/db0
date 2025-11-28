---
icon: simple-icons:prisma
---

# Prisma Postgres

> Connect DB0 to Prisma Postgres

[Prisma Postgres](https://www.prisma.io/postgres?utm_source=db0&utm_campaign=ppg-awareness) provides a fast, managed PostgreSQL database service. While there's no specific DB0 connector for Prisma Postgres, you can use the existing PostgreSQL connector to connect smoothly.

## Create Database

You can either create an account in [Prisma Data Platform](https://console.prisma.io?utm_source=db0&utm_campaign=ppg-awareness) and create a database manually or [use `create-db` cli tool](https://www.prisma.io/docs/postgres/introduction/npx-create-db?utm_source=db0&utm_campaign=ppg-awareness) to create a Prisma Postgres database.

Let's create a new Prisma Postgres database using the `create-db` cli tool:

```terminal
npx create-db
```

This will output something like:

```terminal
┌  🚀 Creating a Prisma Postgres database
│
│  Provisioning a temporary database in us-east-1...
│
│  It will be automatically deleted in 24 hours, but you can claim it.
│
◇  Database created successfully!
│
│
●  Database Connection
│
│
│    Connection String:
│
│    postgresql://username:password@db.prisma.io:5432/postgres?sslmode=require
│
│
◆  Claim Your Database
│
│    Keep your database for free:
│
│    https://create-db.prisma.io/claim?projectID=your_project_id&utm_source=db0&utm_campaign=ppg-awareness
│
│    Database will be deleted on [DATE] if not claimed.
│
└
```

**Important:** Save your actual connection string to an `.env` file:

```bash
DATABASE_URL="postgresql://your_username:your_password@db.prisma.io:5432/postgres?sslmode=require"
```

## Installation

Install the PostgreSQL driver:

:pm-install{name="pg @types/pg"}

## Usage

Install [`db0`](https://npmjs.com/package/db0) npm package:

:pm-install{name="db0"}

Use the [`postgresql`](/connectors/postgresql) connector with your Prisma Postgres database:

```js
import "dotenv/config";
import { createDatabase } from "db0";
import postgresql from "db0/connectors/postgresql";

const db = createDatabase(
  postgresql({
    url: process.env.DATABASE_URL,
  }),
);
```

Then you should be able to query your Prisma Postgres database:

```typescript
import "dotenv/config";
import { createDatabase } from "db0";
import postgresql from "db0/connectors/postgresql";

const db = createDatabase(
  postgresql({
    url: process.env.DATABASE_URL!,
  }),
);

async function main() {
  console.log(await db.sql`SELECT 1`);
}

main();
```
