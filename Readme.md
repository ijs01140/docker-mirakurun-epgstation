# docker-mirakurun-epgstation

[Mirakurun](https://github.com/Chinachu/Mirakurun) + [EPGStation](https://github.com/l3tnun/EPGStation) + [web-bml](https://github.com/otya128/web-bml) の Docker コンテナ

## fork元からの変更点
以下の通り、私個人向けのカスタマイズを施しているので、使用する際は注意してください
- MirakurunのDockerfileを若干変更→[中身](https://github.com/ijs01140/Mirakurun/blob/master/docker/Dockerfile)
- libarib25に[tsukumijima/libaribb25](https://github.com/tsukumijima/libaribb25)を採用
- データ放送閲覧のために[web-bml](https://github.com/otya128/web-bml)を導入

## 前提条件

- Docker, Docker Compose の導入が必須
- ホスト上の pcscd は停止する
- チューナーのドライバが適切にインストールされていること

## インストール手順

```sh
curl -sf https://raw.githubusercontent.com/ijs01140/docker-mirakurun-epgstation/v2/setup.sh | sh -s
cd docker-mirakurun-epgstation

#チャンネル設定
vim mirakurun/conf/channels.yml

#コメントアウトされている restart や user の設定を適宜変更する
vim docker-compose.yml
```

## 起動

```sh
sudo docker compose up -d
```

## チャンネルスキャン地上波のみ(取得漏れが出る場合もあるので注意)

```sh
curl -X PUT "http://localhost:40772/api/config/channels/scan"
```

mirakurun の EPG 更新を待ってからブラウザで http://DockerHostIP:8888 へアクセスし動作を確認する

## 停止

```sh
sudo docker compose down
```

## 更新

```sh
# mirakurunとdbを更新
sudo docker compose pull
# epgstationを更新
sudo docker compose build --pull
# 最新のイメージを元に起動
sudo docker compose up -d
```

## 設定

### Mirakurun

* ポート番号: 40772

### EPGStation

* ポート番号: 8888
* ポート番号: 8889

### web-bml

* ポート番号: 23234

### 各種ファイル保存先

* 録画データ

```./recorded```

* サムネイル

```./epgstation/thumbnail```

* 予約情報と HLS 配信時の一時ファイル

```./epgstation/data```

* EPGStation 設定ファイル

```./epgstation/config```

* EPGStation のログ

```./epgstation/logs```

## v1からの移行について

[docs/migration.md](docs/migration.md)を参照
