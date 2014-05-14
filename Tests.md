# Introduction

We want to improve the code quality of Mirakel.

## Unit Tests

* Models
* Helpers
* Sync

## Functional Tests

* Interactive stuff
* Sync

## How to achive 30% test coverage (Milestone 1)

* The progress must be visible
* Measuring code quality
* Measuring test coverage
* Every new function must have a test for it (Otherwise no +2)
* Every new feature must have a functional test for it (Otherwise no +2)
* Every non-hotfix must have tests for the fixed 
  * A **hotfix** is: 
    * Many users are affected
    * It's a critical crash
    * Absolute sync failures
* Every commit must improve the code quality
* No dirty hacks if there is an alternative

# Unit Tests

1. Models
2. Sync
3. Helpers
4. Loose functions

## Models

### Tests for getter/setters in ..Base

We should write a script which generates the test code. Basically we want to test the following:

```
let a
F.setA(a)
F.getA() == a
```

### Tests for non-getters/setters in ..Base

### Database transactions

For every test class we need a clean demo database!

If possible we should write scripts for that

#### Insert

* count +1
* All old datasets exists
* a → insert → get → == a (except id)

#### Update

* count ==
* all ids exist
* a → update → get → == a (repeat this x times)
* no changes where there shouldn't be

#### Update many

* as Update
* No wrong changes

#### Delete

* Only deleted what should be deleted
* Delete m:n stuff

#### Getter

Here we should be very careful!

* Test vis a vis with hand written select
* Test different variations
* Test all possible parameter variations

#### CursorTo..

Here we should be very careful!

In doubt: rewrite constructors

Test table names in request <=> ALL_FIELDS array <=> Constructor param

#### toJSON

Handwritten item => handwritten JSON == generated JSON => check correctness

Do not forget to test all possible params


## Sync

Input String → parse → toJSON == Input

Input string → parse == handwritten JSON

Using the tests of taskwarrior

We should test every feature independently + random combinations + all data + syntax errors + UDA

## Helpers
## Loose functions
