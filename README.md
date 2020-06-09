# Async Await Mutex Lock
![Tests](https://github.com/malhotra-sidharth/async-await-mutex-lock/workflows/Running%20All%20Tests%20and%20Publish%20to%20NPM/badge.svg)

Mutex locks for async functions with functionality to add keys for separate locks

[![NPM](https://nodei.co/npm/async-await-mutex-lock.png)](https://nodei.co/npm/async-await-mutex-lock/)


# Usage Instructions

#### Without Key
```javascript
import Lock from "async-await-mutex-lock";

let lock = new Lock();

async function test(): Promise<void> {
  await lock.acquire();

  try {
    // Don't return a promise here as Promise may resolve after finally
    // has executed
  }
  finally {
    lock.release();
  }
}
```

#### With Key
All the keys will have their own separate locks and separate waiting lists;
```javascript
import Lock from "async-await-mutex-lock";

let lock = new Lock<string>();

async function test(): Promise<void> {
  await lock.acquire("myKey");

  try {
    // Don't return a promise here as Promise may resolve after finally
    // has executed
  }
  finally {
    lock.release("myKey");
  }
}

async function testTwo(): Promise<void> {
  await lock.acquire("myKeyTwo");

  try {
    // Don't return a promise here as Promise may resolve after finally
    // has executed
  }
  finally {
    lock.release("myKeyTwo");
  }
}
```

#### Checking if a lock is acquired or not
```javascript
import Lock from "async-await-mutex-lock";

let lock = new Lock();

async function test(): Promise<void> {
  await lock.acquire();

  console.log(lock.isAcquired()) // prints true
}
```

`isAcquired()` with `key` checks for the given key separately.
```javascript
import Lock from "async-await-mutex-lock";

let lock = new Lock<string>();

async function test(): Promise<void> {
  await lock.acquire("myKey");

  console.log(lock.isAcquired("myKey")) // prints true
}
```


### Issues or Bugs
In case of any issues or bugs, please open a pull request [here](https://github.com/malhotra-sidharth/async-await-mutex-lock/pulls)

###### Credits
This package has been inspired from [await-lock](https://www.npmjs.com/package/await-lock)
with an added functionality of allowing keys and checking if lock has been acquired or not
