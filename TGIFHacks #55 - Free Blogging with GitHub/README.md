# TGIFHacks #55 - Free Blogging with GitHub

This is a tutorial that guides you through building a blog with Hugo and GitHub Pages. For the slides I used, you can download it [here](https://github.com/ntuoss/Workshops/raw/master/TGIFHacks%20%2355%20-%20Free%20Blogging%20with%20GitHub/slides.pdf).

## Installing Hugo

Here we'll only cover how to install `hugo` on Ubuntu since we'll be using the Cloud9 platform. If you would like to install it on your own computer, please refer to this [link](https://gohugo.io/overview/installing/).

First, we download the package with the following command

```bash
$ wget https://github.com/spf13/hugo/releases/download/v0.16/hugo_0.16-1_amd64.deb
```

Then we install the downloaded package to our system

```bash
$ sudo dpkg -i hugo*.deb
```

Now you should have `hugo` installed, type in the following command to check your installation

```bash
$ hugo version
# Hugo Static Site Generator v0.16 BuildDate: 2016-06-12T08:47:29Z
```

## Building your blog with Hugo

This section tells you how to actually use `hugo` to build your blog.

### Creating a new site

The first thing we need to do is to create our website, go to the folder where you want to store your website and type in the following command

```bash
$ hugo new site my-blog
```

This will create a folder in your current directory named `my-blog` and you will see some files generated by `hugo` in that folder.

```
[my-blog]/
├── [archetypes]/
├── config.toml
├── [content]/
├── [data]/
├── [layouts]/
├── [static]/
└── [themes]/
```

### Choosing a theme

Now that you have a site, the next thing you should do is to pick a theme for your site. Go to [Hugo Themes Site](https://themes.gohugo.io) to find a nice-looking theme for your blog! For our example here, we'll pick the [Hemingway theme](http://themes.gohugo.io/hemingway/). Type the following commands to install the theme to your site

```bash
$ git clone https://github.com/tanksuzuki/hemingway.git themes/hemingway
```

### Configure your theme

Every theme needs some kind of configuration to make it fully functional. For example, you need to set the title of your website. Optionally, you can set thinkgs like your copyright notice, your Google Analytics key, your Disqus shortname for adding a comment section, and some links to your other sites (e.g. GitHub, Twitter).

Here in our case, we need to set up the title and our base URL to make it work. Add the following lines in `config.toml`

```toml
baseurl = "http://replace-this-with-your-hugo-site.com"
title = "Hemingway"
```

### Adding a post

Now you have your site and your theme, you need to put in some contents! Let's create a post for our blog with the following command

```bash
$ hugo new post/hello-world.md
```

You should see that now there is a file in `content/post` named `hello-world.md`

Open that file, and write something inside. The file uses the Markdown syntax. If you don't know any Markdown, don't worry! Plain text will work!

After you finish writing a post, you should run a test server first to see how your site looks like. Type in the following command (when using Cloud9, remove bind and port otherwise)

```bash
$ hugo server --theme=hemingway --bind=$IP --port=$PORT 
```

Now you can check out your site at `http://replace-this-with-your-hugo-site.com`. If you think your site looks good, you wanna undraft that post (it's a draft by default). Type in the following command to undraft it

```bash
$ hugo undraft content/post/hello-world.md
```

### Generating your blog

Ok, now you have everything you need to generate the actual website. And it's surprisingly easy. Just type in the following command

```bash
$ hugo --theme=hemingway
```

After the website code is generated, it should be within the `public` folder.

## Uploading your blog to GitHub Pages

Great, now you already have your blog generated, you wanna put it somewhere on the Internet. GitHub Pages is a great place, because it's completely free. To make it happen, first create a repo named `<your GitHub username>.github.io` (don't initialize it!). Then go to the `public` folder generate by Hugo and type in the following command.

```bash
$ git init
$ git remote add https://github.com/<your GitHub username>/<your GitHub username>.github.io.git
$ git add .
$ git commit -m "add my blog"
$ git push origin master
```

After a few seconds, your site should be available at `http://<your GitHub username>.github.io`.
