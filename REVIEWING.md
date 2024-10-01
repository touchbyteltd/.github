# Completing a Code Review

When picking up a PR for review, ask yourself: are you familiar with the repo enough to judge these changes?

**If you are**, then check the description, make sure the tests are passing and use the [Reviewer Checklist](https://github.com/touchbyteltd/.github/blob/master/PULL_REQUEST_TEMPLATE.md) as a guide.
Be judgy, but **concise and constructive** in your feedback.
Remember: We all make mistakes and we're all trying to become better developers.
However, we mustn't let standards slip when letting code get out into production.
Better to request changes 4, 5, 6 times (working alongside the requester if necessary) than find a critical bug has slipped by and breaks at deployment to prod.

**If you are not**, then get the developer who submitted the PR to talk through their PR.
What is this repo about?
What did it do before the PR and what is the PR trying to achieve?
Get the requester to explain their submission and run through a test of it with you and ask questions about their decisions around different commands and functionality.
We should all aim to be comfortable with the codebase.
Even if you don't understand something now, this will help you to be ready to review or even submit the next PR to this repo.
When you are comfortable with the changes made, any follow-up changes have been pushed and no issues have arisen, you can accept and merge the PR.
Lastly, if you are still uncertain after a thorough explainer about the repo and the PR, get @miketrebilcock to do it. 😉
