---
active_lock_reason: 
assignee: 
assignees: []
author_association: OWNER
closed_at: 
comments: 1
comments_url: https://api.github.com/repos/ma96o/gialog/issues/19/comments
created_at: '2022-08-20T13:14:11Z'
events_url: https://api.github.com/repos/ma96o/gialog/issues/19/events
html_url: https://github.com/ma96o/gialog/issues/19
id: 1345162605
labels: []
labels_url: https://api.github.com/repos/ma96o/gialog/issues/19/labels{/name}
locked: false
milestone: 
node_id: I_kwDOHueoCs5QLY1t
number: 19
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
  url: https://api.github.com/repos/ma96o/gialog/issues/19/reactions
repository_url: https://api.github.com/repos/ma96o/gialog
state: open
state_reason: 
timeline_url: https://api.github.com/repos/ma96o/gialog/issues/19/timeline
title: '0820 _ Aptos のアカウント生成'
updated_at: '2022-08-20T13:55:24Z'
url: https://api.github.com/repos/ma96o/gialog/issues/19
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
Aptosにおける，アカウント作成時の暗号化手順

0. ユーザーがアカウント作成要求を送信
1. 秘密鍵と公開鍵のキーペアの生成
2. ユーザーから，そのアカウントに適した署名方式を取得
    - 単一署名方式 or マルチシグ方式
3. 公開鍵とユーザーの署名方式を組み合わせ，32バイトの認証鍵を生成する
4. 認証鍵とシーケンス番号（初期値0）の両方が，初期アカウントリソースとしてアカウントに保存される
5. 認証鍵から32バイトのアカウントアドレスを生成

シーケンス番号は，そのアカウントから送信されたトランザクション数を示す．トランザクションにはシーケンス番号を含み，トランザクションを処理する際に，トランザクションに含まれるシーケンス番号とアカウントが保持するシーケンス番号を比較し，一致する場合のみ実行に移す．これはリプレイ攻撃を防ぐためのもので，Ethereum だと nonce にあたる．

アカウントアドレスは，アカウントの識別子として重要なリソースであるが，アカウント生成時に導出される32バイトの認証鍵がそのままアカウントアドレスになる（例： `eeff357ea5c1a4e7bc11b2b17ff2dc2dcca69750bfef1e1ebcaccf8c8018175b` ）．
秘密鍵と公開鍵は後から更新でき，その場合は認証鍵も変更される．しかし，アカウントアドレスは永続的（不変）であり，認証鍵とアカウントアドレスが一致するのは，初期のみで必ずしも一致しない．つまり，既存のアカウントアドレスが変更されることはない．

Aptos の署名方式には2つある．
1. 単一署名方式
2. マルチシグ方式

それぞれの署名方式は以下の署名スキームを用いる
1. `Ed25519`
2. `MultiEd25519`

また，アカウントの認証鍵を生成するには，そのアカウントについて1バイトの署名方式の識別子の指定が必要で，それぞれ以下のように識別子が定められている．
1. 単一署名方式： `0x00`
2. マルチシグ方式：`0x01`

それぞれの署名方式によるアカウントの生成手順は以下である．
- 単一署名方式
  1. キーペア（公開鍵，秘密鍵）の生成
     - RFC 8032 で定義された Ed25519 curve 上の PureEdDSA スキームを使用
  3. 公開鍵から，32バイトの認証鍵を導出
      - `auth_key = sha3-256(publicke | 0x00)`
  5. （永続的な）アカウントアドレスとして，2で導出した初期認証鍵を設定

- マルチシグ方式
  - K-of-Nマルチシグ認証を用いるため，定数 N, K を指定する必要がある
  - K-of-Nマルチシグ認証では，アカウントに合計 N 人の署名者が存在し，N 人の署名のうち少なくとも K 人がトランザクションを認証するためにしようされなければならない
  1. キーペア（公開鍵，秘密鍵）の生成
      - N個のEd25519 公開鍵 p_1, ..., p_n を生成
  3. トランザクションの認証に必要な署名の閾値である`K`の値を決定
  4. 公開鍵と`K`から，32バイトの認証鍵を同種
      - `auth_key = sha3-256(p_1 | ... | p_n | K | 0x01)`
  6. （永続的な）アカウントアドレスとして，3で導出した初期認証鍵を設定
