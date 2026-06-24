# DESIGN.md — Mixly Japan

> このファイルはAIエージェントが正確な日本語UIを生成するためのデザイン仕様書です。
> Mixly Japan は「公式ブランドの安心感 × 百貨店の上質感 × 令和のクリーンさ」を体現するショッピングサイトです。
> セクションヘッダーは英語、値の説明・Do's and Don'ts は日本語で記述しています。

---

## 1. Visual Theme & Atmosphere

- **デザイン方針**: 百貨店的・上質・信頼感。お得感より「公式・本物」の安心感を前面に出す。
- **参照イメージ**: 高島屋オンラインストア × 小田急百貨店 × 令和のクリーンUI
- **密度**: ゆとりある余白重視。情報は絞り込み、画像と空白で上質感を演出する。
- **キーワード**: 誠実 / 上質 / 温かみ / 信頼 / 洗練
- **避けるもの**: 楽天・Amazonのような情報過多レイアウト、派手なセール訴求、赤・オレンジの強調色

---

## 2. Color Palette & Roles

### Primary（ブランドカラー）

- **Primary** (`#1A1A2E`): ディープネイビー。ヘッダー・CTAボタン・ブランドロゴに使用。信頼・格調を表現。
- **Primary Light** (`#2D2D4E`): ホバー時・アクティブ状態のプライマリカラー。

### Accent（アクセントカラー）

- **Gold** (`#B8960C`): ゴールド。バッジ・見出しアンダーライン・ランキング番号に限定使用。多用しない。
- **Gold Light** (`#D4AF37`): ホバー時ゴールド。

### Semantic（意味的な色）

- **Official Badge** (`#1A3A5C`): 「公式取扱」「ブランド直営」バッジの背景。お得感より信頼感を示す色。
- **Danger** (`#C0392B`): エラー、削除、在庫切れ表示。
- **Success** (`#27AE60`): 在庫あり、購入完了。
- **Warning** (`#E67E22`): 残り僅か、注意喚起（最小限の使用）。

### Neutral（ニュートラル）

- **Text Primary** (`#1A1A1A`): 本文テキスト。純粋な#000000は使わない（コントラスト強すぎ）。
- **Text Secondary** (`#5C5C5C`): 補足テキスト、ラベル、説明文。
- **Text Tertiary** (`#9B9B9B`): 無効状態、プレースホルダー。
- **Border** (`#E0DDD8`): 区切り線、カード枠線。
- **Background** (`#F8F6F2`): ページ背景。ウォームホワイト。純白は使わない。
- **Surface** (`#FFFFFF`): カード、モーダル、商品画像エリアの面。
- **Surface Dark** (`#F0EDE8`): セカンダリセクション背景（CAMPAIGNセクション等）。

---

## 3. Typography Rules

### 3.1 和文フォント

- **見出し（明朝体）**: Noto Serif JP — 格調・伝統感の演出。H1〜H3に使用。
- **本文（ゴシック体）**: Noto Sans JP — 可読性重視。本文・UI要素・価格に使用。
- **混植方針**: 見出しは明朝体でブランド感を出し、本文・ボタン・価格はゴシック体で読みやすさを確保する。

### 3.2 欧文フォント

- **サンセリフ**: "Helvetica Neue", Arial — 価格・英数字・ナビゲーションに使用。
- **セリフ（装飾用）**: Georgia — キャッチコピーのアルファベット部分に限定使用。
- **等幅**: SFMono-Regular, Consolas — 管理画面等のコード表示用。

### 3.3 font-family 指定

```css
/* 見出し（明朝体混植） */
font-family: "Noto Serif JP", "Georgia", serif;

/* 本文・UI要素（ゴシック体） */
font-family: "Noto Sans JP", "Helvetica Neue", Arial, sans-serif;

/* 価格・数値（欧文優先） */
font-family: "Helvetica Neue", Arial, "Noto Sans JP", sans-serif;

/* 等幅 */
font-family: SFMono-Regular, Consolas, "Liberation Mono", monospace;
```

