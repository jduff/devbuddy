# DevBuddy

[![Go Report Card](https://goreportcard.com/badge/github.com/devbuddy/devbuddy)](https://goreportcard.com/report/github.com/devbuddy/devbuddy)
[![CircleCI](https://circleci.com/gh/devbuddy/devbuddy.svg?style=svg)](https://circleci.com/gh/devbuddy/devbuddy)
[![GitHub Release](https://img.shields.io/github/release/devbuddy/devbuddy.svg)](https://github.com/devbuddy/devbuddy/releases/latest)
[![GitHub Release Date](https://img.shields.io/github/release-date/devbuddy/devbuddy.svg)](https://github.com/devbuddy/devbuddy/releases/latest)

Contents:
- [Install DevBuddy](#install)
- [Usage](#usage)
- [Tasks](docs/Config.md)
- [Contributing to DevBuddy](docs/CONTRIBUTING.md)

## What is this?

**DevBuddy** (previously known as "Dad") is an open-source implementation of an amazing internal tool developed at
[Shopify](https://engineering.shopify.com) called "**Dev**".

The first goal of this tools is to automate the **setup** tasks required to work on a project.

With **DevBuddy**, pushing a change on a project you never touched look like this:

- `bud clone devbuddy/devbuddy`
- `bud up`
- `git commit`
- `bud test`
- `git push`

## Status and progress

**DevBuddy** is mostly useful for Python and Go projects. More languages will be natively
supported. Additional automatic tasks will also be implemented, making **DevBuddy** also
useful for languages without native support.

See the project config [documentation](docs/Config.md).

### Tasks:

Python:
- Python (version + virtualenv): **working**
- Pip (requirements file): **simple**
- Pipenv (support for [Pipfile](https://github.com/pypa/pipfile)): **simple**

Go:
- Go (version): **working**
- Dep (support for [Go Dep](https://github.com/golang/dep)): **simple**

Others
- Custom (conditional shell command): **working**
- Packages (Homebrew, Apt...): **planned**
- Docker Compose (manage a docker-compose setup): **planned**

### Automatic environment:

- Virtualenv: **working**
- Go: **working**

### Features:

- Notification when important files (eg: `requirements.txt`) are updated locally
  (eg: by `git pull`)
- A `help` command to guide a new developer based on `dev.yml`
- A `upgrade` command to auto-upgrade **DevBuddy**

### Hosting platform:

- Github: **working**
- Any git remote-url: **planned**
- Gitlab: **planned**
- Bitbucket (with Git): **planned**

### Shell integration

- Bash: **working**
- Zsh: **working**
- Fish: **planned**

## Install

```bash
$ bash -c "$(curl -sL https://raw.githubusercontent.com/devbuddy/devbuddy/master/install.sh)"
```

Uninstall it:
```bash
$ sudo rm /usr/local/bin/bud
```

## Setup

★ Install the shell integration (in `~/.bash_profile`):
```bash
eval "$(bud --shell-init --with-completion)"
```

A safer version:
```bash
type bud > /dev/null 2> /dev/null && eval "$(bud --shell-init --with-completion)"
```

## Usage

★ Add a `dev.yml` file in your project:
```yaml
up:
  - go: 1.9.2
  - golang_dep
  - python: 3.6.4rc1
  - pip:
    - requirements.txt

commands:
  test:
    desc: Run the tests
    run: script/test
  lint:
    desc: Lint the project
    run: script/lint

open:
  staging: https://staging.myapp.com
  doc: https://godoc.org/github.com/org/myapp
```
See DevBuddy own [dev.yml](dev.yml)

```bash
$ bud
Usage:
  bud [flags]
  bud [command]

Available Commands:
  cd          Jump to a local project
  clone       Clone a project from github.com
  create      Create a new project
  help        Help about any command
  inspect     Inspect the project and its tasks
  open        Open a link about your project
  up          Ensure the project is up and running
  upgrade     [experimental] Upgrade DevBuddy to the latest available release.

Flags:
  -h, --help              help for bud
      --shell-init        Shell initialization
      --version           version for bud
      --with-completion   Enable completion during initialization

Use "bud [command] --help" for more information about a command.
```

## License

[MIT](https://github.com/devbuddy/devbuddy/blob/master/LICENSE)

Authors:
- Pior Bastida (pior@pbastida.net)
- Mathieu Leduc-Hamel (mathieu.leduchamel@shopify.com)
- Emmanuel Milou <manumilou@mykolab.com>
