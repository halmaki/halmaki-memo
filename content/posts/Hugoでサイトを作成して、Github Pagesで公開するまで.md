---
date: "2025-04-01T21:30:00+09:00"
title: "Hugoでサイトを作成して、Github Pagesで公開するまで"

description: ""
tags: [
  'Hugo',
]
---

## Hugoをインストールする

公式の[インストール手順](https://gohugo.io/installation/)に従ってインストールを行う<br>
テーマによってはsassが必要になるので一緒にインストールする

### mac
Homebrewを使用してインストール
```bash
brew install hugo sass/sass/sass
```

サイトのディレクトリを作成
```bash
hugo new site SITE_NAME
```

サイトのディレクトリに移動する
```bash
cd SITE_NAME
```

Gitで管理するので
```bash
git init
```

## テーマを導入&設定

[テーマ一覧](https://themes.gohugo.io/)から好きなテーマを探す<br>
今回は[TeXify3](https://themes.gohugo.io/themes/hugo-texify3/)を導入した

### サブモジュールとして導入する
```bash
git submodule add https://github.com/michaelneuper/hugo-texify3.git themes/hugo-texify3
```

### 必要なファイルをコピーする
```bash
cp themes/hugo-texify3/exampleSite/hugo.toml .
```

### hugo.tomlに設定を色々書く
```bash
vim hugo.toml
```

## 動作確認後にGitにPush

サーバを起動して、動作を確認する
```bash
hugo server -D
```
表示できるのを確認したら、GitにPushしておく

```bash
git add . -m "first commit"
git remote add orgin {リポジトリ}
git push -u origin master
```

## GitHub Pageで公開する設定

### リモートリポジトリの設定

リモートのリポジトリの設定で
> - Deploy keysの設定
> - Actions permissionsを有効化
> - Workflow permissionsの読み書きの権限を許可しておく

### Github Actionの作成<br>
 ActionsからNew workflowを作成
 hugoで検索してConfigure


自分が導入したテーマはPostCSSとかが導入されていてワークフローを少しいじらないとbuildに失敗するので、Hugo CLIがインストールされた後に

```bash
- name: Install postcss
  run: npm install postcss postcss-cli autoprefixer postcss-import
```

を追記しないとビルドが成功しない

## 記事を作成するには

```bash
hugo new posts/POST_NAME.md
```

## 最後に

記事を作成してリモートにPushしたら勝手にビルドしてデプロイまでしてくれるので、<br>
https://{アカウント名}.github.io/{リポジトリ名}/<br>
にアクセスすれば記事が見れるようになっている