**フォールバックの考え方**:
- 見出しは和文明朝体（Noto Serif JP）を先に指定し、未インストール環境ではGeorgia→serifにフォールバック。
- 本文・UIは和文ゴシック体（Noto Sans JP）を先に指定。Helvetica Neue は欧文グリフのみ補完。
- 価格・数値は欧文フォントを先頭に置き、数字の視認性を優先。
- Noto Serif JP / Noto Sans JP は Google Fonts から Web Font として読み込む（weight: 300, 400, 500, 700）。

### 3.4 文字サイズ・ウェイト階層

| Role | Font | Size | Weight | Line Height | Letter Spacing | 備考 |
|------|------|------|--------|-------------|----------------|------|
| Display | Noto Serif JP | 48px | 300 | 1.4 | 0.02em | ヒーローキャッチコピー |
| Heading 1 | Noto Serif JP | 32px | 400 | 1.5 | 0.02em | セクションタイトル |
| Heading 2 | Noto Serif JP | 24px | 400 | 1.5 | 0.02em | サブセクションタイトル |
| Heading 3 | Noto Sans JP | 18px | 500 | 1.6 | 0.02em | カードタイトル・商品名 |
| Body | Noto Sans JP | 15px | 400 | 1.9 | 0.04em | 商品説明文・本文 |
| UI Label | Noto Sans JP | 13px | 500 | 1.6 | 0.06em | ボタン・ラベル・ナビ |
| Price | Helvetica Neue | 20px | 700 | 1.4 | 0 | 価格表示（欧文優先） |
| Price Small | Helvetica Neue | 14px | 400 | 1.4 | 0 | 税込表示・参考価格 |
| Caption | Noto Sans JP | 12px | 400 | 1.7 | 0.04em | 注釈・補足・バッジテキスト |

### 3.5 行間・字間

- **本文の行間 (line-height)**: 1.9。日本語の長文は広めが読みやすい。
- **見出しの行間**: 1.4〜1.5。Noto Serif JP はデフォルトより広めに設定。
- **本文の字間 (letter-spacing)**: 0.04em。全角文字の可読性向上。
- **見出しの字間**: 0.02em。明朝体は少し開けることで格調が増す。
- **価格・英数字の字間**: 0。欧文フォントには letter-spacing を与えない。

**ガイドライン**:
- Noto Serif JP の細ウェイト（300）は line-height 1.4 以上必須（詰まって見える）。
- モバイルでは body を 14px に縮小、line-height は維持する。
- letter-spacing が欧文の価格表示に影響しないよう、価格要素には `letter-spacing: 0` を明示する。

### 3.6 禁則処理・改行ルール

```css
/* 基本設定 */
word-break: break-all;
overflow-wrap: break-word;
line-break: strict;
hanging-punctuation: first last;
```

**禁則対象**:
- 行頭禁止: `）」』】〕〉》、。，．・：；？！`
- 行末禁止: `（「『【〔〈《`
- 商品名・ブランド名は途中で改行しない（`white-space: nowrap` または `<wbr>` で制御）。

### 3.7 OpenType 機能

```css
/* 見出し・ナビゲーション（プロポーショナル字詰め） */
font-feature-settings: "palt" 1, "kern" 1;

/* 本文（字詰めなし・均等） */
font-feature-settings: "kern" 1;
```

- **palt**: 見出し・ナビゲーション・バッジに適用。プロポーショナル字詰めで洗練された印象に。
- **kern**: 全要素に適用。和欧混植時の欧文カーニングを有効化。
- 本文には `palt` を適用しない（均等幅の方が長文は読みやすい）。

### 3.8 縦書き

該当なし（現フェーズでは実装不要）。

---

## 4. Component Stylings

### Header / Navigation

- **ヘッダー背景**: `#FFFFFF` / スクロール後: `rgba(255,255,255,0.96)` + backdrop-filter: blur(8px)
- **ロゴ**: Noto Serif JP または SVG。カラー: `#1A1A2E`。
- **グローバルナビ**: Noto Sans JP 13px / weight 500 / letter-spacing 0.06em / color `#1A1A1A`
- **ナビホバー**: color `#B8960C`（ゴールド）+ bottom border 1px solid `#B8960C`
- **検索窓**: 角丸 20px / border 1px solid `#E0DDD8` / フォーカス時 border `#1A1A2E`
- **アイコン（カート・マイページ）**: 20px / color `#1A1A1A` / ラベル Noto Sans JP 10px

