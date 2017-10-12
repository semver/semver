Semantic Versioning 2.1
=======================

Note for Users of SemVer 2.0.0
------------------------------

Don't be fooled by the new version number; while backward-compatible (of
course), version 2.1 fundamentally changes the way SemVer works. It is
recommended that you read this documentation thoroughly.

In short, 2.1 lets you safely use more versions of your dependancies than 2.0.0
would, without breaking any code. Its implementation is the purest form of
knowing exactly which versions can act as complete substitutes for any other
version. 2.0.0 doesn't quite allow for this, because its hard cap at 3 places of
version precision inherently loses information about forward and backward
compatibility as more and more minor-level changes are added. As you will see,
SemVer 2.1 improves upon this model by explicitly declaring forward- and
backward-compatibility with any other version in an easy-to-understand way.

Don't like it? Don't use it! No deprecation of 2.0.0 standards is planned at
this time, and as mentioned, 2.1 is completely backward-compatible. However,
note that some of your own dependencies may choose to adopt these new versioning
standards.

Summary
-------

Given a hypothetical version 1.2.3:

- If making changes that are both forward- and backward-compatible with the
current version (i.e. a bug fix), add .1 to the far right of the version number.
In this case: 1.2.3.1.
- If making changes that are backward-compatible but not forward-compatible with
the current version (i.e. an addition to the API), increment the version number.
In this case: 1.2.4.
- If making changes that are not backward-compatible with the current version
(i.e. an API removal), increment the shortest part of the version number for
which the changes are not backwards compatible, and drop the rest.
  - In this case, assuming the change is backwards-compatible with version 1
(but not version 1.2): 1.3.
  - Alternately, assuming the change isn't backward-compatible with any prior
version: 2.

So, for example, if you used you used version 1.2 of our hypothetical piece of
software in your code, you know that any version beginning with "1.2" will
function fully as a drop-in replacement. So, in the above examples, 1.2.3,
1.2.3.1 and 1.2.4 will work, but 1.3 and 2 won't. However, the true beauty of
SemVer 2.1 lies in its granularity: because version numbers can be of arbitrary
length, you are able to know exactly which versions are compatible with
(theoretically infinite) precision.

Additional labels for pre-release and build metadata are available as extensions
to the above format.

Introduction
------------

In the world of software management there exists a dreaded place called
"dependency hell." The bigger your system grows and the more packages you
integrate into your software, the more likely you are to find yourself, one
day, in this pit of despair.

In systems with many dependencies, releasing new package versions can quickly
become a nightmare. If the dependency specifications are too tight, you are in
danger of version lock (the inability to upgrade a package without having to
release new versions of every dependent package). If dependencies are
specified too loosely, you will inevitably be bitten by version promiscuity
(assuming compatibility with more future versions than is reasonable).
Dependency hell is where you are when version lock and/or version promiscuity
prevent you from easily and safely moving your project forward.


I call this system "Semantic Versioning." Under this scheme, version numbers
and the way they change convey meaning about the underlying code and what has
been modified from one version to the next.

As a solution to this problem, I propose a simple set of rules and requirements
that dictate how version numbers are assigned and incremented. These rules are
based on but not necessarily limited to pre-existing widespread common practices
in use in both closed and open-source software. For this system to work, you
first need to declare a public API. This may consist of documentation or be
enforced by the code itself. Regardless, it is important that this API be clear
and precise. Once you identify your public API, you communicate changes to it
with specific increments to your version number.

Semantic Versioning Specification (SemVer)
------------------------------------------

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119).

1. Software using Semantic Versioning MUST declare a public API. This API
could be declared in the code itself or exist strictly in documentation.
However it is done, it SHOULD be precise and comprehensive.

1. A normal version number MUST take the form N[...] where N and any following
dot-separated numbers are non-negative integers, and MUST NOT contain leading
zeroes. Each element MUST increase numerically. For instance: 1.9 -> 1.10 ->
1.10.1.

