+++
draft = false
thumbnail = ""
description = ""
slug = "start-to-use-composer"
tags = ["composer", "php"]
categories = ["Composer"]
date = "2017-02-08T00:10:14+09:00"
title = "Composerでプロジェクトの雛形をつくってみた"
author = "nabeen"

+++

最近業務改善ツールを書く機会があって、もともとLaravel実装で進めてたんですが、なんとなく使い方がわかっちゃったっていうのと、少し期間が開いたのでなんか飽きちゃったってのが重なって、フルスクラッチでちょこちょこ書き進めています。といってもシェルの資産が多いので、ラップするような簡単なものですが。

今回はそれをComposerのライブラリっぽく？書いたので、その知見を残しておきます。今までComposerは使うばっかりで作ったことはなかったので、いい勉強になりました。

## 前提条件
以下の状態を前提にしています、あしからず。

1. composer導入済みであること

たったこれだけ！

## composer.jsonの雛形を作成する
雛形は対話式で作ることができます。基本、Enter押すだけでも作れる感じですね。楽ちん楽ちん。※個人情報な部分は一部伏せ字にしています。nameを`algorithm`にしてるのは、最近社内でアルゴリズムの勉強的なことをやってるから、それを楽ちんに書ける雛形がちょうど欲しかったからです。gistだとなんかちょっと味気ないしなと。

```bash
composer init


  Welcome to the Composer config generator



This command will guide you through creating your composer.json config.

Package name (<vendor>/<name>) [nabeen/algorithm]: nabeen/algorithm
Description []: any algorithm
Author [nabeen <nabeen@hogehoge.com>, n to skip]:
Minimum Stability []:
Package Type (e.g. library, project, metapackage, composer-plugin) []: project
License []: MIT

Define your dependencies.

Would you like to define your dependencies (require) interactively [yes]?
Search for a package:
Would you like to define your dev dependencies (require-dev) interactively [yes]?
Search for a package:

{
    "name": "nabeen/algorithm",
    "description": "any algorithm",
    "type": "project",
    "license": "MIT",
    "authors": [
        {
            "name": "nabeen",
            "email": "nabeen@hogehoge.com"
        }
    ],
    "require": {}
}

Do you confirm generation [yes]?
```

これで雛形の完成。でもこれだけじゃなんか味気ないので、試しによく使うMonologでも入れてみましょう(つ、使いますよね、、？)

```json
"require": {
    "monolog/monolog": "1.*"
}
```

これで`composer install`すると、`vendor`配下にMonologを入れてくれます。

## テスト用のコマンドを作成する
とりあえずなんか作って叩きたいので、`composer.json`に一手間加えて、

```json
{
    "name": "nabeen/algorithm",
    "description": "any algorithm",
    "type": "project",
    "license": "MIT",
    "authors": [
        {
            "name": "nabeen",
            "email": "watanabe_kenichiro@hasigo.co.jp"
        }
    ],
    "require": {
    	"monolog/monolog": "1.*"
    },
    "autoload": {
        "psr-4": {
            "nabeen\\algorithm\\": "src"
        }
    },
    "bin": ["test-command"]
}
```

叩く元のファイルを作って、

```php
#! /usr/bin/env php

<?php
$files = array(
    '/vendor/autoload.php',
    '/../../vendor/autoload.php',
);

// autoloadの読み込み
foreach ($files as $file) {
    if (file_exists(__DIR__.$file)) {
        require __DIR__.$file;
        break;
    }
}

// 処理実行
$app = new \nabeen\algorithm\TestCommand();
$app->run($argv);

```

叩くclassを作ってあげます。

```php
<?php
namespace nabeen\algorithm;

use Monolog\Logger;
use Monolog\Handler\StreamHandler;

class TestCommand
{
    public function __construct()
    {
        $this->log = new Logger('app');
        $this->log->pushHandler(new StreamHandler(__DIR__.'/../logs/app.log', Logger::DEBUG));
    }

    public function run ()
    {
        $this->log->addInfo('Info Message');
        $this->log->addError('Error Message');
        $this->log->addDebug('Debug Message');
        echo "excuted TestCommand. And logging by monolog/monolog".PHP_EOL;
    }
}
```

Monolog使ってlogファイルを吐き出す、ただそれだけの処理です。とりあえずこの中でしか使わない予定なので、プロジェクト直下の`logs`ディレクトリに吐いています。

## 最終型のフォルダ構造
こんな感じでにょもにょしてあげた最終結果は、こんな感じになります。

```bash
$ tree -L 2
.
├── README.md
├── composer.json
├── composer.lock
├── logs
├── src
│   └── TestCommand.php
├── test-command
└── vendor
    ├── autoload.php
    ├── composer
    ├── monolog
    └── psr

6 directories, 6 files
```

## 実行してみる
こんな感じで実行すれば、

```bash
$ php test-command

excuted TestCommand. And logging by monolog/monolog
```

こんな感じのログが出ますね！

```
[2017-02-07 15:04:10] app.INFO: Info Message [] []
[2017-02-07 15:04:10] app.ERROR: Error Message [] []
[2017-02-07 15:04:10] app.DEBUG: Debug Message [] []
```

## おわりに
Composerの雛形と言うか、Monologの使い方みたいになっちゃいましたが、まぁ`composer init`の使い方が覚えられたということで・ω・

それではよきComposerライフを！
