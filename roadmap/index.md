---
layout: page
title: Planned Future Enquo Developments
---
As an open source project, Enquo doesn't have a traditional "product roadmap".
The future direction of the project is in the hands of its contributors.
However, this list gives a sense of the things that are intended to be added to Enquo as time and resources permit.
If you would like to sponsor development of any of these (or other) features, to ensure they appear sooner rather than later, please contact [EnquoDB](https://enquodb.com).

# Key Rotation

Being able to *change* a key in use, if it is suspected of compromise, is very important.
Each encrypted value identifies the key which was used to encrypt the data, so what's needed is:

1. the ability to use multiple keys to decrypt data (so that data encrypted with an out-of-date key can still be decrypted);
2. a mechanism in the database server to identify data values which are using the "wrong" key;
3. a loop to fetch all data matching (2), decrypt it via (1), and re-encrypt it with the new key.


# String Matching

While Enquo supports string *equality* queries (eg `WHERE first_name = 'Bob'`), it does not currently support substring matching operations (eg `WHERE first_name LIKE 'B%'`).
This is a common pattern in applications, and is an important feature to support.
We have a plan on how to do this; the limiting factor at the moment is the time to implement it.


# Moah Data Types

You can go a long way with strings and bigints, but databases support many other data types, and we'd like to be able to support as many of them as is practical.
We want to support at least 32 and 16 bit signed integers, 64 bit floats, and timestamps, in addition to the 64 bit integers, strings, and dates already supported.
