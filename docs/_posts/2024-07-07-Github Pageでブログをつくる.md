---
layout: post
title:  "Github Pageでブログをつくる"
date:   2024-07-07 21:44:59 +0900
categories: posts
---


### newRepository
1. Githubで新リポジトリを作成。

### Repository:Settings
1. Githubの上部メニューから`Settings`を選択。
2. サイドパネルのCode and automationから`Pages`を選択。
3. 「Build and deployment」の「Source」で`Github Actions`を選択。
4. （たしか`github-pages`というActionを選択した気がします。スクショし忘れ）
5. `.github/workflows/jekyll-gh-pages.yml`というファイルが作成されます。

### Repository
1. mainブランチに`_post`ディレクトリを作り
2. その中に`yyyy-mm-dd-title.md`という感じの（e.g. `2024-07-07-sample.md`）ファイルを作ります。

後は自動でActionが実行され、`https://ユーザ名.github.io/リポジトリ名`にサイトが公開されます。

**まだサイトホームができてないので、アクセスしてもなにも見れません。**

## Jekyll
このままではデフォルト設定のままなので、設定を変更していきます。

### Github Pagesアクション設定
`.github/workflows/jekyll-gh-pages.yml`を変更します。

`docs`ディレクトリ配下にソースを置くように設定します。

```yml
# Sample workflow for building and deploying a Jekyll site to GitHub Pages
name: Deploy Jekyll with GitHub Pages dependencies preinstalled

on:
  # Runs on pushes targeting the default branch
  push:
    paths:
      - "docs/**" # 変更点
    branches: ["main"]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      - name: Setup Pages
        uses: actions/configure-pages@v5
      - name: Build with Jekyll
        uses: actions/jekyll-build-pages@v1
        with:
          source: ./docs  # 変更点
          destination: ./_site
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### Jekyll設定
`docs/_config.yml`を新規作成します。

中身はこんな感じです。
```yml
title: サイトタイトル
description: >- 
  サイトの説明
baseurl: "/レポジトリ名"
url: "/https://ユーザ名.github.io"
github_username:  ユーザ名

timezone: Asia/Tokyo
encoding: utf-8

# Build settings
theme: minima
plugins:
  - jekyll-feed

markdown: kramdown
kramdown:
  syntax_highlighter: coderay
```

### サイトホームを設定
`docs/index.md`を新規作成します。中身は以下。
```md
---
layout: home
---
```

### Repository2
[Repository](#Repository)で`_post`ディレクトリを作りましたが、`docs`ディレクトリ配下に移動しましょう。

`docs/_posts`配下に`yyyy-mm-dd-title.md`という感じで記事を書いていきます。

あとはCSSを変更する方法ですが、とりあえず備忘録的に書くのはこれで十分ということでおわり。
