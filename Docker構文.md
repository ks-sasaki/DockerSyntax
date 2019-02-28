* Docker構文  
今後使いそうな構文の備忘録  
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
|コンテナのバックグラウンド起動|docker container -d nginx|-d : バックグラウンドで起動するオプション<br>バックグラウンドで起動されるので、コンソール上には起動したコンテナのIDのみ表示される|
|コンテナのlog確認|docker container logs -t コンテナ識別子| -t : タイムスタンプ表示|
|コンテナのポートマッピング|docker container run -d -p 8080:80 nginx|ホストの8080ポートをNginxの80番ポートにマッピング|
|コンテナのDNSサーバ指定|docker container run -d --dns IPアドレス|docker container run -d -dns 192.168.1.1|
|コンテナのディレクトリの共有|docker container run -v ホストディレクトリ:コンテナディレクトリ|docker container run -v /Users/ks-sasaki/webapp:/usr/share/nginx/html nginx|
|コンテナの一覧表示|docker container ls [option]|-a : 停止中のコンテナ含め全表示|
|コンテナの稼働確認|docker container stats コンテナ識別子|※状態の確認が終わったらCtrl+Cキーでコマンドを終了させます|
|コンテナのプロセス確認|docker container top コンテナ識別子|
|コンテナの開始|docker container start コンテナ識別子|複数のコンテナを一度に起動したいときは、引数にコンテナ識別子を複数指定します。|
|コンテナの停止|docker container stop -t 2 コンテナ識別子|-t : コンテナの停止時間を指定する（デフォルトは10秒)|
|コンテナの削除|docker container rm [option] コンテナ識別子|--force : 起動中のコンテナを強制的に削除する|
|ネットワークの一覧表示|docker network ls||
|ネットワークの作成|docker network create [option] ネットワーク名|--ipv6 : IPv6ネットワークを有効にするか(true/false)<br>--ip-range : IPアドレスのレンジ<br>--subnet : サブネットをCIDR形式で指定|
|ネットワークへの接続|docker network connect [option] ネットワーク名 コンテナ|--ip : Ipv4アドレス<br>--ip6 : IPv6アドレス<br>接続後は、同一ネットワーク上にある他のコンテナと通信可能になる|
|コンテナの詳細確認|docker container inspect コンテナ識別子||
|稼働コンテナのポート転送確認|docker container port コンテナ識別子|コンテナポート番号＞ホストのポート番号|
|コンテナの名前変更|docker container rename 旧名 新名|docker container rename nginx webserver|
|不要なイメージ/コンテナの一括削除|docker system prune -a|不要なリソース全削除|

