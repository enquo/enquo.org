---
layout: page
title: The Parts of Enquo
---
In order to be useful, Enquo needs both a ***server*** component and at least one ***client*** component in order to be useful.


# Enquo Server

An Enquo server is not a standalone piece of software.
Instead, it is any existing database server which knows how to query Enquo-encrypted data.
Typically, this functionality will be integrated into a database engine via a plugin or patch.

At this early stage of the Enquo Project, only one database server is supported, [PostgreSQL](https://www.postgresql.org/).
The [`pg_enquo`](https://github.com/enquo/pg_enquo) extension, when loaded into any PostgreSQL 10+ database server, has everything you need to query Enquo-encrypted data.


## Contributing

Support for other SQL and NoSQL database servers will come over time, as resources permit.
If you'd like to take on a challenge, see [our contributing notes](../contributing) for some hints on how to support Enquo in a database.

<a name="clients"></a>

# Enquo Clients

The software which interacts with an Enquo server is an Enquo client.
This is typically an application of some sort, such as a web application or CLI script.
The client is where all of the "heavy lifting" of encrypting and decrypting data occurs.

Enquo clients can be written in any programming language that has an Enquo client library.
At present, Enquo has official support for the following languages:

<!-- if adding to this list, please keep it sorted by language name -->

* [Ruby](https://rubygems.org/gems/enquo-core)
* [Rust](https://crates.io/crates/enquo-core)


## Contributing

To maintain compatibility between Enquo-encrypted data between languages, all of the actual cryptography is implemented in Rust.
Wrappers around this "core" code for other languages is then a relatively straightforward process.
If you'd like to contribute an Enquo core implementation for a new language, grab a copy of [the enquo-core git repository](https://github.com/enquo/enquo-core) and have at it.
If you're not Rust inclined yourself, but would like to sponsor the development of an Enquo core client in a new language, please contact [EnquoDB](https://enquodb.com).


# ORMs

While the Enquo "core" client provides everything you need to work with Enquo-encrypted data, it's quite low level.
Essentially, it's equivalent to using raw SQL -- not something most people do every day.
Instead, most people use higher-level tools, such as ORMs, to work with their database.
In keeping with our philosophy of making things as easy as possible, Enquo also provides adapters for ORMs and other high-level database management libraries.

At present, Enquo has integrations for the following ORMs:

<!-- if adding to this list, please keep it sorted by language and ORM name -->

* Ruby
  * [Rails ActiveRecord](http://rubygems.org/gems/active_enquo)

An ORM integration is written entirely in the target language of the ORM, and doesn't involve any Rust code.
It does, however, require an Enquo "core" to be available for the target language.

If you have written an Enquo integration for an ORM, feel free to raise a PR against [this site's repo](https://github.com/enquo/enquo.org) to add it to the above list.
