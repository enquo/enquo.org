---
layout: page
title: The Enquo Project
---
Enquo, for "ENcrypted QUery Operations", is a project to build the ability to query *encrypted* data in popular database servers.

It consists of a small server-side extension, which teaches the database how to work with Enquo-encrypted data, and code that plugs into your ORM or application code to encrypt and decrypt your data within the application,

# Why do I need this?

Strong encryption is one of the best ways to ensure that your application's data can't be leaked.
However, when you encrypt data, it traditionally can't be searched any more.
So, to build the features your application needs, the data needs to be left unencrypted, where any criminal can come along and dump it.

Or, you can use Enquo.
It encrypts your data before it is written to the database, but the encryption format allows the database to execute common queries *without knowing what the data is*.

This design allows your application to be hardened against attacks such as:

* SQL injection;

* Leaked or brute-forced database access credentials;

* Accidentally leaving a database accessible to the internet;

* Stolen database backups;

* Compromise of a developer's machine, when they're working with data dumped from production.


# Sounds great, how do I use it?

As the project is in an *extremely* early stage, we only support PostgreSQL as the server, and Rails ActiveRecord as an ORM.
If that matches your environment, then check out the [`pg_enquo`](https://github.com/enquo/pg_enquo) README for details on how to install the PostgreSQL extension,
and the [ActiveEnquo](https://github.com/enquo/active_enquo) README for client-side usage instructions.

If you're using another combination of technologies, we're glad to welcome contributors for other languages, ORMs, and databases.
Adding support for other languages is mostly about writing a thin wrapper around the [Rust core cryptographic code](https://github.com/enquo/enquo-core) for your language of choice,
and then writing some sort of extension for your preferred ORM that uses the wrapper.
Feel free to open PRs on GitHub for in-progress work, and we can give you guidance if you get stuck.


# I have more questions...

That's OK, we probably have answers.
Check out [the project FAQ](/faq), and if you're still curious, e-mail us at [`contact@enquo.org`](mailto:contact@enquo.org) and we'll do our best to help you out.
