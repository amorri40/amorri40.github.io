---
title: Rules for Clean Javascript
layout: post
author: amorri40
permalink: /rules-for-clean-javascript/
tags:
- javascript
source-id: 1jhOm9TRRI9Jqe7mks7rForGAPQFKjijEUt_BJx0E_xo
published: true
---
Rules for Clean Javascript 2017

## Create MORE functions (rather than large functions)

* Helps with DRY

* Easier to refactor

## Use Lodash rather than custom looping code (when you can)

* Optimised for most common cases (much more optimised than underscore)

* Peer-reviewed for bugs and performance

* Creates more shareable code as long as both projects are using lodash

## Use a consistent code format throughout the whole project

* Make it auto-format on save

* Can use Standard or SemiStandard

* Auto convert tabs to spaces (IDE plugin or automated task)

* Auto remove any excess spaces at end of line (IDE plugin or automated task)

* Benefit: Removes noise from Pull-Request reviews

