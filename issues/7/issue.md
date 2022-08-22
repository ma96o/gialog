---
active_lock_reason: 
assignee: 
assignees: []
author_association: OWNER
closed_at: 
comments: 1
comments_url: https://api.github.com/repos/ma96o/gialog/issues/7/comments
created_at: '2022-08-04T12:38:09Z'
events_url: https://api.github.com/repos/ma96o/gialog/issues/7/events
html_url: https://github.com/ma96o/gialog/issues/7
id: 1328557893
labels: []
labels_url: https://api.github.com/repos/ma96o/gialog/issues/7/labels{/name}
locked: false
milestone: 
node_id: I_kwDOHueoCs5PMC9F
number: 7
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
  url: https://api.github.com/repos/ma96o/gialog/issues/7/reactions
repository_url: https://api.github.com/repos/ma96o/gialog
state: open
state_reason: 
timeline_url: https://api.github.com/repos/ma96o/gialog/issues/7/timeline
title: '0804 _ Solidity 開発における Visual Studio Code の警告'
updated_at: '2022-08-04T12:49:37Z'
url: https://api.github.com/repos/ma96o/gialog/issues/7
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
Visual Studio Code で開発を行うと，[バックグラウンド分析](https://docs.microsoft.com/ja-jp/visualstudio/code-quality/configure-live-code-analysis-scope-managed-code?view=vs-2022)により警告を表示してくれる．
大体は気になりつつも，その場しのぎで対応してしまっているので，今日は Solidity 開発において初歩的な内容について，いくつか事例を挙げ対応策をまとめた．


## 1. `SPDX license identifier not provided in source file. Before publishing, consider adding a comment containing "SPDX-License-Identifier: <SPDX-License>" to each source file. Use "SPDX-License-Identifier: UNLICENSED" for non-open-source code. Please see https://spdx.org for more information.`

### 現象

![スクリーンショット 2022-08-04 21 35 17](https://user-images.githubusercontent.com/22464192/182848329-a637104e-4203-40c2-b914-6e07f272f208.png)

### 原因

SPDX license identifiers を指定していないから
Solidity はv0.6.8からSPDX license identifiersを取り入れた

### 解決策

SPDX license identifiersを明示する（↓は [UNLICENSED] の場合）

```diff
+ // SPDX-License-Identifier: UNLICENSED
  pragma solidity ^0.8.15;
```

## 2. `Source file requires different compiler version (current compiler is 0.8.13+commit.abaa5c0e.Emscripten.clang) - note that nightly builds are considered to be strictly less than the released version`

### 現象

![スクリーンショット 2022-08-04 21 39 16](https://user-images.githubusercontent.com/22464192/182849111-3da038aa-f071-4142-a87d-6e592f6b8f07.png)

### 原因

Visual Studio Code の workspace compiler のバージョンが，指定したものよりも低いから

### 解決策

workspace compiler をコードで指定したものに揃える

1. 任意の場所で右クリック => 「Solidity Change workspace compiler version (Remote)」を選択
2. コードで指定したバージョン以上のバージョンを選択する

ref. [How to Change the Solidity Compiler in VS Code - Dapp Dev Tips - Medium](https://medium.com/michaels-dapp-dev-tips/how-to-change-the-solidity-compiler-in-vs-code-4c2660a856da)


## 3. `Source "XXX.sol" not found: File import callback not supported`

### 現象

![スクリーンショット 2022-08-04 21 43 50](https://user-images.githubusercontent.com/22464192/182849966-01edbe25-a2c4-4d94-8a96-b7a8c625f924.png)

### 原因

`node_modules/`配下のライブラリを呼んでいないため

### 解決策

デフォルトのパッケージパスに`node_modules/` を指定

1. `settings.json` に↓の記述を追加
   - cmd+shift+p で「settings json」と検索すれば開ける

```diff
+     "solidity.packageDefaultDependenciesContractsDirectory": "",
+     "solidity.packageDefaultDependenciesDirectory": "node_modules",
```

ref. https://ethereum.stackexchange.com/a/111572
