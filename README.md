# 京都聖ステパノ教会 サイト運用メモ

このディレクトリはサイト本体です。素の HTML/CSS のみで作られており、
特別なソフトやビルド作業は不要です。

## ファイル構成

```
church-site/
├── index.html      … ホーム
├── worship.html    … 礼拝のご案内(Googleカレンダー埋め込み)
├── welcome.html    … 初めての方へ
├── about.html      … 教会について
├── access.html     … アクセス(Googleマップ埋め込み)
├── css/style.css   … デザイン(1ファイル)
├── img/            … 写真置き場
└── README.md       … このファイル
```

## 公開前に必ず差し替えるところ

各 HTML ファイル内の `<!-- ▼ ... ▼ -->` コメントが目印です。
検索(Ctrl+F / ⌘+F)で「▼」を探すと該当箇所に飛べます。

### 1. Google カレンダー(worship.html / index.html)

1. 教会用 Google アカウントで専用カレンダーを作成し、
   設定 → 「一般公開して誰でも利用できるようにする」を有効化
2. 設定 → 「カレンダーの統合」から次の3つを控える:
   - カレンダーID(例: `example@group.calendar.google.com`)
   - 埋め込みコード(iframe の src)
   - iCal 形式の公開 URL
3. `worship.html` の以下2箇所を書き換える:
   - PC用の iframe `src` を `mode=MONTH` の埋め込み URL に
   - スマホ用の iframe `src` を `mode=AGENDA` の埋め込み URL に
4. 「Google カレンダーに追加」ボタンの
   `href="https://calendar.google.com/calendar/render?cid=(カレンダーID)"`
   を実際のカレンダーIDに書き換え
5. 「iCal 形式で購読する」ボタンの `href` を iCal 公開 URL に書き換え

### 2. Google マップ(access.html / index.html)

1. Google マップで教会所在地を検索
2. 「共有」→「地図を埋め込む」→ iframe をコピー
3. 各ファイルの `<iframe src="about:blank" ...>` の src を、
   コピーした src(`https://www.google.com/maps/embed?pb=...`)に置き換え

### 3. 写真

`img/` に以下のようなファイル名で保存し、各ページの
`<div class="gallery__img is-placeholder" ...>` のブロックを
`<div class="gallery__img"><img src="img/xxxx.jpg" alt="..."></div>` に置き換える。

- `exterior.jpg` … 聖堂外観
- `interior.jpg` … 聖堂内観
- `stainedglass.jpg` … ステンドグラス
- `altar.jpg` … 祭壇
- `hall.jpg` … 集会室
- `garden.jpg` … 教会の庭
- `route-01.jpg` `route-02.jpg` `route-03.jpg` … 桂駅からの道順

写真は横幅 1600px 程度、JPEG で保存すると読み込みが軽くなります。

### 4. 文面の埋めどころ

- `about.html` … 沿革・司祭紹介
- `access.html` … 桂駅からの具体的な道順
- 全ページ共通 … 住所の番地(現行ブログの文字化けから復元できていません)

## 公開方法(GitHub Pages)

1. GitHub でリポジトリを作成し、この `church-site` の中身をすべてアップロード
2. リポジトリの Settings → Pages → Source を「main」ブランチのルートに設定
3. 数分待つと `https://<ユーザー名>.github.io/<リポジトリ名>/` で公開されます

## 更新の目安

| 更新対象 | 頻度 | 作業 |
|----------|------|------|
| 礼拝スケジュール | 随時 | Google カレンダー側で編集(HTML は触らない) |
| 沿革・司祭など基本情報 | 稀 | 該当ページを編集して GitHub にアップロード |
| 写真 | 稀 | `img/` のファイルを差し替え |

礼拝スケジュールは Google カレンダーへの入力だけで
サイトにも自動反映されます。HTML を編集する必要はありません。
