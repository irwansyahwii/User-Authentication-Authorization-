# User-Authentication-Authorization-
A library that provides reusable authentication and authorization

## Installation

```javascript

npm install simple-user-management

```

## How to use

```typescript
import {User} from 'simple-user-management';

/**
 * Create a new user
 */

let newUser = User.create();

newUser.userName = 'irwan@gmail.com';
newUser.password = 'abcd1234';
newUser.save()
    .subscribe(r => {
        console.log('New user saved!');
    })


/**
 * User login
 */
let loginUser = User.create();

loginUser.userName = 'irwan@gmail.com'
loginUser.password = 'abcd1234';

loginUser.login()
    .subscribe(loginInfo => {
        console.log('Logged in, token: ', loginInfo.token);
        console.log('user id:', loginInfo.uid);
    })

/**
 * User logout
 */
// We didn't keep track user login activity or period so to 
// logout just delete the login token

/**
 * Authorization
 */

let existingUser = User.create();
existingUser.loadById(loginInfo.uid);

existingUser.hasPermissionTo('view-users')
    .subscribe(isHasPermission => {
        if(isHasPermission){
            console.log('OK');
        }
        else{
            console.log('Denied');
        }
    });

/**
 * User roles
 */

let existingUser = User.create();
existingUser.loadById(loginInfo.uid);

existingUser.getRoles()
    .map(roles => {
        return Rx.Observable.from(roles)
            .map(role => role.loadPermissions())
    })
    .subscribe(roles =>{
        console.log('user role:', roles[0].name);

        console.log('role permission:', roles[0].permissions);
    })



```