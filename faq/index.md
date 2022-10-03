---
layout: page
title: Enquo Project Frequently Asked Questions
---
You've got questions?
We've got answers (probably).
If your question isn't in here, feel free to e-mail [`contact@enquo.org`](mailto:contact@enquo.org) and we'll do our best to help you out.


# What Is This Black Magic?

Heh, that's a reasonable question.
Being able to efficiently query securely-encrypted data *does* seem like some sort of trick.
However, Enquo uses recent advances in cryptography, specifically [Order-Revealing Encryption](https://crypto.stanford.edu/ore/), to make this possible.
If you're deeply interested in this area, we suggest you take a look at our [How It Works](/how-it-works) page for all the gory details.


# How Secure is Enquo?

As an early-stage project, none of the Enquo codebase has received a third-party security review yet.
However, as much as possible we're using Rust, which removes large areas of attack surface, and sticking to well-known libraries from reputable third parties.
The cryptographic primitives in use are all robust and well-analysed, such as AES256 and HMAC-SHA256.
The [Order-Revealing Encryption algorithm](/how-it-works) is from a well-respected cryptographic research team at Stanford, has been peer-reviewed, and does not have any severe weaknesses that we're aware of.

At the end of the day, almost anything would be more secure than leaving data unencrypted in the database, which is probably what you're doing now.


# Is Enquo Slow?

Although that's a nice rhyme, Enquo does not significantly reduce the performance of your database.
The overhead of using Enquo-encrypted values is negligible.

At some point in the near(ish) future, we'll actually benchmark this, and then you'll have Real Numbers.


# Surely There are *Some* Downsides, Though?

Yes, there is indeed no such thing as a free lunch.
The cost for an Enquo-enabled database is in disk space.

Enquo-encrypted ciphertexts are significantly larger than just storing the plaintext value.
This is because the [Order-Revealing Encryption](/how-it-works) that underlies a lot of how Enquo works unavoidably produces large ciphertexts.

The exact overhead varies by data type, and is covered in the [data type documentation](https://github.com/enquo/pg_enquo/tree/main/doc/data_types).


# What Languages/ORMs Are Supported?

Currently there is core client support for [Rust](https://github.com/enquo/enquo-core/tree/rust) and [Ruby](https://github.com/enquo/enquo-core/tree/ruby), and [ORM support for Rails ActiveRecord](https://github.com/enquo/active_enquo).
We hope to rapidly grow the languages and ORMs that are supported, by community contributions and sponsored development.
As the cryptographic logic is all in a portable Rust core library, supporting additional languages is typically a relatively low-effort undertaking, and requires minimal cryptographic expertise.


# What Databases Are Supported?

At present, we have an extension for PostgreSQL, called [`pg_enquo`](https://github.com/enquo/pg_enquo).
Other databases, including NoSQL databases, will be supported as time and resources permit.


# Is Enquo Open Source?

Absolutely.
We believe that open source is a great way to maintain trust and transparency, and build a real community around Enquo.
All components are available under an OSI-approved licence, and always will be.


# How Do I Use Enquo with a SaaS Database (such as AWS RDS, GDP Cloud SQL, etc)?

Because Enquo requires an extension to be loaded into the database server, it is not typically compatible with "cloud" database services.
However, all is not lost: [EnquoDB](https://enquodb.com) is a commercial organisation which is developing an Enquo-enabled SaaS database service.
For more info, and to sign up to the private beta waiting list, visit [https://enquodb.com](https://enquodb.com).


# Are There Commercial Support Options Available?

For all your commercial support needs, please contact [EnquoDB](https://enquodb.com).
They can provide development, support, and training services for Enquo.
