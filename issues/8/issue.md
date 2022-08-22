---
active_lock_reason: 
assignee: 
assignees: []
author_association: OWNER
closed_at: 
comments: 0
comments_url: https://api.github.com/repos/ma96o/gialog/issues/8/comments
created_at: '2022-08-05T15:34:03Z'
events_url: https://api.github.com/repos/ma96o/gialog/issues/8/events
html_url: https://github.com/ma96o/gialog/issues/8
id: 1330086605
labels: []
labels_url: https://api.github.com/repos/ma96o/gialog/issues/8/labels{/name}
locked: false
milestone: 
node_id: I_kwDOHueoCs5PR4LN
number: 8
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
  url: https://api.github.com/repos/ma96o/gialog/issues/8/reactions
repository_url: https://api.github.com/repos/ma96o/gialog
state: open
state_reason: 
timeline_url: https://api.github.com/repos/ma96o/gialog/issues/8/timeline
title: '0805 _ ERC721PresetMinterPauserAutoId'
updated_at: '2022-08-05T15:37:41Z'
url: https://api.github.com/repos/ma96o/gialog/issues/8
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
ERC721に準拠したシンプルなNFTを実装する際，OpenZeppelin を利用するのがデファクトスタンダード．
OpenZeppelin は Presets というコントラクトテンプレートを提供してくれているので，開発が楽に済む上に脆弱性の観点からも安心できる．

ERC721に準拠したOpenZeppelin の Presets が `ERC721PresetMinterPauserAutoId` である．

Docs: [Presets - OpenZeppelin Docs](https://docs.openzeppelin.com/contracts/3.x/api/presets#ERC721PresetMinterPauserAutoId)

source code: [openzeppelin-contracts/ERC721PresetMinterPauserAutoId.sol at master · OpenZeppelin/openzeppelin-contracts](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/token/ERC721/presets/ERC721PresetMinterPauserAutoId.sol#L79)

ERC721PresetMinterPauserAutoIdでは、ERC721 で提供される機能に加えて，さまざまな関数が Interface として定義されている．

その一例が以下．

- トークンの burn 機能
- トークンの mint を可能にする mintor の役割
- すべてのトークンに対する transfer を停止させることができる pauser ロール
- トークンIDおよびURIの自動生成

特に，ロール を付与して指定したアカウントに対して，アクション権限を付与できるのが特徴的である．

これは，[AccessControl](https://docs.openzeppelin.com/contracts/3.x/api/access#AccessControl) というモジュールを使用することで可能にしている．

コントラクトをデプロイするアカウントには，minter と pauser のロール，そしてデフォルトの admin ロールが付与され，他のアカウントに minter と pauser の両方のロールを付与できる．

NFT を発行するために提供される基本的な機能は以下．

- 更新系
  - mint(address to) ... 自動生成されたトークンIDでトークンを発行し、トークンの所有者を引数のアドレスのアカウントに設定
  - transferFrom(address from, address to, uint256 tokenId) ... tokenIdのトークンをfrom アカウントから to アカウントに譲渡
  - burn(uint256 tokenId) ... tokenIDのトークンを消す
- 参照系
  - name() ... トークンのnameを取得
  - symbol() ... トークンのsymbolを取得
  - tokenURI(uint256 tokenId) ... tokenURIを取得
  - totalSupply() ... トークンの発行総数を取得
  - ownerOf(uint256 tokenId) ... tokenIdのトークンの所有者のアドレスを取得
  - balanceOf(address owner) ... アドレスのアカウントのトークン保有数を取得
