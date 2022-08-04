What is this project ?
----------------------

This project is **NOT** the official actions-codespell repository.

It is a fork of actions-codespell sources hosted at https://github.com/codespell-project/actions-codespell.

It is used (1) as GitHub Actions that may be directly included workflows to ensure a recent version of codespell
is used (see below more details) and (2) as staging area to maintain and test patches that will be contributed
back to the official repository.


Why maintain this fork ?
------------------------

As of 2022-08-04, since the latest release of the codespell package available on PyPI is 2.1.0 from 2021-06-19,
this project will include a modified `requirements.txt` installing a recent version of the codespell project
directly from GitHub by referencing a specific git hash.


What is the branch naming convention ?
--------------------------------------

Each branch is named following the pattern `slicer-YYYY-MM-DD-SHA{N}`

where:

* `YYYY-MM-DD` is the date of the last official commit associated with the branch.
* `SHA{N}` are the first N characters of the last official commit associated with the branch.


How to reference this project in GitHub Actions workflows ?
-----------------------------------------------------------

To deterministically check the spelling, it is recommended to reference this GitHub Action
using a syntax similar to the following by using a specific git hash:

```
- uses: Slicer/actions-codespell@da9d7dca859f5c302f7fec47b3b2a4267a6891fd
```


How to update the version of actions-codespell ?
------------------------------------------------

1. Clone this repository and add a remote to the official project

```
git clone git://github.com/Slicer/actions-codespell
cd actions-codespell
git remote add upstream git://github.com/codespell-project/actions-codespell
git fetch upstream
```

2. Checkout base to update the `latest`

```
git checkout -b master upstream/master
```

3. Create a new branch following the convention

```
DATE=$(git show -s --format=%ci HEAD | cut -d" " -f1)
echo "DATE [${DATE}]"
SHA=$(git show -s --format=%h HEAD)
echo "SHA [${SHA}]"
BRANCH_NAME=slicer-${DATE}-${SHA}
echo "BRANCH_NAME [${BRANCH_NAME}]"
git checkout -b ${BRANCH_NAME} ${SHA}
```

4. Cherry-pick the Slicer specific commits from last branch. Resolve conflict as needed.

5. Publish the branch. (directly in this repo if you have push rights, or on a fork)


How to be granted push rights ?
-------------------------------

Ask on https://discourse.slicer.org/


Questions
---------

If you have questions, see https://discourse.slicer.org/
