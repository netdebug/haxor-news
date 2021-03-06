Release Checklist
=================

A. Install in a new venv and run unit tests

Note, you can't seem to script the virtualenv calls, see:
https://bitbucket.org/dhellmann/virtualenvwrapper/issues/219/cant-deactivate-active-virtualenv-from

    $ deactivate
    $ rmvirtualenv haxor-news
    $ mkvirtualenv haxor-news
    $ pip install -e .
    $ pip install -r requirements-dev.txt
    $ rm -rf .tox && tox

B. Run code checks

    $ scripts/run_code_checks.sh

C. Run manual [smoke tests](#smoke-tests) on Mac, Ubuntu, Windows

D. Update and review `README.rst` and `Sphinx` docs, then check haxor-news/docs/build/html/index.html

    $ scripts/update_docs.sh

E. Push changes

F. Review Travis, Codecov, and Gemnasium

G. Start a new release branch

    $ git flow release start x.y.z

H. Increment the version number in `haxor-news/__init__.py`

I. Update and review `CHANGELOG`

    $ scripts/create_changelog.sh

J. Commit the changes

K. Finish the release branch

    $ git flow release finish 'x.y.z'

L. Input a tag

    $ vx.y.z

M. Push tagged release to develop and master

N. Set CHANGELOG.rst as `README.rst`

    $ scripts/set_changelog_as_readme.sh

O. Register package with PyPi

    $ python setup.py register -r pypi

P. Upload to PyPi

    $ python setup.py sdist upload -r pypi

Q. Upload Sphinx docs to PyPi

    $ python setup.py upload_sphinx

R. Review newly released package from PyPi

S. Release on GitHub: https://github.com/donnemartin/haxor-news/tags

    1. Click "Add release notes" for latest release
    2. Copy release notes from `CHANGELOG.md`
    3. Click "Publish release"

T. Install in a new venv and run manual [smoke tests](#smoke-tests) on Mac, Ubuntu, Windows

## Smoke Tests

Run the following on Python 2.7 and Python 3.4:

* Craete a new `virtualenv`
* Pip install `haxor-news` into new `virtualenv`
* Run `haxor-news`
* Run targeted tests based on recent code changes
