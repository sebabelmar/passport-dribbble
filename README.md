# Passport-Dribbble

[Passport](https://github.com/jaredhanson/passport) strategy for authenticating
with [Dribbble](http://dribbble.com/) using the OAuth 2.0 API.

This module lets you authenticate using dribbble in your Node.js applications.
By plugging into Passport, dribbble authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Install

    $ npm install passport-dribbble

## Usage

#### Configure Strategy

The Dribbble authentication strategy authenticates users using a dribbble
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

    passport.use(new DribbbleStrategy({
        clientID: DRIBBBLE_CLIENT_ID,
        clientSecret: DRIBBBLE_CLIENT_SECRET,
        callbackURL: "http://127.0.0.1:3000/auth/dribbble/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ dribbbleId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'dribbble'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/dribbble',
      passport.authenticate('dribbble'));

    app.get('/auth/dribbble/callback',
      passport.authenticate('dribbble', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Tests

    $ npm install --dev
    $ make test

## Credits

  [Seba Belmar](http://github.com/sebabelmar)

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2015 [Seba Belmar](http://sebabelmar.com/)