1. Once a versioned package has been released, the contents of that version
MUST NOT be modified. Any modifications MUST be released as a new version.

1. Version zero (0[...]) is for initial development. Anything MAY change at any
time. The public API SHOULD NOT be considered stable.

1. Version 1 defines the public API. The way in which the version number is
incremented after this release is dependent on this public API and how it
changes.

1. The whole normal version number MUST be immediately followed by ".1" if all
changes introduced are both forward- and backward-compatible.

1. The far right intermediate version Z ([...]Z) MUST be incremented if any
backward-compatible but forward-incompatible changes are introduced to the
public API defined in [...]Z. It MAY also include forward-compatible changes.

1. Intermediate version N ([...]N[...]) MUST be incremented if any
backward-incompatible changes are introduced to the public API defined in
[...]N. It MAY also include backward-compatible changes. Parts of the version
number following N SHOULD be removed but MAY be reset to 0 when N is
incremented.

1. A pre-release version MAY be denoted by appending a hyphen and a series of
dot-separated identifiers immediately following the normal version. Identifiers
MUST comprise only ASCII alphanumerics and hyphen [0-9A-Za-z-]. Identifiers MUST
NOT be empty. Numeric identifiers MUST NOT include leading zeroes. Pre-release
versions have a lower precedence than the associated normal version. A
pre-release version indicates that the version is unstable and might not satisfy
the intended compatibility requirements as denoted by its associated normal
version. Examples: 1-alpha, 1-alpha.1, 1-0.3.7, 1-x.7.z.92.

1. Build metadata MAY be denoted by appending a plus sign and a series of
dot-separated identifiers immediately following the normal or pre-release
version. Identifiers MUST comprise only ASCII alphanumerics and hyphen
[0-9A-Za-z-]. Identifiers MUST NOT be empty. Build metadata MUST be ignored when
determining version precedence. Thus two versions that differ only in the build
metadata, have the same precedence. Examples: 1-alpha+001, 1+20130313144700,
1-beta+exp.sha.5114f85.

1. Precedence refers to how versions are compared to each other when ordered.
Precedence MUST be calculated by separating the version into intermediate and
pre-release identifiers in that order (Build metadata does not figure into
precedence). Precedence is determined by the first difference when comparing
each of these identifiers from left to right as follows: intermediate versions
are always compared numerically. Example: 1 < 2 < 2.1 < 2.1.1. When all
intermediate versions are equal, a pre-release version has lower precedence than
a normal version. Example: 1-alpha < 1. Precedence for two pre-release versions
with the same intermediate versions MUST be determined by comparing each dot
separated identifier from left to right until a difference is found as follows:
identifiers consisting of only digits are compared numerically and identifiers
with letters or hyphens are compared lexically in ASCII sort order. Numeric
identifiers always have lower precedence than non-numeric identifiers. A larger
set of pre-release fields has a higher precedence than a smaller set, if all of
the preceding identifiers are equal. Example: 1-alpha < 1-alpha.1 < 1-alpha.beta
< 1-beta < 1-beta.2 < 1-beta.11 <  1-rc.1 < 1

1. Version numbers SHOULD NOT include trailing dot separated zeros. They are
allowed, however, in order to preserve backwards-compatibility with SemVer
2.0.0. They have no effect on precedence.

