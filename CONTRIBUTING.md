# Salto Orion Contributing guide

The short version.
Full processes and information is on [Confluence](https://touchbyte.atlassian.net/wiki/x/AYAiAg).
This is just for handling commits to the [facentry-universe](https://github.com/touchbyteltd/facentry-universe) and its submodules.

## Writing Code

The general process is as follows:

1. Clone your repo.
2. Set-up as per the `README.md`.
3. Create a branch for your work (matching the issue code in [Jira](https://touchbyte.atlassian.net/jira/software/projects/FE/boards/1) where possible.)
4. Do some sweet codemancer magic.
5. Push to the cloud repo.
6. Create a [Pull Request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests).
7. Make any modifications needed to pass the tests.
8. Get reviewed by someone else in the team and make the requested changes. (repeat as needed)
9. Merge into `dev`.

This isn't the place to write out good coding practices, but aim to write code worth being proud of.
We run a bunch of tools to make sure it stays up to a standard but they can only go so far.
Any real concerns about the right way to go can always be solved with a chat or some paired programming.

## Recommended Tools

**Visual Studio Code Extensions**:
Each repo should have a `.vscode/extensions.json` file that contains extensions recommended for the relevant repo.
These vary from local tool equivalents of GitHub Actions to virtual environments for Windows addicts.
Recommended tools will show up in the bottom left of the **extensions** tab, or through a popup in the lower right when opening the repository.
If you don't use VSCode then you can still make use of this file as most extensions can be found online as standalone executables or scripts.

*Authors note: VSCode pets didn't make the cut, but it's really cute and you should download that too.*

## Testing

A super important component in long term reliability is unit testing.
Our CI/CD process will run any unit tests available to the repo and code coverage tools will ensure that standards are kept up.
Any time a new function or class is made, or any time a new pathway through the code is added, **a new unit test must be made** that covers the changes.
Try to aim for successful, unsuccessful, and edge-case pathways to give your code the best chance of surviving future modifications.

## Documentation

The `README.md` in each file should be a comprehensive guide to getting up and running as a developer with this repository.
It should say how to **install**, **configure** and **use** the code within, as well as stating the **purpose** of the repository and any **extra restrictions and guidance** necessary for contributions.
*We would appreciate additions to any and all missing sections of current repository `READMEs`.

The [support site](https://support.saltosystems.com/orion) must be updated upon completion of jobs that alter the following:

- **User interfaces**, including Orion Device lighting and console responses.
- **User processes**, by which we mean any time the user has to do something different along their journey.
This can be a new process altogether (eg. now you can enter with QR codes) or a modification of a current one (eg. when changing Space IP, go to `integrations` instead of `Site Configuration`).
- **Legal alterations** when modifying the back-end, particularly when handling user biometric data.
- **New terminology** is solidified.
The [Glossary](https://support.saltosystems.com/orion/glossary/) may need a new term, with links shared across the site.

Changes to the support site require access (explicitly granted by Ian Cowley) to the [support site](https://github.com/saltosystems-internal/support.saltosystems.com) and [terminology](https://github.com/saltosystems-internal/terminology) repositories managed by Salto.
They have their own restrictions to adhere to, such as the [style guide](https://github.com/saltosystems-internal/.github/blob/main/docs/documentation-style-guide.md) and [code of conduct](https://saltosystems.com/en/sustainability-governance).

## Pull Requests

`dev` is the default branch on every repo attached to the [facentry-universe](https://github.com/touchbyteltd/facentry-universe).

**You cannot commit to `dev`**.

All contributions must be made by creating a branch (matching the issue code in [Jira](https://touchbyte.atlassian.net/jira/software/projects/FE/boards/1), where possible) and creating a [Pull Request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) back in.

When creating your Pull Request, put a useful description in the box to help your reviewer for any non-trivial case.
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

### Commits

Use [Conventional commits](https://www.conventionalcommits.org/en/v1.0.0/), no matter how small the commit, so that the history is easily parsable by people and tools alike.

There's an excellent [VSCode extention](https://marketplace.visualstudio.com/items?itemName=vivaxy.vscode-conventional-commits) that can help with this, including [gitmojis](https://gitmoji.dev/). 💩

### Code Review

When picking up a PR for review, ask yourself: are you familiar with the repo enough to judge these changes?

**If you are**, then check the description, make sure the tests are passing and use the [Reviewer Checklist](https://github.com/touchbyteltd/.github/blob/master/PULL_REQUEST_TEMPLATE.md) as a guide.
Be judgy, but concise and constructive in your feedback.
Remember: We all make mistakes and we're all trying to become better developers.
However, we mustn't let standards slip when letting code get out into production.
Better to request changes 4, 5, 6 times (working alongside the requester if necessary) than find a critical bug has slipped by and breaks at deployment to prod.

**If you are not**, then get the developer who submitted the PR to talk through their PR.
What is this repo about?
What did it do before the PR and what is the PR trying to achieve?
Get the requester to explain their submission and run through a test of it with you and ask questions about their decisions around different commands and functionality.
We should all aim to be comfortable with the codebase.
Even if you don't understand something now, this will help you to be ready to review or even submit the next PR to this repo.
When you are comfortable with the changes made, any follow-up changes have been pushed and no issue shave arisen, you can accept and merge the PR.
Lastly, if you are still uncertain after a thorough explainer about the repo and the PR, get @miketrebilcock to do it. ;)

## CI/CD

We make liberal use of GitHub actions to check our work as well as the Pull Request process.
Some of these are critical and enforced, but all checks can be done locally using command line tools or VSCode extensions.
In emergencies *(such as game-breaking bugs pushed to prod)*, @miketrebilcock can bypass these checks and force through a merge.
@HarrisonHG also has these powers, but he'll just give you the eye and complain about good practice.

It's also worth noting that once a commit does make its way to `Dev`, a long build process will be triggered by `facentry-universe` that is run in the [terraform repo](https://github.com/touchbyteltd/terraform/actions/workflows/create-update-env.yml).
If this dev build fails, you are **strongly** recommended to check the reason for failure and fix it up before our [sprint-ly deployment](https://touchbyte.atlassian.net/wiki/spaces/FaceEntry/pages/113541136/Development+Deployment+Process#Closing-the-Sprint) occurs.

### Linting

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
Any time a new function or class is made, or any time a new pathway through the code is added, **a new unit test must be made** that covers the changes.
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
