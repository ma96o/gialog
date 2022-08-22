---
active_lock_reason: 
assignee: 
assignees: []
author_association: OWNER
closed_at: 
comments: 0
comments_url: https://api.github.com/repos/ma96o/gialog/issues/3/comments
created_at: '2022-07-28T13:51:11Z'
events_url: https://api.github.com/repos/ma96o/gialog/issues/3/events
html_url: https://github.com/ma96o/gialog/issues/3
id: 1320966483
labels: []
labels_url: https://api.github.com/repos/ma96o/gialog/issues/3/labels{/name}
locked: false
milestone: 
node_id: I_kwDOHueoCs5OvFlT
number: 3
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
  url: https://api.github.com/repos/ma96o/gialog/issues/3/reactions
repository_url: https://api.github.com/repos/ma96o/gialog
state: open
state_reason: 
timeline_url: https://api.github.com/repos/ma96o/gialog/issues/3/timeline
title: チームで Scrapbox を運用するときに役立ちそうなメモ
updated_at: '2022-07-28T13:51:11Z'
url: https://api.github.com/repos/ma96o/gialog/issues/3
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
- ページ頭に要約やページ自体の説明を書く
  - 一文で収まるとよい
- 一文は完結に，情報密度の薄い部分は省く
   - 〇〇のように，〇〇のため，〇〇の場合，などで一文を繋ぐと冗長になりがち
- 句点いらない
- 固有名詞，専門用語はとりあえずリンクにしておく
- リンクは # をなるべく使わずに，[] を使い文章で関係をつくる
  - #は名詞の書き投げになってしまいがちで，意味がハイコンテクストになる
- 書きかけの記事は #wip などではなく，[TODO] 運用する
   - コーディングにおけるコメントアウトのように [TODO]:${やること} を書いておく
   - 定期的に TODO リンクをスクリーニングするメンテナンス体制を整えるの重要
- なるべくリンクは入力補完で選択する
   - 表記ゆれを防ぐ
- ページ間はなるべく疎結合に，意味を完結させる
- 一つのページが長いと感じた場合は，部分的に他ページに切り出す