Backus–Naur Form Grammar for Valid SemVer Versions
--------------------------------------------------

    <valid semver> ::= <version core>
                     | <version core> "-" <pre-release>
                     | <version core> "+" <build>
                     | <version core> "-" <pre-release> "+" <build>

    <version core> ::= <numeric identifier>
                     | <numeric identifier> "." <version core>

    <pre-release> ::= <dot-separated pre-release identifiers>

    <dot-separated pre-release identifiers> ::= <pre-release identifier>
                                              | <pre-release identifier> "." <dot-separated pre-release identifiers>

    <build> ::= <dot-separated build identifiers>

    <dot-separated build identifiers> ::= <build identifier>
                                        | <build identifier> "." <dot-separated build identifiers>

    <pre-release identifier> ::= <alphanumeric identifier>
                               | <numeric identifier>

    <build identifier> ::= <alphanumeric identifier>
                         | <digits>

    <alphanumeric identifier> ::= <non-digit>
                                | <non-digit> <identifier characters>
                                | <identifier characters> <non-digit>
                                | <identifier characters> <non-digit> <identifier characters>

    <numeric identifier> ::= "0"
                           | <positive digit>
                           | <positive digit> <digits>

    <identifier characters> ::= <identifier character>
                              | <identifier character> <identifier characters>

    <identifier character> ::= <digit>
                             | <non-digit>

    <non-digit> ::= <letter>
                  | "-"

    <digits> ::= <digit>
               | <digit> <digits>

    <digit> ::= "0"
              | <positive digit>

    <positive digit> ::= "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9"

    <letter> ::= "A" | "B" | "C" | "D" | "E" | "F" | "G" | "H" | "I" | "J"
               | "K" | "L" | "M" | "N" | "O" | "P" | "Q" | "R" | "S" | "T"
               | "U" | "V" | "W" | "X" | "Y" | "Z" | "a" | "b" | "c" | "d"
               | "e" | "f" | "g" | "h" | "i" | "j" | "k" | "l" | "m" | "n"
               | "o" | "p" | "q" | "r" | "s" | "t" | "u" | "v" | "w" | "x"
               | "y" | "z"


Why Use Semantic Versioning?
----------------------------

This is not a new or revolutionary idea. In fact, you probably do something
close to this already. The problem is that "close" isn't good enough. Without
compliance to some sort of formal specification, version numbers are
essentially useless for dependency management. By giving a name and clear
definition to the above ideas, it becomes easy to communicate your intentions
to the users of your software. Once these intentions are clear, flexible (but
not too flexible) dependency specifications can finally be made.

A simple example will demonstrate how Semantic Versioning can make dependency
hell a thing of the past. Consider a library called Firetruck. It requires a
Semantically Versioned package named Ladder. At the time that Firetruck is
created, Ladder is at version 3.1. Since Firetruck uses some functionality that
was first introduced in 3.1, you can safely specify the Ladder dependency as any
version beginning with "3.1". Now, when Ladder version 3.1.1 becomes available,
you can release it to your package management system and know that it will be
compatible with existing dependent software.

As a responsible developer you will, of course, want to verify that any package
upgrades function as advertised. The real world is a messy place; there's
nothing we can do about that but be vigilant. What you can do is let Semantic
Versioning provide you with a sane way to release and upgrade packages without
having to roll new versions of dependent packages, saving you time and hassle.

If all of this sounds desirable, all you need to do to start using Semantic
Versioning is to declare that you are doing so and then follow the rules. Link
to this website from your README so others know the rules and can benefit from
them.


FAQ
---

### How should I deal with revisions in the 0[...] initial development phase?

The simplest thing to do is start your initial development release at 0.1 and
then increment the version accordingly. Naturally, this means ignoring the
leading 0, because every API change is technically backward-compatible with 0,
which is "no API".

### How do I know when to release version 1?

If your software is being used in production, it should probably already be 1.
If you have a stable API on which users have come to depend, you should be 1. If
you're worrying a lot about backwards compatibility, you should probably already
be 1.

### Doesn't this discourage rapid development and fast iteration?

Version zero is all about rapid development. If you're changing the API every
day you should either still be in version 0[...] or on a separate development
branch working on the next backward-incompatible version.

### If even the tiniest backwards incompatible changes to the public API require a base version bump, won't I end up at version 42 very rapidly?

This is a question of responsible development and foresight. Incompatible
changes should not be introduced lightly to software that has a lot of dependent
code. The cost that must be incurred to upgrade can be significant. Having to
bump versions to release incompatible changes means you'll think through the
impact of your changes, and evaluate the cost/benefit ratio involved.

### Similiarly, if even the tiniest changes require extending the version number, won't I quickly end up at version 1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1.1?

