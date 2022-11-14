---
title: "How to Create a Static Website Using Hugo"
date: 2022-11-12T18:20:05-06:00
# weight: 1
# aliases: ["/first"]
tags: ["#how-to", "#hugo"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: true
description: ""
canonicalURL: "https://blog.darrelpol.com/posts/how-to-create-a-static-website-using-hugo"
disableHLJS: true # to disable highlightjs
disableShare: true
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
editPost:
    URL: "https://github.com/poldarreldev/darrelpol.dev/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---
Hello, everyone! Today, I'm gonna talk about how to create a static website using Hugo. It's the first blog for my "***How to start blogging using Amazon S3 and Amazon CloudFront***" series.

Hugo is a framework for building static websites. Actually, I'm using it for this blog where you are reading right now. Using its CLI is just so easy and there are a lot of free themes that we can use. Also, it's open-source, so you don't have to pay anything to use it. You can find more about Hugo framework on their website, [https://gohugo.io/](https://gohugo.io/).

Before we can start using Hugo, let's first make sure we have the correct packages and libraries installed on our machine. For this tutorial, I'll be using the Windows Subsystem for Linux (WSL) but it should also apply if you're using macOS. 

## **Step 1: Install Brew (skip this step if you've already installed Brew on your machine)**
To install Hugo, we first have to install Brew on our machine. 
### **Update packages and repositories available on your WSL**
```
sudo apt update
```

### **Install tools required to set up Brew**
```
sudo apt-get install build-essential curl file git
```

### **Install Homebrew**
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

By default, you will not be able to run Brew without switching to the directory where you installed it. To use it anywhere on your machine, we need to tell WSL about Brew by adding it to your bin. You can do that by executing the following commands one at a time on your machine:
```
test -d ~/.linuxbrew && eval $(~/.linuxbrew/bin/brew shellenv)
```

```
test -d /home/linuxbrew/.linuxbrew && eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)
```

```
test -r ~/.bash_profile && echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.bash_profile
```

```
echo "eval \$($(brew --prefix)/bin/brew shellenv)" >>~/.profile
```

To verify that Brew has been installed on your machine, execute this command:
```
brew --version
```

Output should be something like this:
```
Homebrew 3.6.10
Homebrew/homebrew-core (git revision a7105e7b92c; last commit 2022-11-11)
```

You can visit [Homebrew on Linux](https://docs.brew.sh/Homebrew-on-Linux) website to troubleshoot any problems you may encounter during the installation. 

## **Step 2: Install Hugo**
Assuming that all is well during the Step 1, or you've already installed Brew on your local, we can now install Hugo by executing this command:
```
brew install hugo
```

To verify that Hugo is indeed installed, execute this command:
```
hugo version
```

It should respond with something like this:
```
hugo v0.105.0+extended linux/amd64 BuildDate=unknown
```

According to their website, it should state that it is **extended**. If it does not, uninstall it and try another installation method.

## **Step 3: Create a New Site**
If you're here, then you have probably installed Hugo on your machine. We can now create our website. The following command will create a new site in a folder named `blog.darrepol.com`:
```
hugo new site blog.darrepol.com -f yml
```
**NOTE:** Use `-f` to select `YML` format

The output should be something like this:
```
Congratulations! Your new Hugo site is created in /mnt/c/apps/blog/how to/blog.darrepol.com.

Just a few more steps and you're ready to go:

1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".

Visit https://gohugo.io/ for quickstart guide and full documentation.
```

## **Step 4: Add a theme**
What I really like about Hugo is that you can select from a list of themes on the market for FREE! (at least from what I've seen so far). For this demo, I'll be using a theme called "PaperMod". To start, we have to first make sure that we're inside our Hugo site by running this command:
```
cd blog.darrepol.com
```

Add the PaperMod theme as a submodule by executing these commands:
```
git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
git submodule update --init --recursive # needed when you reclone your repo (submodules may not get cloned automatically)
```

The response should be something like this:
```
Cloning into '/mnt/c/apps/blog/how to/blog.darrepol.com/themes/PaperMod'...
remote: Enumerating objects: 128, done.
remote: Counting objects: 100% (128/128), done.
remote: Compressing objects: 100% (110/110), done.
remote: Total 128 (delta 25), reused 54 (delta 12), pack-reused 0
Receiving objects: 100% (128/128), 248.20 KiB | 1.77 MiB/s, done.
Resolving deltas: 100% (25/25), done.
```

**NOTE:** If you get an error `fatal: not a git repository`, it means you're executing `git` command on a non git folder. So, make sure you execute `git init` first before executing `git submodule` command.

To update the theme, execute `git submodule update --remote --merge`. You can usually find the updates about your selected theme by going to their GitHub repository. In this case, we can find update for PaperMod by going to [hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod). 

Once the theme is added as a submodule for your site, add the following on your `config.yml`:
```
theme: "PaperMod"
```
You can also copy the PaperMod's sample `config.yml` [here](https://github.com/adityatelange/hugo-PaperMod/wiki/Installation#sample-configyml)

## **Step 5: Add your first content**
Now that we have our new Hugo site and have selected a theme, we can now start writing our first content. The following command will create `my-first-post.md` on the `/content/posts` folder:
```
hugo new posts/my-first-post.md
```

The response should be something like this:
```
Content "/mnt/c/apps/blog/how to/blog.darrepol.com/content/posts/my-first-post.md" created
```

Open the file with your favorite editor, and you should see something like this:
```
---

title: "My First Post"

date: 2022-11-12T16:41:41-06:00

draft: true

---
```

The properties you see between the three hyphens are metadata. Writing text after this metadata will be displayed on your page. Let's say you want to write, "Hello, world! This is my first content.", it should look like this:
```
---

title: "My First Post"

date: 2022-11-12T16:41:41-06:00

draft: true

---

Hello, world! This is my first content.
```

**NOTE:** Posts in Hugo uses Markdown Syntax. Not really sure if there are themes that uses different syntax, but you can find a guide here [https://www.markdownguide.org/basic-syntax/](https://www.markdownguide.org/basic-syntax/)

## **Step 6: Start your server**
Now that we have everything set up, we can now start our server and see our first blog on our browser. Execute this command to start the Hugo server:
```
hugo server -D
```

The response should be something like this:
```
Start building sites …
hugo v0.105.0+extended linux/amd64 BuildDate=unknown
                   | EN
-------------------+-----
  Pages            |  4
  Paginator pages  |  0
  Non-page files   |  0
  Static files     |  0
  Processed images |  0
  Aliases          |  0
  Sitemaps         |  1
  Cleaned          |  0

Built in 11 ms
Watching for changes in /mnt/c/apps/blog/how to/blog.darrepol.com/{archetypes,content,data,layouts,static}
Watching for config changes in /mnt/c/apps/blog/how to/blog.darrepol.com/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
```

By looking at the response, your website should be available at http://localhost:1313/:
![sample-running-hugo-server-D](/sample-running-hugo-server-D.png)

And voilà! You now have your own static website. **Congratulations**! 

**But wait**, there's still a lot more to do if you want your website to be accessible by other people over the internet. On my next blog, I'll talk about [how to host your static website using Amazon S3](../how-to-host-static-website-using-amazon-s3). For now, I recommend you exploring other themes or other Hugo features so that when you are ready to share your website to the people of the internet, you will have your favorite theme, customized with your name and texts! Bye for now, and I hope this helps! 

\- Darrel Pol