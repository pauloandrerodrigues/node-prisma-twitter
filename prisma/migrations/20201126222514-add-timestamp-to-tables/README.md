# Migration `20201126222514-add-timestamp-to-tables`

This migration has been generated by Diego Fernandes at 11/26/2020, 7:25:14 PM.
You can check out the [state of the schema](./schema.prisma) after the migration.

## Database Steps

```sql
ALTER TABLE "notifications" ADD COLUMN     "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
ADD COLUMN     "updatedAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP

ALTER TABLE "tweet_likes" ADD COLUMN     "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
ADD COLUMN     "updatedAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP

ALTER TABLE "tweets" ADD COLUMN     "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
ADD COLUMN     "updatedAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP

ALTER TABLE "user_follows" ADD COLUMN     "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
ADD COLUMN     "updatedAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP

ALTER TABLE "users" ADD COLUMN     "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,
ADD COLUMN     "updatedAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP
```

## Changes

```diff
diff --git schema.prisma schema.prisma
migration 20201126221809-tweet-parent-not-required..20201126222514-add-timestamp-to-tables
--- datamodel.dml
+++ datamodel.dml
@@ -2,9 +2,9 @@
 // learn more about it in the docs: https://pris.ly/d/prisma-schema
 datasource db {
   provider = "postgresql"
-  url = "***"
+  url = "***"
 }
 generator client {
   provider = "prisma-client-js"
@@ -21,8 +21,11 @@
   following     UserFollows[]   @relation("UserFollowsUser")
   followers     UserFollows[]   @relation("UserFollowsTarget")
   notifications Notifications[]
+  createdAt DateTime @default(now())
+  updatedAt DateTime @default(now()) @updatedAt
+
   @@map("users")
 }
 model Tweet {
@@ -34,8 +37,11 @@
   comments     Tweet[]      @relation("TweetComments")
   parentId     String?
   likes        TweetLikes[]
+  createdAt DateTime @default(now())
+  updatedAt DateTime @default(now()) @updatedAt
+
   @@map("tweets")
 }
 model UserFollows {
@@ -44,8 +50,11 @@
   userId   String
   target   User   @relation("UserFollowsTarget", fields: [targetId], references: [id])
   targetId String
+  createdAt DateTime @default(now())
+  updatedAt DateTime @default(now()) @updatedAt
+
   @@map("user_follows")
 }
 model TweetLikes {
@@ -54,8 +63,11 @@
   user    User   @relation(fields: [userId], references: [id])
   tweetId String
   userId  String
+  createdAt DateTime @default(now())
+  updatedAt DateTime @default(now()) @updatedAt
+
   @@map("tweet_likes")
 }
 model Notifications {
@@ -63,6 +75,9 @@
   content String
   user    User   @relation(fields: [userId], references: [id])
   userId  String
+  createdAt DateTime @default(now())
+  updatedAt DateTime @default(now()) @updatedAt
+
   @@map("notifications")
 }
```


