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
## Networking
### http
##### app.module.ts
```
import { HttpClientModule } from '@angular/common/http';
```
```
imports: [
    HttpClientModule
  ]
```
##### my.page.ts
```
import { HttpClient } from '@angular/common/http';
```
```
constructor(private http: HttpClient) { }
```
```
async postData(url: string, 
				body: object, 
  				options: object = {}) {
    // options = { responseType: 'text' }
    return await this.http.post(url, 
    							body, 
    							options).toPromise();
}
async getData(url: string, options: object = {}) {
    // options = { responseType: 'text' }
	return await this.http.get(url, options).toPromise();
}
```
## Navigation

### Navigating from code

```
import { Router } from '@angular/router';
```
```
constructor(private router: Router) { }
```
```
myMethod() {
	this.router.navigateByUrl('/dashboard');
}
```
### Navigating from html
```
<ion-button routerLink="/dashboard"
			routerDirection="forward">
	Go to Dashboard
</ion-button>
```




