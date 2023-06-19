---
layout: post
title:  How to Get Jekyll Running locally?
date:   2023-06-14
categories: Eng
tags: HTML+CSS
---

## Life as a blogger before running jekyll locally


If you ever have a [Github](https://www.github.com){:target="_blank"} account, you must hear about [Github pages](https://pages.github.com/){:target="_blank"} and [jekyll](https://jekyllrb.com){:target="_blank"}. I'm just starting using these tools and are not quite familiar with the technical details, so forgive me if I said something wrong. In my rough understanding, Github provides users a function that it can turn the content of your repository to a website, and jekyll is the software running behind this function. 

Jekyll comes with a lot of website themes, but the most popular usage and themes of the jekyll powered website is for blogging. Jekyll recognized content must follow some rules and formats in order to be translated into a website. That being said, you don't need to know jekyll, nor do you have to run jekyll locally. You can just copy, or `fork` a jekyll theme or github, and set the `main` branch of that repository to run github pages. In most of the cases, you will see your copied theme website running at `yourusername.github.io/forkedname`. 

You can clone the repository to your computer, tweak the `_config.yml` file to customize your needs, and then you are pretty good to go. You can right away begin to write your first blog in the `_posts` folder, and then push it the repository. Depending on the time and workload of the github server, it usually takes anywhere between 1 to 5 minutes to rebuild the webste. Once you see the green tick before each push #code, you know the building is done succcessfully, and you can refresh your browser to see the updated website. 

That's the easiest way to start with a blog. I've been maintaining my blog pretty much like that for more than a year. But it also comes with a very obvious disvantage: due to the time lag between each change to the code and the rendering result, this work flow is very low efficient. 

Sooner or later, we have to come back to get jekyll generated website running locally first, then push the final result to the github. 

## A life saving post by Bill Raymond

First of all, let me express my highest respect to Bill Raymond, for his [life saving post](https://gist.github.com/BillRaymond/db761d6b53dc4a237b095819d33c7332){:target="_blank"} on how to run Jekyll on your computer locally. 

I don't know how other people handle this problem, but for me, I've been trying to run jekyll locally on my computer more than a year, but was frustrated to find one failure after another.

Why it's so hard to run jekyll on your computer? It's because jekyll runs on ruby, a program language, and jekyll also needs a lot of dependencies (another word for library, apps, and all kinds of other supportive softwares). What makes things even complicated is all these softwares comes with differenent versions, and not all versions work along together. 

I searched online for all posts about how to install jekyll and get it running, but none of them seems to work at all. It's a huge challenge to a greenhorn blogger like me to pick the right versions for ruby and jekyll, and collect all necessary dependencies. You just don't know which one you missed what will lead to a mistake warning, and you're stuck forever. 

## The key solution: Docker

Even if I tell you in the most detailed way of each step toward the establishment of a working environment for jekyll, you are destined to fail in 99% of the situations, because when you see the install instruction, the versions available online may be different due to version update, and any previous installed softwares on your computer also might easily compromise the whole effort. 

Bill comes around these pitfalls by using `Docker`. Using his method, I finally get jekyll running on my computer for the first time in past two years!

I can explain a bit more about `Docker` some day in a different post, here you just need to know that, `Docker` is to create a mini virtual environment, isolated from anything else on your computer, and Bill listed the right ruby, jekyll and all dependencies for us already. Running `Docker` is just like replicating an environment that has already been proved working on Bill's computer to yours. 

## Walking through from scratch

This walk through is a summary of Bill's post, you don't need to read the content below if you want to go straight to study [Bill's post](https://gist.github.com/BillRaymond/db761d6b53dc4a237b095819d33c7332){:target="_blank"}. 

The reason why I came up with this summary is that it's functioning as a study note. I omitted a lot of stuff in Bill's post that I'm already quite familiar with, so I can find the key points fast here. On top of that, I'm also afraid that Bill's post might be lost or deleted one day, so I treat this summary as a backup. 

### Preparation

- Go to [git-scm](https://git-scm.com){:target="_blank"} and download, install, and configure Git. MacOS comes with Git already, so for Mac user we don't need to worry much about it 
- Go to [visual studio code](https://code.visualstudio.com){:target="_blank"} and download and install the version of Visual Studio Code (VSC) for your operating system and chipset. When you have vs-code installed and running, you may also want to install two extensions, `docker` and `dev container`, both are developed by Microsoft.
- Go to [Github](https://github.com){:target="_blank"} and sign up for a free account. Make sure you can sign in completely before continuing
- Go to [Docker](https://docker.com){:target="_blank"} and download and install Docker Desktop for your operating system and chipset. Also, sign up for a Docker account and make sure you sign in with that account in Docker desktop

### Create a repository

This step is a little bit different from Bill's instruction, as I found it's easier and more straigher forward for me. I used to create an empty repository on github, and `git clone repository-url` to my computer. 

At this step, the only thing you need to pay attention to is giving the repository a fancy and easy to remember name. If you don't use third party hosting service like [Netlify](https://www.netlify.com/){:target="_blank"}, the repository name will company your blog for as long as it exists.

### Build docker

This is the most critical step to build a developing environment. First of all, you want to open the repository folder in vs-code, then create a new file in the root folder, named `Dockerfile`. Pleae be noted that this file doesn't have an extension name. Next, you just copy and paste all content in [this file](https://drive.google.com/file/d/1iovMX1uNVWhflaisow04z2AUkpu91wB4/view?usp=sharing){:target="_blank"} to `Dockerfile`, save and close it. 

Now you want to open the `Command Palette` in vs-code. Since you've installed docker extensions, you can now type `open folder in container`. Yes, you hear me right, you've already opened repository folder, but now you need to use this command to open it again. Why? because this command is telling computer to open the folder in docker container.

vs-code will ask you how to open? choose `from a dockerfile`, and then a lot of options will pop up, you don't need to choose any of them, but click `ok` to go aheard.

If you open the folder in container for the first time, it takes up some time, because the computer will be downloading all softwards and install them in the docker environment for you. In my case, I waited for almost 10 minute for the container being installed. 

Under the hood, the docker is building an image, you can simply understand it as the very environment that helps to set up all the dependencies required for Ubuntu and Ruby. It will also install Jekyll, but it will not create the Jekyll website.

After you open it once, it's pretty fast to open folder in container again. However, if you make some changes to the `Dockerfile`, you may want to open the `Command Palette` and type `rebuild` to create the docker environment again. 

### Run SH file

Up to now, we still don't have any website content in the folder. We will use jekyll to create one from us. But before that, we still need to run couple of commands in terminal. 

To make life easier for bloggers, Bill create a `sh` file for us. 

`sh`, or shell script, is a text file that contains one or more UNIX commands. You run a shell script to perform commands you might otherwise enter at the command line.

You can give the `sh` file any name you want, but to remind us that this file is to run after the docker image creation, and to run only once, name it [run-once-after-docker](https://drive.google.com/file/d/148ss8bB9usDLmVztFw-1B__FcdexyGgq/view?usp=sharing){:target="_blank"}. You want to copy all text in the linked text file, and create the same name file under root folder, with an extension name `.sh`. 

Next, Open the vs-code terminal window by pressing `CTRL` + `` ` ``, then type `sh run-once-after-docker.sh` and press return.

This `sh` file comes with very detailed comments. If you want to know what exactly each line of command means or what function are they going to realize, these comments give a good explanation, or point to the right direction for you to explore further. 

Now you must see there creates a lot of folders and files. You can push them to your github repositoary, and change the setting of pages to let github render them into a static website. Or, you can also run your site locally by typing the following command in the terminal:

```
bundle exec jekyll serve --livereload
```

## Conclusion

You may open your browser at local port to check tou the website. 

Just for your information, this very simple while elegant site is based on minima theme. I will constinue introduce what Bill said about the modification of the theme in another post.





