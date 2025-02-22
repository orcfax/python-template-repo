# Template repository

Template repository for Python projects.

## Developer install

### pip

Setup a virtual environment `venv` and install the local development
requirements as follows:

```bash
python3 -m venv venv
source venv/bin/activate
python -m pip install -r requirements/local.txt
```

#### Upgrade dependencies

A `just` recipe is included, simply call `just upgrade`. Alternatively run
`pip-upgrader` once the local requirements have been installed and follow the
prompts. `requirements.txt` and `local.txt` can be updated as desired.

### tox

#### Run tests (all)

```bash
python -m tox
```

#### Run tests-only

```bash
python -m tox -e py3
```

#### Run linting-only

```bash
python -m tox -e linting
```

### pre-commit

Pre-commit can be used to provide more feedback before committing code. This
reduces reduces the number of commits you might want to make when working on
code, it's also an alternative to running tox manually.

To set up pre-commit, providing `pip install` has been run above:

* `pre-commit install`

This repository contains a default number of pre-commit hooks, but there may
be others suited to different projects. A list of other pre-commit hooks can be
found [here][pre-commit-1].

[pre-commit-1]: https://pre-commit.com/hooks.html

## Packaging

The `justfile` contains helper functions for packaging and release.

`justfile` functions can be reviewed by calling `just`  from the root of this
repository:

```just
Available recipes:
    clean               # Clean the package directory
    docs                # Generate documentation
    help                # Help
    package-check       # Check the distribution is valid
    package-deps        # Upgrade dependencies for packaging
    package-source      # Package the source code
    package-upload      # Upload package to pypi
    package-upload-test # Upload package to test.pypi
    pre-commit-checks   # Run pre-commit-checks.
    serve-docs          # Serve the documentation
    tar-source          # Package repository as tar for easy distribution
    upgrade             # Upgrade project dependencies
```

### pyproject.toml

Packaging consumes the metadata in `pyproject.toml` which helps to describe
the project on the official [pypi.org][pypi-2] repository. Have a look at the
documentation and comments there to help you create a suitably descriptive
metadata file.

### Local packaging

To create a python wheel for testing locally, or distributing to colleagues
run:

* `just package-source`

A `tar` and `whl` file will be stored in a `dist/` directory. The `whl` file
can be installed as follows:

* `pip install <your-package>.whl`

### Publishing

Publishing for public use can be achieved with:

* `just package-upload-test` or `just package-upload`

`just-package-upload-test` will upload the package to [test.pypi.org][pypi-1]
which provides a way to look at package metadata and documentation and ensure
that it is correct before uploading to the official [pypi.org][pypi-2]
repository using `just package-upload`.

[pypi-1]: https://test.pypi.org
[pypi-2]: https://pypi.org
