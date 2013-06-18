Heroku buildpack: Perl
======================

This is a Heroku buildpack for Perl. It installs dependencies with Carton, then runs any PSGI based web applications using Starman.

Usage
-----

Example usage:

    $ ls
    cpanfile
    app.psgi
    lib/

    $ cat cpanfile
    requires 'Plack', '1.0000';
    requires 'DBI', '1.6';

    $ carton install
    $ git add carton.lock
    $ git commit -m 'bundle carton.lock'

    $ heroku create --stack cedar --buildpack https://github.com/miyagawa/heroku-buildpack-perl.git#carton

    $ git push heroku master
    ...
    -----> Heroku receiving push
    -----> Fetching custom buildpack
    -----> Perl/PSGI app detected
    -----> Installing dependencies with Carton

The buildpack will detect that your app has an `app.psgi` in the root.

Libraries
---------

Dependencies can be declared using `cpanfile` and frozen with `carton install`. The buildpack will install these dependencies using [Carton](https://metacpan.org/release/carton) into a cached `./local` directory.

