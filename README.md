# database

Install a PouchDB-Server globally with PNPM `pnpm install -g pouchdb-server`, and run `pouchdb-server --dir ./dist --port 5984` to spawn the database server.

Then, open `http://localhost:5984/_utils/#/verifyinstall` in a browser, to view the dashboard and verify the installation.

Add this line to your `.gitignore` file, to keep the database log files out of your repository.

```
# PouchDB
log.txt
```

Since we've installed PouchDB-Server, a CORS solution is already added by default. Otherwise, run `pnpm install -g add-cors-to-couchdb` to add CORS to your CouchDB server.

Next, run `pnpm install pouchdb @types/pouchdb`; note that we're including PouchDB @types since we'll be writing in Typescript. After those modules install, run `tsc --init` to create a `tsconfig.json` file.
We'll need to set `"allowSyntheticDefaultImports"` to `true`, so default imports from modules without a default export work, and set the `"outDir"` to `"./dist"` to maintain seperation of source and distribution files.

```json
{
  "compilerOptions": {
    "outDir": "./dist",
    ...
    "allowSyntheticDefaultImports": true
  }
}
```

In our `dist` sub-directory, we can create our `index.ts`, and write the following:

```typescript
import * as PouchDB from 'pouchdb';
```

Change into the `src` directory and compile with `tsc --build ../tsconfig.json --watch` to generate the `dist/index.js` file and to continually watch for updates.
