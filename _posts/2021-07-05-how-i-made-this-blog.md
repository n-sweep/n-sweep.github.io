---
layout:     post
title:      "How I Made This Blog With Github Pages, Jekyll and Docker"
date:       2021-07-05
categories: github-pages docker jekyll python github
---

Recently I learned how to use a `Dockerfile` to build custom Docker images and. After building an image based on Alpine Linux to run neovim and zsh for a consistent and portable text editor and python environment (I'll write about that soon), I wanted to document the process for my future self. Coincidentally, I had also recently read how easy it was to host a website with [Github Pages](https://pages.github.com/) and I just needed an excuse to learn how. It's all coming together.

---

# Hosting with Github Pages

> Note: I completed these steps on a `Pop!_OS 21.04` machine.

## First, Some Prerequisites
You will need Git and Docker installed. Later, we're going to use Docker to pull down a Jekyll image so we don't have to install Jekyll and all its dependencies. If you have trouble with these commands, check these installation links for [Git](https://github.com/git-guides/install-git) & [Docker](https://docs.docker.com/engine/install).

``` bash
# Update
sudo apt-get update

# Install Git
sudo apt-get install git-all

# Install Docker
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

## [Create](https://docs.github.com/en/get-started/quickstart/create-a-repo) A New GitHub Repository
If you don't know how, just visit the link above. Your repo should be named with your github username in the format `username.github.io` for GitHub to host it correctly.

## Clone the Repo and Add Some Content!
Next, move to the directory that you would like to store your site's files and clone the repo to your local machine. Navigate into the repo directory and create an index markdown file, which will serve as your site's home page, and finally push your changes back up to GitHub:

``` bash
# From pages.github.com

# Clone Repo
git clone https://github.com/username/username.github.io.git

# Navigate into project folder
cd username.github.io

# Create index.md
echo "C O N T E N T" > index.md

# Push changes
git add --all
git commit -m "initial commit"
git push -u origin main
```

<br />

## And You're finished!
Well done. Grab a cold beverage, pat yourself on the back, and visit **https://_username_.github.io** in a browser to view your handiwork.
 
<img src="{{ site.url }}/assets/images/content.jpg" />

### Looks Kinda Boring Though, Doesn't It?
Sure does. I'm no good at front end though, and rather than pretend otherwise we'll take GitHub's advice and use Jekyll, whatever that is.

---

# Adding Some Spice with a Jekyll Theme

From the GitHub [docs](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll):

> Jekyll is a static site generator with built-in support for GitHub Pages and a simplified build process. Jekyll takes Markdown and HTML files and creates a complete static website based on your choice of layouts...

I'm not familiar with Jekyll in the slightest, but I am familiar with Docker, and a quick trip to Docker Hub yields an official [Jekyll Docker image](https://hub.docker.com/r/jekyll/jekyll)! Now we can pull down the image and use Jekyll without installing it locally. Score.
