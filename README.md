# Passport-google-drive

[Passport](https://github.com/jaredhanson/passport) strategy for authenticating
with [Google Drive](https://drive.google.com/) using the OAuth 2.0 API.

This module lets you authenticate using Google Drive, in your Node.js applications.  
By plugging into Passport, Drive
authentication can be easily and unobtrusively integrated into any application or
framework that supports [Connect](http://www.senchalabs.org/connect/)-style
middleware, including [Express](http://expressjs.com/).

## Install

    $ npm install passport-google-drive

## Usage

#### Configure Strategy

The Google Drive authentication strategy authenticates users using a Google
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

The consumer key and secret are obtained by [creating an application](https://console.developers.google.com) at
Google's [developer](https://developers.google.com) site.

```js
    passport.use(new GoogleDriveStrategy({
        clientID: DRIVE_CLIENT_ID,
        clientSecret: DRIVE_CLIENT_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/google-drive/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ driveId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));
```

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'google-drive'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

```js
    app.get('/auth/google-drive',
      passport.authenticate('google-drive'));

    app.get('/auth/google-drive/callback', 
      passport.authenticate('google-drive', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });
```

## Examples

For a complete, working example, refer to the [login example](https://github.com/slugbay/passport-google-drive/tree/master/example/login).

## Credits

  - [Sluggy Bear](http://github.com/slugbay)

  Copyright (c) 2016 Sluggy Bear <[https://www.slugbay.com](https://www.slugbay.com)>

## Thanks

  - [Jared Hanson](http://github.com/jaredhanson)

## License

  - [The MIT License](http://opensource.org/licenses/MIT)
