# hackathon-2023-05-13-ticket-management

# 開発ドキュメント

  - 画面イメージ(figma)
    - https://www.figma.com/file/EUBLOB2SSgbTxeLG4smd1Z/%E3%82%BF%E3%82%B9%E3%82%AF%E7%AE%A1%E7%90%86%E3%82%A2%E3%83%97%E3%83%AA?type=design&node-id=0-1&mode=design&t=GNS9VmfjQRqEVDA0-0
  - 設計メモ（googleスプレッドシート)
    - https://docs.google.com/spreadsheets/d/1EWXh1RvuEcLJTJB4EBGAwSC7eh3O-boaBuEZHcr-PoQ/edit#gid=0

# 環境について
## はじめに

以下の順番で作業を行ってください。

1. WSL2のインストールを行う（Windowsのみ）

2. git,docker,docker-composeのインストール（※）

3. gitリポジトリをcloneする

4. dockerイメージやコンテナの構築、立ち上げを行う

5. 動作確認

※インストール済みの方は手順を飛ばしてください。古いバージョンを利用している方はアップデートしたほうがいいかもしれません。

## WSL2のインストール（Windowsのみ）

以下の手順でインストールしてください。Windowsの方のみが対象です。

- https://www.kagoya.jp/howto/it-glossary/develop/wsl2_linux/

環境構築時のバージョンは以下の通りです。後続の環境構築がうまくいかない場合はバージョン差異の影響が無いか確認してみてください

    ```
    $ lsb_release -a
    No LSB modules are available.
    Distributor ID: Ubuntu
    Description:    Ubuntu 22.04.2 LTS
    Release:        22.04
    Codename:       jammy
    ```

## git,docker,docker-composeのインストール

git,docker,docker-composeをインストールします。参考手順は無いです。ググって適宜インストールしてください。

Windowsの方はWSLのubuntuでインストールを行ってください。既にインストール済みの方は手順を飛ばしてください。

環境構築時のバージョンは以下の通りです。後続の環境構築がうまくいかない場合はバージョン差異の影響が無いか確認してみてください

 - git
    ```
    $ git --version
    git version 2.34.1
    ```
  - docker
    ```
    $ docker -v
    Docker version 24.0.2, build cb74dfc
    ```
  - docker-compose
    ```
    $ docker-compose -v
    docker-compose version v2.4.1
    ```

## gitリポジトリをcloneする

gitリポジトリをcloneします。これ以降、Windowsの方はWSLのubuntuで操作を行ってください。

```
cd 作業ディレクトリ（※）
git clone https://github.com/ShotaMinegishi/hackathon-2023-05-13-ticket-management.git
cd hackathon-2023-09-task-management
```

※WSLの方は`/mnt/c`以下のどこかを作業ディレクトリにするとよいと思います。WSLの`/mnt/c` = Windows上の`C:\`なので、Windows側から普段利用しているテキストエディタを使って開発することが出来ます。

## dockerイメージやコンテナの構築、立ち上げを行う

すみません、DBサーバーしか構築できていないです…。

`docker compose up`が通るところまでしか確認できていないので、不備があるかもしれません。

以下の手順を実行してdockerコンテナ構築、立ち上げを行ってください。

```
# docker image構築
docker compose build
# docker container作成
docker compose up
```


エラー状況
```
# docker compose up を実行すると、frontendサーバにてエラー。
task-frontend  | npm ERR! code ENOENT
task-frontend  | npm ERR! syscall open
task-frontend  | npm ERR! path /app/package.json
task-frontend  | npm ERR! errno -2
task-frontend  | npm ERR! enoent Could not read package.json: Error: ENOENT: no such file or directory, open '/app/package.json'
task-frontend  | npm ERR! enoent This is related to npm not being able to find a file.
task-frontend  | npm ERR! enoent
task-frontend  |
task-frontend  | npm ERR! A complete log of this run can be found in: /root/.npm/_logs/2023-09-16T00_55_30_236Z-debug-0.log
```

`no such file or directory, open '/app/package.json'`と言われており、frontendコンテナがpackage.jsonを見つけられていない模様。

frontend/dockerfileに記載している`COPY ./vue-project/package*.json ./`あたりがおかしいと思われます。

作業状況をまともに引き継げないので、トラブルシュートするより、frontendのみ一から構築し直したほうが早いかもしれません…。

スミマセンがよろしくお願いします。