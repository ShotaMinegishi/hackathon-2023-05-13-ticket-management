# hackathon-2023-05-13-ticket-management

# 環境について
## はじめに
構築時のローカル環境の各バージョンを記載します。

下記と同一でなくても大丈夫だとは思いますが、メジャーバージョンくらいは合わせておくとよいかもしれません。

皆さんのPCは他の用途でも使っていると思いますので、無理のない範囲でバージョンを合わせることを検討してみてください。

WindowsPCの方はWSLを利用してUbuntuで環境構築を行ってください。

  - OS
    ```
    lsb_release -a
    No LSB modules are available.
    Distributor ID: Ubuntu
    Description:    Ubuntu 22.04.2 LTS
    Release:        22.04
    Codename:       jammy
    ```
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

## インストール
  - WSL（Windowsのみ）
    - インストール手順：https://www.kagoya.jp/howto/it-glossary/develop/wsl2_linux/
  - git
    - インストール手順：ググってみてください…。
  - docker
    - インストール手順(WSL環境)：https://docs.docker.com/desktop/wsl/
  - docker-compose
    - インストール手順：ググってみてください…。

## アプリケーションの立ち上げまで

すみません、DBサーバーしか構築できていないです…。

`docker compose up`が通るところまでしか確認できていないので、不備があるかもしれません。

```
cd 作業ディレクトリ（※）
git clone https://github.com/ShotaMinegishi/hackathon-2023-05-13-ticket-management.git
cd hackathon-2023-09-task-management
```

※WSLの方は`/mnt/c`以下のどこかを作業ディレクトリにするとよいと思います。WSLの`/mnt/c` = Windows上の`C:\`なので、Windows側から普段利用しているテキストエディタを使って開発することが出来ます。


```
# docker image構築
docker compose build
# docker container作成
docker compose up
```

# 開発ドキュメント

  - 画面イメージ(figma)
    - https://www.figma.com/file/EUBLOB2SSgbTxeLG4smd1Z/%E3%82%BF%E3%82%B9%E3%82%AF%E7%AE%A1%E7%90%86%E3%82%A2%E3%83%97%E3%83%AA?type=design&node-id=0-1&mode=design&t=GNS9VmfjQRqEVDA0-0
  - 設計メモ（googleスプレッドシート)
    - https://docs.google.com/spreadsheets/d/1EWXh1RvuEcLJTJB4EBGAwSC7eh3O-boaBuEZHcr-PoQ/edit#gid=0