# Contributing to Hugo

We welcome contributions to Hugo of any kind including documentation, themes,
organization, tutorials, blog posts, bug reports, issues, feature requests,
feature implementations, pull requests, answering questions on the forum,
helping to manage issues, etc.

The Hugo community and maintainers are very active and helpful, and the project benefits greatly from this activity. We created a [step by step guide](https://gohugo.io/tutorials/how-to-contribute-to-hugo/) if you're unfamiliar with GitHub or contributing to open source projects in general.

[![Throughput Graph](https://graphs.waffle.io/spf13/hugo/throughput.svg)](https://waffle.io/spf13/hugo/metrics)

## Table of Contents

* [Asking Support Questions](#asking-support-questions)
* [Reporting Issues](#reporting-issues)
* [Submitting Patches](#submitting-patches)
  * [Code Contribution Guidelines](#code-contribution-guidelines)
  * [Git Commit Message Guidelines](#git-commit-message-guidelines)
  * [Using Git Remotes](#using-git-remotes)
  * [Build Hugo with Your Changes](#build-hugo-with-your-changes)
  * [Add Compile Information to Hugo](#add-compile-information-to-hugo)

## Asking Support Questions

We have an active [discussion forum](http://discuss.gohugo.io) where users and developers can ask questions.
Please don't use the Github issue tracker to ask questions.

## Reporting Issues

If you believe you have found a defect in Hugo or its documentation, use
the Github [issue tracker](https://github.com/spf13/hugo/issues) to report the problem to the Hugo maintainers.
If you're not sure if it's a bug or not, start by asking in the [discussion forum](http://discuss.gohugo.io).
When reporting the issue, please provide the version of Hugo in use (`hugo version`) and your operating system.

## Submitting Patches

The Hugo project welcomes all contributors and contributions regardless of skill or experience level.
If you are interested in helping with the project, we will help you with your contribution.
Hugo is a very active project with many contributions happening daily.
Because we want to create the best possible product for our users and the best contribution experience for our developers,
we have a set of guidelines which ensure that all contributions are acceptable.
The guidelines are not intended as a filter or barrier to participation.
If you are unfamiliar with the contribution process, the Hugo team will help you and teach you how to bring your contribution in accordance with the guidelines.

### Code Contribution Guidelines

To make the contribution process as seamless as possible, we ask for the following:

* Go ahead and fork the project and make your changes.  We encourage pull requests to allow for review and discussion of code changes.
* When you’re ready to create a pull request, be sure to:
    * Sign the [CLA](https://cla-assistant.io/spf13/hugo).
    * Have test cases for the new code. If you have questions about how to do this, please ask in your pull request.
    * Run `go fmt`.
    * Add documentation if you are adding new features or changing functionality.  The docs site lives in `/docs`.
    * Squash your commits into a single commit. `git rebase -i`. It’s okay to force update your pull request with `git push -f`.
    * Make sure `go test ./...` passes, and `go build` completes. [Travis CI](https://travis-ci.org/spf13/hugo) (Linux and OS&nbsp;X) and [AppVeyor](https://ci.appveyor.com/project/spf13/hugo/branch/master) (Windows) will catch most things that are missing.
    * Follow the **Git Commit Message Guidelines** below.

### Git Commit Message Guidelines

This [blog article](http://chris.beams.io/posts/git-commit/) is a good resource for learning how to write good commit messages,
the most important part being that each commit message should have a title/subject in imperative mood starting with a capital letter and no trailing period:
*"Return error on wrong use of the Paginator"*, **NOT** *"returning some error."*

Also, if your commit references one or more GitHub issues, always end your commit message body with *See #1234* or *Fixes #1234*.
Replace *1234* with the GitHub issue ID. The last example will close the issue when the commit is merged into *master*.

Sometimes it makes sense to prefix the commit message with the packagename (or docs folder) all lowercased ending with a colon.
That is fine, but the rest of the rules above apply.
So it is "tpl: Add emojify template func", not "tpl: add emojify template func.", and "docs: Document emoji", not "doc: document emoji."

Please consider to use a short and descriptive branch name, e.g. **NOT** "patch-1". It's very common but creates a naming conflict each time when a submission is pulled for a review.

An example:

```text
tpl: Add custom index function

Add a custom index template function that deviates from the stdlib simply by not
returning an "index out of range" error if an array, slice or string index is
out of range.  Instead, we just return nil values.  This should help make the
new default function more useful for Hugo users.

Fixes #1949
```

### Using Git Remotes

Due to the way Go handles package imports, the best approach for working on a
Hugo fork is to use Git Remotes.  Here's a simple walk-through for getting
started:

1. Get the latest Hugo sources:

    ```
    go get -u -t github.com/spf13/hugo/...
    ```

1. Change to the Hugo source directory:

    ```
    cd $GOPATH/src/github.com/spf13/hugo
    ```

1. Create a new branch for your changes (the branch name is arbitrary):

    ```
    git checkout -b iss1234
    ```

1. After making your changes, commit them to your new branch:

    ```
    git commit -a -v
    ```

1. Fork Hugo in Github.

1. Add your fork as a new remote (the remote name, "fork" in this example, is arbitrary):

    ```
    git remote add fork git://github.com/USERNAME/hugo.git
    ```

1. Push the changes to your new remote:

    ```
    git push --set-upstream fork iss1234
    ```

1. You're now ready to submit a PR based upon the new branch in your forked repository.

### Build Hugo with Your Changes

```bash
cd $GOPATH/src/github.com/spf13/hugo
go build
mv hugo /usr/local/bin/
```

### Add Compile Information to Hugo

To add compile information to Hugo, replace the `go build` command with the following *(replace `/path/to/hugo` with the actual path)*:

    go build -ldflags "-X /path/to/hugo/hugolib.CommitHash=`git rev-parse --short HEAD 2>/dev/null` -X github.com/spf13/hugo/hugolib.BuildDate=`date +%FT%T%z`"

This will result in `hugo version` output that looks similar to:

    Hugo Static Site Generator v0.13-DEV-8042E77 buildDate: 2014-12-25T03:25:57-07:00

Alternatively, just run `make` &mdash; all the “magic” above is already in the `Makefile`.  :wink:
