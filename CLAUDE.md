# sun_r nail salon — 公式サイト 引き継ぎ

## 作業ルール
- 変更を push（＝公開サイトに反映）したら、返信に必ず公開URLを添える（変更したページのURL。両サイトに関わる場合は両方）
  - sun_r brands：https://sun-r-brands.pages.dev/（/shop・/creative・/build）
  - sun_r nail：https://sun-r-nail.pages.dev/
- sun_r nail と sun_r brands は連動させる。片方を変えたら、もう片方に関わる部分（nail のロゴ・表示名・色・URL・説明文、フッターのブランドナビ、brands のトップの nail の行など）も同じ作業の中で更新し、両方を push する（リポジトリ：`nyancolosan/sun-r-nail`／`nyancolosan/sun-r-brands`）


ネイルサロン「sun_r」の1ページ公式サイト。デザインと中身は確定済みで、`public/index.html` が完成品（動作確認済み）。
このリポジトリの目的は **Cloudflare で一般公開すること**。

## まずやること（公開）

1. `public/index.html` の仕上げ（下の「公開前の仕上げ」）
2. Cloudflare にデプロイ（下の「デプロイ」）
3. 公開URLをスマホとPCで開き、下の「確認項目」をチェック

デザインや文言は変えないこと。迷ったら `docs/spec.md`（デザイン・仕様の正本）に従う。

## ファイル構成

```
public/
  index.html        完成品。CSS・JSはインライン、ロゴはdata URIで埋め込み済み
  images/logo.svg   ロゴ（青い手描きの花、背景透過）
  images/logo.png   同 PNG 2000px 透過
  images/logo-ivory.png  同 PNG 2000px 生成り背景
  images/og-image.png    OGP用 1200x630（生成り地の中央にロゴ）
  images/apple-touch-icon.png  180px
docs/
  spec.md           デザイン・仕様書（色・フォント・構成・料金・アニメーション・波の音）
  logo-with-SUN.svg 「SUN」文字入りの旧ロゴ（参考。サイトでは使わない）
  logo-R.svg        青い「R」の旧ロゴ（参考。サイトでは使わない）
wrangler.jsonc      Cloudflare 設定（public/ を静的配信）
```

## 公開前の仕上げ（index.html）

- ロゴの data URI（3か所：ヘッダー、ヒーロー、favicon）を `images/logo.svg` への相対パスに置き換えて軽量化する（任意だが推奨。見た目は変えない）
- `<head>` に追加：
  - `<link rel="canonical">`（公開URLが決まったら）
  - OGP：`og:title`=sun_r nail salon / `og:description`=既存の meta description / `og:image`=`images/logo-ivory.png`（絶対URL）/ `og:type`=website / `twitter:card`=summary
  - `apple-touch-icon`（logo-ivory.png を180pxに縮小したもの）
  - JSON-LD（`@type: NailSalon`、name: sun_r、url、logo、sameAs: Instagram URL）。住所は載せない。openingHours は定休日が確定するまで入れない
- 外部リンクはすべて `target="_blank" rel="noopener"` 済み。変更不要

## デザインの要点（変更禁止）

