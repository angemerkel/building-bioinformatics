### Basic branching workflow

<https://git-scm.com/book/en/v2/Git-Branching-Branching-Workflows>

or

### gitHub workflow

= a simple workflow including feed back through pull requests

<https://docs.github.com/en/get-started/using-github/github-flow>

### git-flow

The initial workflow model git workflow developed in 2010 by Vincent Driessen

<https://www.gitkraken.com/learn/git/git-flow>

### biogit-flow

= an adaptation of the git workflow model extended to the development of bioinformatic pipelines

<https://pmc.ncbi.nlm.nih.gov/articles/PMC7921891/>

The management of the different bioinformatics pipeline versions is based on four different git branches:

-   **devel** contains the code of the current version under development.

-   **release** contains the code with both candidate and official releases. The release branch comes from the devel branch.

-   **hotfix** is a mirror of the release branch and is used to patch the code that is in production. If a critical bug occurs in production, this branch is used to fix the issue.

-   **master** is only used to archive the code from the release and hotfix branches. This branch is not used for development.

\_\_\_\_\_\_\_\_\_\_\_\_\_\_ master\
\\\_\_\_\_\_ release\
\\\_\_\_\_\_/ hotfix\
\\\_\_\_\_\_\_ devel\
\\\_\_\_local (feature)

Among these four branches, the release, hotfix and master are protected branches such that only the developers with the Maintainer role in the [GitLab](https://about.gitlab.com/) repository can directly push code on these branches (the other users have to use the GitLab merge request functionality to push on protected branches).

In addition to these four branches, the developer can create local branches to i) implement a new feature (the branch is named with a prefix feature plus any meaningful suffix) and ii) fix a bug in production or resolve a problem during the third step (these branches are either named with the prefix release or hotfix depending on the use case plus some relevant contextual information).

Testing\
\
*unit testing* = confirms that a piece of code provides the expected output according to the input parameters

*integration testing* = checks that the interfaces of the different bioinformatics pipeline components are consistent with each other and that the result of their integration allows the expected functionalities to be performed

*system (or functional) testing* = validates that the full bioinformatics pipeline works and fits well the end-user’s needs

*regression testing =* checks that the correction of bugs or the development of new functionalities did not introduce defects in unchanged areas of the bioinformatics pipeline.

*operational testing* (very important!) *=* to check that the bioinformatics pipeline provides the expected results on a reference dataset (golden dataset) in the production environment (systematically launched prior to any new analysis by the bioinformatics pipeline in the production environment to ensures that the results are reproducible as long as the exact same version of the bioinformatics pipeline is used)

see more at 'guidelines for software testing' ( [Hamburg & Mogyorodi, 2019](https://pmc.ncbi.nlm.nih.gov/articles/PMC7921891/#ref-3)).

## 
