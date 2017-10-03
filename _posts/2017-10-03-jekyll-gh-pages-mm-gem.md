---
title:  "Howto: Create a blog with Jekyll, Github pages, Minimal Mistakes gems"
categories: 
  - Jekyll
  - Github
  - Minimal Mistakes
tags:
  - blog
---

Trying to build a blog. Clone repo unbelievably messy. Gem seems like a good idea
undocumented...

```bash
# Clone and enter repo
git clone git@github.com:${USER}/${REPONAME}.git
cd ${REPONAME}

# Create gh-pages branch.
# Github seems to enable the gh-pages automatically
# if repo has this branch
git branch gh-pages
git checkout gh-pages
git push --set-upstream origin gh-pages

# Clone repo again within the repo and move it to
# _site folder (that's where Jekyll will generate)
# the webpage
git clone git@github.com:${USER}/${REPONAME}.git
mv ${REPONAME} _site
cd _site
git checkout gh-pages
cd ..
echo _site > .gitignore
```

Now that we're finished setting up the repo structure, we can begin adding the
minimal mistakes theme and first content. The original [asfd](http://www.google.com)


