# Dealerdirect: PHP CI Docker Container

These are simple Docker containers containing all tools for testing PHP codebases.

We use this container in conjunction with BitBucket Pipelines to ensure code quality.

## Contents

[![Docker Stars](https://img.shields.io/docker/stars/dealerdirect/ci-php.svg)][dockerhub]
[![Docker Pulls](https://img.shields.io/docker/pulls/dealerdirect/ci-php.svg)][dockerhub]
[![Docker Automation](https://img.shields.io/docker/automated/dealerdirect/ci-php.svg)][dockerhub]

This container is based the latest [official PHP Docker images].

Preinstalled in these containers:
* **[PHP]**: Hypertext Preprocessor
* **[Composer]**: Composer is a tool for dependency management in PHP
* **[Dealerdirect PHP QA Tools]**: All PHP quality assurance tools we use at Dealerdirect
* **[JSONLint]**: For checking JSON files within the project
* **[XMLLint]**: For checking XML syntax
* **[YamlLint]**: Linting / style checking YAML files
* **[Flake8]**: For Python PEP8 style guide enforcement
* **[RuboCop]**: For Ruby files style guide enforcement

[dockerhub]: https://hub.docker.com/r/dealerdirect/ci-php/
[official PHP Docker images]: https://github.com/docker-library/php
[PHP]: http://www.php.net
[Composer]: https://getcomposer.org
[Dealerdirect PHP QA Tools]: https://github.com/DealerDirect/php-qa-tools
[JSONLint]: https://github.com/zaach/jsonlint
[XMLLint]: http://xmlsoft.org/xmllint.html
[YamlLint]: https://github.com/adrienverge/yamllint
[Flake8]: http://flake8.pycqa.org/en/latest
[RuboCop]: https://github.com/bbatsov/rubocop

## BitBucket Pipelines Example

This is an example `bitbucket-pipelines.yml`. Place this file in the root of your project.

```yaml
---
image: dealerdirect/ci-php:7.1
pipelines:
  default:
    - step:
        script:
          - find . -type f -name "*.json" -print0 | xargs -0 -n1 jsonlint -c -q
          - find . -type f -name "*.yml" -print0 | xargs -0 -n1 yamllint
          - phpcs --standard=PSR2 .
```

In order to tweak the rulesets of the checks, please check the documentation of each tool.

Most of these tools have support for placing a configuration file in the root of your project. (e.g. a `.yamllint` file).

## Contributing

This is an active open-source project. We are always open to people who want to use the code or contribute to it.

We've set up a separate document for our [contribution guidelines].

Thank you for being involved! :heart_eyes:

[contribution guidelines]: https://github.com/dealerdirect/docker-ci-php/blob/master/CONTRIBUTING.md

## Authors & Contributors

The original idea and setup of this repository is by [Franck Nijhof], employee @ Dealerdirect.

For a full list off all author and/or contributors, please check [this page].

[this page]: https://github.com/dealerdirect/docker-ci-php/graphs/contributors
[Franck Nijhof]: https://github.com/frenck

## Would you like to work @ Dealerdirect?

Dealerdirect is always on the looking for energetic and hard working developers and devops engineers.

Interested in working at Dealerdirect? Then please be sure to check out [our vacancies].

Did not find a matching vacancy? Just [get in touch]!

[WorkingAtDealerdirect.eu]

[our vacancies]: http://workingatdealerdirect.eu/?post_type=vacancy&s=&department=99
[get in touch]: http://workingatdealerdirect.eu/open-sollicitatie/
[WorkingAtDealerdirect.eu]: http://www.workingatdealerdirect.eu

## License

The MIT License (MIT)

Copyright (c) 2016 Dealerdirect B.V.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
