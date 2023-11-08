# KH Coder in Docker
Docker の KH Coder を提供した。
docker として host タイプのネットワークを使っている事に注意。

## 必要ファイルのダウンロード

必要なファイル群。

```
$ git clone https://github.com/sinchiba-backyard/NL2E.git
$ cd NL2E
$ git submodule init
$ git submodule update
```

KH Coderを最新版に更新。

```
$ git submodule update --remote
```

チュートリアル用ファイル。

```
$ wget https://khcoder.net/tutorial_data_3x.zip
$ unzip -x tutorial_data_3x.zip -d khcoder/
```

## 起動と設定

```
$ xhost +local:docker
$ docker compose up --build
```

xeyesの目玉が表示され、「/usr/sbin/mysqld: ready for connections. Version...」の表示が出れば成功。以降の作業は別ターミナルで。

```
$ /bin/bash do.sh
```

MySQLの設定後、KH Coderが起動する。起動したら[チュートリアル](https://khcoder.net/tutorial.html)を試してみよう。

## 補遺

日常利用のコマンド。一例。

```
$ cd NL2E
$ docker compose up -d                  # dockerコンテナ起動
$ docker compose ps                     # dockerコンテナ起動確認（任意）
$ docker exec -it nl2e-nl2e-1 /bin/bash # dockerに入る
# cd /khcoder                   # KH Coderのフォルダに移動して
# perl kh_coder.pl                      # KH Coder起動
# exit                                  # dockerから出る
$ docker-compose down                   # dockerコンテナ終了
```


## WSL/Ubuntu22.04の場合

## macOSの場合

- [XQuartz](https://www.xquartz.org/)をインストールする
- XQuartzの環境設定「セキュリティ」タブで、「接続を認証」のチェックを外し、「ネットワーク・クライアントからの接続を許可」にチェックを入れ、XQuartzを再起動する
- docker-compose.ymlの「DISPLAY: $DISPLAY」という箇所を「DISPLAY: host.docker.internal:0」に変更して上書き保存
- コンテナ名の「nl2e_nl2e_1」が、「nl2e-nl2e-1」になるなど、コンテナ名のアンダーバーがハイフンにかわることがある

参考URL
https://zenn.dev/hogenishi/articles/6bcffa389bcfb6

![khcoder](khcoder.png)
