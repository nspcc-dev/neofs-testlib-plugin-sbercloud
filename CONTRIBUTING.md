# Contribution guide

First, thank you for contributing! We love and encourage pull requests from
everyone. Please follow the guidelines:

- Check the open [issues](https://github.com/nspcc-dev/neofs-testlib-plugin-sbercloud/issues) and
  [pull requests](https://github.com/nspcc-dev/neofs-testlib-plugin-sbercloud/pulls) for existing
  discussions.

- Open an issue first, to discuss a new feature or enhancement.

- Write tests, and make sure the test suite passes locally.

- Open a pull request, and reference the relevant issue(s).

- Make sure your commits are logically separated and have good comments
  explaining the details of your change.

- After receiving feedback, amend your commits or add new ones as appropriate.

- **Have fun!**

## Development Workflow

Start by forking the `neofs-testlib-plugin-sbercloud` repository, make changes in a branch and then
send a pull request. We encourage pull requests to discuss code changes. Here
are the steps in details:

### Set up your GitHub Repository
Fork [Sbercloud plugin upstream](https://github.com/nspcc-dev/neofs-testlib-plugin-sbercloud/fork) source
repository to your own personal repository. Copy the URL of your fork and clone it:

```shell
$ git clone <url of your fork>
```

### Set up git remote as ``upstream``
```shell
$ cd neofs-testlib-plugin-sbercloud
$ git remote add upstream https://github.com/nspcc-dev/neofs-testlib-plugin-sbercloud
$ git fetch upstream
```

### Set up development environment
To setup development environment, please, take the following steps:
1. Prepare virtualenv

```shell
$ virtualenv --python=python3.10 venv
$ source venv/bin/activate
```

2. Install all dependencies:

```shell
$ pip install -r requirements.txt
```

3. Setup pre-commit hooks to run code formatters on staged files before you run a `git commit` command:

```shell
$ pre-commit install
```

### Create your feature branch
Before making code changes, make sure you create a separate branch for these
changes. Maybe you will find it convenient to name branch in
`<type>/<issue>-<changes_topic>` format.

```shell
$ git checkout -b feature/123-something_awesome
```

### Commit changes
After verification, commit your changes. There is a [great
post](https://chris.beams.io/posts/git-commit/) on how to write useful commit
messages. Try following this template:

```
[#Issue] Summary
Description
<Macros>
<Sign-Off>
```

```shell
$ git commit -am '[#123] Add some feature'
```

### Push to the branch
Push your locally committed changes to the remote origin (your fork):
```shell
$ git push origin feature/123-something_awesome
```

### Create a Pull Request
Pull requests can be created via GitHub. Refer to [this
document](https://help.github.com/articles/creating-a-pull-request/) for
detailed steps on how to create a pull request. After a Pull Request gets peer
reviewed and approved, it will be merged.

## DCO Sign off

All authors to the project retain copyright to their work. However, to ensure
that they are only submitting work that they have rights to, we are requiring
everyone to acknowledge this by signing their work.

Any copyright notices in this repository should specify the authors as "the
contributors".

To sign your work, just add a line like this at the end of your commit message:

```
Signed-off-by: Samii Sakisaka <samii@nspcc.ru>
```

This can easily be done with the `--signoff` option to `git commit`.

By doing this you state that you can certify the following (from [The Developer
Certificate of Origin](https://developercertificate.org/)):

```
Developer Certificate of Origin
Version 1.1
Copyright (C) 2004, 2006 The Linux Foundation and its contributors.
1 Letterman Drive
Suite D4700
San Francisco, CA, 94129
Everyone is permitted to copy and distribute verbatim copies of this
license document, but changing it is not allowed.
Developer's Certificate of Origin 1.1
By making a contribution to this project, I certify that:
(a) The contribution was created in whole or in part by me and I
    have the right to submit it under the open source license
    indicated in the file; or
(b) The contribution is based upon previous work that, to the best
    of my knowledge, is covered under an appropriate open source
    license and I have the right under that license to submit that
    work with modifications, whether created in whole or in part
    by me, under the same open source license (unless I am
    permitted to submit under a different license), as indicated
    in the file; or
(c) The contribution was provided directly to me by some other
    person who certified (a), (b) or (c) and I have not modified
    it.
(d) I understand and agree that this project and the contribution
    are public and that a record of the contribution (including all
    personal information I submit with it, including my sign-off) is
    maintained indefinitely and may be redistributed consistent with
    this project or the open source license(s) involved.
```

## Code Style
We use `black` and `isort` for code formatting. Please, refer to [Black code style](https://black.readthedocs.io/en/stable/the_black_code_style/current_style.html) for details.

Type hints are mandatory for:
 - class attributes;
 - function or method's parameters;
 - function or method's return type.

The only exception is return type of test functions or methods - there's no much use in specifying `None` as return type for each test function.

Do not use relative imports. Even if the module is in the same package, use the full package name.

To format docstrings, please, use [Google Style Docstrings](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_google.html). Type annotations should be specified in the code and not in docstrings (please, refer to [this sample](https://sphinxcontrib-napoleon.readthedocs.io/en/latest/index.html#type-annotations)).

## Building and publishing package
To build Python package of the plugin, please run the following command in the plugin root directory:
```shell
$ python -m build
```

This command will put wheel file and source archive under `dist` directory.

To check that package description will be correctly rendered at PyPI, please, use command:
```shell
$ twine check dist/*
```

To upload package to [test PyPI](https://test.pypi.org/project/neofs-testlib-plugin-sbercloud/), please, use command:
```shell
$ twine upload -r testpypi dist/*
```

It will prompt for your username and password. You would need to [create test PyPI account](https://test.pypi.org/account/register/) in order to execute it.

To upload package to actual PyPI, please, use command:
```shell
$ twine upload dist/*
```

It will prompt for your username and password. You would need to [create PyPI account](https://pypi.org/account/register/) in order to execute it.
