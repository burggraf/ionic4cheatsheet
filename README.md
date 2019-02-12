# Ionic 4 Cheat Sheet
This page is designed to help you to quickly do those things you've already figured out how to do in Ionic 4, but can't remember the steps involved.

## Storage

### IonicStorageModule (localStorage)
```
npm install @ionic/storage --save
```

##### app.module.ts:

```
import { IonicStorageModule } from '@ionic/storage';
imports[
    IonicStorageModule.forRoot()
]
```

##### my.page.ts:

```
import { Storage } from '@ionic/storage';
constructor(private storage: Storage) {
    this.storage.get('key');
    this.storage.set('key', 'value');
}
```

### PouchDB
```
npm install pouchdb --save
```

##### polyfills.ts
```
(window as any).global = window;
```

##### my.page.ts
```
import PouchDB from 'pouchdb';
```

```
private localDB: any;
async initDB() {
   this.localDB = await new PouchDB('localDB');
}
async get(id: string, options) {
      return await this.localDB.get(id, options);
}
```




