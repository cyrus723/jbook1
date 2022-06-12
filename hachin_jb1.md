# how to create the Jupyter Book
###### Note: _the content here has been benefited from multiple sources, but mostly from jupyterbook.org_. Juyter Book is open-sourced by the [ExecutableBooksProject](https://executablebooks.org/en/latest/), "an international collaboration to build open source tools that facilitate publishing computational narratives using the Jupyter ecosystem."
ExecutableBooksProjct uses [several tools](https://executablebooks.org/en/latest/tools.html) for Jupyter book, including Sphinx, MyST, Jupyter Cache, Markdown-it-py. 
I also use the Dillinger which is a cloud-enabled, mobile-ready, offline-storage compatible, AngularJS-powered HTML5 Markdown editor.

[![N|Solid](https://jupyterbook.org/en/stable/_static/logo-wide.svg)](https://jupyterbook.org/en/stable/intro.html)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

My Texas State University web page is at [here](https://hachinyi.wp.txstate.edu).

**Jupyter Book** is a cloud-based publishing capability for any kinds of contents. Here, I am about to create the book for my students in Texas State University to teach Python, Finance, Economis, Data Science, Econometrics, and other subjects. 

### Install Jupyter Book
You can install Jupyter Book via pip:
**`pip install -U jupyter-book`**
or via conda-forge:
**`conda install -c conda-forge jupyter-book`**
This will install everything you need to build a Jupyter Book locally.

Jupyter Book comes bundled with a lightweight _sample book_ to help you understand a book’s structure. Again, this is just a sample book. Create a sample book by running the following command:
**`jupyter-book create mynewbook/`**

This will generate a mini Jupyter Book that you can both build and explore locally. It will have a few decisions made for you, and you can explore the configuration of the book in `_config.yml` and its structure in `_toc.yml`. Use this book as as a starting point to work from.

There are three things that you need in order to build a Jupyter Book, each of which was just created by running `jupyter-book create`:

1.  A configuration file (`_config.yml`)
2.  A table of contents file (`_toc.yml`)
3.  Your book’s content

A typical book strucuture looks like:
```sh
$ tree mybookname
mybookname/
├── _config.yml
├── _toc.yml
├── intro.md
├── logo.png
├── markdown-notebooks.md
├── markdown.md
├── notebooks.ipynb
├── references.bib
└── requirements.txt
```
### Build your book
Once you’ve added content and configured your book, it’s time to build outputs for your book. We’ll use the `jupyter-book build` command line tool for this.
```
jupyter-book build mybookname
```
**Important:** This will generate a fully-functioning HTML site using a static site generator. The site will be placed in the `_build/html` folder, something like this:
```
mybookname
 └──_build
    └── html
       ├── _images
       ├── _static
       ├── index.html
       ├── intro.html
       ...
```
These are the static files for a standalone website! They contain the HTML and all assets needed to view your book in a browser.
You can open the pages in the site by navigating to that folder and opening the html files with your web browser.

> key points

-   Jupyter Book uses markdown files to create chapters of an online book. In this tutorial, these files are placed in a directory called `mybookname`.
-   All the images used in the file should also be stored in `mybookname`.
-   References used in the book should be stored in a `references.bib` file, which should also be stored in book
-   A `_toc.yml` should be generated inside the folder book to structure the jupyter Book (toc is abbreviation for table of content)
-   With these files in place, you can create a minimal book using the command `$ jupyter-book build {path-to-book}`

### Create an online repository for your book
First, log in to GitHub, then go to the “create a new repository” page: https://github.com/new. Next, give your online repository a name and a description. Make your repository public and do not initialize it with a README file, then click “Create repository”.
> warning: 
-   **make sure that you log in github.com site first.**
-   you can watch the youtube by Chris Holdgraf which is really good becasue he is one of the founders/major contributors but the video drops some cmd commands that jupyterbook.org instruction. [His video is here.](https://jupyterbook.org)

Now, clone the (currently empty) online repository to a location on your local computer. You can do this via the command line with: However, the question is why not directly load the original directory to the GitHub site

```
git clone https://github.com/<my-org>/<my-repository-name>
```

Copy all of your book files and folders into this newly cloned repository. For example, if you created your book locally with jupyter-book create mylocalbook and your new repository is called myonlinebook, you could do this via the command line with:

```
cp -r mylocalbook/* myonlinebook/
```
Now you need to sync your local and remote (i.e., online) repositories. You can do this with the following commands:
```sh
cd myonlinebook
git add ./*
git commit -m "adding my first book!"
git push
```

### Publish your book online with GitHub Pages
We have just pushed the source files for our book into our GitHub repository. This makes it publicly accessible for you or others to see. So, it is saying that pushing all those source files into the GitHub site alone is not going to be sufficient. You need to go through `ghp-import` process. 

Next, we’ll publish the build _artifact_ of our book online, so that it is rendered as a website.

The easiest way to use GitHub Pages with your built HTML is to use the `ghp-import` package. `ghp-import` is a lightweight Python package that makes it easy to push HTML content to a GitHub repository.

`ghp-import` works by copying all of the contents of your built book (i.e., the `_build/html` folder) to a branch of your repository called gh-pages, and pushes it to GitHub. The gh-pages branch will be created and populated automatically for you by ghp-import. To use `ghp-import` to host your book online with GitHub Pages follow the steps below:

Note

Before performing the below steps, ensure that HTML has been built for each page of your book (see the previous section). There should be a collection of HTML files in your book’s `_build/html` folder.

Install ghp-import
```
pip install ghp-import
```
Update the settings for your GitHub pages site:

a. Use the gh-pages branch to host your website.

b. Choose root directory / if you’re building the book in it’s own repository. Choose /docs directory if you’re building documentation with jupyter-book.

From the main branch of your book’s root directory (which should contain the `_build/html` folder) call `ghp-import` and point it to your HTML files, like so:
```
ghp-import -n -p -f _build/html
```
> Warning

Make sure that you included the `-n` - this tells GitHub not to build your book with ==Jekyll==, which we don’t want because our HTML is already built! If you do not do this you may see 404 not found for your deployed content.
 

 
Typically after a few minutes your site should be viewable online at a url such as: `https://<user>.github.io/<myonlinebook>/`. If not, check your repository settings under `Options -> GitHub Pages` to ensure that the `gh-pages` branch is configured as the build source for `GitHub Page`s and/or to find the url address GitHub is building for you.

To update your online book, make changes to your book’s content on the main branch of your repository, re-build your book with `jupyter-book build mybookname/` and then use `ghp-import -n -p -f mylocalbook/_build/html` as before to push the newly built HTML to the gh-pages branch.



----------------

------------------

---------------


```
e = mc^2
```





X^2^
$$\sqrt{k}$$
Inline: $\sqrt{k}$
|Left |Center|Right|
|:-----|:----:|----:|
|1 |A |C |
|2 |B |D |




- Type some Markdown on the left
- See HTML in the right
- ✨Magic ✨
- 
## Features

- Import a HTML file and watch it magically convert to Markdown
- Drag and drop images (requires your Dropbox account be linked)
- Import and save files from GitHub, Dropbox, Google Drive and One Drive
- Drag and drop markdown and HTML files into Dillinger
- Export documents as Markdown, HTML and PDF

Markdown is a lightweight markup language based on the formatting conventions
that people naturally use in email.
As [John Gruber] writes on the [Markdown site][df1]

> The overriding design goal for Markdown's
> formatting syntax is to make it as readable
> as possible. The idea is that a
> Markdown-formatted document should be
> publishable as-is, as plain text, without
> looking like it's been marked up with tags
> or formatting instructions.

This text you see here is *actually- written in Markdown! To get a feel
for Markdown's syntax, type some text into the left window and
watch the results in the right.

## Tech

Dillinger uses a number of open source projects to work properly:

- [AngularJS] - HTML enhanced for web apps!
- [Ace Editor] - awesome web-based text editor
- [markdown-it] - Markdown parser done right. Fast and easy to extend.
- [Twitter Bootstrap] - great UI boilerplate for modern web apps
- [node.js] - evented I/O for the backend
- [Express] - fast node.js network app framework [@tjholowaychuk]
- [Gulp] - the streaming build system
- [Breakdance](https://breakdance.github.io/breakdance/) - HTML
to Markdown converter
- [jQuery] - duh

And of course Dillinger itself is open source with a [public repository][dill]
 on GitHub.

## Installation

Dillinger requires [Node.js](https://nodejs.org/) v10+ to run.

Install the dependencies and devDependencies and start the server.

```sh
cd dillinger
npm i
node app
```

For production environments...



## Plugins

Dillinger is currently extended with the following plugins.
Instructions on how to use them in your own application are linked below.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |


## License

MIT

**Free Software, Hell Yeah!**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
