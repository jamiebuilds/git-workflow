Git Workflow
============

This is a document that I have been working on for a while, I've used it across multiple teams. Although it caters towards agile methodology, it's not completely tied to it. Most of this document is obvious things that most developers already do.

It also requires a good amount of knowledge of git/github. You can certainly use other tools and get the same value, but you might have to do some translating.

## Preamble

The most important rule of this workflow, is that the developer who is writing the code is responsible for making sure it goes through the entire process smoothly and in a timely manner.

Other developers need to reach out and help in any way possible, even if it's not a piece of code you have worked on in the past or the code is in a language you don't know.

While this may seem like a lot of steps, it's very verbose and probably repeats a lot of things you're already doing. From experience I can say that it becomes very natural after a little while, and you stop really noticing it at all.

Of course there is no One True Way™ of working with code across teams, it's a never ending process of improving upon your existing workflow. No document should keep you from improving things, and you should always use your best judgement.

## New Code

### Create Branch

1. Update the **master**, **staging** and/or **feature** branches to latest version(s)
  - Always branch from the place it will be merged back into
2. Create branch 
  - short descriptive name
  - prefixed with initials (eg. `tjk_branch_name`)

### Make Changes

3. Make change
  - Make sure all watch tasks are running (build, unit tests)
4. Test
  - Run full test suite locally
5. Commit with descriptive name
  - prefix with `[WIP]` ("work in progress") if any tests are broken 

### Push changes

6. Pull master for any changes
7. Rebase branch onto master
8. Squash any `[WIP]` commits
    - Make sure all commit names make sense for their content
    - Don't leave any broken commits
9. Push branch up to github
    - Create new origin branch with same name

### Pull Request

10. Open pull request into a **staging** or **feature** branch
    - Longer descriptive title of task
    - Bullet points with descriptions of changes (changelog)
11. CI server should run tests on pull request and update its status
    - (eg. Travis CI)

### Code Review

12. Other devs should review code and leave notes
    - no confusing code
    - check for potential issues
    - any architectual improvements
    - code is properly abstracted
    - make sure there are appropriate tests

13. Code owner is responsible for making any necessary fixes any pushing them up
    - Follow same commit process
14. Other devs should give the code the thumbs up (at least two other devs)
    - Literally leave a comment with an emoji thumbs up (`:+1:` on github)
    - add short text of why you are okay with merging the pull request

### Code Review (alt)

If there is a quick change that needs to be done, one that either doesn't affect any of the actual code, or that needs to go out quickly, this version of code review can be used.

If this is an emergency, pull other people in right away. Don't trust yourself to not make silly mistakes, the last thing you want to do is make more. Notify team members that you are doing this.

12. Review the code yourself, or try and get someone to look at it with you
    - make sure everything is clean
    - no confusing code
    - check for potential errors
    - any architectual improvements
    - code is properly abstracted
    - make sure there are appropriate tests
13. Make any other changes locally and push them up, make sure to review again what you just did.
    - Follow same commit process
14. Explain why you need to merge this code in yourself. Give yourself the thumbs up
    - Literally leave a comment with an emoji thumbs up (`:+1:` on github)
    - add short text of why you are okay with merging the pull request

### Merging Code

Once you have had enough people review it, you are confident in the code you have written, and everything is well tested and passing. You can start the deploy process.

15. Merge the pull request into the **staging** or **feature** branch, and then delete it on github.
16. Let the full test suite run again on the merged code

### Releasing Code

Everyone has their own steps to take when releasing, but these are a couple things to be sure to do on github.

17. Add any notes to a `CHANGELOG.md` file
    - include version number and release date
    - This can generally be done directly on staging since you shouldn't have any code that depends on the content of a markdown file
18. Merge **Staging** into **Master**
19. Create a new release on github
    - creating a (semver) version tag
20. Begin deploy process, and send release notes to the appropriate people
    - Cross your fingers

## Master Branch

The **Master Branch** is sacred, it's code that is always working and deployable. You should never work directly on master and never push to it from a local version or from any branch other than staging. You also generally shouldn't be pushing to the **Master branch** unless you are about to make a release.

The master branch should be named: `master`

## Staging Branch

The **staging branch** is where you branch off and merge in most of your code, it should be ahead of the latest release to master and should attempt to always be working. If something does break then you want to fix it as soon as possible.

The staging branch should be named: `staging`

## Feature Branches

Sometimes new features take several team members to create, need code changes on several repositories, or take a long period of time to create. In these cases **feature branches** should be used.

A feature branch is similar to the **Staging branch** in that you never directly write code to it. You make pull requests into it before making a pull request into staging.

If feature branches are tied together in multiple repositories then they should be given the same name and link to eachother from their pull requests.

Feature branches should be named: `feature_[branch_name]`

## Working branches

These are branches that you create locally and push up to origin. They should be branched off of either the staging branch or a feature branch before being pull requested back into them. They don't have to be completely working at any point, but should always be working towards it.

Keep running the test suite, if lots of things start breaking outside the scope of the changes, then make sure the changes you are making are safe to do. Just use your best judgement and everything will be just fine.

Working branches should be named: `[initials]_[branch_name]`

## Spike Branches

**Spike branches** are code that will never get merged in. It's throwaway, experimental code that is meant to implement a feature or change as quickly as possible.

Generally these are to test a new idea, or see how plausible a feature is. They can be used to make architectural decisions, or to educate oneself about a new piece of technology. 

Spike branches should be named: `spike_[branch_name]`

## Additional Resources

- [A Successful Git Branching Model](http://nvie.com/posts/a-successful-git-branching-model/)
- [Understanding the Git Workflow](https://sandofsky.com/blog/git-workflow.html)
- [Github: Understanding the Git Flow](http://guides.github.com/overviews/flow/)
- [Issues with Git Flow](http://scottchacon.com/2011/08/31/github-flow.html)
