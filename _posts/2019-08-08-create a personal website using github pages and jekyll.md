---
# layout: post
author: Henry
topic: Geek
comments: true
---

This is a guide to help you setup your personal website using Github Pages and jekyll.

What do you need for a personal website?
- some webpages.
- a server.

Webpages are some HTML that defines the content of your website.

A server will host your website so that anybody can get access to it through the internet.

Github Pages allow you create a repository with the name of your accountname.github.io, if you put some HTML files on that repository and push it to github. It will generate your website for you, __for free__!

---

### 1. setup Github Pages

Following content will tell you how to setup Github Pages (the server side) and create a simple HTML page. The content are directly copied from [Github Pages](<https://pages.github.com>)\[1\]

1. Head over to GitHub and create a new repository named username.github.io, where username is your username (or organization name) on GitHub.

2. Go to the folder where you want to store your project, and clone the new repository.
   ```bash
   git clone https://github.com/username/username.github.io
   ```

3. Enter the project folder and add an index.html file.
   ```bash
   cd username.github.io
   echo "Hello World" > index.html
   ```

4. Add, commit, and push your changes:
   ```bash
   git add --all
   git commit -m "Initial commit"
   git push -u origin master
   ```

5. Fire up a browser and go to https://username.github.io.
   
   Actually, be patient as there might be a delay : )

---

### 2. build your local website

Now, you should be able to see you website hosted by github. The next step is to create your website pages  and setup you blog.

What do you need for your webpages?
- HTML for web content
- CSS for style, like layout and formatting.

Jekyll is a powerful tool in a sense that you don't need to know much about HTML or CSS for your website. It's default theme will work fine for the style. And the cool part is that you can write webpages in Markdown. Jekyll will generate the HTML for you.

I would recommand you go through the [install guide](https://jekyllrb.com/docs/installation/) and [jekyll tutorial](https://jekyllrb.com/docs/step-by-step/01-setup)\[1\] for a step by step setup. I will list a few keypoints here for your reference.

1. install the environment for jekyll.

   install Ruby >= 2.4

   note that Ubuntu user might need to add repository
    
   ```bash
   sudo apt-add-repository ppa:brightbox/ruby-ng
   sudo apt-get update
   sudo apt-get install ruby2.6 ruby2.6-dev
   sudo apt-get build-essential zlib1g-dev
   ``` 
   Then follow [the guide for ubuntu](https://jekyllrb.com/docs/installation/ubuntu/).

2. go through the tutorial to setup your website.
   1. [Ruby 101](https://jekyllrb.com/docs/ruby-101/) will give you an idea what it can do. You can follow this quick demo to get a template website with just a few lines of commands.
   2. After seeing the pattern at [Ruby 101](https://jekyllrb.com/docs/ruby-101/), you can start to build your own website. Go to your local clone of your website repository, follow the [step by step tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/) to setup your website.

      It major contain the following contents

      - create a simple site
      - adding a few pages
      - make a navigation bar for all pages
      - adding style
      - adding blogs
      - organizing blogs by author (I did this by topic)
      - deploy your website

      A few comments would be.

      - you can choose some [nice themes](https://github.com/pages-themes), and even change them, check the github pages for the theme for more information.
      - for each file you generated in this repo, look for their corresponding file in [Ruby 101](https://jekyllrb.com/docs/ruby-101/), you may copy some of the contents (\_\_config.yml, Gemfile) and try to understand them.

---

### 3. adding comments to your posts

I think allowing interaction would be important for feedback, thus this part is added. If you definitely want to find the best solution for you, check this post for reference. [A post about different methods of hosting comments](https://darekkay.com/blog/static-site-comments/).

I pick the easiest one, using Disqus.

Here are the steps:

- go to register an account in Disqus.
- [accociate your website shortname](https://disqus.com/admin/create/) with your account, notice that this step cannot be changed once set.
- add templates to your website
  - choose Jekyll as your platform.
  - copy the Embedded code to "comments.html" in your \_includes folder. You might want to uncomment some field here, check [this post](https://desiredpersona.com/disqus-comments-jekyll/) for reference, it use '\{\{ page\.url absolute\_url \}\}' for both PAGE\_URL and PAGE\_IDENTIFIER.
  - add {% raw %} {% include comments.html %} {% endraw %} to your \_layouts/post\.html
  - wrap the include statement with {% raw %} {% if page.comments %} ... {$ endif %} {% endraw %} so that you can decide if you want comments in each post by setting comments: true or comments: false.
  - you can hide your comment by default, which make it load faster. Check out [this post](https://esc.sh/blog/load-disqus-on-click/).
  - add a field in your post header "comments: true" to the posts you want the comments.

---

### 4. next step

You have already had a nice website here, the most important thing should be blogging, to organize your knowledge and contribute to the community.

But there are a few things you can do also.

- update you github profile with you website.
- link your github page to the website.
- try out some [nice themes](https://github.com/pages-themes) offered by jekyll. [Hacker](https://github.com/pages-themes/hacker) is the one I am using, which is dark for eye care :p
- blogging and more.

---

### Reference:

[1] <https://pages.github.com>

[2] <https://jekyllrb.com/docs/step-by-step/01-setup>

[3] <https://github.com/pages-themes/hacker>