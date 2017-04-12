# libodonjs
JavaScript library for interfacing with mastodon

https://github.com/Gargron/mastodon/wiki/API

## Notice

This library isn't finished, and doesn't yet support posting to a mastodon instance.

## Registering an app
```
var app = new Libodon(app_name, redirect_url)
var connection = app.connect(server_url, user_email)
connection.then(conn=>{
  if(conn.result == 'redirect') {
    // conn.target now holds an URL that the browser / user agent should be directed to
  } else if(conn.result == 'success'){
    // connection is successful and the app is usable
  }
})
```
`app_name` is the name of your app - can be anything.
`redirect_url` should be the address of your app, but can be the special value of `urn:ietf:wg:oauth:2.0:oob` to ask to server to just provide the auth code.
`server_url` should be the address of your server e.g. `https://mastodon.social`
`user_email` is probably unnecessary, but is intended to be the users login email.
If the auth code is provided without redirecting back to your app, then you need to load your app with the url parameter `code` set to the auth code. E.g. `localhost/app.html?code=XXXXX`

Once you've loaded your app with the auth code, the connection should succeed, and you're ready to use the rest of the API.

## Docs

### `.timeline(target, options)`

**GET** a timeline, an array of the lasts 20 statuses

#### Args: `target` *required*

- `home`
- `public`
- `#`hashtag (retrieve the give tag)

#### Args: `options` *optional*

- `local` (public and tag timelines only): Only return statuses originating from this instance


### `.status(id)`

**GET** a status

#### Args: `id` *required*

Status id.


### `.context(id)`

**GET** the full context of a status

#### Args: `id` *required*

Status id.


### `.reblogged_by(id)`

**GET** an array of all accounts who reblogged the status

#### Args: `id` *required*

Status id.


### `.favourited_by(id)`

**GET** an array of all accounts who favourited the status

#### Args: `id` *required*

Status id.


### `.account(id)`

**GET** an account

#### Args: `id` *required*

Account id.


### `.account_self()`

**GET** the account your are connected with (`/verify_credentials`)


### `.account_statuses(id,options)`

**GET** an array of the lasts 20 statuses of an account

#### Args: `id` *required*

Account id.

#### Args: `options` *optional*

*To be tested.*


### `.followers(id)`

**GET** an array of the followers of an account

#### Args: `id` *required*

Account id.


### `.relationships()`

*To be tested.*


### `.suggestions()`

**GET** suggestions.

*To be tested.*


### `.search(q)`

**GET** the result of the search

#### Args: `q` *required*

If `q` is a URL, Mastodon will attempt to fetch the provided account or status. Otherwise, it will do a local account and hashtag search.
