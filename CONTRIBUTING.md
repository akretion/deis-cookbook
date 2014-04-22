# Contributing to the Deis cookbook
Contributions are much appreciated! To help ensure reliability, this cookbook includes style checking and unit and integration tests.
Contributions to this cookbook will only be accepted once all tests pass successfully:

    bundle exec rake

## Setting up the test environment

Install the latest version of [Vagrant](http://www.vagrantup.com/downloads.html) and [VirtualBox](https://www.virtualbox.org/wiki/Downloads) (free) or [VMWare Fusion](http://www.vmware.com/products/fusion) (paid).

Clone the latest version of the cookbook from the repository.

    git clone git@github.com:deis/deis-cookbook.git
    cd deis-cookbook

Install the gems used for testing:

    bundle install

## Running style tests
Style testing runs rubocop for Ruby linting and foodcritic for Chef linting. To run the style checks:

    bundle exec rake style

Generally, we follow all recommendations from these tools. However, it is possible to ignore a rule for some code:

    bad 'style' or something... # rubocop:disable SpaceBeforeFirstArg

    more "bad" style # ~FC014

These ignore the rubocop SpaceBeforeFirstArg and Foodcritic's rule #14, respectively.

## Running unit tests
ChefSpec unit tests are located in `spec`. Each recipe has a `recipename_spec.rb` file that contains unit tests for that recipe. Your new functionality or bug fix should have corresponding test coverage - if it's a change, make sure it doesn't introduce a regression (existing tests should pass). If it's a change or introduction of new functionality, add new tests as appropriate.

To run unit tests for the whole cookbook:

    bundle exec rake unit

To run rspec for a specific recipe:

    bundle exec rspec spec/controller_spec.rb

## Running integration tests

Test Kitchen test suites are defined in [.kitchen.yml](.kitchen.yml). Running `kitchen test` will cause Test Kitchen to spin up a test VM and attempt
to provision a Deis controller. After the Chef run completes, integration tests are run using [serverspec](http://serverspec.org/). These live in `test/integration/controller/serverspec` and ensure that services are running and listening on expected ports.