### Buttons

**Primary（メインCTA）**
- Background: `#1A1A2E`
- Text: `#FFFFFF` / Noto Sans JP 13px / weight 500 / letter-spacing 0.06em
- Padding: 14px 32px
- Border Radius: 2px（角丸は控えめ。百貨店らしい端正さ）
- Hover: background `#2D2D4E` / transition 0.2s ease

**Secondary（サブCTA）**
- Background: `transparent`
- Text: `#1A1A2E`
- Border: 1px solid `#1A1A2E`
- Padding: 13px 31px
- Border Radius: 2px
- Hover: background `#1A1A2E` / color `#FFFFFF`

**Ghost（軽量CTA: "VIEW MORE" 等）**
- Background: `transparent`
- Text: `#5C5C5C` / 12px / letter-spacing 0.1em
- Border: none / border-bottom 1px solid `#9B9B9B`
- Padding: 4px 0
- Hover: color `#1A1A2E` / border-bottom-color `#1A1A2E`

### Inputs

- Background: `#FFFFFF`
- Border: 1px solid `#E0DDD8`
- Border (focus): 1px solid `#1A1A2E`
- Border Radius: 2px
- Padding: 12px 16px
- Font: Noto Sans JP 14px / color `#1A1A1A`
- Placeholder: color `#9B9B9B`
- Height: 48px（タッチターゲット確保）

### Cards（商品カード）

- Background: `#FFFFFF`
- Border: none（影で浮かせない。フラットに置く）
- Border Radius: 0px（端正さを重視）
- Image Ratio: 1:1 または 3:4（縦長）。object-fit: cover
- Padding（テキストエリア）: 12px 4px 16px
- Gap between cards: 24px（PC）/ 16px（SP）
- **商品名**: Noto Sans JP 14px / weight 500 / 2行まで表示
- **ブランド名**: Noto Sans JP 12px / color `#5C5C5C` / 商品名の上に表示
- **価格**: Helvetica Neue 18px / weight 700 / color `#1A1A1A`
- **税込表示**: Noto Sans JP 11px / color `#9B9B9B`
- **「公式取扱」バッジ**: 背景 `#1A3A5C` / テキスト `#FFFFFF` / 10px / padding 2px 6px / 商品画像左上に絶対配置

### Official Badge（信頼感の核心）

```
背景: #1A3A5C
テキスト: #FFFFFF / Noto Sans JP 10px / weight 500
表示文言: 「公式取扱」または「Brand Official」
位置: 商品画像の左上（position: absolute, top: 8px, left: 8px）
```

- 「セール」「お得」バッジより優先して表示する。
- バッジの色は Primary Color（#1A1A2E）より少し明るい紺（#1A3A5C）で差別化。

### Ranking Numbers

- **1位**: color `#B8960C`（ゴールド）/ Helvetica Neue 20px / weight 700
- **2位**: color `#8C8C8C`（シルバー）
- **3位**: color `#A0785A`（ブロンズ）
- **4位以降**: color `#9B9B9B` / 14px

### Section Headings

```
構成:
  - 英字サブタイトル: Helvetica Neue 11px / letter-spacing 0.15em / color #9B9B9B / 上段
  - 日本語メインタイトル: Noto Serif JP 28px / weight 400 / color #1A1A1A / 下段
  - ゴールドアンダーライン: width 32px / height 1px / background #B8960C / タイトル直下中央
```

例: 上段「RANKING」→ 下段「人気商品ランキング」→ ゴールドライン

---

## 5. Layout Principles

### Spacing Scale

| Token | Value | 用途 |
|-------|-------|------|
| XS | 4px | アイコンと文字の間 |
| S | 8px | バッジ内余白、タグ間 |
| M | 16px | カード間（SP）、入力フィールド内 |
| L | 24px | カード間（PC）、コンポーネント間 |
| XL | 40px | セクション内余白 |
| 2XL | 64px | セクション間余白（PC） |
| 3XL | 96px | ヒーローエリア上下余白 |

### Container

