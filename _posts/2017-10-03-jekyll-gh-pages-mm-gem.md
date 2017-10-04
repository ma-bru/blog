---
title:  "Howto: Create a blog with Jekyll, Github pages, Minimal Mistakes gems"
categories:
  - Howto
tags:
 - Jekyll
 - Github
 - Minimal Mistakes
 - Blog
 - Howto
 - Ruby
 - Bundler
---
Some time ago. I started a blog using Github pages and Jekyll.
Since I didn't like any of the default [themes](https://pages.github.com/themes/) I decided to use the modern and clean [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/) theme.
Back then (and unfortunately still today when using a Github user/organization page), in order to use the theme, it was necessary to fork the [repo](https://github.com/mmistakes/minimal-mistakes) and modify the relevant files.
I stronlgy disliked doing this.
Forking and modifying repos should imho only be done if you want to modify the theme and plan to give back some of your modifications.
For just using it it's inconvenientJust using it is not a good enough reason.
As expected, this method only worked until I first tried to update the theme, got overwhelmed by merge conflicts and basically lost interest in the maintenance.

Recently I noticed, that Minimal Mistakes is now available as a ruby gem.
This seems to be a much saner option, since theme and content/configuration are clearly seperated eliminating the risk of a repeated merge desaster.

## Github pages

There's two types of github pages, user/organization pages and project pages.
The difference is, that for each user (or organization), there can be only one
user page served at `https://<USER>.github.io`. Furthermore, the page is automatically
built from the master branch of the corresponding repo (`https://github.com/<USER>/<USER>.github.io`).
Which limits you to either use one of the supported themes, or commit all of the themes files in
your repo.
As mentioned earlier, in order to keep upgrading the theme easy, this is not an option for me.

The other option is a project page. There you can choose to publish your page from the `master`
or `gh-pages` branch or from a `docs` subfolder in your master branch. I'll use the gh-pages
method, since that way commit messages for updated content are seperated from commits that update
generated files.

## Setting up Ruby and Bundler
First choose a directory where gem/bundler should install the ruby dependencies (`GEM_HOME`).
Then install bundler if not already on the system:

```bash
export GEM_HOME=${USER}/.gem
export PATH=${GEM_HOME}/bin:${PATH}
gem install bundler

```

## Setting up the repo
First off all, log in to Github and create a new repo. We'll refer to this repo
by REPONAME later. Start by cloning the repo on your harddrive: 

```bash
# Clone and enter repo
git clone git@github.com:${USER}/${REPONAME}.git
cd ${REPONAME}
REPOPATH=`pwd`
```
Then create the gh-pages branch. Once it's created, github will automatically
use it to serve it's content under `https://USER.github.io/REPO/`:

```bash
git branch gh-pages
git checkout gh-pages
git push --set-upstream origin gh-pages
```
The next step is not strictly necessary, but it will later simplify the release
process:
```bash
# Clone repo again within a `_site` foler within the repo
# (that's where Jekyll will generate) the webpage
cd ${REPOPATH}
git clone git@github.com:${USER}/${REPONAME}.git _site
echo _site > .gitignore
cd _site
git checkout gh-pages
```
Note, that instead of cloning the repo and checking out the gh-pages branch in
the `_site` folder, you could as well clone it somewhere else and manually copy the
generated files over. Or use the `--destination` flag when running jekyll:
```bash
cd ${REPOPATH}
bundle exec jekyll build --destination /path/to/gh-pages/branch
```
## Adding the theme, configuration and release
Now that we're finished setting up the repo structure, we can begin adding the
minimal mistakes theme and first content. The original [description](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/) is unfortunately not too verbose about how to setup your page.
Personally, I think it's the easiest, to just download the files from the minimal mistakes
[example folder](https://github.com/mmistakes/minimal-mistakes/tree/master/test)
to the repo:

```bash
cd ${REPOPATH}
wget https://raw.githubusercontent.com/mmistakes/minimal-mistakes/master/test/_config.yml
wget https://raw.githubusercontent.com/mmistakes/minimal-mistakes/master/test/Gemfile
wget https://raw.githubusercontent.com/mmistiakes/minimal-mistakes/master/test/index.html
# Remove the relative path for the jekyll theme in the Gemfile:
sed -i 's%gem "minimal-mistakes-jekyll", path: "../"%gem "minimal-mistakes-jekyll"%g' Gemfile
# Use bundler to install dependencies
bundler install
```

Afterwards execute:
```bash
# Build and release the webpage
bundle exec jekyll build
cd _site
git add -A
git commit
git push
```
to build and publish your page. you can check your page at: "https://USER.github.io/REPO/".
As you can see some resources can't be found and the page looks broken. To fix
this, we need to adjust some lines in the _config.yml file
```
url : "https://<USER>.github.io"
baseurl : "/<REPO>"
```
and build and release (as above).

The last thing that is missing, is of course a first post. You can find examples
[here](https://mmistakes.github.io/minimal-mistakes/year-archive/) and the corresponding
md files [here](https://github.com/mmistakes/minimal-mistakes/tree/master/test/_posts).
To start with one of the examples create a "_posts" folder and download one example:

```bash
mkdir _posts
cd _posts
wget https://raw.githubusercontent.com/mmistakes/minimal-mistakes/master/test/_posts/2016-02-24-welcome-to-jekyll.md
```

In order to locally test your generated page you can use:
```bash
bundle exec jekyll serve --incremental -destination /tmp/page
```
If you don't add the "-destination" flag, jekyll will overwrite the contents
of your "_site" folder. Which is not a problem per se, but might lead to problems
if you accidentaly push it to github. (The site.url will be overwritten with localhost)
