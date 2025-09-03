# Editing the Wiki

This wiki uses [mkdocs-material](https://squidfunk.github.io/mkdocs-material/) to generate the site html from markdown files.

If you would like to add or edit content on this site, first make sure you are familiar with how to use Git and GitHub. If you are new to Git, check out our [Git & GitHub Workshop](workshops/git-github.md).

To make changes, follow these steps:

1. Create a branch of the [wiki repository](https://github.com/ubieee/wiki).
2. Make your changes (add/edit markdown files in `docs/`). Use Visual Studio Code or your favorite text editor.
    - If you add a new page, make sure to add it to the `nav:` section of `mkdocs.yml` so it shows up in the site navigation.
    - To add abbreviations, add them to `includes/abbreviations.md`.
    - For markdown syntax help, see this [markdown guide](https://www.markdownguide.org/basic-syntax/).
    - To learn about mkdocs-material features, see the [mkdocks-material reference](https://squidfunk.github.io/mkdocs-material/reference/).
3. To preview the site, you must first [install mkdocs-material](https://squidfunk.github.io/mkdocs-material/getting-started/#installation), then [serve the site locally](https://squidfunk.github.io/mkdocs-material/creating-your-site/#previewing-as-you-write).
4. Commit your changes and push your branch to GitHub.
5. Create a pull request to the `main` branch of the wiki repository on GitHub.
6. At least one other club member should review your changes, then approve and merge the pull request.
7. After merging, your changes should show up on the site in a few minutes.

