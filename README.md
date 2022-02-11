Ideal state after running `npx prisma ...` commands from inside the server directory, which already has both Prisma dependencies installed:

```
/db
  /migrations
  dev.db-journal
  schema.prisma
/server
  /node_modules
  .gitignore
  index.js
  package-lock.json
  package.json
```

Actual state adds Prisma dependencies outside the directory we are running from:

```
/db
  /migrations
  /node_modules       👈
  dev.db-journal
  package-lock.json   👈
  package.json        👈
  schema.prisma
/server
  /node_modules
  .gitignore
  index.js
  package-lock.json
  package.json
```

Note: `[server] >` represents the command prompt for running commands from within the server directory. There are helpers in server/package.json so you can just run `[server] > npm run <blah>`

`[server] > npx prisma studio --schema ../db/schema.prisma` does not create the node_modules setup in the db directory, but `[server] > npx prisma generate --schema ../db/schema.prisma` and thus, by extension, `[server] > npx prisma migrate dev --schema ../db/schema.prisma` both do.
