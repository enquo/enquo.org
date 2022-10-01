---
layout: page
title: The Enquo Philosophy
---
# The Enquo Philosophy

These are the ideas that underlie all our design and development work.
They are in descending order of priority.


## Security First

The most important part of Enquo is security.
If we can't be relied upon to provide secure tooling, then we can't be relied upon.
Mistakes and bugs happen, of course, and when they do we'll fix them, own them, and work hard to do better in the future.

All features in their default mode will be secure against our [primary threat model](../threat-models#snapshot-security).
When there are options to reduce security in exchange for more features or performance, those options will clearly be "security sensitive".
Any developer writing or reading the code should be able to trivially identify when security is being compromised.

For example, an option that could reduce the security properties should never be called "`enable_blob_frobbing_mode`", because it isn't obvious that weaker security is needed to frob blobs.
Instead, the option would be called something like "`enable_low_security_blob_frobbing`".


## Transparency Means Trust

As far as is possible, all design and development on Enquo will happen in the open.
Only those things that *have* to be done in private (such as handling security bugs, or dealing with Code of Conduct violations) will be kept out of the public eye.


## Developer!  Developer!  Developer!  (Experience)

A tool that nobody uses, because it is too complicated, is useless.
Thus, features won't be shipped unless they're the very best developer experience possible.
Ergonomic issues won't be worked around with warnings and caveats in documentation -- docs are never a substitute for good DX.

Yes, this requires more up-front work, but the benefits are worth it, if it allows one more developer to secure the data they store.