- 色：背景 生成り `#F8F7F3`／文字 黒 `#111111`（サブ `#555555`、注記 `#6B6B6B`）／アクセント ブルー `#134CA5`（主ボタン・英字ラベル・カテゴリ名・予約セクション背景のみ）
- フォント：和文 Noto Sans JP、英字（ブランド名 sun_r 含む）League Spartan Regular（オーナー支給の TTF を woff2 に変換し `public/fonts/league-spartan-regular.woff2` から自前で配信。SIL OFL）（2026-11-23 に Zen Kaku Gothic New／Jost から変更。英字は Smooch Sans・Science Gothic・Caveat・Knewave・Boogaloo・Sue Ellen Francisco・Pacifico・Abril Fatface・Cinzel・Special Elite・Mrs Saint Delafield・Abril Fatface を経て League Spartan に）
- 写真は使わない（ロゴのみ）。住所・地図は載せない。LINEは使わない
- アニメーション：読み込み時のロゴ／文字、スクロールでセクションがふわっと表示、ボタンのホバー。`prefers-reduced-motion` で無効化
- 波の音：ヘッダーの「SOUND」ボタンでON（初期OFF）。Web Audio で生成（音声ファイルなし）
- ヒーローのロゴ（2026-11-23 に R から青い花に変更）には番号もイラストも重ねない
- 表示名は「sun_r nail」（ヘッダーとヒーローの大きな文字）。フッターのロゴ文字は「sun_r」のまま
- ヒーローの「PRIVATE NAIL SALON」の下にネイルチップ（`.drops`：爪の形の楕円5つ。色はブルー #134CA5／くすみピンク #E3A9AE／マスタード #E5BD42／セージ #A7C1AA／ベージュ #DCCBB8。派手にしすぎない）。読み込み時に左から順にポンと出て、出たあとにやわらかい光が1回だけ順に横切る。ツヤのハイライトや星などの絵文字的な表現は入れない（チープに見えるため）。常時動く演出にはしない
- スマホのヘッダー：600px 以下でロゴ文字を 16px、420px 以下と 360px 以下で段階的にロゴ文字・SOUND・ご予約の字間と余白を詰めて（Science Gothic のときに追加。以降のフォントでもそのまま）、320px 幅でも横スクロールが出ないようにしている
- フッターに sun_r のブランドナビ（sun_r brands／sun_r nail（現在地）／handmade shop／creative／build）。リンク先は https://sun-r-brands.pages.dev/ 配下で、同じタブで開く（brands へ戻るための導線）

## 確定している情報

- ネット予約：https://beauty.hotpepper.jp/kr/slnH000732849/
- Instagram：https://www.instagram.com/sun___r_nail/
- アクセス：南海電鉄 岸和田駅 中央出口から徒歩2分
- 営業時間：10:00〜20:00
- スタイリスト：riho（JNECネイリスト技能検定 1級／JNAジェルネイル技能検定 上級）
- 料金（税込/税抜は未確定）：
  | メニュー | ご新規様 | リピーター様 |
  |---|---|---|
  | HAND ワンカラー | ¥5,000 | ¥5,000 |
  | HAND グラデーション | ¥5,300 | ¥5,800 |
  | HAND マグネット／ミラー／フラッシュワンカラー | ¥5,800 | ¥6,000 |
  | HAND 定額デザイン | ¥6,300 | ¥6,800 |
  | HAND クリアネイル | ¥4,800 | ¥4,800 |
  | FOOT マグネットワンカラー | ¥8,000 | ¥8,000 |
  | FOOT ワンカラー | ¥7,500 | ¥7,500 |

## 未確定（オーナー確認待ち）

- 定休日・お支払い方法：現在「仮の情報」表示。確定したら差し替え、注記「※定休日・お支払い方法は仮の情報です」を消す。載せない場合は行ごと削除
- 料金の税込/税抜表記

**公開前にオーナーへ確認すること**：仮の情報（定休日・お支払い）が表示されたまま公開してよいか。

## デプロイ（公開済み：Cloudflare Pages + GitHub 自動デプロイ）

- 公開URL：https://sun-r-nail.pages.dev/
- GitHub `nyancolosan/sun-r-nail` の `main` に push すると自動でデプロイされる
- Pages 設定：フレームワークなし／ビルドコマンドなし／ビルド出力ディレクトリ `public`
- 独自ドメインを使う場合：Workers & Pages → sun-r-nail → カスタムドメイン で追加し、index.html の canonical・og:url・og:image・JSON-LD の URL も差し替える
- `wrangler.jsonc` は Workers で配信する場合の設定（現在の Pages 公開では未使用）

## 確認項目（公開後）

- スマホ幅（375px）とPC幅（1280px）でレイアウト崩れがない（スマホではナビが隠れ、ヘッダーはロゴ・SOUND・ご予約の3つ）
- 「ご新規様／リピーター様」で料金が切り替わる
- 「空き状況を見る」「ネット予約」→ホットペッパー、「Instagram」→インスタが別タブで開く
- SOUND ボタンで波の音が鳴り、もう一度押すと止まる
- favicon とロゴが表示される／OGP（LINEやXにURLを貼った時のカード）が出る
