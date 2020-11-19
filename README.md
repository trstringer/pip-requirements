# pip_requirements

Wrapper functions to easily divide prod, test, and dev Python package requirements.

## Problem

When working in Python (virtual) environments, we typically `pip install <dependency>` to install a needed dependency. `pip` doesn't distinguish between production dependencies and non-production dependencies. This is a problem because in our production environments we don't want to have unnecessary dependencies for security and operational best practices.

## Why not use a `pip` alternative?

I know that there are other package managers for Python out there that handle this type of scenario, but from my experience I'd much prefer to use `pip` directly and create a few wrapper functions (like these) to work better with my development workflow.

## Install

```
$ git clone https://github.com/trstringer/pip_requirements
```

Source it in your `~/.bashrc`:

```
source ~/clone_dir/pip_requirements/pip_requirements
```

## Usage/Example

```
$ pip-install-dev-requirement wheel jedi
$ pip-install-test-requirement pylint flake8
$ pip-install-prod-requirement requests
```

The output of this should look like:

```
$ tree -L 1
.
├── requirements.dev.txt
├── requirements.test.txt
├── requirements.txt
└── venv

$ cat requirements.dev.txt
wheel==0.35.1
jedi==0.17.2

$ cat requirements.test.txt
pylint==2.6.0
flake8==3.8.4

$ cat requirements.txt
requests==2.25.0
```

Now when you need to install your dependencies, it'll most likely look like this:

**Dev environment**

```
$ pip install -r requirements.dev.txt -r requirements.test.txt -r requirements.txt
```

**Test environment/build server/CI-CD**

```
$ pip install -r requirements.test.txt -r requirements.txt
```

**Production server**

```
$ pip install -r requirements.txt
```

**Note: You must be in the context of a virtual environment.**

> To create a virtual environment:
>    $ python3 -m venv venv
> 
> To activate the virtual environment:
>    $ . venv/bin/activate
