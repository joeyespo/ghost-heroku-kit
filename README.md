Ghost Heroku Kit
================

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)


Run **Ghost on Heroku** with as **little effort as possible**.


Running locally
---------------

1. Clone or download

   ```bash
   $ git clone git@github.com:joeyespo/ghost-heroku-kit.git
   ```

2. Install dependencies

   ```bash
   $ npm install
   ```

3. Run

   ```bash
   $ npm start
   ```

By default, `sqlite3` and the file system will be used like usual. Related
paths are included in `.gitignore` to prevent any accidental commits.


Deploying
---------

Push your repo to GitHub and click the Deploy to Heroku button.

That's it!


Preparing your project
----------------------

You may also want to edit / replace the following to reflect your own project

- [app.json](app.json)
- [package.json](package.json)
- [this readme file](README.md)
- [content/images/logo.png](content/images/logo.png)


Swapping out services
---------------------

The following backing services are supported out of the box

- [Heroku Postgres][]
- [Mandrill][]
- [Mailgun][]
- [Sendgrid][]
- [Cloudinary][]

To switch, simply include the appropriate addon in [app.json](app.json).


Using S3
--------

Amazon S3 is supported too, but you'll have to manually create an account since
there's no S3 addon. To use it, remove your current storage addon and set the
following environment variables:

- `S3_BUCKET`
- `S3_ACCESS_KEY_ID`
- `S3_SECRET_ACCESS_KEY`

You'll get a chance to set these after clicking Deploy to Heroku.


Under the hood
--------------

Ghost Heroku Kit doesn't contain Ghost [directly][ghost-module]. This
allows you to exclude the underlying blog engine from your repository.
This also allows Ghost upgrades to be as simple as `npm update`.

Heroku addons are what fills in the missing pieces. By default, this
project uses [Mandrill][] and [Cloudinary][] to provide the required services
with zero config.

This project also follows Heroku best practices by [using environment variables][]
instead of [named environments][]. This is what allows people to independently
deploy to their own targets without requiring any code changes to `config.js`.
For convenience, you can create an `.env` file to configure locally without
accidentally committing anything.


Known Issues
------------

Using a database other than Postgres will require a change to `config.js`
until [knex accepts general connection strings][connection-string].

Ghost currently requires you to set the public `url`. Because of this,
you can't use the Heroku button or [PR apps][] without explicitly setting
the `SITE_URL` environment variable.

Heroku doesn't take `app.json` into account when using `heroku create`.
Once it does, you'll be able to use that instead of deciding between the
Deploy button and configuring your app manually.


Support Ghost!
--------------

Many thanks to the entire Ghost team for building such an amazing platform.

Running on Heroku might be helpful for running small / experimental one-off
blogs, but if you plan on using Ghost professionally, please consider
[supporting them][].


[get-app-name]: http://stackoverflow.com/questions/12570579/how-to-get-heroku-app-name-url-from-inside-the-app
[ghost-module]: https://github.com/tryghost/Ghost/wiki/Using-Ghost-as-an-NPM-module
[using environment variables]: http://12factor.net/config
[named environments]: http://support.ghost.org/config/#about-environments
[heroku postgres]: https://addons.heroku.com/heroku-postgresql
[mandrill]: https://addons.heroku.com/mandrill
[mailgun]: https://addons.heroku.com/mailgun
[sendgrid]: https://addons.heroku.com/sendgrid
[cloudinary]: http://cloudinary.com/
[pr apps]: https://devcenter.heroku.com/articles/github-integration-pull-request-apps
[sendgrid]: https://addons.heroku.com/sendgrid
[connection-string]: https://github.com/tgriesser/knex/issues/780
[supporting them]: https://ghost.org/pricing
