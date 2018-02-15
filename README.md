# Heroku Buildpack: Python Django

This is a custom fork of the official [Heroku buildpack](https://devcenter.heroku.com/articles/buildpacks) for Python apps, powered by [Pipenv](http://docs.pipenv.org/en/latest/), [pip](https://pip.pypa.io/) and other excellent software.

Recommended web frameworks include **Django** and **Flask**. The recommended webserver is **Gunicorn**. There are no restrictions around what software can be used (as long as it's pip-installable). Web processes must bind to `$PORT`, and only the HTTP protocol is permitted for incoming connections.

Some Python packages with obscure C dependencies are [not compatible](https://devcenter.heroku.com/articles/python-c-deps).

See it in Action
----------------

Deploying a Python application couldn't be easier:

    $ ls
    Pipfile		Procfile	web.py

    $ heroku create --buildpack https://github.com/VillgeLimited/heroku-buildpack-python-django.git

    $ git push heroku master
    …
    -----> Python app detected
    -----> Installing python-3.6.4
    -----> Installing pip
    -----> Installing requirements with latest pipenv…
           ...
           Installing dependencies from Pipfile…
    -----> Discovering process types
           Procfile declares types -> (none)

A `Pipfile` or `requirements.txt` must be present at the root of your application's repository.


Specify a Python Runtime
------------------------

Specific versions of the Python runtime can be specified with a `runtime.txt` file:

    $ cat runtime.txt
    python-2.7.14

Or, with a `Pipfile.lock` (generated from the following `Pipfile`):

    [requires]
    python_version = "2.7"

Or, more specifically:

    [requires]
    python_full_version = "2.7.14"

Runtime options include:

- `python-3.6.4`
- `python-2.7.14`
- `pypy-5.7.1` (unsupported, experimental)
- `pypy3-5.5.1` (unsupported, experimental)


Specify a Django Project
------------------------

Specific Python `requirements.txt` file and `manage.py` files can be specified for a contained Django project within a subfolder by setting the environment variable `DJANGO_PROJ`

    $ export DJANGO_PROJ=myproj

