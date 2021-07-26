---
title: 'Codeception 101: Start to test'
author: Kenneth Schabrechts
type: post
date: 2017-10-21T00:00:00+00:00
url: /development/codeception-101-start-to-test/
categories:
  - Development
tags: ['Development', 'Testing', 'Codeception', 'Tools']
summary: 'Testing our code is so important. But how can you easily manage all those different tests? Introducing Codeception. In this post I will show you how to setup this tool so you can easily test your code.'

---
We all know we should be testing our code. To do just that there are a lot of possibilities. Unit testing being the most popular and well known possibility.

But off course you also have functional and acceptance tests. Each of these are important to have in their own unique way.

There are a lot of different tools out there to do your testing. Ranging from PHPUnit for unit testing to Behat and Mink for acceptance tests.

All of this means you will have to maintain different packages from different developers.

In comes Codeception which can handle all three different types of testing and more. Think for example about API testing.

To handle all these different testing scenarios Codeception uses something they call suites.

## Suite

As mentioned above Codeception does not limit you to just one type of testing. It’s main advantage is that you can choose what types of test you would like to support. Should you decide to add another type of test later on than it is still possible by just adding the suite that you need.

Codeception consists of three default suites: A “unit suite” for all unit tests, a “functional suite” for all functional tests, and an “acceptance suite” for all acceptance tests.

In a later post we’ll go over each type of test. Those posts will explain what they are and how they can benefit you.

## Install and setup

First we need to add Codeception to your project. For this I prefer to use composer:

``` bash
composer require codeception/codeception
```

Next we’re going to setup codeception using the bootstrap command. This bootstrap function will install codeception for acceptance, functional and unit testing.

``` bash
./vendor/bin/codecept bootstrap
```

If you want you can add some more data to bootstrap to setup your suite as desired.

Add `—empty` for a test dir without any suites.

The `—namespace Frontend` creates tests, and uses Frontend namespace for actor classes and helpers.

With `—actor Wizard` you can set the actor as Wizard, so you have a TestWizard actor in each test.

Lastly, with `path/to/project` you can provide a different path to a project, where the tests should be placed.

## Configuration

Now we’re going to update the different configuration files for codeception itself and the different suites.

The first one is the codeception.yml in the root. We can actually leave this one as it is with it’s default setup. It is fine for now.

Feel free to have look at it. In this file you will see all the paths for the tests.

If you provided any extra’s in the bootstrap than they will be configured here as well.

Because we used the regular bootstrap we’ll have our 3 default test suites in our tests folder.

Each test suite has their own configuration file. These are named the same as your suite with the ‘.suite.yml’ extension.

We’ll go deeper into each one of these in our follow up posts. These will contain, per suite, the configuration and an example of a test.

For now we’ll start by looking at our acceptance suite yml file to get a general idea. Default there is an actor configured and you can enable extra modules.

In the example below we enabled the WebDriver module as it will be used by the test to test using a browser.

``` YAML
actor: AcceptanceTester
modules:
    enabled:
        - WebDriver:
            url: <url>
            browser: chrome
            host: <host>
        - \test\Helper\Acceptance
        - Asserts
```

Next up is the functional suite yml file. Here we define the framework the functional tests should use.

In my case this would be the Symfony framework. Besides that we also use the Doctrine2 plugin and the Functional helper class.

``` YAML
actor: FunctionalTester
modules:
    enabled:
        - Symfony:
            app_path: 'app'
            var_path: 'var'
            environment: 'test'
        - Doctrine2:
            depends: Symfony
            cleanup: true
        - \test\Helper\Functional
```

The unit suite yml is fine as it is in default. It will use PHPUnit to run those tests correctly.

``` YAML
actor: UnitTester
modules:
    enabled:
        - Asserts
        - \test\Helper\Unit
```

## Profiles

Now as you have noticed we did not talk about environments. But it may be handy to set-up different configurations depending on the environment.

If we take the acceptance test, for example, the url and host can change depending on the environment we’re on.

This is handled by Codeception using the env tag. These environments can be added in the corresponding suite’s configuration file.

If we take the acceptance.suite.yml file for example:

``` YAML
env:
    development:
        modules:
            config:
                WebDriver:
                    url: <server url>
    staging:
        modules:
            config:
                WebDriver:
                    url: <server url>
    test:
        modules:
            config:
                WebDriver:
                    url: <server url>
```

To run a test suite in the correct configuration all you need to do is add the following:

``` bash
—env staging
```

## Build

When you are done with setting up the configuration we just need to run the build command. This will generate the Actor classes that we need according to the suites configuration.

Note that actor classes are now auto generated starting Codeception 2.0.

We do this with the following command:

``` bash
./vendor/bin/codecept build
```

## Next

In our next posts we’ll go over each suite separately and provide an example. So follow this channel to be updated on when the new posts are published.