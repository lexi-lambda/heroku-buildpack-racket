# heroku-buildpack-racket

This is a custom [Heroku buildpack][heroku-buildpacks] for building and deploying [Racket][racket] applications on [Heroku][heroku].

To use this custom buildpack, use the Heroku toolbelt's `buildpacks:set` command:

```sh
$ heroku buildpacks:set https://github.com/lexi-lambda/heroku-buildpack-racket
```

When the application is next deployed, the new buildpack will be used.

The Racket buildpack requires that the `RACKET_VERSION` environment variable be set in order to decide what version of Racket to use. It may either be set to a specific version (such as `6.2`) or to either `current` or `HEAD`, which will use nightly, bleeding-edge snapshots.

To configure environment variables for your Heroku application, either use the web interface, or use the `heroku config:set` command.

[racket]: http://racket-lang.org/
[heroku]: https://www.heroku.com/
[heroku-buildpacks]: https://devcenter.heroku.com/articles/buildpacks