- Max Width: 1280px
- Padding (horizontal / PC): 40px
- Padding (horizontal / SP): 16px

### 背景色の切り替わり部分のpadding

セクションの背景色が変わる箇所（例: ウォームホワイト→白、白→グレーなど）では、**切り替わりの直前セクションの下部padding** と **切り替わり後セクションの上部padding** を必ず同じ値（2XL / 64px）に揃える。

```
[背景色A のセクション]
  padding-bottom: 64px;  ← 色が変わる直前はここに64pxを入れる
─────────── 背景色が切り替わる境界 ───────────
  padding-top: 64px;     ← 色が変わった直後はここに64pxを入れる
[背景色B のセクション]
```

- 同じ背景色が続くセクション同士の間（境界で色が変わらない場合）は、通常のセクション間余白（上部paddingのみ、64px）でよい。下部に追加のpaddingは不要。
- 背景色を新たに追加・変更する際は、必ず上下のセクション両方のpaddingを確認し、この64px/64pxのルールに揃えること。

### Grid（商品一覧）

| ブレークポイント | カラム数 | ガター |
|---|---|---|
| PC (≥1024px) | 5列 | 24px |
| Tablet (768〜1023px) | 3列 | 20px |
| SP (〈768px) | 2列 | 12px |

### Campaign / PICK UP セクション（Bento UI）

```
PC: 大バナー1枚（左・2列分）+ 小バナー2枚（右・1列×2行）の非対称レイアウト
SP: 1列積み重ね
```
均等4分割グリッド（現構成案）から Bento UI へ変更することで、視線が主役バナーへ自然に誘導される。

### Hero Section

- 全幅（100vw）。コンテナ幅に制限しない。
- 画像は `object-fit: cover` / height: 560px（PC）/ 420px（SP）
- テキストオーバーレイは左寄せ・垂直中央。背景に薄いグラデーション（左→透明）で可読性確保。
- CTAボタンは最大2つまで（Primary + Ghost）。

---

## 6. Depth & Elevation

Mixly Japan はフラットデザインを基本とする。影は最小限に留め、余白と色の濃淡で階層を表現する。

| Level | Shadow | 用途 |
|-------|--------|------|
| 0 | none | 商品カード、一般コンテンツ |
| 1 | `0 1px 4px rgba(0,0,0,0.06)` | ヘッダー（スクロール後）、ドロップダウン |
| 2 | `0 4px 16px rgba(0,0,0,0.08)` | モーダル、カートポップアップ |

- **商品カードに影をつけない**。影ではなく余白とボーダーで分離する。
- ホバー時に影を追加する場合は Level 1 のみ許可。

---

## 7. Do's and Don'ts

### Do（推奨）

- 見出しに Noto Serif JP を使い、日本の百貨店らしい格調を出す。
- 「公式取扱」バッジを商品カードの最優先要素として表示する。
- セクション間に十分な余白（64px以上）を設け、上質感を演出する。
- 価格表示は欧文フォント（Helvetica Neue）を使い、数字の視認性を高める。
- ブランドロゴエリアは薄いグレー（#F0EDE8）のカード上に配置し、ホバーで軽く浮かせる。
- ボタンの角丸は 2px 以下に抑え、百貨店らしい端正さを維持する。
- 商品一覧の行間・カード間は余裕を持たせ、ゆっくり選べる体験を作る。
- すべてのインタラクティブ要素に 44px 以上のタッチターゲットを確保する。
- コントラスト比は WCAG AA（4.5:1）以上を維持する（幅広い年代がターゲットのため）。

### Don't（禁止）

- 赤・オレンジのセール訴求色（`#FF0000`, `#FF6600` 等）を目立つ位置に使わない。
- 「○○%OFF」「激安」「SALE」を大きく表示しない（お得感よりブランド感を優先）。
- 商品カードに影をつけてごちゃごちゃさせない。
- 情報を詰め込みすぎない。1カードに表示するのは「ブランド名・商品名・価格・バッジ」のみ。
- font-family に Noto Serif JP のみを指定しない（フォールバックチェーンを必ず書く）。
- 本文に line-height: 1.4 以下を使わない（日本語が読みにくくなる）。
- ボタンの角丸を 8px 以上にしない（カジュアルすぎる印象になる）。
- 背景を純白（`#FFFFFF`）にしない。ページ背景は必ずウォームホワイト（`#F8F6F2`）を使う。
- ランキングセクションのバッジに金銀銅以外の派手な色を使わない。
- グローバルナビに 8 カテゴリ以上を並べない（現構成案の 7 カテゴリは上限ぎりぎり）。

