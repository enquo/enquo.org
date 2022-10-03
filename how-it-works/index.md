---
layout: page
title: Enquo: How Does It Work?
---
*This page is a work-in-progress.*

Enquo consists of two parts: a client-side cryptography library, that encrypts and decrypts values, and a server-side extension that knows how to compare Enquo-encrypted ciphertexts, without being able to read the values they represent.
It's easiest to consider these in isolation.

Since Enquo uses Order-Revealing Encryption ("ORE") for practically all of its magic, it's worth starting off with a brief primer on ORE to get your juices flowing.
After that, we'll go through the Enquo client and server-side extensions.


# Order-Revealing Encryption

The general goal of ORE is to produce ciphertexts that reveal no information about the underlying values, *other than* their relative ordering.
Several schemes have been proposed in the ten years or so that research in this area has been very hot.
However, they all "leak" a certain amount of additional information, in various circumstances.

The "best" (for our purposes) ORE scheme that has been released so far comes from the [Stanford Applied Cryptography Group](https://crypto.stanford.edu/)'s [ORE team](https://crypto.stanford.edu/ore/), specifically described in the paper ["Order-Revealing Encryption: New Constructions, Applications, and Lower Bounds"](https://eprint.iacr.org/2016/612.pdf), by Kevin Lewi and David J. Wu.
This scheme produces ciphertexts that come in two parts: a "left" ciphertext, which is identical for all ciphertexts derived from the same value and keys, and a "right" ciphertext, which is [IND-CPA](https://en.wikipedia.org/wiki/Ciphertext_indistinguishability#Indistinguishability_under_chosen-plaintext_attack_(IND-CPA)) secure (that is, the "right" ciphertext by itself leaks no information at all).

Comparison between two ciphertexts uses the "left" ciphertext from one and the "right" ciphertext from the other.
This means that in many circumstances you can store only the "right" ciphertext in your database, which keeps the data completely secure, and send "left" ciphertexts when you need to query the database.
In circumstances where you *do* need to store both "left" and "right" ciphertexts, the "left" ciphertext only reveals the fact that two values are equal to each other[^1].

The Lewi-Wu scheme is not 100% perfect, within the definition of an ideal ORE scheme.
The ciphertexts are split up into a series of "blocks" of ideal ORE ciphertexts, and the comparison allows the database to know not just the relative ordering of two values, but also which "block" the difference occurs.
This trade-off is used to reduce the size of ciphertexts, and is only a problem when "left" ciphertexts are stored.


## Compare the Pair

One interesting property of the Lewi-Wu ORE scheme is that it is not *just* an order-revealing scheme -- it can be used for arbitrary comparisons.
In some cases, the relative ordering of values isn't important, but simply whether or not two values are equal or not.
While "blind indexing" is commonly used for this purpose, it suffers from the "all ciphertexts for the same value are the same" problem, which is... not great.
Instead, if we change the comparison function used in ORE from "less-than / equal / greater-than" to "equal / not-equal", and only store the right ciphertexts, then we've got a far more secure database.
When we want to find elements that are equal, we send a query with the left ciphertext of the value we're interested in, compare that against the stored right ciphertexts, and we're in business.


# The Enquo Client

With a (very basic) grounding in ORE under our belt, we can now start to talk about Enquo itself.
The vast majority of the logic is in the client, so we'll deal with that first.

Most of the Enquo codebase is written in Rust, a high-performance, memory-safe language which is fast becoming the "go-to" language of choice for safe cryptography.
By using Rust, we can produce a library that is very fast, much more secure than something written in C/C++, and broadly portable.
Bindings to most other languages can be thin "shims" around this Rust library, ensuring interoperability and a minimum of security headaches.

The functionality of the Enquo client can be broken down into three major parts: cryptographic primitives, encrypted data types, and key management.


# Enquo in the Server

There's not a huge amount of work that a database server that works with Enquo-encrypted data needs to do.
Mostly it needs to be able to recognise that it's working with Enquo-encrypted data, and use the appropriate comparison algorithms for encrypted values.
All of the comparison algorithms, which work on encrypted data, are found in the same "core" library that the clients use.

-----


[^1]: This isn't great, because there are statistical attacks that can be used to try and discern values from their frequencies and likely distributions.
    But it's still a heck of a lot more work for an attacker to do that than it is to take a database full of plaintext data and sell it on the dark web.
