+++
draft = false
title = "Courseraの機械学習コースを始めたのでメモ Week1-1"
author = "nabeen"
thumbnail = ""
tags = ["MachineLearning", "DeepLearning", "mokumoku"]
categories = ["MachineLearning", "DeepLearning"]
description = ""
slug = "mokumoku-first"
date = "2017-03-07T19:46:44+09:00"

+++

社内でもくもく会を定例化しようという動きになり、今日、まさに今、もくもくしています。僕は、前からQiitaでも「機械学習ならまずこれだろjk」って言われているコイツをやることにしました。

[Machine Learning \- Stanford University \| Coursera](https://www.coursera.org/learn/machine-learning)

やろうやろうと思ってはや一ヶ月以上。こういう機会がないと自宅ではNetflixしか見ないので、がんばってこのコースを卒業しようと思います。

## 機械学習の範囲
機械学習の応用範囲は無限大。

- マーケットデータ
- スパムメール
- ゲノム解析
- 医療
- クリックマイニングデータ

などなど。

コンピュータに学ばせることで、こちらで明示的に支持することなく、いい感じにデータを予測させる。

## 回帰問題と分類問題
僕らが予測したいデータは基本的に「連続値」か「離散値」であって、それぞれ以下の問題として取り扱われる。

* 回帰問題：連続値を予測する際に用いる（例：◯平米の家なら◯円で売れる、など。連続する数（スカラー値など）を予測結果としたい場合。
* 分類問題：離散値を予測する際に用いる（例：◯cm以上の腫瘍は悪性、など。2値、あるいはそれ以上の「カタマリ」として分けられるような問題のこと。


## 教師あり学習と教師なし学習
データセットを与える際に、あらかじめ正解があるかないかで、以下の学習方法がある。

* 教師あり学習：事前に正解がある
* 教師なし学習：事前に正解がない

教師あり学習は、特徴量とその結果を予めデータセットとして与えておき学習させる。そこで新しいデータセットに対して、過去に学習した正解データから新しいデータセットの結果を予測する。

教師なし学習は、データセットのみ与えて学習によって特徴量による分類をさせ結果を予測させる。

## 今後使用していく言語
このコースでは、Octave（オクターブ）を使っていく。

Octaveは手軽で便利なので、実際にOctaveで試作レベルのものを作った後、Java,Pythonなど他の言語にアルゴリズムを移植してプロダクトを作っていくことも多い。

[GNU Octave \- Wikipedia](https://ja.wikipedia.org/wiki/GNU_Octave)

## おわりに
ふぅ、今日はここまで！続きはまた今度ー。

結構実例を用いて説明してくれるから、案外すんなり入ってくる。実際にこのコースを終わった人のレビュー見る感じ、Octaveもそんなに難しいもんでもない（むしろ簡単）っぽいし、引き続き頑張っていきます。

というか、前にちょろっとだけ（イントロ）進めちゃってたので、既に現実世界ではweek3に突入していることになっている罠。

これから始める方、注意して下さい；；
