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
### Encrypted PouchDB
```
npm install pouchdb --save
npm install crypto-js --save
nmp install transform-pouch --save
```
##### polyfills.ts
```
(window as any).global = window;
(window as any).process = window;
```
##### my.page.ts
```
import PouchDB from 'pouchdb';
import CryptoJS from 'crypto-js';
import TransformPouch from 'transform-pouch';
PouchDB.plugin(TransformPouch);
```
```
private localDB: any;

async initDB(key: string) {
  this.localDB = await new PouchDB('localDB');
  this.localDB.transform({
    incoming: function (doc) {
      Object.keys(doc).forEach(function (field) {
        if (field.substr(0, 1) !== '_') {
          doc[field] = CryptoJS.AES.encrypt(doc[field], key).toString();
        }
      });
      return doc;
    },
    outgoing: function (doc) {
      Object.keys(doc).forEach(function (field) {
        if (field.substr(0, 1) !== '_') {
          const bytes  = CryptoJS.AES.decrypt(doc[field], key);
          doc[field] = bytes.toString(CryptoJS.enc.Utf8);
        }
      });
      return doc;
    }
  });
  return await this.localDB.info();
}

use_db() {
  this.initDB('secret key 123').then((info) => {
    this.localDB.allDocs({include_docs: true})
    .then((docs) => {
      console.log('docs', docs);
    });
  });
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
    return await this.http.post(url, body, options).toPromise();
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
### Passing data (id) to page through url
##### app-routing.module.ts
```
{ path: 'detail/:id', loadChildren: './pages/detail/detail.module#DetailPageModule' },
```
##### detail.page.ts
```
import { ActivatedRoute } from '@angular/router';
```
```
constructor(private route: ActivatedRoute) { }
```
```
ionViewWillEnter(){
  const id = this.route.snapshot.paramMap.get('id');
}
```
## Styles & CSS
### Colors
* primary => var(--ion-color-primary)
* secondary => var(--ion-color-secondary)
* tertiary => var(--ion-color-tertiary)
* success => var(--ion-color-success)
* warning => var(--ion-color-warning)
* danger => var(--ion-color-danger)
* light => var(--ion-color-light)
* medium => var(--ion-color-medium)
* dark => var(--ion-color-dark)

## Shared Custom Components
##### Generate first component
```
ionic g component components/mycomponent
ionic g module components/shared
```
##### shared.module.ts:

1. import component
2. add to declarations [ ]
3. add to exports [ ]

##### To consume:
```
import { SharedModule } from '../../components/shared.module';
```
* add to imports [ ]
* use tag in html file

Adding new components with:  ```ionic g component components/newcomponent``` will automatically update shared.module.ts.




