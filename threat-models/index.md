---
layout: page
title: Enquo Project Threat Modelling
---
# Enquo Project Threat Models and Security Properties

Threat modelling is where we try to think about how an attacker might try to do something to a system.
By clearly describing the threats that we have accounted for, everyone -- project team members and users -- knows what we (try to) protect against, and what we don't.
That helps Enquo development, by making sure we consider the threats in our development.
It also helps our users, because it means they can see what we *don't* protect against, and make other arrangements for those threats.

On this page, we define the threat models and attacker capabilities that Enquo is intended to protect against, and a brief description of how.
You may also wish to read our [more detailed explanation of how Enquo works]({{ site.url }}/how-it-works).


<a name="snapshot-security"></a>

## Our Primary Threat Model: Snapshot Security

The primary category of attacker that Enquo is intended to defeat is someone who can read the entire Enquo-protected database.
That means they can get the schema itself, as well as the contents of the rows and columns.
Essentially, if it could show up in an SQL dump, or be read off disk, then it's in-scope.

This data could be obtained in any number of ways, such as:

* SQL injection through an application vulnerability;

* Finding the database server exposed on an attacker-accessible network, with weak or non-existent credentials;

* Getting access to the storage volume (such as disks from a server, or an EBS volume);

* Finding a database backup somewhere.

In addition, we assume that an attacker is also able to be a *user* of the application(s) that use the database, and cause data to be modified in the database through the application, and see the results of those modifications in the database.


### Default Security Properties

In the face of this scenario, Enquo in a default configuration is designed to be able to make the following guarantees.

First off, an attacker should not be able to infer anything from the data other than the structure of the data and the presence or absence of data.

For an SQL database, for example, "structure of the data" means the names of the tables and columns, and the type of data stored in each column.
By "presence or absence", we mean that the attacker can see whether a value is NULL or not, and also determine how many rows there are in each table.

Beyond that, however, an attacker should not be able to infer anything from the data.
Even if the attacker is able to cause the application to encrypt data the attacker provides, the resulting ciphertexts don't give the attacker any information they can use to attack other data in the database.
In "the biz", this is referred as "[indistinguishability under chosen-plaintext attack](https://en.wikipedia.org/wiki/Ciphertext_indistinguishability#Indistinguishability_under_chosen-plaintext_attack_(IND-CPA))", or IND-CPA.


### Lower-Bound Security Properties

Some features that are very useful to provide require us to accept less security in exchange for more features.
Enabling these additional features requires developers to explicitly enable them, with option names that make it clear that it results in degraded security.
However, under no circumstances will we provide features that don't provide at least the following guarantees in our Snapshot Security threat model, regardless of how big and scary we make the option names.

An attacker who finds a minimum-security Enquo database will not be able to directly determine the plaintext value of any Enquo-protected data item.
They may, however, be able to infer, with [varying degrees of accuracy](https://eprint.iacr.org/2019/011.pdf), the values of individual data items.

Yes, this is absolutely a big deal, which is why we don't permit this sort of thing in our default settings.
However, doing complicated statistical work to infer values is still a heck of a lot harder than just reading plaintext data out of your database, which is what you've got at the moment.


## Secondary Threat Model: The Ghost in the Machine

A lesser threat model that we think about is one where an attacker is able to gain complete visibility over the operation of the database server itself.
This includes being able to see all queries coming in, and the results of those queries going out, as well as perform arbitrary modifications to the stored data, and repeating execution of prior queries.
They can also examine the system configuration, logs, and even the memory of the running database server processes, which would allow the attacker to (for example) obtain any cryptographic material relied upon by the database server.

This sort of situation can arise when an attacker manages to get arbitrary code execution on the machine that runs the database.
Say, they steal an administrator's SSH key, or find a fairly spectacular flaw in the database server that grants them RCE (Remote Code Execution).

In this situation, we still guarantee that an attacker won't be able to directly determine the plaintext value of any Enquo-protected data item.
No keys or other sensitive materials are ever held by an Enquo database server, so an attacker with total control over the server can't decrypt anything.

What complete visibility and control over the stored data and queries being run *can* allow, however, is various types of inference attacks.
This is, unfortunately, a fundamental limitation of queryable encryption -- if an attacker can run arbitrary queries over a dataset they fully control, sooner or later they can figure out the values of all the data.
It's like being able to play "20 questions", but with no actual limit on the number of questions.
The set of possible answers is small enough to be enumerated in a reasonable time, so I can just keep asking questions and eventually get the answer.

The good news is that is that it is much harder for an attacker to get -- and more importantly *maintain* -- full control over a database server than it is to read the data stored in the database.
Inference attacks take time, and a certain amount of skill.
Again, the bar is much higher than what you get when the data is just lying around unencrypted.


## Game Over Threat Model: Attacker-Controlled Application

For the avoidance of doubt, it's worth highlighting the threat model that Enquo can do practically nothing about.
That's the complete compromise of an application that is using the Enquo-protected database.

Intuitively, this makes sense -- if someone has control over the thing that's reading and writing the data, then they can just *do whatever the application does* to get the data in its plaintext (unencrypted) form.
Enquo cannot, unfortunately, fix application security problems.

Enquo *can* provide a certain amount of protection for the keys that are used to encrypt and decrypt the data, though, which raises the bar for an attacker.
This involves using an HSM (Hardware Security Module) or cloud-based key management service, to allow a key to be used, but not read.
It prevents an attacker from being able to grab the "root" key and a copy of the entire database, and decrypting everything at their leisure.
Since HSMs and cloud KMS aren't universal, however, many applications will use a locally-controlled root key, in which case, if an attacker gets a hold of the data and the root key, your data is on the dark web.
The moral of the story is: use an HSM or cloud KMS.
