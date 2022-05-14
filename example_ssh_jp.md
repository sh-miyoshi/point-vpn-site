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

### 1. ログイン

ブラウザからPoint-VPN Console(https://point-vpn-web.onrender.com/login)にアクセスします

初回の場合は「Sign up」、2回目以降の場合は「Login」を選択してください

![Login](./images/1_login.png)

初回ログインの場合は、ログイン後、User名の登録もお願いします

![Create User](./images/2_user_create.png)

### 2. Routeの作成

まずはアクセスを管理するRouteを作成します。
RouteはどのServer AgentとどのClient Agentが通信するかといった情報を管理しています。
ログイン後、「New route」を選択してください
必要な情報を入力後、「Create」ボタンを押してください

Client AgentブロックのIncomming AddressはSSHクライアントでアクセスするためのアドレスを指定してください
ユーザー名、パスワードは入力できますが、現在は無視されます

Server AgentブロックのOutgoing AddressにはServer AgentからSSHサーバーへのアクセス先を指定します
Formatは`ssh://<username>:<password>@<address>:<port>`になります
※SSHは現在パスワード認証のみサポートしており、公開鍵認証は制作中です

![Create Route](./images/3_create_route.png)

### 3. Server Agentの起動

次にServer Agentを起動してみましょう。
Route一覧ページから先ほど作成したRouteの「Edit」ボタンを押してください

![Route Index](./images/4_route_index.png)

移動先はRoute詳細ページで、ここでServer AgentとClient Agentの情報を確認できます

![Route Show](./images/5_route_show.png)

Server Agentの起動コマンドは、Server Agentのブロックの「Run Command」ボタンを押すと表示されます
その値をコピーし、事前に準備したServer Agentをインストールするサーバー上で実行してServer Agentを起動してください

![Server Agent Run Command](./images/6_server_agent_run_command.png)

### 4. Client Agentの起動

最後に自身がアクセスするClient Agentを登録し起動させます。
再びブラウザのRoute詳細画面からClient Agentのブロックの「Run Command」ボタンを押してください
表示された値をコピーし、自身のPCで実行してClient Agentを起動してください
Client Agent起動後、Incomming Addressで指定したアドレスに対してSSHコマンドでアクセスしてください

![Client Agent Run Command](./images/7_client_agent_run_command.png)

```bash
ssh localhost -p 30000
```

Happy SSH!
