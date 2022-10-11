---
layout: page
title: "pg_enquo: Queryable encryption with PostgreSQL"
banner: pg_enquo
---
Strong encryption is one of the best ways of preventing attackers from obtaining and leaking your sensitive data.
When you encrypt your data, attackers can't read it, but neither can PostgreSQL, which means your queries don't work any more.
At least, they didn't, until `pg_enquo`.

The `pg_enquo` extension provides PostgreSQL 11+ databases with leading edge cryptographic capabilities.
It enables efficient and secure queries against a range of [common data types](https://github.com/enquo/pg_enquo/tree/main/doc/data_types/).


# Getting Started

Using `pg_enquo` is straightforward.
You simply:

1. [Install `pg_enquo`](https://github.com/enquo/pg_enquo/tree/main/doc/installation.md) into your PostgreSQL database;

2. Create columns in your tables that use an `enquo_*` datatype; and

3. Use an [Enquo client](../#clients) in your application to encrypt data and queries before they are sent to PostgreSQL.

All your Enquo-protected data is then encrypted before it is sent to PostgreSQL, and decrypted after it is retrieved from a query.
Query data itself is also encrypted, for maximum protection.


# Want To Know More?

All [source code for `pg_enquo`](https://github.com/enquo/pg_enquo) is open source, under an OSI-approved licence, so you can see exactly how it works.

If you'd like a summary of the cryptographic basis for the entire Enquo project, check out [our "How It Works" page](../../how-it-works/).
