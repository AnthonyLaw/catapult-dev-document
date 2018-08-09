# Catapult (nem2) API document

Source code are deploy on this https://catapult-api.netlify.com/

This repository is for all related API information.

Document theme is powerd by [Slate](https://github.com/lord/slate).

### Running in html format

you are able run in `Build/index.html` without install any package.

### Prerequisites

You're going to need:

- **Linux or OS X** — Windows may work, but is unsupported.
- **Ruby, version 2.3.1 or newer**
- **Bundler** — If Ruby is already installed, but the `bundle` command doesn't work, just run `gem install bundler` in a terminal.

### Getting Set Up

1.  Clone or download the project.
2.  `cd catapult-dev-document`
3.  Initialize and start. You can either do this locally, or with Vagrant:

```shell
# either run this to run locally
bundle install
bundle exec middleman server

# OR run this to run with vagrant
vagrant up
```

You can now see the docs at http://localhost:4567.
