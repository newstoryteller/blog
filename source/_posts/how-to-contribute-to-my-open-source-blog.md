---
title: 博客已完全开源欢迎修改和添加你的故事！
date: 2022-01-16 14:48:49
tags:
- github
- open source
- tutorial
- hexo
- 教程
---

## Welcome to my blog
Hello, I'm *p1slave* and this is my personal blog to document my fetish life online and I do not wish to reveal my identity on the internet. I have been using VPN and proxy to hide my traces even with fake names when browsing the websites and pushing my commits here. Please don't try to figure out who I am but you are welcome to share your stories with the rest of the world freely by sending pull requests to this repo [**p1slave/blog**](https://github.com/p1slave/blog) or even start your own blog. 


## Make contribution
You are welcome to follow the instructions and post new stories about the following topics:

* Stories about your fetish and BDSM related experience. 
* Interesting dating experience outside your own bubble with people from different countries and cultures.
* Discussion and your in-depth thoughts on some controversial topics about special relationships or general relationships.
* Anything valuable for the betterment of humanity that you want to spread to more audiences and persist it with distributed storage on Github. 
* Trump's latest nude photos? Why not? You can directly add photos to `source/images` without publishing a post at all. I may quote your photos one day:)

<!-- more -->

Preferably, the stories you write should be very detailed followed by your own thoughts, reflections, analysis, photos or even videos but do not leak any personal information unless you intentionally want to be famous. 

I hope you can publish your stories here because eventually I will build a fetish forum exclusively for all the well-mannered lovely kinksters I love to hear from and I will automate the migration of your blog posts to the new website so you don't have to copy and paste your stories one by one to a new place. 

Note that your story will be added to my blog immediately once your PR is merged into the master branch if you follow the instruction to make contribution to my repo. If you see typos and errors in the existing posts and blog, feel free to send PR to correct them too. The pen sign on the upper right corner of each blog post is the editing link of that post on Github so you can directly make changes on Github rather than clone the repo locally. 


## Git config for your alt life
 I want to make my repo public so everyone can fork my repo and add their own stories to my blog. Therefore, I have to be extra cautious about my privacy and I cannot use the same username and email from my normal life because my alt life will shock many people in my real life. The following commands will change your contact info globally if you are working on a complete new laptop or VM for your alt life blog writing.
```
git config --global user.name "p1slave"
git config --global user.email "yourname@yourmail.com"
```

However, I don't want to switch machines and choose to set my alt life username and email specifically only for this repo so I put the git configuration file in `/git-config/config` and I can just replace `/.git/cofig` with this file to avoid the horrible accident when I use my alt life username and push commits to my daily work repo. 

The other tricky thing is that this blog is hosted under a different GitHub account with different SSH keys but Windows may still use the default `id_rsa` private key and fail to authenticate.

A workaround to solve this issue is to add the following one line `sshCommand = ssh -i ~/.ssh/id_ed25519_xxx` to the git configuration file so now we specify which key we want to use instead of the default key.

The complete git configuration is below:
```
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        symlinks = false
        ignorecase = true
        sshCommand = ssh -i ~/.ssh/id_ed25519_xxx
[user]
        name = p1slave
        email = xxx@yourmail.com
[remote "origin"]
        url = git@github.com:p1slave/blog.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
        remote = origin
        merge = refs/heads/master
```

What if we want to clone the repository for the first time? The solution is to add the same `sshCommand` as parameter when cloning the repository. The complete clone command will be:
```
git clone git@github.com:p1slave/blog.git --config core.sshCommand="ssh -i ~/.ssh/id_ed25519_xxx"
```

## Installation and testing
I'm not an expert on Nodejs and the installation of conflicted dependencies could be a nightmare sometimes. Try to use a Node Package Manager like [nvm](https://github.com/nvm-sh/nvm) and switch back to a previous version of Node if a newer version of some packages does not work.

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

# Download and use the latest version of Node
nvm install node
nvm use node
# Download and use a previous version of Node
nvm install 8
nvm use 8
```

Install all dependencies in `package.json`:
```bash
npm install
```

Install the Hexo command line tools from [Hexo](https://hexo.io) globally:
```bash
npm install hexo-cli -g
```

Run Hexo blog locally with commands:
```bash
# Run in linux or MacOS environment and add `npx` before your commands in Windows
hexo server # or `hexo s`
```

Generate a new post if you have a new story to share. The post title should start with `external-contribution-` and please follow the naming convention of my other blog posts for the rest of your post title. The Chinese version of your post title should start with `XXX投稿 - 你的文章标题` to be consistent. 

```bash
# Here is a good example for naming
hexo new post external-contribution-yourname-crushed-under-the-ass-of-some-goddesses 
```

After the execution of the command above, a new Markdown post file will be created in `_posts` folder and inside `_post` folder there is another folder with the exact same name of your post to hold assets. Put your photos and videos in the corresponding folder and they can be accessed directly in your post without specifying the relative path.

Add the following code block to the end your blog post for showing some multimedia assets. For example, if you have four pictures and choose the third layout to group pictures, you write `{% grouppicture 4-3 %}` followed by `{% asset_img xxx.jpg %}` for each picture you add to the group. No need to specify the path since the photos are put into the asset folder. 

```bash
{% grouppicture 4-3 %}

{% asset_img 1.jpg %}
{% asset_img 2.jpg %}
{% asset_img 3.jpg %}
{% asset_img 4.jpg %}

{% endgrouppicture %}
```

The complete documentation about how to use tags can be found in [Next theme](https://theme-next.js.org/docs/tag-plugins/group-pictures.html) and the official [Hexo tags](https://hexo.io/docs/tag-plugins). You can easily add and render some Youtube links with `{% youtube xxx_id %}` or even tabs and buttons, etc. There are a lot of goodies for you to explore if you try to play around with [Hexo plugins](https://hexo.io/plugins/) from the Hexo ecosystem or even you may want to write your plugins at some point.


## Deployment
I deploy my blog to [Netlify](www.netlify.com) with 100GB bandwidth for free and actually don't have to do anything for the deployment. Every time I push the latest commits to my repo, the webhook will automatically pull the latest commit from master branch to Netlify and build the blog. Netlify even builds your blog for every pull request and provides a preview link. It's the best solution I found so far and hope I don't have to pay extra money once I have more visitors and traffic beyond 100GB.  

If your pull request is merged into the master branch but you accidentally commit a photo of you holding your dick and ID card, you are screwed because you cannot reverse the commit without my permission. Send me an Github issue, email or DM immedicately and I will help you to take it down before more people see it. Be careful about the things you want to post online because now anyone can access and analyze the information. Don't tell your friends in your real life about your alt life unless you are ready to take the risk.
