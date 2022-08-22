---
active_lock_reason: 
assignee: 
assignees: []
author_association: OWNER
closed_at: 
comments: 0
comments_url: https://api.github.com/repos/ma96o/gialog/issues/18/comments
created_at: '2022-08-19T13:46:00Z'
events_url: https://api.github.com/repos/ma96o/gialog/issues/18/events
html_url: https://github.com/ma96o/gialog/issues/18
id: 1344468308
labels: []
labels_url: https://api.github.com/repos/ma96o/gialog/issues/18/labels{/name}
locked: false
milestone: 
node_id: I_kwDOHueoCs5QIvVU
number: 18
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
  url: https://api.github.com/repos/ma96o/gialog/issues/18/reactions
repository_url: https://api.github.com/repos/ma96o/gialog
state: open
state_reason: 
timeline_url: https://api.github.com/repos/ma96o/gialog/issues/18/timeline
title: '0819 _ Aptos SDK'
updated_at: '2022-08-19T13:46:00Z'
url: https://api.github.com/repos/ma96o/gialog/issues/18
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
Aptos は SDK を提供している．クライアントが，[公開API](https://fullnode.devnet.aptoslabs.com/v1/spec#/) に接続して Aptosブロックチェーンとインタラクションを行うための開発者向けのインターフェイスである．

提供している主な機能としては以下である．
- キーペアの生成
- トランザクションの署名・送信
- 送信したトランザクションの状態取得
- BCSライブラリ
- 特定のアカウントに属するリソース，モジュール，トランザクションのクエリ
- 開発のための faucet クライアント
- NFTトークンのミントやクエリ

異なる言語に対応しており，Typescript SDK と Python SDK の2つを提供している．おそらく Typescript SDK がメイン．

Typescript SDK は3つのレイヤーで構成されている
- トランスポート層
- コアSDK層
- アプリケーション層(optional)

- アーキテクチャ
   - ![アーキテクチャ](https://user-images.githubusercontent.com/22464192/185632261-6389b9b3-85d2-440b-a3a7-ff96c0b822a7.png "サンプル")


トランスポート層は，Aptosの公開APIの仕様に基づいた class のセットを提供していて，APIのエンドポイントにペイロードを送信する役割．

コアSDK層は，殆どのアプリケーションで必要とされるような機能を提供していて，上述の主な機能のほとんどを提供する役割．

アプリケーション層が提供する機能は限定的で（おそらく今後はサードパティが担っていくと思う），NFTトークンの作成とクエリのためのメソッドを提供している．

インストール手順はそれぞれ以下
- Typescript SDK
  -`$ npm install aptos`
- Python SDK
  - `$ pip3 install aptos-sdk`
  - あるいは，[ソースコードからインストールする方法もある](https://aptos.dev/sdks/python-sdk/)
