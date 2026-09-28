# mornie! サポートサイト

mornie! のアプリのサポート情報・プライバシーポリシーをまとめた静的サイトです。
HTML / CSS のみで構成しています（JavaScript・外部ライブラリ・解析ツール・Cookie は使っていません）。

このリポジトリは **サイト全体の枠と導線** を管理します。
各アプリのサポート本文・プライバシーポリシー本文は、各アプリのプロジェクト側で作成し、
このサイトの **[BODY] エリア** に差し替えます。

---

## ファイル構成

**公開されるのは `docs/` の中だけ** です。それ以外（`templates/`・この README）は管理用で、公開されません。

```
/
├─ README.md                           この説明（管理用・非公開）
├─ templates/                          ★ 管理用：新しいページを作るときのひな形（非公開）
│  ├─ app/                             公開中アプリ用
│  │  ├─ index.html                      サポート
│  │  └─ privacy/index.html              プライバシーポリシー
│  └─ app-coming-soon/                 準備中アプリ用
│     ├─ index.html                      サポート（準備中）
│     └─ privacy/index.html              プライバシーポリシー（準備中）
└─ docs/                               ★ 公開領域（GitHub Pages の公開元）
   ├─ index.html                       トップページ
   ├─ .nojekyll                        Jekyll 処理を無効化するための空ファイル
   ├─ assets/
   │  ├─ css/style.css                 全ページ共通のスタイル
   │  └─ img/favicon.svg               ファビコン
   └─ apps/                            アプリ別ページ
      ├─ mornie/                       公開中
      │  ├─ index.html                   サポート
      │  └─ privacy/index.html           プライバシーポリシー
      ├─ ikimono-no-sumika/            準備中
      │  ├─ index.html
      │  └─ privacy/index.html
      └─ okaimono-memo/                準備中
         ├─ index.html
         └─ privacy/index.html
```

URL は `docs/` を基準に次の形になります。

| ページ | ファイル | URL |
|---|---|---|
| トップ | `docs/index.html` | `/` |
| サポート | `docs/apps/<スラッグ>/index.html` | `/apps/<スラッグ>/` |
| プライバシーポリシー | `docs/apps/<スラッグ>/privacy/index.html` | `/apps/<スラッグ>/privacy/` |

---

## GitHub Pages の公開設定

リポジトリの **Settings → Pages** で次のように設定します。

| 項目 | 値 |
|---|---|
| Source | Deploy from a branch |
| Branch | `main` |
| Folder | `/docs` |

- すべて相対パスで書いているため、プロジェクトサイト（`https://<user>.github.io/<repo>/`）でも独自ドメインでもそのまま動作します。
- 独自ドメインを使う場合、`CNAME` ファイルは `docs/` 直下に置かれます（Pages の設定画面から登録すると自動で作られます）。

---

## 目印（コメント）のルール

各 HTML には、次の3種類の目印コメントを入れています。
エディタで `[BODY]` などを検索すると、すぐに該当箇所へ移動できます。

| 目印 | 意味 | 誰が編集するか |
|---|---|---|
| `[BODY]` | **本文エリア**。`▼▼▼` から `▲▲▲` までの間を自由に差し替えてよい | 各アプリのプロジェクト |
| `[FRAME]` | ページの枠（見出し・パンくず・お問い合わせ・戻るリンクなど）。**アプリ名だけ** 書き換える | このサイト |
| `[COMMON]` | 全ページ共通のヘッダー・フッター。変更するときは **全ページ** 同じように直す | このサイト |

トップページ（`docs/index.html`）では、ほかに次の目印を使っています。

| 目印 | 内容 |
|---|---|
| `[TOP]` | サイト説明 |
| `[APP-LIST]` | アプリカード一覧（公開中・準備中） |
| `[SUPPORT-TABLE]` | サポート・プライバシーポリシーの一覧表 |
| `[CONTACT]` | 共通問い合わせ先 |

---

## 差し替え箇所の一覧

