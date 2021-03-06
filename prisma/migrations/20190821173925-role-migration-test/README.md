# Migration `20190821173925-role-migration-test`

This migration has been generated by Ryan King at 8/21/2019, 5:39:25 PM.
You can check out the [state of the datamodel](./datamodel.prisma) after the migration.

## Database Steps

```sql
CREATE TABLE "public"."Role"("id" text NOT NULL  ,"name" text   ,PRIMARY KEY ("id"))
;

ALTER TABLE "public"."User" ADD COLUMN "role" text   REFERENCES "public"."Role"("id") ON DELETE SET NULL;

CREATE UNIQUE INDEX "Role.id._UNIQUE" ON "public"."Role"("id")
```

## Changes

```diff
diff --git datamodel.mdl datamodel.mdl
migration 20190820191028-init..20190821173925-role-migration-test
--- datamodel.dml
+++ datamodel.dml
@@ -16,8 +16,9 @@
   id    String  @default(cuid()) @id @unique
   email String  @unique
   name  String?
   posts Post[]
+  role  Role?
 }
 model Post {
   id        String   @default(cuid()) @id @unique
@@ -26,5 +27,11 @@
   published Boolean
   title     String
   content   String?
   author    User?
+}
+
+model Role {
+  id    String  @default(cuid()) @id @unique
+  name  String?
+  users User[]
 }
```

## Photon Usage

You can use a specific Photon built for this migration (20190821173925-role-migration-test)
in your `before` or `after` migration script like this:

```ts
import Photon from '@generated/photon/20190821173925-role-migration-test'

const photon = new Photon()

async function main() {
  const result = await photon.users()
  console.dir(result, { depth: null })
}

main()

```
