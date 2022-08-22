---
active_lock_reason: 
assignee: 
assignees: []
author_association: OWNER
closed_at: 
comments: 1
comments_url: https://api.github.com/repos/ma96o/gialog/issues/5/comments
created_at: '2022-08-02T16:05:12Z'
events_url: https://api.github.com/repos/ma96o/gialog/issues/5/events
html_url: https://github.com/ma96o/gialog/issues/5
id: 1326072585
labels: []
labels_url: https://api.github.com/repos/ma96o/gialog/issues/5/labels{/name}
locked: false
milestone: 
node_id: I_kwDOHueoCs5PCkMJ
number: 5
performed_via_github_app: 
reactions:
  "+1": 0
  "-1": 0
  confused: 0
  eyes: 0
  heart: 0
  hooray: 0
  laugh: 0
  rocket: 0
  total_count: 0
  url: https://api.github.com/repos/ma96o/gialog/issues/5/reactions
repository_url: https://api.github.com/repos/ma96o/gialog
state: open
state_reason: 
timeline_url: https://api.github.com/repos/ma96o/gialog/issues/5/timeline
title: '0802 _ Ethereumのアカウントについて'
updated_at: '2022-08-02T16:12:19Z'
url: https://api.github.com/repos/ma96o/gialog/issues/5
user:
  avatar_url: https://avatars.githubusercontent.com/u/22464192?v=4
  events_url: https://api.github.com/users/ma96o/events{/privacy}
  followers_url: https://api.github.com/users/ma96o/followers
  following_url: https://api.github.com/users/ma96o/following{/other_user}
  gists_url: https://api.github.com/users/ma96o/gists{/gist_id}
  gravatar_id: ''
  html_url: https://github.com/ma96o
  id: 22464192
  login: ma96o
  node_id: MDQ6VXNlcjIyNDY0MTky
  organizations_url: https://api.github.com/users/ma96o/orgs
  received_events_url: https://api.github.com/users/ma96o/received_events
  repos_url: https://api.github.com/users/ma96o/repos
  site_admin: false
  starred_url: https://api.github.com/users/ma96o/starred{/owner}{/repo}
  subscriptions_url: https://api.github.com/users/ma96o/subscriptions
  type: User
  url: https://api.github.com/users/ma96o

---
Ethereum の アカウントという概念について，きちんと理解できていなかったので整理した．

## Ethereumにおけるアカウントとは
> イーサリアムアカウントは、イーサリアム上でトランザクションを送信できるイーサ（ETH）残高を持つエンティティである。アカウントは、ユーザーが管理することも、スマートコントラクトとして展開することもできる。
> [Ethereum accounts | ethereum.org](https://ethereum.org/ja/developers/docs/accounts/#contract-accounts)

- つまり，アカウント = ETHが保管される場所
  - アカウントとアカウント残高は，EVMの大きなテーブルに格納されていて，EVM全体の状態の一部として管理されている

## ２種類のアカウントが存在
- EOA（Externally Owned Account: [外部所有アカウント]）
  - 秘密鍵を持っている人なら誰でもコントロールが可能
- コントラクトアカウント（CA）
  - Ethereum ネットワークに展開されたスマートコントラクトで、コードによってコントロールされる

- いずれのアカウントも以下の機能を備えている
  - [ETH]と[トークン]の受信、保有、送信
  - デプロイされた[スマートコントラクト]と対話する
- 2つのアカウントの重要な違い

| | EOA | コントラクトアカウント|
|--|--|--|
|作成コスト|かからない|かかる（ネットワークのストレージを使用するため）|
|Txの送信|起点となる|Tx の受信に応答してのみ Tx を送信できる|
|EOAからのTx|	EOA間はETH or トークンのみ可能|EOAからのTxはトークンの転送やコントラクトの作成等,多くのアクションを実行できる
|対応する秘密鍵|持つ|持たない|

## Ethereum におけるアカウントを理解する上で、重要な３つのキーワード
- アカウント
  - トランザクションを送り、残高があるエンティティ
- アドレス
  - アカウント]は「0x」から始まるアドレスをもつ
  - このアドレスを使用してアカウントに資金を送金する
- ウォレット
  - アカウント残高の確認、トランザクションの送信等、Ethereumのアカウントを管理できるインターフェイスあるいはアプリケーション
  - MetaMaskなど

- アカウントはウォレットの実態のような認識だとイメージしやすい

## アカウントは4つのフィールドをもつ
![account](https://ethereum.org/static/19443ab40f108c985fb95b07bac29bcb/302a4/accounts.png "account")

https://ethereum.org/ja/developers/docs/accounts

- nonce
  - アカウントから実行されたトランザクションの総数，カウンター
  - トランザクションが一度だけ処理されることを保証するもの（リプレイ攻撃を防ぐ）
  - コントラクトアカウントの場合、この数値はそのアカウントで作成されたコントラクトの数を表す
- balance
  - 所有するweiの数
  - Wei は ETH の最小単位であり、1 ETH = 10^18 Wei
- codeHash
  - EVMコードのハッシュ値
  - コントラクトアカウントは、異なる操作を実行できるコードフラグメントがプログラムされている
     - このEVMコードは、アカウントがメッセージコールを取得した場合に実行される
     - 他のアカウントのフィールドとは異なり、変更することはできない
     - このようなコードフラグメントはすべて、後で検索できるように、対応するハッシュの下で状態データベースに含まれている
  - EOAでは、codeHash フィールドは空文字列のハッシュ
- storageRoot
  - ストレージハッシュともいう
  - Merkle Patricia tree のルートノードのハッシュ値
  - デフォルトでは空

