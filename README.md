
  #VirusDB
	
[![Version](https://img.shields.io/npm/v/dev.db.svg?color=3884FF&label=version)](https://www.npmjs.com/package/dev.db)

[![Downloads](https://img.shields.io/npm/dt/dev.db.svg?color=3884FF)](https://www.npmjs.com/package/dev.db)

[![Dependencies](https://img.shields.io/badge/dependencies-0-brightgreen?color=3884FF)](https://www.npmjs.com/package/dev.db)

[![Quality](https://packagequality.com/shield/dev.db.svg?color=3dd164)](https://packagequality.com/#?package=dev.db)


A lightweight, 0 dependency, easy-to-use local database using JSON to store data.

- **[Documentation](https://clony.vercel.app)**
- **[Yarn Package](https://yarnpkg.com/package/dev.db)**
- **[NPM Package](https://npmjs.com/package/dev.db)**
- **[NPM Package Statistics](https://npm-stat.com/charts.html?package=dev.db&from=2021-05-07)**

Installation
------------

```sh-session
npm install dev.db
yarn add dev.db
```

Example Usage
-------------

### JsonDatabase

```js
const VirusDB = require('dev.db');
const db = new VirusDB();


db.set('money', 100);
db.set('person.name', 'virus');


db.has('money'); // true
db.has('person.name'); // true
db.has('person.age'); // false


db.get('person.name'); // 'virus'
db.get('person.job'); // undefined


db.toJSON(); // { money: 100, person: { name: 'virus' } }
```

### JsonCollections

```js
const dbConfig =  {
  autoSave: false,
  encryptionKey: 'qwertyuiopasdfghjkpzxxcvbnm',
  dataFile: 'database/dev.db.json',
  collectionsFolder: 'database/collections'
}
const VirusDB = require('dev.db');
const db = new VirusDB(dbConfig);

const Users = db.createCollection('users');


Users.create({ name: 'virus', age: 19 });
Users.create({ name: 'virus24', age: 19 });


Users.update(
  user => user.age = 20,
  target => target.name === 'virus'
);
// or (dev.db@0.0.2+)
const user = Users.get(target => target.name === 'virus');
user.age = 20;
user.save();


Users.get(user => user.name === 'virus'); // { name: 'virus', age: 20 }
Users.getMany(user => user.age > 18); // [{ name: 'virus', age: 20 }, { name: 'virus24', age: 19 }]
```

### With TypeScript:

```ts
import { JsonDatabase, Modifiable } from 'dev.db';
const dbConfig =  {
  autoSave: false,
  encryptionKey: 'qwertyuiopasdfghjkpzxxcvbnm',
  dataFile: 'database/dev.db.json',
  collectionsFolder: 'database/collections'
}

const db = new JsonDatabase(dbConfig);

type User = {
  name: string
  age: number
}

const Users = db.createCollection<User>('users');


Users.create({ name: 'virus', age: 19 });
Users.create({ name: 'virus24', age: 19 });


Users.update(
  user => user.age = 20,
  target => target.name === 'virus'
);
// or (dev.db@0.0.2+)
const user = <Modifiable<User>> Users.get(target => target.name === 'virus');
user.age = 20;
user.save();


Users.get(user => user.name === 'virus'); // { name: 'virus', age: 20 }
Users.getMany(user => user.age > 18); // [{ name: 'virus', age: 20 }, { name: 'virus24', age: 19 }]
```

Contributing
------------

Before [creating an issue](https://github.com/virgel1995/dev.db/issues), please ensure that it hasn't already been reported or suggested.

When [submitting a new pull request](https://github.com/virgel1995/dev.db/pulls), please make sure the code style/format used is the same as the one used in the original code.

License
-------

Refer to the [LICENSE](LICENSE) file.
