---
active_lock_reason: 
assignee: 
assignees: []
author_association: OWNER
closed_at: 
comments: 0
comments_url: https://api.github.com/repos/ma96o/gialog/issues/4/comments
created_at: '2022-08-01T12:49:25Z'
events_url: https://api.github.com/repos/ma96o/gialog/issues/4/events
html_url: https://github.com/ma96o/gialog/issues/4
id: 1324366146
labels: []
labels_url: https://api.github.com/repos/ma96o/gialog/issues/4/labels{/name}
locked: false
milestone: 
node_id: I_kwDOHueoCs5O8DlC
number: 4
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
  url: https://api.github.com/repos/ma96o/gialog/issues/4/reactions
repository_url: https://api.github.com/repos/ma96o/gialog
state: open
state_reason: 
timeline_url: https://api.github.com/repos/ma96o/gialog/issues/4/timeline
title: '0801 _ Cosmos SDK チュートリアル'
updated_at: '2022-08-01T12:49:25Z'
url: https://api.github.com/repos/ma96o/gialog/issues/4
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
今日は，Cosmos SDK のチュートリアルを進めていた．

[Cosmos SDK](https://github.com/cosmos/cosmos-sdk) は，ブロックチェーンを開発するための開発キットで，
Cosmos Networkに対応するブロックチェーンを比較的簡単に作れる．
開発は [Go言語](https://go.dev/) で行う，[Rust](https://www.rust-lang.org/ja)でも開発できるみたい．
[Terra](https://github.com/terra-money/core) や [Secret Network](https://github.com/scrtlabs/SecretNetwork) などが Cosmos SDK を使って構築されていて，ソースコードを読むと勉強になる．

具体的には Cosmos SDK の開発者向けインターフェイスである [Ignite CLI](https://github.com/ignite/cli) を用いて開発を行う．
ブロックチェーンの機能は，提供されるモジュールを利用することで実装できる．
モジュールは [/x](https://github.com/cosmos/cosmos-sdk/tree/main/x) で確認できる．

主要なモジュールは以下．
- Tendermintモジュール
  - コンセンサスエンジンを管理
- IBCモジュール
  - IBCへの対応
- Authモジュール
  - アカウントを管理
- Bankモジュール
  - その各アカウントが持つトークン残高を管理
- Govモジュール
   - ガバナンスを管理
- Stakingモジュール
   - Stakingに関する機能を提供

ローカルでテストするためのコマンドが提供されていて，`$ ignite chain serve`でテストネットを起動できる．
ただ，実行で躓いている．
上記コマンドを実行すれば，ソースコードをプロジェクト名のバイナリにコンパイルしてくれて，プロジェクト名（チェーン名）+d（例えば `checkers`というチェーンなら `$ checkersd`）というコマンドを利用できる，とあるのだが `command not found`エラーで実行できない． 
ref. https://tutorials.cosmos.network/academy/3-my-own-chain/ignitecli.html#

このコマンドが使えないと，トランザクションを実行できないのでもう少し粘ってみる．

