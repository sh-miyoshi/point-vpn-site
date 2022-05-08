# SSHサーバーにアクセスする方法

ここではあなたが管理するSSHサーバーにアクセスする手順を説明します。

## 事前に準備するもの

- SSHサーバー
  - アクセス先のSSHサーバー
- Server Agentをインストールするサーバー
  - SSHサーバーにアクセスできる場所であればどこでも大丈夫です
    - SSHサーバーと同じサーバーでも問題ありません
  - Dockerをインストールしてください
  - FirewallでOutbound通信を制御している場合は、https://point-vpn-controller.onrender.com と https://router-wq3ixsscka-uc.a.run.app への通信を許可してください
- SSHでアクセスするPC
  - Dockerをインストールしてください
  - SSHクライアント(sshコマンド)をインストールしてください
  - FirewallでOutbound通信を制御している場合は、https://point-vpn-controller.onrender.com と https://router-wq3ixsscka-uc.a.run.app への通信を許可してください

## 手順

- ChromeなどのブラウザからPoint-VPN Console(TODO)にアクセスします
- 初回の場合は「Sign up」、2回目以降の場合は「Login」を選択してください
  - 初回ログインの場合は、ログイン後、User名の登録もお願いします
- 「New project」を選択してください
- 必要な情報を入力後、「Create」ボタンを押してください
  - Outgoing AddressにはServer AgentからSSHサーバーへのアクセス先を指定します
  - 現在パスワード認証のみサポートしており、公開鍵認証は制作中です
- 次にProject一覧ページから先ほど作成したProjectの「Edit」ボタンを押してください
- 次にServer Agentを起動してみます
- Server Agentのブロックの「Run Command」ボタンを押すとServer Agentの起動に必要なコードが表示されます
- その値をコピーし、事前に準備したServer Agentをインストールするサーバー上で実行してServer Agentを起動してください
- 次にClient Agentを登録します
- 再びブラウザのProject詳細画面から「Add Agent」ボタンを押してください
- 必要な情報を入力し「Create」ボタンを押してください
  - Incomming AddressはSSHクライアントでアクセスするためのアドレスを指定してください
- Server Agentの場合と同様に「Run Command」ボタンから起動コードを取得し、自身のPCで実行してClient Agentを起動してください
- Client Agent起動後、Incomming Addressで指定したアドレスに対してSSHコマンドでアクセスしてください
- Happy SSH!
