# Raspberry Pi 4B に .NET 6.0 SDK をインストールする方法

Created on September 12, 2023  
Updated on September 12, 2023  
Copyright (c) 2023 led-mirage  

## はじめに

この資料では Raspberry Pi 4B に .NET 6.0 SDK をインストールする方法について説明します。

使用した環境とSDKのバージョンは以下の通りです。

- Raspberry Pi 4B 4GB 64bit
- .NET 6.0 SDK 6.0.413

## ダウンロード

ブラウザで以下のURLにアクセスし SDK 6.0.xxx のバイナリを取得します。

https://dotnet.microsoft.com/en-us/download/dotnet/6.0

ダウンロードするのは Linux の Arm64 もしくは Arm32 です。使用しているラズパイOSのビット数が64bitならArm64を、32bitならArm32をダウンロードしてください。使用しているラズパイOSのビット数を調べるにはターミナルで以下のコマンドを実行します。

```bash
getconf LONG_BIT
```

## 解凍

まずターミナルを起動して、次のコマンドを実行しインストール先のディレクトリを作成します。ここでは `/usr/share/dotnet` にインストールすることを想定しています。

```bash
sudo mkdir -p /usr/share/dotnet
```

次にバイナリをダウンロードしたフォルダに移動し、圧縮ファイルをインストール先に解凍します。ここでは Downloads フォルダにダウンロードしたことを想定しています。-xvf につづくファイル名には実際にダウンロードしたバイナリのファイル名を指定してください。

```bash
cd ~/Downloads
sudo tar -xvf dotnet-sdk-6.0.413-linux-arm64.tar.gz -C /usr/share/dotnet
```

## PATH を通す

ターミナルに bash を使用している場合は、次のコマンドで設定ファイルを開きます。

```bash
nano ~/.bashrc
```

テキストエディタが開いたら、ファイル末尾に以下のコマンドを追加し保存します。

```bash
export DOTNET_ROOT=/usr/share/dotnet
export PATH=$PATH:/usr/share/dotnet
```

保存したらテキストエディタを終了し、ターミナルで次のコマンドを実行し設定を反映させます。

```bash
source ~/.bashrc
```

## 動作確認

次のコマンドを実行し、.NET SDK のバージョンが表示されればOKです。

```bash
dotnet --version
```

実行結果例

```bash
6.0.413
```

## プロジェクトを作成し実行してみる

ターミナルでプロジェクトを作成するディレクトリに移動し、次のコマンドでコンソールアプリケーションを作成してみます。

```bash
dotnet new console -o MyConsoleApp
```

ソースの自動生成が終わったら、次のコマンドを実行して実行してみます。

```bash
cd MyConsoleApp
dotnet run
```

以下のような実行結果が表示されればOKです。

```bash
Hello, World!
```

お疲れさまでした。
