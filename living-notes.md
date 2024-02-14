---
editor_options: 
  markdown: 
    wrap: 80
---

# Living notes on using git in research

["Ulysses Pact" ](https://en.wikipedia.org/wiki/Ulysses_pact)

-   Give yourself constraints/restrictions.

-   Leaving your keys/credit card at home before going out for a night, etc.

-   Using git is a ulysses pact.

-   In order to do more, you must have the discipline to do LESS. Constrain
    yourself to a simple approach with git/plain text.

## Example workflow of creating a repo and identifying tasks

-   Start with a file - penguins.R (now [pengweens
    repo](https://github.com/njtierney/pengweens/))

-   Turn into a git directory + repo on github

    -   Start with github/username/new (starting repo first - see
        <https://happygitwithr.com/new-github-first> )
        -   Can also use `usethis::use_github()` if you have credentials set up
        -   See `?usethis::use_github()` for more details on the arguments
            (e.g., you might want to set an organisation to push to for example
    -   Consider using the gh command line to also manage github things like
        creating issues or cloning repositories locally, viewing issues etc. See
        <https://github.com/cli/cli> for instructions
        -   There might be some credential/handshaking that needs to happen
        -   See credentials R package for managing this

-   Issue / PR flow

    -   Make an issue - give it a name, write a clear task
        -   e.g., "Add an R file, 'packages.R' that lists all R packages used
            and writes them as library(PKGNAME)"
    -   Make a branch
        -   I like to use RStudio to make branches, it removes one step of
            typing from doing it via the terminal, but you can absolutely use
            the terminal instead
        -   Naming the branch after the issue
            -   Each branch should be tied to (ideally) just one issue.
                Sometimes this isn't quite possible though.
            -   Name the branch with a few keywords from the issue you care
                about, plus the issue number
            -   "some-key-description-ISSUENUMBER"
            -   e.g., "add-r-packages-file-1"
        -   The core idea here is that it is one branch per issue
    -   Make changes on this new branch
        -   In this case we used `codelens::write_package(".")` to write the
            package.R file
    -   Write a commit that finishes the sentence: "This commit will..."
    -   My commit said:

    ```         
    Remove library calls

    * Remove individual `library`
    * remove namespace (pkg::fun) calls from penguins.R
    * move them into packages.R file.
    * resolves #1
    ```

    -   A couple of things to note about this
        -   Your commit can be more than one sentence!
        -   The `#1` will be specially formatted on github to link to issue 1
        -   The keyword "resolves" will mean that when the issue is pushed onto
            the "main" branch, issue #1 will automatically close.
        -   To see a list of special keywords (close, fix, resolve & co), see
            <https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/using-keywords-in-issues-and-pull-requests>
    -   You can make a pull request interactively online via github
    -   You can also use the `gh` command line utility to do it from the command
        line with
    -   `gh pr create`
        -   Which is also interactive, but from the terminal, which is fun!
    -   (also see the `tldr` command line utility for giving helpful information
        on how to use certain command line tools: <https://tldr.sh/>)
    -   You can then go through the github website to merge the PR from your
        branch into main
    -   A note on "pull requests"
        -   I often thought it should be a "push request", but "push" is already
            used in git speak to mean pushing your code from your local computer
            to a remote computer (e.g., github)
        -   I think of "pull" as in you are requesting that the main branch
            pulls the code into the main branch. You are asking them to pull
            code in.
    -   Merge the pull request
        -   You can do this via the github website interactively
        -   Can also do this interactively via the terminal with
            `gh pr merge <pr_number>`
        -   Once you are done merging, you need to do a couple of steps locally
            -   change branch back to main
                -   `git checkout main`
            -   pull changes from main remote
                -   `git pull`
            -   Delete git branch remotely  + locally
                -   `git push origin -d <branc-name>`
                -   `git branch --delete <branch-name>`
        -   This is important for a couple of reasons
            -   keeping branches that have been merged already leaves you open
                to keep working on that branch even though it has been merged.
                This leads to committing to an already merged branch and
                strangeness follows.
            -   If you've got a bunch of branches hanging around locally it
                might not be clear which ones are important / alive, and they
                kind of get in the way.
        -   You can automate a bunch of these steps above using
            `usethis::pr_finish(<pr_number>)`
            -   This changes to main branch, pulls from main, and then deletes
                remote and local branches.

## Notes on using issues to track ideas / tasks

-   It's not always possible to break things down into discrete issues

-   Research tasks don't always align well with being able to have small
    discrete tasks

-   But it can be useful to think about these principles and think about how we
    can apply them. Striving towards these ideas can get you a lot of the way
    towards improving how you approach a problem.

-   If we can understand how we can apply these principles to our own work

-   Imagine "branches" or other ideas that require changes, try to get at the
    idea of "when to make a branch" in the context of a research workflow

# Other fun videos/resources

-   Video: [The Unreasonable Effectiveness of Plain
    Text](https://youtu.be/WgV6M1LyfNY?si=cwRfiIWyxHI9CByA)

-   Book: [Happy Git with R](https://happygitwithr.com/)

-   Website: ["Oh Shit, Git!?!"](https://ohshitgit.com/)  - heaps of
