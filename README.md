# heroku-buildpack-racket

This is a custom [Heroku buildpack][heroku-buildpacks] for building and deploying [Racket][racket] applications on [Heroku][heroku].

To use this custom buildpack, use the Heroku toolbelt's `buildpacks:set` command:

```sh
$ heroku buildpacks:set https://github.com/lexi-lambda/heroku-buildpack-racket
```

When the application is next deployed, the new buildpack will be used.

## Configuration

The Racket buildpack requires that the `RACKET_VERSION` environment variable be set in order to decide what version of Racket to use. It may either be set to a specific version (such as `6.2`) or to either `current` or `HEAD`, which will use nightly, bleeding-edge snapshots.

By default, the buildpack will use the full Racket distribution. If you want to only install a minimal Racket distribution, append `-minimal` to the end of the version string (e.g. `6.2-minimal` or `HEAD-minimal`).

You can also customize the [package catalogs][pkg-catalogs] that Racket will use to install packages. This is useful if you want to specify package sources that are different or not available in the main package catalog. To do this, specify a space-separated list of packages using the `RACKET_EXTRA_PKG_CATALOGS` environment variable, which will be prepended to the default list of package catalogs before your application’s package is installed.

To configure environment variables for your Heroku application, either use the web interface, or use the `heroku config:set` command.

## Running

The Racket buildpack will install your repository as a package, so it *must* include an `info.rkt` file in the root. Once installed, it will be moved to the `app/` directory. It is recommended that you specify your application entry point via the `racket` executable's `-l` flag so you can pass a module path instead of a file path, which will work no matter what the filesystem layout.

For example, if your package contained a file called `server.rkt` in a collection called `my-app`, the Procfile entry to start your application might look like this:

```sh
web: racket -l my-app/server
```

[racket]: http://racket-lang.org/
[heroku]: https://www.heroku.com/
[heroku-buildpacks]: https://devcenter.heroku.com/articles/buildpacks
[pkg-catalogs]: http://docs.racket-lang.org/pkg/Package_Concepts.html#%28tech._package._catalog%29
