# How to Contribute

This is a GitHub repo for the [Roar User Guide] in Markdown format using mkdocs.

The live documentation is hosted from the `main` branch. This branch is protected and 
changes can only be proposed via pull requests. This can be viewed at https://docs.icds.psu.edu

There is also a `staging` branch which can be viewed at https://docs.icds.psu.edu/staging
Any changes made to the `staging` branch will be incorporated into the site every 5 minutes. If the change does not show or the site becomes inoperable, it is likely due to an error in the code sent.


## Recommended Workflow:

To prevent conflicts with others, it is recommended to create your own fork of the repository and 
work on changes there. 

You can preview changes locally by following these steps:

1. Install necessary tools on your local machine
	- Python - https://www.python.org/downloads/release/python-3132/ 
	- mkdocs - https://www.mkdocs.org/user-guide/installation/
	- PyMdown - https://facelessuser.github.io/pymdown-extensions/installation/

1. Clone your repository fork (or create a new branch on the PSU-ICDS repo)
1. Commit desired modifications
1. Build the site: `mkdocs build`
1. Start the server: `mkdocs serve`
1. View the site in your browser: http://127.0.0.1:8000/en/latest/

Once you are satisfied with the changes, create a pull request to the staging branch. Once the PR is approved and merged, 
the changes will be reflected in the staging site.

Once the changes are approved and checked via the staging portal, submit a pull request to the main branch to have the changes integrated into the live site.

## Helpful links:

- https://www.mkdocs.org/user-guide/
- https://www.markdownguide.org/tools/mkdocs/

Converters:
- [HTML -> Markdown](https://www.browserling.com/tools/html-to-markdown)
- [HTML table -> Markdown](https://jmalarcon.github.io/markdowntables/)

[//]:<> (Admonition options: https://squidfunk.github.io/mkdocs-material/reference/admonitions/)
