# Code quality

The quality of the code is very important. That is why we have linters, unit tests, API
docs, in code docs, developer docs, modular code and have put a lot of thought in the 
underlying architecture of both the backend and the web-frontend.

## Running linters and tests

If you have the [development environment](./development-environment.md) up and running.
you can easily run the linters. Both the backend and the web frontend have make files
to make this easier.

* `make lint` (backend): all the python will be checked with flake8.
* `make eslint` (web-frontend): all the javascript code will be checked with eslint.
* `make stylelint` (web-frontend): all the scss code will be checked with stylelint.

## Running tests

There are also commands to easily run the tests.

* `make test` (backend): all the backend python code will be tested with pytest.
* `make jest` (web-frontend): all the web frontend code will be tested with jest.

## Continuous integration

To make sure nothing has been missed while developing we also have a continuous 
integration pipeline that runs every time a branch is pushed. All the above explained
commands are going to be executed in an isolated environment. In order to improve speed
they are separated by lint and test stages. It is not allowed to merge the branch if 
one of these jobs fails.

The pipeline also has a build job. Via for example the 
[plugin boilerplate](../plugins/boilerplate.md) Baserow will be installed as a 
dependency. This job will make sure that that still works.

### Run the GitLab runners locally

If you want to check if your job would succeeds before pushing your branch then you can 
also run them locally. Make sure that you have installed the GitLab runner by following
the steps on https://docs.gitlab.com/runner/install/. After that you should be able to
run the `gitlab-runner --help` command in your terminal. The jobs can be executed by 
running the following commands below.

> Make sure that you are in the root of the Baserow repository and that all changes 
> have been commited because the runner checks out the current branch.

* `gitlab-runner exec docker web-frontend-eslint`
* `gitlab-runner exec docker web-frontend-stylelint` 
* `gitlab-runner exec docker web-frontend-test`
* `gitlab-runner exec docker backend-flake8`
* `gitlab-runner exec docker backend-pytest` 
* `gitlab-runner exec docker backend-setup` 
