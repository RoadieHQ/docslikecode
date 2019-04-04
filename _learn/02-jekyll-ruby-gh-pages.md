---
title: "Set Up Jekyll with Ruby"
layout: learn
image:
  path: /images/learn/jekyll-docs-page.png
  thumbnail: /images/learn/ruby-logo400x200.png
  caption: "Screenshot using Minimal Mistakes theme"
---

Jekyll is a Static Site Generator that typically accepts [Markdown](http://commonmark.org/help/) for authoring. [Jekyll](https://jekyllrb.com/) has its own documentation site and a [Quickstart](https://jekyllrb.com/docs/). To prepare your environment to build Jekyll sites locally, follow the instructions for either Windows or MacOS.

## Set up Ruby and Jekyll on Windows with Docker

On Windows, first install [Docker](https://docs.docker.com/docker-for-windows/) and [Git Bash](https://gitforwindows.org/), so that you are able to use Linux-based Docker images and commands. Then follow these steps to set up Jekyll and Ruby.

1. Open Git Bash.
1. Make sure that Docker commands run in Git Bash by checking the version value:
```
$ docker --version
```
1. Next, get a copy of the Jekyll Docker image that has all the gems for GitHub Pages deployment with this command:
```
$ docker pull jekyll/jekyll:pages
```
1. Now, you can run Jekyll with Ruby within the Docker image with one command, aliased and run in Git Bash.

Let's make an alias though so you can follow the rest of the commands in this instruction set. Open Git Bash and then set up Notepad as your default editor by typing:

```
$ git config core.editor notepad
```
Then, you can type this in Git Bash to edit the `.bash_profile` file in Notepad:
```
$ notepad .bash_profile
```

Or, open `.bash_profile` in the Vim editor if you prefer to remain in Git Bash:
```
$ vim .bash_profile
```
1. Next, copy these two commands into the `.bash_profile` file:
```
alias jekyll="docker run --rm --volume=$(pwd):/srv/jekyll -p 4000:4000  jekyll/jekyll:pages jekyll"
alias jekyll-serve="docker run --rm --volume=$(pwd):/srv/jekyll -p 4000:4000  jekyll/jekyll:pages jekyll serve --watch --incremental --force_polling"
```
1. Save the `.bash_profile` file and close the editor. On Vim, you save and close by entering command by pressing the **esc** key and then typing **colon*** + **w** + **q**, `:wq`, and then pressing **enter**.

When you start Git Bash the next time, the `.bash_profile` is automatically run and then the two commands, `jekyll` and `jekyll-serve` become available in Git Bash, run in Docker.

## Set up Ruby and Jekyll on Windows Subsystem for Linux

You must be running Windows 10 x64 Creators Update Home, Pro, or Enterprise (non-LTSB SKU) or later in order to install Windows Subsystem for Linux (WSL). Use the [WSL instructions](https://docs.microsoft.com/en-us/windows/wsl/about) to install WSL.

Then you can install Jekyll using the [Jekyll instructions for the Linux distribution you chose](https://jekyllrb.com/docs/installation/) such as [Ubuntu](https://jekyllrb.com/docs/installation/ubuntu/) or [Fedora](https://jekyllrb.com/docs/installation/other-linux/).

## Set up Ruby and Jekyll on MacOS

1. Install Homebrew. See the [Homebrew site](https://brew.sh) for instructions.
1. Use Homebrew to install a Ruby version manager.

   ```
   $ brew install rbenv ruby-build
   ```

1. Add rbenv to bash so that it loads every time you open a terminal.

   ```
   $ echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile
   ```

1. Source your `.bash_profile` file.

   ```
   $ source ~/.bash_profile
   ```

1. Install a specific version of Ruby.

   ```
   $ rbenv install 2.3.1
   $ rbenv global 2.3.1
   $ ruby -v
   ```

## Starting a Jekyll site

This [help page from GitHub](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/) provides a great starting point for building a Jekyll site. In our case, we have a specific theme, minimal-mistakes, that we want to use, so these instructions offer exact steps.

1. Install the Bundler gem, which helps with Ruby dependencies.

   ```
   $ gem install bundler
   ```
1. In the folder where you want to create the project, start with a new Jekyll build and use the `jekyll new` command. Use `.` to indicate you want it created in the current directory.
   ```
   $ jekyll new .
   ```
1. Take a look at the files created in the directory with an `ls` command:

```
$ ls -A
.gitignore	Gemfile		_config.yml	about.md
404.html	Gemfile.lock	_posts		index.md
```
1. Edit `_config.yml` in any text editor you like. Add these lines to ensure you use the Minimal Mistakes theme, and choose a color collection for the theme:

```
# Theme Settings
#
# Review documentation to determine if you should use `theme` or `remote_theme`
# https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#installing-the-theme

theme                  : "minimal-mistakes-jekyll"
# remote_theme           : "mmistakes/minimal-mistakes"
minimal_mistakes_skin    : "default" # "air", "aqua", "contrast", "dark", "dirt", "neon", "mint", "plum", "sunrise"

```
1. Also in the `_config.yml` file, edit the following:

* `title: "Site Title"`: Enter the title you want for the site that appears in the `<title>` tag.
* `name: "Your Name"`: Enter the name for the authorship and ownership of the site. Could be a company name or team name.
* `description: "An amazing website."`: Write a one-line description of the site and its purpose.

You can work on the rest of the settings as you continue to build out the site.
1. Move the root `index.md` file to `index.html` to work best with the Minimal Mistakes theme.
```
$ mv index.md index.html
```
1. Write any text you want to appear on the landing page, below the front matter, which indicates to the theme how to build the file.

```
---
layout: home
author_profile: true
---

Welcome to our site! Please take a look around at the content available.
```

1. In the `Gemfile` in the root directory, replace gem "jekyll" with:
```
gem "github-pages", group: :jekyll_plugins
```

1. Run `bundle update` and verify that all gems install properly.
```
$ bundle update
```
If you see an error, copy the error and enter it into Google to search for solutions to the error message.

> Note: If you are working on an already-set-up Jekyll site, run `bundle install` the first time you are in a Jekyll docs directory or when you need to pick up theme changes locally.

## Build a Jekyll site locally

Once you've prepared your environment, you can build locally and review the site in your browser.

1. Run the serve command.

   ```
   $ bundle exec jekyll serve
   Configuration file: /path/to/configuration/file/project-name/_config.yml
   Configuration file: /path/to/configuration/file/project-name/_config.yml
               Source: /path/to/configuration/file/project-name
          Destination: /path/to/configuration/file/project-name/_site
    Incremental build: disabled. Enable with --incremental
         Generating...
                       done in 22.964 seconds.
    Auto-regeneration: enabled for '/path/to/configuration/file/project-name'
   Configuration file: /path/to/configuration/file/project-name/_config.yml
       Server address: http://127.0.0.1:4000/
     Server running... press ctrl-c to stop.
   ```

1. Use the **Server address** URL  `http://127.0.0.1:4000/latest/` in a browser to preview the content.
   ![Example Jekyll site]( /images/learn/jekyll-docs-page.png)
1. Press `Ctrl+C` in the serve terminal to stop the server.
    > ***TIP***
    > Leave the serve terminal open and running. Every time you save changes to a file, it automatically regenerates the site so you can test the output as you write. That said, if you change the `_config.yml` file, you must stop (ctrl-c) and then re-run the serve command to see changes.

1. Don't forget to add the files to a commit and then commit the changes so that you can track the changes and work with others on GitHub. Refer to [Working with content in GitHub repositories](https://docslikecode.com/learn/04-add-content-workflow/).

## What's next

* [Working with content in GitHub repositories](https://docslikecode.com/learn/04-add-content-workflow/)
* [Continuous Deployment (CD) for Documentation Sites](https://www.docslikecode.com/learn/05-cd-for-docs/)
* [Set Up Automated Tests for Docs](https://www.docslikecode.com/learn/06-test-docs-as-code/)

## Evaluating options

* [Evaluating Static Site Generator themes](https://www.docslikecode.com/learn/07-evaluating-ssg-themes/)
* [Evaluating table layouts and formatting](https://www.docslikecode.com/learn/08-evaluating-table-layouts/)
* [Evaluating Static Site Generator search options](https://www.docslikecode.com/learn/09-ssg-search-implementations/)

## Additional references

* [Markdown reference](http://commonmark.org/help/)
* [Documentation Theme for Jekyll](https://idratherbewriting.com/documentation-theme-jekyll/)
* [Lynda.com Web foundations, GitHub Pages](https://www.lynda.com/Web-Development-tutorials/GitHub-pages/609031/654613-4.html)
* [Jekyll documentation about GitHub Pages](https://jekyllrb.com/docs/github-pages/)
