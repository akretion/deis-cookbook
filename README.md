# Deis Cookbook
The [deis/deis-cookbook](https://github.com/deis/deis-cookbook) project
contains Chef recipes for provisioning Deis nodes.
To get started with your own private PaaS, check out the
[Deis](https://github.com/deis/deis) project.

[![Build Status](https://travis-ci.org/deis/deis-cookbook.png)](https://travis-ci.org/deis/deis-cookbook)

## Requirements

The Deis cookbook is designed to work with **Ubuntu 12.04 LTS**.  While other Ubuntu or Debian distros may work, they have not been tested.

#### Cookbooks

Deis depends on the following cookbooks:

- `apt` - for managing Ubuntu PPAs
- `sudo` - for managing /etc/sudoers.d
- `rsyslog` - for configuring log routing and aggregation

[Berkshelf](http://berkshelf.com) is used for managing cookbook dependencies.

    bundle install                # to install required gems, including berkshelf
    bundle exec berks install     # to install cookbooks to the berkshelf directory
    bundle exec berks upload      # to upload cookbooks to your chef server

# Attributes
TODO: List Deis cookbook attributes.

# Usage

#### deis::controller
The controller recipe will create a complete Deis controller on a single node including:

 * PostgreSQL database
 * Django API Server
 * RabbitMQ installation
 * Celery worker service
 * Nginx site for API
 * Docker daemon
 * Docker-based build system
 * Nginx site for hosting build "slugs"
 * Rsyslog server

The controller will iterate over the `deis-build` databag and configure gitosis access controls in order to restrict `git push` access to repositories.

#### deis::runtime
The runtime recipe will prepare a node for hosting Docker containers as part of a Deis runtime layer.  This recipe will configure:

 * Docker daemon
 * Buildstep Docker image
 * Rsyslog client

The runtime recipe will iterate over the `deis-formations` databag and configure and start upstart daemons for any Docker containers assigned to this node.

#### deis::proxy
The proxy recipe will prepare a node for routing traffic to containers in a Deis runtime layer.  This recipe will configure:

 * Nginx site
 * Rsyslog client

The proxy recipe will iterate over the `deis-formations` databag and configure Nginx backends for any Docker containers assigned to a given formation.

### Notes

The destination for rsyslog clients is determined by a Chef search for recipe[deis::controller], and using the `ipaddress` attribute.

# Contributing

Contributions are welcome! Please open a pull request after fully testing your changes.

This cookbook tests Ruby style with [rubocop](https://github.com/bbatsov/rubocop), Chef style with [foodcritic](http://acrmp.github.io/foodcritic/),
unit tests with [ChefSpec](https://github.com/sethvargo/chefspec) and a full integration with [test-kitchen](http://kitchen.ci/).

See [CONTRIBUTING](https://github.com/deis/deis-cookbook/blob/master/CONTRIBUTING.md) for more details.

# License

Copyright:: 2013, OpDemand LLC

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at <http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
