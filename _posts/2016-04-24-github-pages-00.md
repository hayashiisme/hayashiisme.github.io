---
layout: post
title:  "GitHub Pages導入: 概略"
date:   2016-04-24 19:00:00 +0900
categories: github-pages install
---

WordPressの代替として使えるCMSを検討してみて、Jekyllがよさそうに思えたのが事の発端。
調べてみると、GitHubのリポジトリがそのままサイトになるGitHub Pagesというのがあって、これがJekyllで動いている。

なら、最終的には自前のサーバや各種ホスティングサーバ上に構築するにせよ、
ひとまずgithub上に一つサイトを立ち上げてgitを使ってローカルのコンテンツ作成環境を構築してみるのが早道。
というわけで、learning by doing the GitHub Pagesとあいなる。

ローカルのリポジトリ上でJekyllを動かしてテストまでした上で、GitHub Pagesにプッシュして公開する、という流れ。

GitHub PagesとJekyllの組み合わせでどうサイトが作れるかは[Aboutページ](https://help.github.com/articles/about-github-pages-and-jekyll/)にざらっと書いてある。

構築だが…、

[Jekyllのホームページ](http://jekyllrb-ja.github.io)には、

```````````````````````````````````````

~ $ gem install jekyll
~ $ jekyll new my-awesome-site
~ $ cd my-awesome-site
~/my-awesome-site $ jekyll serve
# => http://localhost:4000 を見てください

```````````````````````````````````````

とあって、えらく簡単そうに書いてあるが、Rubyの2.x.xが必要で、Debian/UbuntuだとまずRubyからインストールしなければいけなかったりして、ちと前段階がある。
どんな感じかてばやく知りたいので、以下のストーリーで進めてみた。

1. 自分のGitHub上にGitHub Pagesを作成
1. デフォルトでruby 2.0.0p481が入ってるOS X Mavericks上にクローンする
1. Jekyllの環境を構築してGitHub Pagesにプッシュ
1. Debian/Ubuntu(をメインとしてサブでWindowsも)のローカルリポジトリでもコンテンツ作成できるようにする
1. GitHub Pages以外のサイトへの導入を試す

というわけで、まずクローンできるGitHub Pagesを作る。

## github.com上にGitHub Pagesのリポジトリを作成する

[GitHub Pagesについてもっと知る](https://pages.github.com)ためのページに行って言われるままに手を動かしていく。

サイトには`User or organization site`と`Project site`の2種類あって、`Project site`は公開のリポジトリをサイト化するものらしい(後で検討)。`User or organization site`が今回の目的に合致した道だ。

その示すところに沿って行く。

### リポジトリを作る

***username***.github.io(***username***はgithubのユーザ名)という名前のリポジトリを作る。
Bitbucketなんかとも同じ方式だな。

ローカルにクローンして、ターミナルからしこしこgitコマンドを打つ。
ページインストラクションをコピペ。

````````````````````````````````````````````

~ $ git clone https://github.com/username/username.github.io
~ $ cd username.github.io
~/username.github.io $ echo "Hello World" > index.html
~/username.github.io $ git add --all
~/username.github.io $ git commit -m "Initial commit"
~/username.github.io $ git push -u origin master

````````````````````````````````````````````

***username***.github.ioリポジトリができた。



***→ 「[GitHub Pages導入: OS Xから作成](github-pages-01.html)」へ続く***

