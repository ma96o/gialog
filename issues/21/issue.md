---
active_lock_reason: 
assignee: 
assignees: []
author_association: OWNER
closed_at: 
comments: 0
comments_url: https://api.github.com/repos/ma96o/gialog/issues/21/comments
created_at: '2022-08-22T14:57:59Z'
events_url: https://api.github.com/repos/ma96o/gialog/issues/21/events
html_url: https://github.com/ma96o/gialog/issues/21
id: 1346556211
labels: []
labels_url: https://api.github.com/repos/ma96o/gialog/issues/21/labels{/name}
locked: false
milestone: 
node_id: I_kwDOHueoCs5QQtEz
number: 21
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
  url: https://api.github.com/repos/ma96o/gialog/issues/21/reactions
repository_url: https://api.github.com/repos/ma96o/gialog
state: open
state_reason: 
timeline_url: https://api.github.com/repos/ma96o/gialog/issues/21/timeline
title: '0822 _ PATH'
updated_at: '2022-08-22T15:24:05Z'
url: https://api.github.com/repos/ma96o/gialog/issues/21
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
Linux の PATH について．一度プログラミングを始めた頃に学んだが，そこからなんとなくの理解でこれまでやってきた．今日バイナリファイルをダウンロードして，そのコマンドのパスを通すという作業をしたので，改めて整理しておこうと思う．

そもそも「パスを通す」などで用いられる"パス"は，"コマンドサーチパス"の略称である．

Linux では通常，コマンドを実行するには `$ /usr/bin/passwd` のように，フルパスを指定する必要がある．しかしそれは面倒である．

そこで，Linus のシェルは，フルパスを指定しなくても，設定されたディレクトリにコマンドの実行ファイルを探しにいくようになっている．このとき「シェルがコマンドのバイナリファイルを探しに行くディレクトリを設定する」ことを「パスを通す」という．言い換えれば，コマンドサーチパスを設定するという意味になる．

コマンドサーチパスは，`PATH` という環境変数に格納されている．`$ echo $PATH` を実行すれば，設定されているパスを確認できる．`PATH`には，通したいパスを「:」区切りで指定する．

以下のような出力であれば，`/usr/local/bin`, `/usr/bin`, `/bin` にパスが通っていることが分かる．

```zsh
$ echo $PATH
/usr/local/bin:/usr/bin:/bin
```

追加したいときは，`$ export PATH=$PATH:/usr/sample` のように，現在の `$PATH` に「:」で繋げて通したいパスを指定すれば良い．また，同名のファイルが複数のディレクトリにあった場合，`PATH` に定義されたディレクトリのうち先頭から優先してファイルを実行するので注意が必要．また，セキュリティの観点からも余計なディレクトリを追加せず（パスを通さず），安全なディレクトリに絞って指定することが重要である．