---
layout: post
title:  "GitHub Pages導入: OS Xから作成"
date:   2016-04-24 19:21:00 +0900
categories: github-pages install
---

次は、"[Setting up your GitHub Pages site locally with Jekyll](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/)"である。


## Jekyll付きのGitHub Pagesをローカルで設営する

前述の通り、Jekyllを動かすには、Ruby 2.0.0 or higherがインストールされていないといけない。
また言われるままに手を動かす。


### Bundlerをインストール

要sudoだった。

`````````````````````````````

# sudo gem install bundler
Fetching: bundler-1.11.2.gem (100%)
Successfully installed bundler-1.11.2
Parsing documentation for bundler-1.11.2
Installing ri documentation for bundler-1.11.2
1 gem installed

`````````````````````````````

### BundlerでJekyllをインストール

`~/username.github.io`に`Gemfile`を作って中に以下を書く。


`````````````````````````````````````````

source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins


`````````````````````````````````````````

ターミナル作業。


````````````````````````````````````````````

~/username.github.io $ bundle install
Fetching gem metadata from https://rubygems.org/............
Fetching version metadata from https://rubygems.org/...
Fetching dependency metadata from https://rubygems.org/..
Resolving dependencies.......
Rubygems 2.0.14 is not threadsafe, so your gems will be installed one at a time. Upgrade to Rubygems 2.1.0 or higher to enable parallel gem installation.

Your user account isn't allowed to install to the system Rubygems.
  You can cancel this installation and run:

      bundle install --path vendor/bundle

  to install the gems into ./vendor/bundle/, or you can enter your password
  and install the bundled gems to Rubygems using sudo.

(パスワード入力)
Installing RedCloth 4.2.9 with native extensions
Installing i18n 0.7.0
Installing json 1.8.3 with native extensions
Installing minitest 5.8.4
Installing thread_safe 0.3.5
Installing addressable 2.4.0
Installing coffee-script-source 1.10.0
Installing execjs 2.6.0
Installing colorator 0.1
Installing ffi 1.9.10 with native extensions
Installing multipart-post 2.0.0
Installing gemoji 2.1.0
Installing net-dns 0.8.0
Installing public_suffix 1.5.3
Installing sass 3.4.22
Installing rb-fsevent 0.9.7
Installing kramdown 1.10.0
Installing liquid 3.0.6
Installing mercenary 0.3.6
Installing rouge 1.10.1
Installing safe_yaml 1.0.4
Installing jekyll-feed 0.5.1
Installing mini_portile2 2.0.0
Installing jekyll-paginate 1.1.0
Installing jekyll-sitemap 0.10.0
Installing rdiscount 2.1.8 with native extensions
Installing redcarpet 3.3.3 with native extensions
Installing terminal-table 1.5.2
Using bundler 1.11.2
Installing jekyll-textile-converter 0.1.0
Installing tzinfo 1.2.2
Installing coffee-script 2.4.1
Installing ethon 0.8.1
Installing rb-inotify 0.9.7
Installing faraday 0.9.2
Installing jekyll-sass-converter 1.3.0
Installing nokogiri 1.6.7.2 with native extensions
Installing activesupport 4.2.6
Installing jekyll-coffeescript 1.0.1
Installing typhoeus 0.8.0
Installing listen 3.0.6
Installing sawyer 0.7.0
Installing html-pipeline 2.4.0
Installing jekyll-watch 1.3.1
Installing octokit 4.3.0
Installing jekyll 3.0.4
Installing github-pages-health-check 1.1.0
Installing jekyll-gist 1.4.0
Installing jekyll-github-metadata 1.11.1
Installing jekyll-mentions 1.1.2
Installing jekyll-redirect-from 0.10.0
Installing jekyll-seo-tag 1.3.3
Installing jemoji 0.6.2
Installing github-pages 75
Bundle complete! 1 Gemfile dependency, 54 gems now installed.
Use `bundle show [gemname]` to see where a bundled gem is installed.
Post-install message from html-pipeline:
-------------------------------------------------
Thank you for installing html-pipeline!
You must bundle Filter gem dependencies.
See html-pipeline README.md for more details.
https://github.com/jch/html-pipeline#dependencies
-------------------------------------------------
Post-install message from github-pages:
---------------------------------------------------
Thank you for installing github-pages!
GitHub Pages recently upgraded to Jekyll 3.0, which
includes some breaking changes. More information:
https://github.com/blog/2100-github-pages-jekyll-3
---------------------------------------------------


``````````````````````````````````




``````````````````````````````````

~/username.github.io $ bundle exec jekyll new . --force
New jekyll site installed in /Users/hayashiisme/GitHub/hayashiisme.github.io. 

``````````````````````````````````


以下のようなフォルダ構成ができあがる。


``````````````````````````````````

-rw-r--r-- Gemfile
-rw-r--r-- Gemfile.lock
-rw-r--r-- _config.yml
drwxr-xr-x _includes
drwxr-xr-x _layouts
drwxr-xr-x _posts
drwxr-xr-x _sass
-rw-r--r-- about.md
drwxr-xr-x css
-rw-r--r-- feed.xml
-rw-r--r-- index.html

``````````````````````````````````

コンテンツをどう作成するかは置いといて、ローカルでサーバを立ちあげてサイトを確認する。


``````````````````````````````````

~/username.github.io $ bundle exec jekyll serve
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.

``````````````````````````````````

## GitHub Pagesにプッシュ

いつもの手順。


``````````````````````````````````

~/username.github.io $ git add -A
~/username.github.io $ git commit -am "comment"
~/username.github.io $ git push


``````````````````````````````````

`http://username.github.io/`で確認できる。



***→ 「[GitHub Pages導入: OS Xから作成](github-pages-01.html)」へ続く***


