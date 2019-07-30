# Branching/Merging strategies

### Git Flow

The Git Flow is the most known workflow on this list. It is based in two main branches with infinite lifetime:

·         `master` — this branch contains production code. All development code is merged into `master` in sometime.

·         `develop` — this branch contains pre-production code. When the features are finished then they are merged into develop.

During the development cycle, a variety of supporting branches are used:

·         `feature-*` — feature branches are used to develop new features for the upcoming releases. May branch off from `develop` and must merge into `develop`.

·         `hotfix-*` — hotfix branches are necessary to act immediately upon an undesired status of `master`. May branch off from `master` and must merge into `master` and `develop`.

·         `release-*` — release branches support preparation of a new production release. They allow many minor bug to be fixed and preparation of meta-data for a release. May branch off from `develop` and must merge into `master` and `develop`.

Advantages

·         Ensures a clean state of branches at any given moment in the life cycle of project

·         The branches naming follows a systematic pattern making it easier to comprehend

·         It has extensions and support on most used git tools

·         It is ideal when there it needs to be multiple version in production

Disadvantages

·         The Git history becomes unreadable

·         The master/develop split is considered redundant and makes the Continuous Delivery and the Continuos Integration harder

·         It isn’t recommended when it need to maintain single version in production

### GitHub Flow

The GitHub Flow is a lightweight workflow. It respects the following 6 principles:

1.       Anything in the `master` branch is deployable

2.       To work on something new, create a branch off from `master` and given a descriptively name\(ie: n`ew-oauth2-scopes`\)

3.       Commit to that branch locally and regularly push your work to the same named branch on the server

4.       When you need feedback or help, or you think the branch is ready for merging, open a [pull request](http://help.github.com/send-pull-requests/)

5.       After someone else has reviewed and signed off on the feature, you can merge it into `master`

6.       Once it is merged and pushed to `master`, you can and should deploy immediately

Advantages

·         it is friendly for the Continuous Delivery and Continuous Integration

·         A simpler alternative to Git Flow

·         It is ideal when it needs to maintain single version in production

Disadvantages

·         The production code can become unstable most easily

·         Are not adequate when it needs the release plans

·         It doesn’t resolve anything about deploy, environments, releases, and issues

·         It isn’t recommended when multiple versions in production are needed

### GitLab Flow

The GitLab Flow combines feature-driven development and feature branches with issue tracking. The most difference between GitLab Flow and GitHub Flow are the environment branches having in GitLab Flow \(e.g. staging and production\) because there will be a project that isn’t able to deploy to production every time you merge a feature branch

The GitLab Flow is based on 11 rules:

1.       Use feature branches, no direct commits on `master`

2.       Test all commits, not only ones on `master`

3.       Run all the tests on all commits \(if your tests run longer than 5 minutes have them run in parallel\).

4.       Perform code reviews before merges into `master`, not afterwards.

5.       Deployments are automatic, based on branches or tags.

6.       Tags are set by the user, not by CI.

7.       Releases are based on tags.

8.       Pushed commits are never rebased.

9.       Everyone starts from `master`, and targets master.

10.   Fix bugs in `master` first and release branches second.

11.   Commit messages reflect intent.

Advantages

·         It defines how to make the Continuous Integration and Continuous Delivery

·         The git history will be cleaner, less messy and more readable

·         It is ideal when it needs to single version in production

Disadvantages

·         It is more complex that the GitHub Flow

·         It can become complex as Git Flow when it needs to maintain multiple version in production

### One Flow

The main condition that needs to be satisfied in order to use OneFlow is that every new production release is based on the previous release. The most difference between One Flow and Git Flow that it not has develop branch.

Advantages

·         The git history will be cleaner, less messy and more readable

·         It is flexible according to team decisions

·         It is ideal when it needs to single version in production

Disadvantages

·         It isn’t recommended for projects with Continuous Delivery or Continuous Deploy.

·         The feature branches make it harder the Continuos Integration

·         It isn’t recommended when it needs to maintain single version in production

