---
layout: post
tags:
- Development
- Workflow
- Process
- Staging
---
Some examples of Development Workflows

## My current Development Workflow (using Jira, Bitbucket, Git, AWS)

> This process works well as part of a larger development team

1. Create a branch from the `master` branch `[In Development]`

    > The name should be or start with the Jira ticket name/number.

2. Do some work `[In Development]`

        Make some changes, commit them, push them (to Bitbucket)

3. Create a pull request to merge your branch into the `dev` branch `[Code Review]`

4. The work is reviewed and the pull request is approved (or rejected) `[Code Review]`

    > If the pull request is rejected, check the comments, action any issues raised and create a new pull request for the new work/changes

5. QA is done and the branch is merged into the `dev` branch (or bugs are raised) `[Testing]`

    > If bugs are raised, the Jira ticket is returned to the `[In Development]` state

6. The new features are demonstrated (on Staging) `[Demo]`

7. The `dev` branch is merged with the `master` branch

## My previous Development Workflow (using Redmine, Github, Git, AWS)

> This process works well as part of a smaller development team. There is more testing to compensate for fewer reviewers and the lack of a design, QA and dev-ops team. The developer does more of the testing and dev ops work

1. Create a branch from the `staging` branch

    > The name should be or start with the Redmine ticket number

2. Do some work

    Make some changes, commit them, push them (to Github)

3. Create a pull request to merge your branch into the `staging` branch and ask someone else to review the code before merging it.

    If issues are raised, action them and update the pull request

    If there are no issues, merge the branch and test on the AWS Opsworks staging stack

5. Ask anyone you can find to test functionality on staging

6. Merge your branch with the `per-production` branch and test on the AWS Opsworks pre-production stack

    > `pre-production` testing differs from `staging` testing in that real connections to payment gateways and order processors are used

7. Create a pull request to merge your branch into the `master` branch

8. Finally double-check the new functionality on live