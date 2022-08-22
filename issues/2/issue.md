---
active_lock_reason: 
assignee: 
assignees: []
author_association: OWNER
closed_at: 
comments: 0
comments_url: https://api.github.com/repos/ma96o/gialog/issues/2/comments
created_at: '2022-07-28T13:24:25Z'
events_url: https://api.github.com/repos/ma96o/gialog/issues/2/events
html_url: https://github.com/ma96o/gialog/issues/2
id: 1320928750
labels: []
labels_url: https://api.github.com/repos/ma96o/gialog/issues/2/labels{/name}
locked: false
milestone: 
node_id: I_kwDOHueoCs5Ou8Xu
number: 2
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
  url: https://api.github.com/repos/ma96o/gialog/issues/2/reactions
repository_url: https://api.github.com/repos/ma96o/gialog
state: open
state_reason: 
timeline_url: https://api.github.com/repos/ma96o/gialog/issues/2/timeline
title: Scrapbox のページに関連用語の説明は含めない方が，情報管理がスッキリする
updated_at: '2022-07-28T13:24:25Z'
url: https://api.github.com/repos/ma96o/gialog/issues/2
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
Scrapbox の運用を始めてから1か月弱が経った．
個人での運用と，複数人での運用を同時期に始めた．

僕が Scrapbox を使う最大の理由は，リンクによってページ間のネットワークを作れることにある．
リンクを有効に使うことで，最低限のコストで快適な情報管理を実現できる．
しかし，そのリンクの使い方にはクセがあり．提供される機能はミニマムなので，使いようによっては情報管理を快適にもするし煩雑で分かりづらいものにもできる．

今日はチームで運用する中で，リンクの使い方について感じたことを書く．
前置きとして，チームや個人毎の目的に沿った適切なリンクの使い方というのがあると思うので，これはその一例である．

それは，リンク運用を行う中で，ある用語もしくは概念，手順を解説するページに関連用語の説明を入れない，つまり関連用語をリンク化するのが良さそうということ．
これは Scrapboxer にとっては当たり前かもしれないが，Scrapbox に使い慣れていない人にとってはやりがちなバッドプラクティスではないかと思う．

例えば，「カレーの作り方」というページがあったときに，「じゃがいもとは」というセクションは不要だろう．
もしもページの中に組み込んでしまえば，「じゃがいも」を用いる他のページで情報が重複してしまって冗長になるか，省いた場合には「じゃがいも」を知らない人にとっては不親切である．
このときに，「じゃがいもを切る」という記述があれば，「じゃがいも」をリンク化し，その説明を別のページに切り出すことが有効だろう．

そうすれば，「じゃがいも」を知らない人が「カレーの作り方」もしくは「ポテトサラダの作り方」を参照したとしても，「じゃがいも」ページを参照すれば済むし，「じゃがいも」を知っている人にとっては，情報の密度が薄まることがなくカレーを作るための必要な情報だけを参照できる．

しかし，そのような運用をしたときに考慮しなければならないのは，同じ用語でも文脈によって意味が変わることである．
そのようなときは，「じゃがいも」ページには一般的な説明を記述して，特定の文脈の中で補足が必要な部分だけを文章として記述すればよい．
つまりページはなるべく疎結合にリンクさせ，独立して意味が完結することを目指す．リンクとして用いるページではその文脈に沿った補足情報を記述するのが良い．

Scrapbox は機能がミニマムだからこそ，（複数人で使う場合は特に）運用ルールが肝心になる．
使えば使うほど，細かいこういうふうに運用すればもっといい感じになるのでは？というのが湧き出てきて，どんどんハマってしまう不思議なツールである．
