# wavether.com website

This website is built with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/getting-started/), which is a theme for [MkDocs](https://www.mkdocs.org/getting-started/)

## Install Python 3 and dependencies

### Python 3

There are many ways to install Python 3 depending on your OS and setup. For macOS, see [Installing Python 3 on Mac OSX](https://docs.python-guide.org/starting/install3/osx/). Verify you have Python 3 installed by

```bash
$ python --version
Python 3.12.2
```

### Dependencies

All dependencies are specified in [requirements.txt](requirements.txt), and they can be installed by using `pip`:

```bash
$ pip install -r requirements.txt
```

### Build and serve from your working copy

Use the `mkdocs` command-line tool and run from the root directly of the repo:

```bash
$ mkdocs serve -s
INFO    -  Building documentation...
INFO    -  Cleaning site directory
INFO    -  Documentation built in 0.30 seconds
INFO    -  [12:51:09] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO    -  [12:51:09] Serving on http://127.0.0.1:8000/
```

Then you can access the site from http://127.0.0.1:8000/. The tool also monitors file changes and automatically rebuild.

The `-s` option enables strict mode, which will check spelling (see [below](#spelling-check-and-known-words)) and throw out errors among other things.

Passing `-o` option to `mkdocs serve`, e.g. `mkdocs serve -s -o` will open the website in your default browser after the initial build finishes.

## Customizations

- [extra.css](docs/stylesheets/extra.css) defines some customizations of colors from the default Material theme.
- Unlike normal mkdocs contents written in Markdown, the [homepage](docs/overrides/home.html) and [aboutus](docs/overrides/about.html) pages are written in HTML with stylesheets defined in [pages.css](docs/stylesheets/pages.css) and [about.css](docs/stylesheets/about.css). To change the meta data such as the pages' titles, however, you still need to update the markdown files [index.md](docs/index.md) and [about.md](docs/about.md).
- Navigation is defined in [mkdocs.yml](mkdocs.yml) under the `nav` section.

## Spelling check and known words

In Github workflow [checks.yml](.github/workflows/checks.yml), we use mkdocs strict build mode, which will perform spelling checks. If your PR fails the check, you'll need add the words that are legit to [known_word.txt](docs/known_words.txt) and update your PR.

## Gotchas

1. Sometimes the social cards are not re-built locally in development environment when you change the meta info. Remove the `.cache` folder in the root directory would force rebuild of the assets:

   ```bash
   $ rm -rf .cache
   $ mkdocs serve
   ```

   Our CD pipeline always build from fresh so this shouldn't be a problem for production deployments

2. To preview or debug social cards, you can use [socialsharepreview.com](https://socialsharepreview.com/browser-extensions) which offer an online debugger as well as a browser extension for Firefox or Chrome.
