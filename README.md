# Threequals

![Maintenance Status](https://img.shields.io/badge/maintenance-active-green.svg)

Add Ruby-like `#===` to Visualworks Smalltalk.

Threequals is licensed under the MIT license.  See the copyright tab
in the RB, the 'notice' property of this package, or the License.txt
file on GitHub.

Threequals' primary home is the
[Cincom Public Store Repository](http://www.cincomsmalltalk.com/CincomSmalltalkWiki/Public+Store+Repository).
Check there for the latest version.  It is also on
[GitHub](https://github.com/randycoulman/Threequals).

Threequals was developed in VW 7.9.1, but is compatible with VW 7.7
and later.  If you find any incompatibilities with VW 7.7 or later,
let me know (see below for contact information) or file an issue on
GitHub.

# Introduction

Threequals adds the Ruby-like `#===` method to Visualworks Smalltalk.
The `#===` method, or "case equals" as it is known, is used
in Ruby case statements, and allows for very flexible comparisons
between objects in other situations as well.

In this implementation, two objects are `===` if they are `=`.  In
addition:

* A block is `===` to an object if the block evaluates to `true` when
  passed that object.

* A class is `===` to an object if the object is an instance of the
  class or one of its subclasses.

* An interval is `===` to a number if that number is within the
  endpoints of the interval, including the endpoints.

* If the optional Threequals-Regex package is loaded, a regular
  expression is `===` to a string if the string matches the regex.

Be aware that `===` is asymmetric.  The object that has specialized `===` behavior
must be the receiver of the message.  That is, `(1 to: 5) === 4`
answers true, but `4 === (1 to: 5)` answers false.

This seems like an arbitrary restriction, but consider the following:

```
BlockClosure === [:x | x isBehavior not]

[:x | x isBehavior not] === BlockClosure
```

Should this evaluate to `true` or `false`?

You can add `#===` to your own classes.  Keep in mind the following
guidelines:

1. Send to `super` to maintain the default `#=` comparison.

2. Trap any errors and simply return `false`.

# Understanding the Code

This package is made up entirely of extensions on base and other
classes.  `Object>>===` is the base implementation and simply defaults
to `#=`.  Other implementations always send to `super`, but also do
something extra, being careful not to raise exceptions.

# Contributing

I'm happy to receive bug fixes and improvements to this package.  If
you'd like to contribute, please publish your changes as a "branch"
(non-integer) version in the Public Store Repository and contact me as
outlined below to let me know.  I will merge your changes back into
the "trunk" as soon as I can review them.

# Contact Information

If you have any questions about Threequals and how to use it, feel
free to contact me.

* Web site: http://randycoulman.com
* Blog: Courageous Software (http://randycoulman.com/blog)
* E-mail: randy _at_ randycoulman _dot_ com
* Twitter: @randycoulman
* GitHub: randycoulman
