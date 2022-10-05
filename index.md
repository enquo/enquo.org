---
layout: page
title: The Enquo Project
banner: true
---
Enquo, for "ENcrypted QUery Operations", provides the ability to query *encrypted* data in popular database servers.

Your application encrypts the data, inserts in the database in its encrypted form, and nobody can read it again until it is loaded by your application.
The database never knows what the data is, because it remains encrypted at all times in the database.


# Why do I need this?

Because data leaks or gets stolen *all the time*.
Strong encryption is one of the best ways to ensure that your sensitive data is kept safe.

However, when you encrypt data, you can't search it.
If you can't search your data, you can't build the features you need.

***Or, you can use Enquo.***

Enquo encrypts your data in your application, before it is written to the database.
But the encryption format allows the database to execute queries *without knowing what the data is*.


# Sounds great, how do I use it?

We currently support PostgreSQL 11+ and Rails ActiveRecord as an ORM.
*Support for more databases, languages, and ORMs is a work-in-progress.*

Check out [the `pg_enquo` installation instructions](https://github.com/enquo/pg_enquo/tree/main/doc/installation.md) for details on how to install the PostgreSQL extension,
and [the ActiveEnquo README](https://github.com/enquo/active_enquo#readme) for client-side usage instructions.


## But I'm not using Rails!

We're hard at work adding support for more languages and ORMs.
If you'd like to get involved, and develop support for your personal preferred technology,
check out [our contributor guide](/contributing) for some basic pointers on how to get started.

If you want Enquo support for a new technology, but don't have coders on-hand, [EnquoDB](https://enquodb.com) is the commercial arm of the project, offering development, consulting, and training.


# I have more questions...

That's OK, we probably have answers.

You may wish to know [more about the Enquo project](about) -- our mission and purpose, essentially.
Closely related is [our development philosophy](about/philosophy).

If you're curious about whether Enquo solves the specific threats your data is facing, our [threat models and security properties](threat-models) page is where you want to go.
You may also be interested in [the minutiae of how Enquo works](how-it-works).

Finally, check out [the project FAQ](/faq), and if you're still curious, e-mail us at [`contact@enquo.org`](mailto:contact@enquo.org) and we'll do our best to help you out.
