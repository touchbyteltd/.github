# Salto Orion Contributing guide

The short version.
Full processes and information is on [Confluence](https://touchbyte.atlassian.net/wiki/x/AYAiAg).
This is just for handling commits to the [facentry-universe](https://github.com/touchbyteltd/facentry-universe) and its submodules.

## Recommended Tools

**[Visual Studio Code Extensions](https://code.visualstudio.com/)**:
Each repo should have a `.vscode/extensions.json` file that contains extensions recommended for the relevant repo.
Recommended tools will show up in the bottom left of the **extensions** tab, or through a popup in the lower right when opening the repository.
If you don't use VSCode then you can still make use of this file as most extensions can be found online as standalone executables or scripts.

*Authors note: VSCode pets didn't make the cut, but it's really cute and you should download that too.*

**[*nektos/act](https://github.com/nektos/act)**: For testing workflow files locally.
There is also a [dedicated repo](https://github.com/touchbyteltd/workflow-tests) for workflow testing to minimize potential damage to "real" code repositories.

**[Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/install)**: WSL is great for the Windows users amongst us who *need* a quick linux box to run tests in.

### Writing and Committing your Code

Once you have your environment set up, go and do your codemancer magic!
This isn't the place to write out good coding practices, but aim to write code worth being proud of.
Any real concerns about the right way to go can always be solved with a chat or some paired programming.

`dev` is the default branch on every repo attached to the [facentry-universe](https://github.com/touchbyteltd/facentry-universe).

**You cannot commit to `dev`**.

All contributions must be made by creating a branch (matching the issue code in [Jira](https://touchbyte.atlassian.net/jira/software/projects/FE/boards/1), where possible) that will contain all commits related to your changes.
We call these the **feature branches**.

After work has been completed, use [Conventional commits](https://www.conventionalcommits.org/en/v1.0.0/), no matter how small the commit, so that the history is easily parsable by people and tools alike.

There's an excellent [VSCode extention](https://marketplace.visualstudio.com/items?itemName=vivaxy.vscode-conventional-commits) that can help with this, including [gitmojis](https://gitmoji.dev/). 💩

Commit little and often, so that any need to check the history can be easily tracked and rollbacks are minimally disruptive.

## Unit Tests

A super important component in long term reliability is unit testing.
Any time a new function or class is made, or any time a new pathway through the code is added, **a new unit test must be made** that covers the changes.
Try to aim for successful, unsuccessful, and edge-case pathways to give your code the best chance of surviving future modifications.

When you get to submitting a PR, a collection of GitHub actions will run any unit tests available to the repo and code coverage tools will ensure that standards are kept up.

## Documentation

The `README.md` in each file should be a comprehensive guide to getting up and running as a developer with this repository.
It should say how to **install**, **configure** and **use** the code within, as well as stating the **purpose** of the repository and any **extra restrictions and guidance** necessary for contributions.
*We would appreciate additions to any and all missing sections of current repository `READMEs`.*

The [support site](https://support.saltosystems.com/orion) must be updated upon completion of jobs that alter the following:

- **User interfaces**, including anything that the user interacts with such as Orion Device lighting and console output.
- **User processes**, by which we mean any time the user has to do something different along their journey.
This can be a new process altogether (eg. now you can enter with QR codes) or a modification of a current one (eg. when changing Space IP, go to `integrations` instead of `Site Configuration`).
- **Legal alterations** when modifying the back-end, particularly when handling user biometric data.
- **New terminology** is solidified.
The [Glossary](https://support.saltosystems.com/orion/glossary/) may need a new term, with links shared across the site.

Changes to the support site require access (explicitly granted by Ian Cowley) to the [support site](https://github.com/saltosystems-internal/support.saltosystems.com) and [terminology](https://github.com/saltosystems-internal/terminology) repositories managed by Salto.
They have their own restrictions to adhere to, such as the [style guide](https://github.com/saltosystems-internal/.github/blob/main/docs/documentation-style-guide.md) and [code of conduct](https://saltosystems.com/en/sustainability-governance).

## Pull Requests

After completing your feature/bugfix, adding relevant tests and documenting the changes, create a [Pull Request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) in GitHub for someone else to review and merge into `dev`.

> We work on a peer-review basis, where we check each other's work and merge without the need for the team leader to approve all pull requests.
> This way, we all learn about each other's work and become experts on the whole of Orion over time.
> For a quick guide on reviewing tasks yourself, check the `REVIEWING.md` doc.

When creating your pull request The title should either:

- Be the issue number in [Jira](https://touchbyte.atlassian.net/jira/software/projects/FE/boards/1).
- Follow the [Conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) style.
- Be a mixture of the two, such as: `FE-1888: add markdown linting`

Then put useful description in the box to help your reviewer for any non-trivial case.
Do they need to test any particular action?
What is the purpose of your PR?
Did you need to make any difficult decisions?
etc...

Once a PR is created, all of the CI/CD goodness below can begin and you must wait for someone else in the team to review your changes.
Only under the following conditions will the merge button turn green:

- Your branch is up to date with `dev`.
- All `Required` checks have passed.
These are usually the linters, license checks and unit tests.
- At least 1 other dev has accepted your **latest** changes.
(Any `changes requested` will require a follow up review.)
- All conversations have been resolved.

While the PR is sitting waiting for a review, you can move your card  to `Review` in [Jira](https://touchbyte.atlassian.net/jira/software/projects/FE/boards/1) (if applicable) and get started on something else.

Please note that pull requests are an iterative process.
It is expected that there will be some things that need changing or fixing - we are all human after all.
Only once both reviewer and coder are happy and understand changes, will the pull request be approved.

## Automated Tests

We make liberal use of GitHub actions to check our work during the Pull Request process.
Some of these are critical and enforced, but all checks can be done locally using command line tools or [VSCode extensions](#recommended-tools).

It's also worth noting that once a commit does make its way to `Dev`, a long build process will be triggered by `facentry-universe` that is run in the [terraform repo](https://github.com/touchbyteltd/terraform/actions/workflows/create-update-env.yml).
If this dev build fails, you are **strongly** recommended to check the reason for failure and fix it up before our [sprint-ly deployment](https://touchbyte.atlassian.net/wiki/x/EIDEBg) occurs.

### Linting

Linters perform a light quality check on your code for things such as spacing, naming convention and unused variables.
All linters have clear documentation indicating which rule is broken and when, so if you get a linting error, search for the code in the respective documentation for a detailed case on what's wrong, why it's bad and how to fix it.

Look out for these badges in each repository:

[![Pylint Badge](https://img.shields.io/badge/linting-pylint-darkblue)](https://github.com/pylint-dev/pylint)
[![Markdown Lint Badge](https://img.shields.io/badge/linting-MarkdownLint-blue)](https://github.com/DavidAnson/markdownlint-cli2-action)
[![Shell Lint Badge](https://img.shields.io/badge/linting-ShellCheck-brightgreen)](https://github.com/koalaman/shellcheck)
[![ESLint Badge](https://img.shields.io/badge/linting-ESLint-blue)](https://eslint.org/)
[![Terraform Format Badge](https://img.shields.io/badge/formatter-Terraform-purple)](https://developer.hashicorp.com/terraform/cli/commands/fmt)

These indicate which linters are running on that repo and will be tested at PR.
Click any of these badges to see where the testing action or tool is hosted.

### Unit Tests & Code Coverage

Code coverage means to cover our code in unit tests.
These tests are run automatically using the tools appropriate to the repository and its languages.

[![PyTest Badge](https://img.shields.io/badge/testing-PyTest-darkblue)](https://pypi.org/project/pytest/)
[![Jest Badge](https://img.shields.io/badge/testing-Jest-green)](https://jestjs.io/docs/getting-started)
[![Terraform Validate Badge](https://img.shields.io/badge/validater-Terraform-purple)](https://developer.hashicorp.com/terraform/cli/commands/validate)
[![ESLint Badge](https://img.shields.io/badge/testing-ESLint-blue)](https://eslint.org/)

The above tests can have their results extracted and displayed in PRs to run code coverage checks on many repos.
We can't practically enforce this check, but the results will be visible for appropriate repositories.
Whenever contributing new code to a repository, these values must increase.

[![Pytest Coverage Badge](https://img.shields.io/badge/Code_Coverage-PyTest-darkblue)](MishaKav/pytest-coverage-comment)
[![Jest Badge](https://img.shields.io/badge/Code_Coverage-Jest-green)](https://github.com/ArtiomTr/jest-coverage-report-action)

### Static Code Analysis, Licenses and Security Checks

Snyk performs up to 3 jobs on PRs depending on the repository.

- **License**: As a commercial entity with proprietary code, we must be aware of the license behind **every** library we build into software that we distribute.
If this error is thrown, click `Details` to go to Snyk and see which new library has been added.
A new line must be added to the open source declarations in the support site.
Create a PR in the [support site repo](https://github.com/saltosystems-internal/support.saltosystems.com) or notify @HarrisonHG with a link to the online source (such as GitHub or package hosting site).
Then you can mark the check as a success in the Snyk site and the PR will update.
- **Security**: Checks dependencies for security vulnerabilities.
If this error is thrown, it usually means you need to use a more up-to-date version of a library, or find an alternative one because this library is unsafe.
- **static-code-analysis**: Sometimes blended in with other actions to save a few pennies, this looks over your code for potential security vulnerabilities **in your code**, such as hard-coded API keys or opportunities for SQL injection.
If this error is thrown, you've got some re-writes to do.
