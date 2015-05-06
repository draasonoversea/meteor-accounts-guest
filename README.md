# accounts-guest
============

Automatically add visitor as anonymous guest with userId

## Features
- each non-logged in visitor gets a userId, accessible via Accounts and Meteor:userId()
- includes configurable cleanup function


## Installation
```sh
meteor add artwells:accounts-guest
```
Removed dependency on accounts-ui package. Must manually install a ui package like:
```sh
meteor add accounts-ui
```
or
```sh
meteor add ian:accounts-ui-bootstrap-3
```
and you are done!




optionally (to clean out old guest accounts) in server-only code
```javascript
Accounts.removeOldGuests([time before]);
```

Now Meteor.userId() will be populated for each new visitor, including across reloads

## Examples

```javascript
/* clean out all guest accounts more than 24 hours old (default behavior) */
Accounts.removeOldGuests();
```
or

```javascript
/* clean out all guest accounts more than 2 hours old */
var before = new Date();
before.setHours(before.getHours() - 2);
Accounts.removeOldGuests(before);
```



## Options (Set in server code at start up)

* `AccountsGuest.enabled`,  default true. Automatically logs in all visitors.
* `AccountsGuest.forced`,  default true. Will force recently logged out accounts into guest mode.

##Option Examples

In code available to server, to temporarily or conditionally disable guest login
```javascript
AccountsGuest.enabled = false
```

In code available to client, to temporarily or conditionally disable guest login after user logout
```javascript
AccountsGuest.enabled = true
```

In code available to server, to assign the guest a friendly nickname
```javascript
AccountsGuest.name = true
```


## TODO
- tests for forced, and enabled options
- Allow guest session merged into new session if a visitor logs in
- Allow merged session/other variables to be specified in config
