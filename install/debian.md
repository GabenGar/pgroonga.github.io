---
title: Install on Debian GNU/Linux
---

# Install on Debian GNU/Linux

This document describes how to install PGroonga on Debian GNU/Linux.

## Supported versions

Here are supported Debian GNU/Linux versions:

  * [bullseye](#install-on-bullseye)

## How to install on Debian GNU/Linux bullseye {#install-on-bullseye}

You can use the following instruction to install PGroonga on Debian GNU/Linux bullseye.

Install `groonga-apt-source` package:

```console
$ sudo apt install -y -V wget
$ wget https://packages.groonga.org/debian/groonga-apt-source-latest-bullseye.deb
$ sudo apt install -y -V ./groonga-apt-source-latest-bullseye.deb
```

If you want to use the PostgreSQL packages provided by PostgreSQL, you need to add [the APT repository by PostgreSQL][postgresql-apt]:

```console
$ echo "deb http://apt.postgresql.org/pub/repos/apt/ bullseye-pgdg main" | sudo tee /etc/apt/sources.list.d/pgdg.list
$ wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```

Install `postgresql-*-pgdg-pgroonga` package:

```console
$ sudo apt update
$ sudo apt install -y -V postgresql-14-pgdg-pgroonga
Or
$ sudo apt install -y -V postgresql-12-pgdg-pgroonga
Or
$ sudo apt install -y -V postgresql-13-pgdg-pgroonga
```

If you want to use [MeCab](http://taku910.github.io/mecab/) based tokenizer, you also need to install `groonga-tokenizer-mecab` package:

```console
$ sudo apt install -y -V groonga-tokenizer-mecab
```

Create a database:

```console
$ sudo -u postgres -H psql --command 'CREATE DATABASE pgroonga_test'
```

(Normally, you should create a user for `pgroonga_test` database and use the user. See [`GRANT USAGE ON SCHEMA pgroonga`](../reference/grant-usage-on-schema-pgroonga.html) for details.)

Connect to the created database and execute `CREATE EXTENSION pgroonga`:

```console
$ sudo -u postgres -H psql -d pgroonga_test --command 'CREATE EXTENSION pgroonga'
```

That's all!

Try [tutorial](../tutorial/). You can understand more about PGroonga.

[postgresql-apt]:https://www.postgresql.org/download/linux/debian/