---

## 8. Responsive Behavior

### Breakpoints

| Name | Width | 説明 |
|------|-------|------|
| SP | ≤ 767px | スマートフォン |
| Tablet | 768〜1023px | タブレット |
| PC | ≥ 1024px | デスクトップ |

### タッチターゲット

- 最小サイズ: 44px × 44px（WCAG 2.1 基準）
- ナビアイコン・カートボタン・CTAは必ず 44px 以上確保する。

### モバイル固有の設計

- グローバルナビはハンバーガーメニューに収納（SP時）。
- ヒーローエリアの Display テキストは SP で 28px に縮小（1行に収まるよう調整）。
- 商品カードは 2列グリッド。画像は縦長（3:4）を推奨。
- CTAボタンは画面下部固定（カートへの追加・購入ボタン）または中央配置。
- 価格は目立たせるが、「公式取扱」バッジは省略しない。
- フォントサイズ最小: 12px（Captionのみ）。本文は 14px 以上を維持する。

### 大画面対応（6.5インチ超スマートフォン）

- 主要な操作（検索・カート・購入ボタン）は画面下部から親指で届く領域（下320px以内）に配置。
- 片手・両手操作の両方を考慮したハイブリッド設計。

---

## 9. Agent Prompt Guide

### クイックリファレンス

```
サイト名: Mixly Japan
コンセプト: 公式ブランドの安心感 × 百貨店の上質感 × 令和のクリーンUI

--- カラー ---
Background:    #F8F6F2  （ウォームホワイト）
Surface:       #FFFFFF
Primary:       #1A1A2E  （ディープネイビー）
Gold Accent:   #B8960C  （限定使用）
Text Primary:  #1A1A1A
Text Secondary:#5C5C5C
Border:        #E0DDD8

--- フォント ---
見出し: "Noto Serif JP", "Georgia", serif
本文:   "Noto Sans JP", "Helvetica Neue", Arial, sans-serif
価格:   "Helvetica Neue", Arial, "Noto Sans JP", sans-serif

--- タイポグラフィ ---
Body size: 15px / line-height: 1.9 / letter-spacing: 0.04em
H1 (Serif): 32px / weight 400
H3 (Sans): 18px / weight 500
Price: Helvetica Neue 20px / weight 700

--- ボタン ---
Primary: bg #1A1A2E / text #FFFFFF / border-radius 2px
Secondary: border 1px solid #1A1A2E / transparent bg
Ghost: border-bottom 1px solid / letter-spacing 0.1em

--- キー信念 ---
・「公式取扱」バッジ（#1A3A5C）を最優先で表示
・お得感より信頼感
・余白を贅沢に使う
・影は最小限（フラットデザイン基本）
```

### プロンプト例

```
Mixly Japan の DESIGN.md に従って、商品カードコンポーネントを作成してください。

要件:
- 背景: #F8F6F2
- 商品画像: 縦長（3:4）、object-fit: cover、角丸なし
- 左上に「公式取扱」バッジ（背景 #1A3A5C / テキスト #FFFFFF）
- ブランド名: Noto Sans JP 12px / #5C5C5C
- 商品名: Noto Sans JP 14px / weight 500 / 2行まで
- 価格: Helvetica Neue 18px / weight 700 / #1A1A1A
- 税込表示: 11px / #9B9B9B
- 影なし
- カード間ガター: 24px（PC）
- タッチターゲット: 商品名・価格エリアは 44px 以上
```

---

*Last updated: 2026-06-23 | Version 1.0*
*作成者コメント: カラーパレットは未確定のため、クライアント確認後に Section 2 を更新すること。*
*特にゴールドアクセント（#B8960C）と Official Badge（#1A3A5C）はブランド承認が必要。*
