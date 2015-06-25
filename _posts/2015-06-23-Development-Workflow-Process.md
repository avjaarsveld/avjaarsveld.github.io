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

```
*---------------------------------------*
| Select first open ticket from backlog | <--------------------------.
*---------------------------------------*                            |
                  ||                                                 |
                  \/                                                 |
*-----------------------------------*                                |
| Set Jira ticket to In Development | => *-----------------------*   |
*-----------------------------------*    | Branch from master,   |   |
                          *---------*    | the name should start |   |
     .------------------->|         |    | with Jira ticket name |   |
     |   .-----------.    | Do work | <= *-----------------------*   |
    (no)-| finished? | <= *---------*                                |
         .-----------.                                               |
               |      *-----------------------------------------*    |
             (yes)--->| Create pull request (to merge into dev) |    |
                      *-----------------------------------------*    |
                        ||    _____________________________________  |
                        L==> ( Ticket moved to Review lane in Jira ) |
                              -------------------------------------  |
           .---------------------------------.     ||                |
           |                                 | <===                  |
     (yes)-| Pull request to review present? |                       |
       |   .---------------------------------.-(no)-------------------
       v
*-------------*    .-------------.        .-----------.--------(yes)
| Select pull | => | has issues? |-(yes)->| critical? |          |
| request     |    .-------------.        .-----------.---(no)   |
*-------------*          /    ^       ______________________|     |
                        /     |      |                           v
*-----------------*    /      |      v       *-----------------------*
| Approve request |<-(no)  *--------------*  | Reject pull request - |
*-----------------*        | Add Comments |  | New request required  |
        ||                 *--------------*  *-----------------------*
        \/
 ___________________________
( Ticket moved to test lane )
 ---------------------------


```

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