---
layout: page
title: Contributing to Enquo
---
Do you want to Enquo?  Excellent.


# Supporting a new language

Before Enquo can be used in a particular programming language, the `enquo-core` library needs to be made available.
This is a Rust library that provides the cryptographic primitives used to encrypt and decrypt data so it can be searched.

Supporting a new language is simply(?) a matter of writing enough "wrapper" code to make the basic primitives available in the target language.
It should be fairly close to a one-to-one mapping of the Rust functions into a useable form.

All officially-supported language wrappers live together in the [`enquo-core`](https://github.com/enquo/enquo-core) GitHub repo.
They're kept together so that new features can be more easily added to all supported languages in parallel.
If you'd like to contribute a wrapper for a new language, please open a PR on that repo.
Even if you haven't gotten very far, post what you have, and we'll all work on it together.


# Supporting a new ORM

If your favourite programming language has an `enquo-core` library, but your pet ORM doesn't work well with Enquo, this is your chance to shine!
You don't need to know any Rust, you only need to figure out how to hook into your ORM to encrypt values as they go towards the database, and decrypt them again when they're retrieved.
By calling into the relevant functions in the `enquo-core` library, all the hard stuff is taken care of for you.

Integrations are typically maintained separately from each other, as they can have independent bugfix and release schedules.
If you'd like your integration to be officially supported, we can "adopt" it into the [Enquo GitHub org](https://github.com/enquo), or you can keep it separate.
In either event, create a PR against [the website's repo](https://github.com/enquo/enquo.org) to add your integration to [the Components page](../components).


# Supporting a new database

This is the biggie.
Thankfully, there aren't many databases out there (compared to the number of languages and ORMs), so we don't have to do this as often.
Unfortunately, there's not a lot of *general* guidance that can be given about adding Enquo to a database, because every one is very, *very* different.

Supporting Enquo in a database server is mostly a matter of teaching the database (a) how to recognise Enquo data, and (b) how to do comparisons between Enquo data items.
There's also how to store and retrieve Enquo data, but that tends to be more straightforward.

The `enquo-core` library has everything you need for serializing/deserializing Enquo data, and performing the comparison operations.
What you have to do is figure out how to hook into the database itself and make it call out to `enquo-core` when appropriate.
