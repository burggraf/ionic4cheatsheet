# Ionic 4 Cheat Sheet
This page is designed to help you to quickly do those things you've already figured out how to do in Ionic 4, but can't remember the steps involved.

## Storage

### app.module.ts:

```
import { IonicStorageModule } from '@ionic/storage';
imports[
    IonicStorageModule.forRoot()
]
```

### my.page.ts:

```
import { Storage } from '@ionic/storage';
constructor(private storage: Storage) {
    this.storage.get('key');
    this.storage.set('key', 'value');
}
```




