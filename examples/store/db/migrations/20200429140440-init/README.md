# Migration `20200429140440-init`

This migration has been generated by Brandon Bayer at 4/29/2020, 2:04:40 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
PRAGMA foreign_keys=OFF;

CREATE TABLE "quaint"."User" (
    "email" TEXT NOT NULL  ,
    "id" INTEGER NOT NULL  PRIMARY KEY AUTOINCREMENT,
    "name" TEXT   ,
    "role" TEXT   ,
    "storeId" INTEGER   
) 

CREATE TABLE "quaint"."Product" (
    "description" TEXT   ,
    "handle" TEXT NOT NULL  ,
    "id" INTEGER NOT NULL  PRIMARY KEY AUTOINCREMENT,
    "name" TEXT   ,
    "price" INTEGER   
) 

CREATE UNIQUE INDEX "quaint"."User.email" ON "User"("email")

CREATE UNIQUE INDEX "quaint"."Product.handle" ON "Product"("handle")

PRAGMA "quaint".foreign_key_check;

PRAGMA foreign_keys=ON;
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration ..20200429140440-init
--- datamodel.dml
+++ datamodel.dml
@@ -1,0 +1,37 @@
+// This is your Prisma schema file,
+// learn more about it in the docs: https://pris.ly/d/prisma-schema
+
+datasource sqlite {
+  provider = "sqlite"
+  url      = "file:./db.sqlite"
+}
+
+// SQLite is easy to start with, but if you use Postgres in production
+// you should also use it in development with the following:
+//datasource postgresql {
+//  provider = "postgresql"
+//  url      = env("DATABASE_URL")
+//}
+
+generator client {
+  provider = "prisma-client-js"
+}
+
+
+// --------------------------------------
+
+model User {
+  id      Int      @default(autoincrement()) @id
+  email   String   @unique
+  name    String?
+  role    String?
+  storeId Int?
+}
+
+model Product {
+  id          Int      @default(autoincrement()) @id
+  handle      String   @unique
+  name        String?
+  description String?
+  price       Int?
+}
```