| やりたいこと | ファイル | 編集する場所 |
|---|---|---|
| アプリのサポート本文を差し替える | `docs/apps/<スラッグ>/index.html` | `[BODY]` |
| アプリのプライバシーポリシー本文を差し替える | `docs/apps/<スラッグ>/privacy/index.html` | `[BODY]` |
| トップのアプリ説明文を変える | `docs/index.html` | `[APP-LIST]` の該当カードの `app-card__desc` |
| サイト説明文を変える | `docs/index.html` | `[TOP]` |
| 問い合わせメールアドレスを変える | `docs/` と `templates/` の全 HTML | `mornie.official@gmail.com` を一括置換 |
| ヘッダー・フッターを変える | `docs/` と `templates/` の全 HTML | `[COMMON]` |
| 色を変える | `docs/assets/css/style.css` | 先頭の `:root` |

### [BODY] を書くときに使える部品

| 部品 | 書き方 |
|---|---|
| セクション見出し（サポート） | `<h2 class="section-title">見出し</h2>` |
| 囲み | `<div class="panel">…</div>`（淡色は `panel panel--soft`） |
| 条項見出し（ポリシー） | `<h2>` / `<h3>`（`.policy` の中で自動的に整います） |
| 制定日・改定日（ポリシー） | `<div class="policy-dates"><p>制定日：…</p></div>` |
| 補足の小さい文字 | `<p class="note">…</p>` |
| ボタン | `<a class="btn" href="…">` / `<a class="btn btn--ghost" href="…">` |

### 現在の mornie の本文について

`docs/apps/mornie/` の `[BODY]` には **正式な本文** が入っています。
サポートページの「お問い合わせの際にお知らせいただけると助かること」は、mornie 向け（iPhone / iOS）の項目に調整しています。

---

## 新しいアプリを追加する手順（準備中として追加）

例：スラッグ `new-app`、アプリ名「新しいアプリ」

1. **フォルダをコピー**
   `templates/app-coming-soon/` をコピーして `docs/apps/new-app/` にする
2. **プレースホルダーを置換**（`docs/apps/new-app/` 内の2ファイル）
   - `{{APP_NAME}}` → `新しいアプリ`
   - `{{APP_INITIAL}}` → アイコンに表示する1文字（例：`新`）
3. **ひな形用の説明を削除**（2ファイルとも）
   先頭の `【ひな形】…` のコメントブロック（`<html>` の直後）
4. （任意）アイコン色を `coming-soon__icon--sky` / `--peach` / `--sage` から選ぶ
5. **トップページに追加**（`docs/index.html`）
   - `[APP-LIST]` の「準備中のアプリ」に、既存の準備中カード `<li>`（`▽`〜`△` の範囲）をコピーして書き換え
   - `[SUPPORT-TABLE]` に `<tr>` を1行追加（「（準備中）」付き）

## 準備中のアプリを公開する手順

1. **ページを差し替え**
   `templates/app/` の2ファイルで `docs/apps/<スラッグ>/` の2ファイルを上書きし、
   上の手順2・3と同じように置換・削除する（`{{APP_INITIAL}}` はありません）
2. **本文を入れる**
   各ファイルの `[BODY]` にある `body-placeholder` を、アプリのプロジェクトで作った本文に置き換える
3. **トップページを更新**（`docs/index.html`）
   - `[APP-LIST]` の該当カードを「準備中のアプリ」から「公開中のアプリ」へ移動
   - `app-card--soon` を外し、`badge--soon` → `badge--live`、「準備中」→「公開中」
   - 説明文を書き換え、mornie のカードと同じようにボタン2つを追加
   - `[SUPPORT-TABLE]` の該当行から「（準備中）」を削除

## 確認チェックリスト

- [ ] `docs/` 内を `{{` で検索して、置換漏れがない
- [ ] `docs/` 内に `【ひな形】` が残っていない
- [ ] トップのカード・一覧表から、各ページへ移動できる
- [ ] スマホ幅でも表示が崩れない

---

## パスについて

- `templates/app/` と `docs/apps/<スラッグ>/` は、`assets/` から見て同じ深さになるよう作ってあります。
  コピーするだけで、パスの修正は不要です。
- そのため `templates/` 内のファイルを **その場で開くと CSS は効きません**（コピー元専用のため問題ありません）。

## ローカルでの確認

リンクがフォルダ（`apps/mornie/` など）を指しているため、ファイルを直接開くより
簡易サーバーで確認するのがおすすめです（Node.js が必要）。
公開時と同じ見え方にするため、**`docs/` を起点に** 起動します。

```
npx serve docs
```
