---
layout: page
title: About the Enquo Project
---
# About the Enquo Project

The mission of the Enquo Project is to provide developers with tools to encrypt the data they store, while allowing them to continue to query and aggregate that data using their existing tools and processes.

Barely a week goes by that there isn't a news story about a massive data breach that has exposed the personal information of thousands or millions of people.
There are many more losses of personal information that don't even make the news, yet for the people involved the leak can be devastating.

Yet the organisations that collect and store this data have not, on the whole, solved the problems that allow these breaches to happen.
They put up firewalls, they audit their code, they have long and tedious change control processes, and yet still the data leaks.
We know that strong cryptography could go a long way to preventing, or at least mitigating the harm of, data breaches.
Why do organisations not just encrypt all this data, then?

When encrypted, data cannot be queried or otherwise manipulated by the database server.
That is an absolute non-starter for practically every use of the data, because almost all applications are built around querying, sorting, aggregating, and presenting data.
The result of this is that one of the most powerful tools available for protecting personal data -- strong encryption -- is totally unviable.

**Until now.**

The Enquo Project exists to solve this problem.
By giving every software developer the ability to encrypt stored data, and yet still query it when required, we intend to take the sting out of data breaches.
The tools that we build are secure, easy-to-use, *and* have acceptable real-world performance.

## Further Reading

* The [Enquo Project's philosophy](philosophy) may come in handy.

* Our [threat modelling](../threat-models) will be of interest to anyone who is developing for, or with, Enquo tools.

* If you have a hankering for cryptographic minutiae, the [How Enquo Works](../how-it-works) page will satisfy your cravings.
