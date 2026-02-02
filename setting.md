**説明開始**

# Docker Composeを用いたWeb+DBの2コンテナ構成環境の構築

この手順書は、Webとデータベースを繋げた環境をDocker Composeを用いて構築することが目的です。

http://127.0.0.1:5000/ にアクセスすると、データベースを操作可能な簡易的なWebアプリが表示されることを完成とします。

## 1.前提条件

・実行環境: Ubuntu 22.04.5 LTS

windowsで実行している方は
[こちら](https://learn.microsoft.com/ja-jp/windows/wsl/install)を参照してインストールしてください。

## 2.dockerのインストール

### 2.1 dockerのインストールのためのコマンド

```
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

古いバージョンや競合する可能性のあるパッケージを削除します。

```
sudo apt-get update
```

パッケージリストを最新の状態にします。

```
sudo apt-get install ca-certificates curl
```

curlコマンドをインストールします。

```
sudo install -m 0755 -d /etc/apt/keyrings
```

公式のGPGキーを保存するフォルダを作成し、権限を追加します。

```
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
```

Dockerの公式サイトからGPGキーをインストールします。

```
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

保存したGPGキーに読み取り権限を付与します。

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

リポジトリに公式のDockerリポジトリを追加します。

```
sudo apt-get update
```

改めてパッケージリストを最新の状態にします。

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

docker関係のツールをまとめてインストールします。

### 動作確認

```
sudo docker run hello-world
```

docker公式のテストプログラムです。\
"Hello from Docker!"というログが確認出来たらOKです。
