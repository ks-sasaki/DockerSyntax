* Docker構文
(ctlr+k→v : display preview on same window)

* イメージ

イメージの実態は、「Dockerでサーバ機能を動かすのに必要なファイル群」

| 概要 | 構文 | 例 |
| --- | --- | --- |
|イメージ作成|docker image pull [オプション名] "image name"[:タグ名]||
|イメージ表示|docker image ls [optioin]|-a:すべてのイメージを表示|
|イメージ詳細表示|docker image inspect [option] "image name"[:tag name]|docker image inspect --format="{{ .Os}}" centos:7<br>--format:オプション指定|
|イメージのタグ設定|docker image tag イメージ名 <ユーザー名>/イメージ名:タグ名|docker image tag nginx ks-sasaki/webserver:1.0|
|イメージの削除|docker image rm イメージ名 [optioin]|docker image rm nginx --force<br>--force : 強制的に削除|
|未使用のイメージ削除|docker image prune イメージ名 [option]|docker image prune nginx -a <br>未使用イメージ全削除|

* コンテナ

「イメージのスナップショットがコンテナ」というイメージ。

| 概要 | 構文 | 例 |
| --- | --- | --- |
|コンテナ生成/起動|docker container run [option] イメージ名[:タグ名][引数]|docker container run -it --name "test" centos /bin/cal<br>-it : コンソールに結果を出力する<br>--name "" : コンテナ名指定<br>centos : イメージ名 <br>/bin/cal : コンテナで実行するコマンド|
