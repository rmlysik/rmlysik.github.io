---
title: Migrating from WordPress to Jekyll
categories:
- Jekyll
tags:
- Ruby
- Jekyll
- Workpress
- WSL
- GitHub Pages
comments: []
---
I decided to do some clean-up of this blog and migrate off of WordPress in the process. The site is now hosted on [GitHub Pages](https://pages.github.com/ "GitHub Pages") and uses [Jekyll](https://jekyllrb.com/ "Jekyll"){:target="_blank"} for static site generation.

The following sections explain the steps I took to do this migration.

### Backup WordPress Site

First, I logged in to my existing WordPress site and did a full backup and export, this includes the MySQL database as well as the static site files, such as images, associated with the posts.

I then imported the WordPress database into a MySQL instance on my local Windows machine using MySQL Workbench. 

### Enable Windows Subsystem for Linux

Jekyll requires the Ruby development environment, and although there is a description for how to [install via RubyInstaller](https://jekyllrb.com/docs/installation/windows/#installation-via-rubyinstaller "Install via RubyInstaller"), the better option appears to be to use the Windows Subsystem for Linux and [install via bash](https://jekyllrb.com/docs/installation/windows/#installation-via-bash-on-windows-10 "Install via Bash on Windows 10"), if possible. 

Since I'm using a Windows 10 machine for development the [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about "Windows Subsystem for Linux"){:target="_blank"} is available and is easy enough to enable.

To enable [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10 "WSL"){:target="_blank"}, run the following PowerShell command as administrator, and then restart the computer when prompted.

{% highlight powershell %}
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
{% endhighlight %}

Once WSL has been enabled, you can then install your Linux distribution of choice using the Windows Store app. In my case, I chose to install the Ubuntu LTS distro.

### Install Jekyll and Import Posts from WordPress

Now that WSL is enabled and Ubuntu has been installed, it should be possible to [install Jekyll via the WSL bash prompt](https://jekyllrb.com/docs/installation/windows/#installation-via-bash-on-windows-10 "Install Jekyll via Bash on Windows 10").

Update repo lists and packages:

`sudo apt-get update -y && sudo apt-get upgrade -y`

Install Ruby:

{% highlight shell %}
sudo apt-add-repository ppa:brightbox/ruby-ng
sudo apt-get update
sudo apt-get install ruby2.5 ruby2.5-dev build-essential dh-autoreconf
{% endhighlight %}

Update Ruby gems:

`gem update`

And finally, install Jekyll:

`gem install jekyll bundler`

**NOTE**: I ran into an issue with permissions when running `gem update` and `gem install jekyll bundler`. In order to fix this the following lines had to be added to the end of my .bashrc file as described [here](https://jekyllrb.com/docs/troubleshooting/#no-sudo){:target="_blank"}.

{% highlight shell %}
# Ruby exports

export GEM_HOME=$HOME/gems
export PATH=$HOME/gems/bin:$PATH
{% endhighlight %}

Now that Jekyll was up and running, I ran `jekyll new blog` and then changed directory into the newly created blog folder.

Jekyll provides utilies to import posts from other blogging systems, such as WordPress. In order to use the import utility for WordPress, I first needed to install some additional gems:

`gem install unidecode sequel mysql2 htmlentities` 

I could now import the posts from WordPress using the `jekyll-import` utility as described [here](https://import.jekyllrb.com/docs/wordpress/).

{% highlight shell %}
ruby -r rubygems -e 'require "jekyll-import";
    JekyllImport::Importers::WordPress.run({
      "dbname"         => "[database-name]",
      "user"           => "[user-name]",
      "password"       => "[password]",
      "host"           => "127.0.0.1",
      "port"           => "3306",
      "socket"         => "",
      "table_prefix"   => "wp_",
      "site_prefix"    => "",
      "clean_entities" => true,
      "comments"       => true,
      "categories"     => true,
      "tags"           => true,
      "more_excerpt"   => true,
      "more_anchor"    => true,
      "extension"      => "html",
      "status"         => ["publish"]
    })'
{% endhighlight %}

**NOTE**: ipaddress, rather than 'localhost', seems to work for the host setting. I was able to connect to the MySQL instance running in Windows from the WSL environment.

This command extracts the posts from the WordPress database and creates a folder named _posts. Each post consists of a file with an .html extension and contains the YAML front-matter at the top of the page with post title, author, tags, etc. The remainder of the file consists of the post content in HTML markup.

I also copied all the image files that I had exported from WordPress to a new `/images/posts/` folder within the blog folder in WSL.

### Editing Posts with Visual Studio Code

I could use VIM to edit the posts from the command line, but I'd really prefer to use a tool like Visual Studio Code. Thankfully, there is the [Remote - WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl "Remote - WSL") extension for VS Code that allows you to open a folder in the Windows Subsystem for Linux from VS Code running under Windows.

As described on the Remote - WSL extension page:

> Remote - WSL runs commands and extensions directly in WSL so you don't have to worry about pathing issues, binary compatibility, or other cross-OS challenges. You're able to use VS Code in WSL just as you would from Windows.

I decided to rename the files in the _posts folder using the .md extenstion and reformat manually using [Markdown](https://daringfireball.net/projects/markdown/basics "Markdown") using global search and replace. Much of this can be quickly done, but links and image tags require some extra care. The path to the image files had changed since I had moved all the images under an `/images/posts/` folder. I also went through each of the links and tested them out. Most had been upgraded to use HTTPS since I had first posted the blog entries. Surprisingly, most links were still valid, or required only minor modifications.

The end result is a very satisfying easy to read post using Markdown with no distracting HTML syntax.

I was then able to test the result by running `jekyll serve` in the WSL bash prompt, and view the result in my browser.

Once I was satisfied with the conversion to Markdown, I did a `git init` within the blog folder, followed by `git add .` and `git commit -m "Initial version"`. 

**NOTE**: Before you add files with git, make sure you have a .gitignore file, mine contains:

{% highlight shell %}
_site
.sass-cache
.jekyll-cache
.jekyll-metadata
vendor
{% endhighlight %}

You definitely don't want to add the generated output in the _site folder to your repository.

### Create GitHub Pages Repo

To create a [GitHub Pages Site](https://help.github.com/en/github/working-with-github-pages/creating-a-github-pages-site "Create a GitHub Pages Site"), create a new repository in your GitHub account named *{username}.github.io*, or in my case: rmlysik.github.io.

Now that the GitHub repo had been created, I could add it as a remote for the blog repo: 

`git remote add origin https://github.com/rmlysik/rmlysik.github.io.git`

followed by:

`git push` 

to upload the committed changes.

### Configure Custom Domain

Since I already had a domain registered for my previous WordPress blog, I figured I would transfer this over to the GitHub pages site after I had gotten it working. This was also very straightforward, as described [here](https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site "Managing a Custom Domain for Your GitHub Pages Site"). 

I chose to configure a subdomain as the custom domain using 'www.robertlysik.com' as the subdomain.

The only hitch appeared to be that I had previously registered my domain for [HSTS](https://hstspreload.org/ "HSTS"), and initally I was getting certificate errors. I couldn't enable SSL immediately for the GitHub pages site after configuring the custom URL, I was told I needed to wait 24 hours. But the next day, I was able to tick the box to enable SSL, and that fixed the issues I was having. 

### Final Thoughts

Although there's a bit of setup involved, I like the fact that my entire blog is now under version control and I don't have any additional requirements, such as a database and blogging application to maintain. It's very easy to edit the posts using VS Code, and Markdown is a lot cleaner and faster to work with than HTML. I can preview my changes locally in a browser while running `jekyll serve` in my WSL bash prompt, and it's just a matter of a `git push` to deploy my changes to the site. 