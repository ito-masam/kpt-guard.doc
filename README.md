# kpt-guard

Slackを使ったKPTを取りまとめるbot

## チャートの閲覧方法

- google chrome
  - install [plantuml viewer](https://chrome.google.com/webstore/detail/plantuml-viewer/legbfeljfbjgfifnkmpoajgpgejojooj)
  - 各チャートをraw表示にする

## document

1. [設計](1.design)
1. [テストシナリオ](2.test-scenario)

### deploy

- [heroku dashboard](https://dashboard.heroku.com/apps/kpt-guard-bot)

## usage

引数は半角スペースで区切ります。

### 新規登録

新規登録状態では、statusをproblemとして登録します

```
@kpt-bot post メッセージ

@kpt-bot post ほげ
```

### 編集

```
@kpt-bot post #ID メッセージ

@kpt-bot post #759a8188b5ce4ee98c223710ac1ae7b1 ばー
```

### status変更

ステータス変更にはルールがあり、遷移方向は下記のとおりです。

```
problem --> try <--> keep
```

```
@kpt-bot post #ID :(keep|problem|try)

@kpt-bot post #759a8188b5ce4ee98c223710ac1ae7b1 :try
```

### 一覧表示

```
@kpt-bot list
```
