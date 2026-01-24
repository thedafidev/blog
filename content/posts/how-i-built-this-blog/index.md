---
date: '2026-01-24T16:48:27+01:00'
title: "How I built this blog"
description: "A concise, practical guide to creating and serving a Hugo blog locally."
tags: ["hugo", "hosting", "git"]
categories: ["guides"]
cover: "cover.png"
---

## Scope

This post documents the steps you can follow to build a similar blog as fast as possible and serve it locally. It focuses on getting started only.

Not covered:
- Deployment (Cloudflare Pages example explained in [this post]({{< relref "posts/deploy-on-cloudflare-pages" >}}))
- Analytics

## Prerequisites

- Own a computer

## Setup

### Install Hugo

On Fedora install Hugo from the package manager:

```bash
sudo apt update
sudo apt install hugo
```

The package may be outdated (happened to me when trying to install it), in this case you can install the latest version from GitHub:

```bash
VERSION=0.154.5
wget https://github.com/gohugoio/hugo/releases/download/v${VERSION}/hugo_extended_${VERSION}_linux-amd64.deb
sudo dpkg -i hugo_extended_${VERSION}_linux-amd64.deb
```

`hugo` package is available on most Linux distributions. If you're not on Linux you may want to first [install Linux](https://www.wikihow.com/Install-Linux) (just kidding, Hugo is available for [Windows and MacOS](https://gohugo.io/installation/) too)

### Git and VS Code

Install `git` and [VS Code](https://code.visualstudio.com/):

```bash
sudo apt install git
sudo snap install --classic code
```

More VS Code installation options: https://code.visualstudio.com/docs/setup/linux

## Create the site

### Create a new Hugo site

Create a site:

```bash
hugo new site blog --format=yaml
cd blog
git init
```

### Add the Hugo Narrow theme

I used the [Hugo Narrow](https://hugo-narrow-docs.vercel.app/) theme and its example site as a configuration reference

```bash
git submodule add https://github.com/tom2almighty/hugo-narrow.git themes/hugo-narrow
```

The theme's `exampleSite/` folder contains a working configuration you can adapt.

## Project configuration

### VS Code recommendations

Add recommended extensions in `.vscode/extensions.json` to make editing Hugo projects smoother:

```json
{
    "recommendations": [
        "gydunhn.hugo-essentials"
    ]
}
```

### Useful .gitignore entries

Add a `.gitignore` file at the root of the project to ignore generated files and OS-specific Hugo binaries:

```gitignore
# Generated files by Hugo
/public/
/resources/_gen/
/assets/jsconfig.json
hugo_stats.json

# Executables that might be added to repo by mistake
hugo.exe
hugo.darwin
hugo.linux

# Temporary lock file while building
/.hugo_build.lock
```

## Development workflow

### Create your first post

Use Hugo's new command to create a draft post:

```bash
hugo new posts/my-first-post.md
```

This creates a new file under `content/posts/` with front matter you can edit.

### Serve the site locally

Preview your site while developing with the built-in server:

```bash
hugo serve -D
```

Then visit [http://localhost:1313/](http://localhost:1313/)

## Version control

### Push to a remote repository

When you're ready to track the project in Git and push to a remote git server if you have any:

```bash
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/your-username/blog.git
git branch -M main
git push -u origin main
```

## Next steps

- Configure `config.yaml`/`config.toml` to match your site settings
- Explore the theme's `exampleSite` for various examples
- Deploy: Cloudflare Pages deployment is covered [here]({{< relref "posts/deploy-on-cloudflare-pages" >}})

## Resources

- [Hugo documentation](https://gohugo.io/documentation/)
- [Hugo Narrow documentation](https://hugo-narrow-docs.vercel.app/)
- [Source code of this blog](https://github.com/thedafidev/blog)
