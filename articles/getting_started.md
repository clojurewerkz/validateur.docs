---
title: "Getting Started with Validateur, a Clojure validations library"
layout: article
---

## About this guide

This guide combines an overview of Validateur with a quick tutorial that helps you to get started with it.
It should take just a few minutes to read and study the provided code examples. This guide covers:

 * Features of Validateur
 * Clojure version requirement
 * How to add Validateur dependency to your project
 * A brief introduction to Validateur capabilities
 * An overview of built-in validators

This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/3.0/">Creative Commons Attribution 3.0 Unported License</a> (including images & stylesheets). The source is available [on Github](https://github.com/clojurewerkz/validateur.docs).


## What version of Validateur does this guide cover?

This guide covers Validateur 1.2.x.



## Validateur Overview

Validateur is a validation library inspired by Ruby's ActiveModel. Validateur is functional: validators are
functions, validation sets are higher-order functions, validation results are returned as values.

Around this small core, Validateur can be extended with any custom validator you may need: it is as easy as
defining a Clojure function that conforms to a straightforward contract.


## Supported Clojure versions

Validateur requires Clojure 1.4+.


## Adding Validateur Dependency To Your Project

Validateur artifacts are [released to Clojars](https://clojars.org/com.novemberain/validateur).

### With Leiningen

    [com.novemberain/validateur "1.6.0"]

### With Maven

Add Clojars repository definition to your `pom.xml`:

{% gist 65642c4b53d26539e5f6 %}

And then the dependency:

    <dependency>
      <groupId>com.novemberain</groupId>
      <artifactId>validateur</artifactId>
      <version>1.6.0</version>
    </dependency>

It is recommended to stay up-to-date with new versions. New releases and important changes are announced [@ClojureWerkz](http://twitter.com/ClojureWerkz).



## Usage

With Validateur you define validation sets that compose one or more validators:

{% gist 4d1178a2e4b0065c0a08 %}

Any function that returns either a pair of `[true #{}]` to indicate successful validation or `[false set-of-validation-error-messages]`

to indicate validation failure and return error messages can be used as a validator. Validation sets are then passed to
`validateur.validation/valid?` together with a map to validate:

{% gist 7c62a3e0ca96653b3a8a %}

`validateur.validation/invalid?` is a complement to `validateur.validation/valid?`.


## Tell Us What You Think!

Please take a moment to tell us what you think about this guide [on Twitter](http://twitter.com/clojurewerkz).

Let us know what was unclear or what has not been covered. Maybe you do not like the guide style or grammar or discover spelling mistakes. Reader feedback is key to making the
documentation better.
