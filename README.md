# The Convenient Cookiecutter JupyterLab Notebook

![tests](https://github.com/zentekmx/cookiecutter-jupyterlab/workflows/tests/badge.svg)
![deploy](https://github.com/zentekmx/cookiecutter-jupyterlab/workflows/deploy/badge.svg)
[![release](https://img.shields.io/github/release/zentekmx/cookiecutter-jupyterlab.svg)](https://github.com/zentekmx/cookiecutter-jupyterlab/releases)
[![python](https://img.shields.io/badge/python-3.7%2C%203.8-blue)]()
[![os](https://img.shields.io/badge/OS-Archlinux%2C%20Centos%2C%20Ubuntu%2C%20Mac%2C%20Windows-yellow)]()

<p align="center">
  <img src="{{cookiecutter.book_slug}}/{{cookiecutter.book_slug}}/logo.png" width="400">
</p>

A cookiecutter template for creating a convenient [Jupyter Lab](https://jupyter.org/) a web-based interactive development environment for Jupyter notebooks **plus** [Jupyter Book](https://jupyterbook.org/intro.html) for building beautiful, publication-quality books and documents **plus** [Makefile](https://www.gnu.org/software/make/manual/make.html) for using make build automation tool. See the rendered version of this cookiecutter template [here](https://zentekmx.github.io/cookiecutter-jupyterlab/).

## Template

An example template created by this cookiecutter is shown below:

```
my_book
├── .github
│   └── workflows
│       └── deploy.yml
├── CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE
├── notebooks
│   ├── _config.yml
│   ├── _toc.yml
│   ├── content.md
│   ├── intro.md
│   ├── logo.png
│   ├── markdown.md
│   ├── notebooks.ipynb
│   └── references.bib
├── README.md
└── requirements.txt
```

## Usage

1. Install [Cookiecutter](https://github.com/cookiecutter/cookiecutter/tree/1.7.2) if you haven't installed it yet:

```bash
$ pip install -U cookiecutter
```

2. Use `cookiecutter-jupyterlab` to generate a Jupyter Book template and fill out the requested information (default templating values are shown in square brackets `[]` and will be used if no other information is entered):

```bash
$ cookiecutter git@github.com:zentekmx/cookiecutter-jupyterlab.git

author_name [Captain Jupyter]: Tomas Beuzen
github_or_gitlab_username [tomasbeuzen]:
book_name [My Awesome Book]:
book_slug [my_book]:
book_short_description [This cookiecutter creates a simple boilerplate for a Jupyter Book.]: My first Jupyter Book!
version ['0.1.0']:
Select open_source_license:
1 - MIT license
2 - BSD license
3 - ISC license
4 - Apache Software License 2.0
5 - GNU General Public License v3
6 - None
Choose from 1, 2, 3, 4, 5, 6 [1]:
Select include_ci_files:
1 - github
2 - gitlab
3 - no
Choose from 1, 2, 3 [1]:
```

3. Install the package requirements from the `requirements.txt` file (it is recommended to do this in a virtual environment, e.g., using [conda](https://docs.conda.io/en/latest/)):

```bash
# Optional steps to create and activate virtual environment
$ mkvirtualenv mybook
$ workon mybook
```

```bash
$ cd my_book
$ make install
```

4. Start the Jupyter Lab development environment:

```bash
# Rename .env.sample and apply settings
$ mv .env.sample .env
```

```bash
$ make jupyterlab
```

5. Build the HTML render of your Jupyter Book:

```bash
$ make jupyterbook
```

6. View your rendered book in `my_book/_build/html/index.html`.

7. Make edits to your book by adding more content, updating the table of contents in `my_book/_toc.yml`, and and/or by editing the configuration file `my_book/_config.yml`. See the [Jupyter Book documentation](https://jupyterbook.org/intro.html) for more information on customizing your book.

8. `cookiecutter-jupyterlab` optionally comes with CI workflow files to help easily deploy your book online. A CI workflow file would have been included in your directory structure if you chose `1 - github` or `2 - gitlab` for `Select include_ci_files:` in Step 2 above. For example, if you chose `1 - github`, when ready to deploy your book online:
   1. Make sure your book builds locally as expected (`make jupyterbook`) and that you have updated the `requirements.txt` file to include any additional packages required to build your book;
   2. Create a new public [GitHub repository](https://github.com/new) to host your book;
   3. Push your local book (including the `.github` hidden directory) to your GitHub repository. There are many ways to do this, for example:

      ```bash
      $ git init
      $ git add .
      $ git commit -m "first commit"
      $ git remote add origin git@github.com:<user>/<repository-name>.git
      $ git push -u origin main
      ```

   4. The GitHub Actions workflow provided with the cookiecutter (`my_book/.github/workflows/deploy.yml`) will automatically deploy your book to the `gh-pages` branch of your repository once pushed. It is typically available after a few minutes at `https://<user>.github.io/<myonlinebook>/`. You may need to go to the `Settings` tab of your repository and under the **GitHub Pages** heading, choose the `gh-pages branch` from the **Source** drop-down list. For alternative methods of deploying your book online, see the See the [Jupyter Book documentation](https://jupyterbook.org/intro.html).

   > Note: by default, the GitHub Actions workflow file included with this cookiecutter builds the book with Ubuntu and Python 3.8. You can modify the OS/Python version for the build in the `.github/workflows/deploy.yml` file on lines 15 and 16 respectively.

   > Read more about GitHub Pages and Jupyter Book [here](https://jupyterbook.org/publish/gh-pages.html#automatically-host-your-book-with-github-actions), or using GitLab Pages [here](https://docs.gitlab.com/ee/user/project/pages/getting_started/pages_from_scratch.html).

## Contributing

We welcome and recognize all contributions. If you'd like to contribute to the project by providing feedback, identifying a bug or working on a new feature, check out the [contributing guide](CONTRIBUTING.md) to get started.

You can see a list of current contributors in the [contributors tab](https://github.com/zentekmx/cookiecutter-jupyterlab/graphs/contributors).

## Acknowledgements

This template was inspired and made possible by the [Cookiecutter project](https://github.com/cookiecutter/cookiecutter), the [Jupyter Lab project](https://jupyter.org/) and the [Jupyter Book project](https://jupyterbook.org/). Credits to [cookiecutter-jupyter-book](https://github.com/executablebooks/cookiecutter-jupyter-book) 
