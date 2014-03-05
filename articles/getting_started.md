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

This guide covers Validateur 2.0.x, including pre-release versions.


## Validateur Overview

Validateur is a validation library inspired by Ruby's ActiveModel. Validateur is functional: validators are
functions, validation sets are higher-order functions, validation results are returned as values.

Around this small core, Validateur can be extended with any custom validator you may need: it is as easy as
defining a Clojure function that conforms to a straightforward contract.


## Supported Clojure versions

Validateur requires Clojure 1.4+ or ClojureScript 0.0-2138+.


## Adding Validateur Dependency To Your Project

Validateur artifacts are [released to Clojars](https://clojars.org/com.novemberain/validateur).

### With Leiningen

    [com.novemberain/validateur "2.0.0-beta3"]

### With Maven

Add Clojars repository definition to your `pom.xml`:

``` xml
<repository>
  <id>clojars.org</id>
  <url>http://clojars.org/repo</url>
</repository>
```

And then the dependency:

``` xml
<dependency>
  <groupId>com.novemberain</groupId>
  <artifactId>validateur</artifactId>
  <version>2.0.0-beta3</version>
</dependency>
```

It is recommended to stay up-to-date with new versions. New releases and important changes are announced [@ClojureWerkz](http://twitter.com/ClojureWerkz).

## Usage

With Validateur you define validation sets that compose one or more validators:

``` clojure
(ns my.app
  (:require [validateur.validation :refer :all]))
 
(validation-set
  (presence-of :email)
  (presence-of [:address :street])
  (presence-of [:card :cvc]))
```

Any function that returns either a pair of `[true #{}]` to indicate successful validation or `[false set-of-validation-error-messages]` to indicate validation failure and return error messages can be used as a validator. Validation sets are then passed to `validateur.validation/valid?` together with a map to validate:

``` clojure
(ns my.app
  (:require [validateur.validation :refer :all]))
 
(let [v (validation-set
         (presence-of :name)
         (presence-of :age))]
  (println (valid? v {:name "Joe" :age 28}))
  (println (invalid? v {:name "Joe" :age 28}))
  (println (valid? v {:name "Joe"})))
```

`validateur.validation/invalid?` is a complement to `validateur.validation/valid?`.

To retrive a map of keys to error messages simply call the validator with a map:

``` clojure
(ns my.app
  (:require [validateur.validation :refer [validation-set presence-of format-of]]))
 
(let [v (validation-set
         (presence-of :user-name)
         (format-of :user-name
                    :format #"^[^\s]*$"
                    :message "may not contain whitespace"))]
  (v {:user-name "99 bananas"}))
;= {:user-name #{"may not contain whitespace"}}
```

## Tell Us What You Think!

Please take a moment to tell us what you think about this guide [on Twitter](http://twitter.com/clojurewerkz).

Let us know what was unclear or what has not been covered. Maybe you do not like the guide style or grammar or discover spelling mistakes. Reader feedback is key to making the
documentation better.