You might, but you don't necessarily have to. However, in a world of insanely
long cryptographic keys and million-line programs, it is not unreasonable to see
the inherent usefulness of infinitely precice versioning. SemVer has never
claimed that its goal is to create "short" version numbers. Rather, it aims to
create useful, consistent version numbers. SemVer 2.1 is just the latest step in
the realization of this goal. However, you are allowed to reduce this precision
if you feel it's worth it: All you need to do is increment the version number at
some arbitrary point, and drop the rest. So, the above version could be
shortened to 2, or 1.2, or 1.1.2, or 1.1.1.2, etc... Just know that as the
version number becomes shorter and shorter, fewer and fewer projects will deem
the new version "safe" to use. Even if the version number is kept at 3 places
(as in SemVer 2.0.0), SemVer 2.1 still commuinicates the same (or in many cases,
more) information about compatibility than earlier numbering schemes did.

### Documenting the entire public API is too much work!

It is your responsibility as a professional developer to properly document
software that is intended for use by others. Managing software complexity is a
hugely important part of keeping a project efficient, and that's hard to do if
nobody knows how to use your software, or what methods are safe to call. In
the long run, Semantic Versioning, and the insistence on a well defined public
API can keep everyone and everything running smoothly.

### What do I do if I accidentally release a backward-incompatible change as a "backward-compatible" version?

As soon as you realize that you've broken the Semantic Versioning spec, fix the
problem and release a new "backward-incompatible" version that corrects the
problem and restores backwards compatibility. Even under this circumstance, it
is unacceptable to modify versioned releases. If it's appropriate, document the
offending version and inform your users of the problem so that they are aware of
the offending version.

### What should I do if I update my own dependencies without changing the public API?

That would be considered compatible since it does not affect the public API.
Software that explicitly depends on the same dependencies as your package should
have their own dependency specifications and the author will notice any
conflicts. Determining whether the change is a forward-compatible modification
depends on whether you updated your dependencies in order to fix a bug or
introduce new functionality. I would usually expect additional code for the
latter instance, in which case it's obviously a forward-incompatible level
increment.

### What if I inadvertently alter the public API in a way that is not compliant with the version number change (i.e. the code incorrectly introduces a breaking change in a forward- and backward-compatible release)?

Use your best judgment. If you have a huge audience that will be drastically
impacted by changing the behavior back to what the public API intended, then it
may be best to perform a "backward-incompatible" version release, even though
the fix could strictly be considered a backward-compatible release. Remember,
Semantic Versioning is all about conveying meaning by how the version number
changes. If these changes are important to your users, use the version number to
inform them.

### How should I handle deprecating functionality?

Deprecating existing functionality is a normal part of software development and
is often required to make forward progress. When you deprecate part of your
public API, you should do two things: (1) update your documentation to let
users know about the change, (2) issue a new backward-compatible release with
the deprecation in place. Before you completely remove the functionality in a
new backward-incompatible release there should be at least one
backward-compatible release that contains the deprecation so that users can
smoothly transition to the new API.

### Does SemVer have a size limit on the version string?

No, but use good judgment. A 255 character version string is probably overkill,
for example. Also, specific systems may impose their own limits on the size of
the string.

### Is "v1.2.3" a semantic version?

No, "v1.2.3" is not a semantic version. However, prefixing a semantic version
with a "v" is a common way (in English) to indicate it is a version number.
Abbreviating "version" as "v" is often seen with version control. Example:
`git tag v1.2.3 -m "Release version 1.2.3"`, in which case "v1.2.3" is a tag
name and the semantic version is "1.2.3".


About
-----

The Semantic Versioning specification is authored by [Tom
Preston-Werner](http://tom.preston-werner.com), inventor of Gravatar and
cofounder of GitHub.

If you'd like to leave feedback, please [open an issue on
GitHub](https://github.com/mojombo/semver/issues).


License
-------

Creative Commons - CC BY 3.0
http://creativecommons.org/licenses/by/3.0/
