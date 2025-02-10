# How to Contribute

This is a GitHub repo for the [Roar User Guide] in Markdown format using mkdocs.

The live documentation is hosted from the `main` branch. This branch is protected and 
changes can only be proposed via pull requests. This can be viewed at https://docs.icds.psu.edu

There is also a `staging` branch which is not push protected and can be viewed at https://docs.icds.psu.edu/staging
Any changes made to the `staging` branch will be incorporated into the site every 5 minutes. If the change 
does not show or the site becomes inoperable, it is likely due to an error in the code sent.


## Recommended Workflow:

To prevent conflicts with others, it is recommended to create your own fork of the repository and 
work on changes there. 

If you use your own fork, you can set up readthedocs to serve the site. Additional information on how to do this can be found here:

 - https://docs.readthedocs.io/en/stable/tutorial/
 - https://docs.readthedocs.io/en/stable/intro/getting-started-with-mkdocs.html


Or, you can preview these changes locally by following these steps:

1. Install necessary tools on your local machine
	- Python - https://www.python.org/downloads/release/python-3132/ 
	- mkdocs - https://www.mkdocs.org/user-guide/installation/
	- PyMdown - https://facelessuser.github.io/pymdown-extensions/installation/

1. Clone your repository fork (or create a new branch on the PSU-ICDS repo)
1. Commit desired modifications
1. Build the site: `mkdocs build`
1. Start the server: `mkdocs serve`
1. View the site in your browser: http://127.0.0.1:8000/en/latest/

Once you are satisfied with the changes, you can push them to the staging branch to view in place. Finally, 
submit a pull request to incorporate your changes into the main branch.

## Helpful links:

- https://www.mkdocs.org/user-guide/
- https://www.markdownguide.org/tools/mkdocs/

Converters:
- [HTML -> Markdown](https://www.browserling.com/tools/html-to-markdown)
- [HTML table -> Markdown](https://jmalarcon.github.io/markdowntables/)

[//]:<> (Admonition options: https://squidfunk.github.io/mkdocs-material/reference/admonitions/)
