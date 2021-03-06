# import-ready
[![image](https://img.shields.io/github/license/dksmiffs/import-ready.svg)](https://github.com/dksmiffs/import-ready)
[![image](https://img.shields.io/github/release/dksmiffs/import-ready.svg)](https://github.com/dksmiffs/import-ready/releases)
[![image](https://img.shields.io/pypi/v/import-ready.svg)](https://pypi.org/project/import-ready/)
[![image](https://img.shields.io/travis/dksmiffs/import-ready.svg)](https://travis-ci.org/dksmiffs/import-ready)
[![image](https://img.shields.io/codecov/c/github/dksmiffs/import-ready.svg)](https://codecov.io/gh/dksmiffs/import-ready)
[![image](https://img.shields.io/codacy/grade/d02f4f80df0445738821c692f4bbe16f.svg)](https://app.codacy.com/project/dksmiffs/import-ready/dashboard)

This repository demonstrates steps needed to publish an importable Python package first to [TestPyPI][1], and second to [PyPI][7].  If this demonstration deviates from best practice in any way, please submit an [issue][8] on GitHub.

Inside _import-ready_ is a package called `huntsville_havoc` that divulges a couple of bona fide secrets that most diehard SPHL [Huntsville Havoc][6] fans don't know.

## Prepare the Package
1.  [Prepare your environment][2] before installing Python packages.
2.  Update version in setup.py per [semantic versioning][3] guidance.

## Test in Development Environment
Run as follows from the top level directory in a clean venv with [pip-tools][12] installed:
<pre>python -m piptools compile --upgrade --generate-hashes dev-requirements.in
python -m piptools sync dev-requirements.txt
python -m pytest -s tests</pre>

## Publish to TestPyPI
1.  Git commit, tag, & push all desired edits for release.
2.  Create a new release in GitHub to mirror your new version.
3.  [Generate distribution archives][4] for your package.
4.  [Upload your package][5] to TestPyPI.

## Test the TestPyPI-Published Package
Run as follows from the `tests` directory in another clean venv with [pip-tools][12] installed:
<pre>TEST_PYPI_FLAG='--extra-index-url https://test.pypi.org/simple/'
python -m piptools compile --upgrade --generate-hashes $TEST_PYPI_FLAG \
      --output-file testpypi-requirements.txt pub-requirements.in
python -m piptools sync $TEST_PYPI_FLAG testpypi-requirements.txt
python -m pytest -s</pre>

## Publish to PyPI
After passing the above tests, [upload your package][9] to PyPI.

## Test the PyPI-Published Package
Run as follows from the `tests` directory in _yet another_ clean venv with [pip-tools][12] installed:
<pre>python -m piptools compile --upgrade --generate-hashes \
      --output-file pypi-requirements.txt pub-requirements.in
python -m piptools sync pypi-requirements.txt
python -m pytest -s</pre>

## [Thanks][11]

## License
[MIT][10]

[1]: https://test.pypi.org/
[2]: https://packaging.python.org/tutorials/installing-packages/#requirements-for-installing-packages
[3]: https://semver.org/
[4]: https://packaging.python.org/tutorials/packaging-projects/#generating-distribution-archives
[5]: https://packaging.python.org/tutorials/packaging-projects/#uploading-the-distribution-archives
[6]: http://huntsvillehavoc.com/view/huntsvillehavoc
[7]: https://pypi.org/
[8]: https://github.com/dksmiffs/import-ready/issues
[9]: https://packaging.python.org/tutorials/packaging-projects/#next-steps
[10]: https://gitlab.com/dave.k.smith/import-ready/raw/master/LICENSE
[11]: https://github.com/dksmiffs/import-ready/blob/master/THANKS.md
[12]: https://github.com/jazzband/pip-tools
[13]: https://github.com/jazzband/pip-tools/issues/638
