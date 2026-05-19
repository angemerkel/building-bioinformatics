## GitHub

[**GitHub**]{.underline} is a **platform for hosting, managing, and collaborating on code using Git**.

-   it is a remote server where you can backup your code (git is distributed!))

-   it allows you easily collobarate and share your code (e.g. public repositories, code review and discussions via pull request and issues)

-   it allows you to manage your code using workflows and projects

-   it allows you to automioze workflows by using 'actions'

-   you can host webpages or blogs through 'pages'

-   being part of the microsost ecosystem in incoorportaes co-pilot and integrates with VS code and azure cloud

## GitHub pages

create a blog from markdown files and config yml's using jekyll and publish for free at github.

Personally, I prefer using quarto, since it feels more feature rich, and I am more acutomed to it after usinf R and rmds for data analysis.

## GitHub markdown

Markdown

Use markdown to on gitHub for

-   comments on [issues](https://docs.github.com/issues/tracking-your-work-with-issues/about-issues), [pull requests](https://docs.github.com/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests), and [discussions](https://docs.github.com/discussions/collaborating-with-your-community-using-discussions/about-discussions)

-   Files with the `.md` or `.markdown` extension (e.g. README.md)

Great markdown cheet sheet:

<https://github.com/adam-p/markdown-here/wiki/Markdown-Here-Cheatsheet>

## GitHub for code management

### **Pull request reviews**

A **pull request review** is feedback from other collaborators or community members on the proposed changes. It helps ensure quality and project momentum. Even more importantly, it's an awesome opportunity to learn more about the project and grow as a developer by seeing how others approach the problem.

Naturally, the best way to get a review is to ask for one. By assigning a reviewer, they get 3 options for providing feedback:

-   **Comment** - General feedback without approval or rejection.

-   **Approve** - Allows merging if [rulesets](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets), [code owners](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners), or other policies are enforced.

-   **Request Changes** - The proposed changes need do not meet expectations and need additional work. A review should be re-requested after the changes are made.

The **Files changed** tab is the primary place for collecting feedback. It allows for adding comments directly to lines before submitting a review.

#### **What does a review typically look like?**

1.  Reviewing the **title** and **description** are clear and concise. It should easily convey the intended changes and any associated issues.

2.  Reviewing the **Files changed** tab to ensure all proposed code matches the description.

3.  For most updates, try out the proposed change to verify they match the intention.

4.  Use the repository's [contributing guide](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/setting-guidelines-for-repository-contributors) for any guidance on review requirements, testing, quality verification, etc.

#### **Review ideas**

-   Identify potential issues, risks, and limitations.

-   Suggest changes and improvements.

-   Share awareness of upcoming changes that the pull request doesn't account for.

-   Ask questions to verify shared understanding.

-   Highlight what the author did well and what they should keep doing.

-   Prioritize the most important feedback.

-   Be concise *and* provide meaningful detail.

-   Treat the pull request author with kindness and empathy.
