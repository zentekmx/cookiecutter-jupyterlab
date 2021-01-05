
# {{ cookiecutter.book_name }}
========================

{{ cookiecutter.book_short_description }}

SetUp
---------------

Below you will find basic setup instructions for the ``DSBA``. 

To begin you should have the following applications installed on your
local development system:

- git >= 2 <https://git-scm.com/book/en/v2/Getting-Started-Installing-Git>
- python >= 3.6 <http://www.python.org/getit/>
- pip > 10 <http://www.pip-installer.org/>
- docker >= 1.12 <https://docs.docker.com/get-started/>
- node >= 12 <https://nodejs.org/en/download/>
- make >= 4 <https://www.gnu.org/software/make/>

##### Project dependencies

The project depends of the following external products:

| Name | Description | Installation type | Notes |
| ---- | ---- | ---- | --- |
| Postgres | DBMS | docker | No installation needed since the administration tool will do the job |

- Postgres <http://postgresguide.com/setup/install.html>

Getting Started
---------------

#### Enter Environment

To enter the environment quickly, first install Python. It comes with virtualenv built-in.
So create a virtual env by:

```
# Option 1: Create virtualenv by python3 venv
python -m venv {{ cookiecutter.book_slug }}
source {{ cookiecutter.book_slug }}/bin/activate

# Option 2: Create virtualenv by mkvirtualenv
mkvirtualenv {{ cookiecutter.book_slug }}
workon {{ cookiecutter.book_slug }}

# Option 3: Create virtualenv by conda
conda create -n {{ cookiecutter.book_slug }} anaconda
conda activate {{ cookiecutter.book_slug }}
```

Then install all dependencies:

```
make install
```

```
# Optionally install jupyterlab extensions
make jupyterlab-extensions
```

Starting jupyterlab IDE

```
make jupyterlab
```

Building jupyterbook. A fully-rendered HTML version of the book will be built in `notebooks/_build/html/`.

```
make jupyterbook
```

Extras
---------------

Check project requirements

```
make check
```

Cleansing temporary / built files and migrations

```
make clean
```

Accessing dbms shell console

```
make dbshell
```

Obtaining DDL schema (without data)

```
make schema

```

Hosting the book
---------------

The html version of the book is hosted on the `gh-pages` branch of this repo. A GitHub actions workflow has been created that automatically builds and pushes the book to this branch on a push or pull request to main.

If you wish to disable this automation, you may remove the GitHub actions workflow and build the book manually by:

- `make ghp-publish`

This will automatically push your build to the `gh-pages` branch. More information on this hosting process can be found [here](https://jupyterbook.org/publish/gh-pages.html#manually-host-your-book-with-github-pages).

Contributors
---------------

We welcome and recognize all contributions. You can see a list of current contributors in the [contributors tab](https://github.com/{{ cookiecutter.github_username }}/{{ cookiecutter.book_slug }}/graphs/contributors).

Credits
---------------

This project is created using excellent open source projects [Jupyter Lab](https://jupyter.org/), [Jupyter Book project](https://jupyterbook.org/) and the [zentekmx/cookiecutter-jupyterlab template](https://github.com/zentekmx/cookiecutter-jupyterlab).

Reference
---------------

Take a look at the docs for more information.

* https://www.python.org/
* https://jupyter.org/
* https://jupyterbook.org/
