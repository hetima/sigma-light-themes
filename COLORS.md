# CSS変数（vars.css）使用箇所まとめ

[src/styles/vars.css](src/styles/vars.css) の `:root`（ライトテーマ）と `.dark`（ダークテーマ）で定義されている色・サイズ変数の一覧と、コードベース内での使用箇所のまとめ。

色は基本的に `hsl(var(--変数名))` の形式で参照され、HSL値（色相 彩度 明度）のトリプレットとして定義されている。

---

## テーマカラー（SIGMA-UI 基本色）

ライト（`:root`）とダーク（`.dark`）で値が切り替わる色。

| 変数 | ライト | ダーク | 役割と主な使用箇所 |
|---|---|---|---|
| `--background` | `50 24% 96%` | `225 10% 16%` | アプリ全体の背景色。`main.css` の `body`、トースト、ダイアログ、ボタン、スイッチ、スライダー、ドラッグオーバーレイ、設定画面など約25ファイル |
| `--foreground` | `20 20% 13%` | `0 0% 75%` | 基本の文字色。最多使用（約85ファイル）。ボタン・ラベル・各種UIコンポーネント、ナビゲーター、設定、拡張機能、ホーム画面などほぼ全域 |
| `--background-2` | `45 20% 90%` | `225 10% 16%` | 一段違いの背景色。タブ（[tab.vue](src/modules/tab-bar/tab/tab.vue)）、ナビサイドバー、情報パネル、リスト列エディター、ステータスバー、グローバル検索など |
| `--background-3` | `50 21% 95%` | `225 12% 13%` | さらに深い背景色。アプリルート（[app.vue](src/app.vue)、[layouts/window/app.vue](src/layouts/window/app.vue)）、ウィンドウツールバー、グリッドビュー、リストヘッダー、クリップボードツールバーなど |
| `--muted` | `45 18% 90%` | `225 10% 20%` | 控えめな背景色。スケルトン、タブトリガー、セパレーター、ダイアログ群、拡張機能カード、リストビューなど約35ファイル |
| `--muted-foreground` | `22 12% 34%` | `0 0% 62%` | 補助テキスト色。2番目に多用（約90ファイル）。説明文・ショートカット表示・プレースホルダー・アイコンなど全域 |
| `--popover` | `50 26% 97%` | `225 10% 16% / 50%` | ポップオーバー系の背景。tooltip / select / dropdown-menu / context-menu / popover / dialog / command / combobox の各 content コンポーネント |
| `--popover-foreground` | `20 20% 13%` | `0 0% 75%` | ポップオーバー系の文字色。上記 content と item / trigger 系コンポーネント |
| `--card` | `50 22% 95%` | `225 10% 16% / 80%` | カード背景。[card.vue](src/components/ui/card/card.vue)、エントリーカード、ドライブカード、ユーザーディレクトリカード、拡張機能カード、設定アイテムなど |
| `--card-foreground` | `20 20% 13%` | `210 20% 98%` | カード文字色。card.vue、ユーザーディレクトリカード、ドライブカード |
| `--border` | `36 18% 82%` | `225 10% 20%` | 境界線色。`main.css` の全要素デフォルト境界色のほか、各種UIコンポーネント・セパレーター・リストヘッダーなど約75ファイル |
| `--input` | `45 18% 91%` | `225 10% 16% / 50%` | 入力欄の境界・背景。[input.vue](src/components/ui/input/input.vue)、[select-trigger.vue](src/components/ui/select/select-trigger.vue)、拡張機能フォーム |
| `--primary` | `16 53% 50%` | `198 19% 38%` | アクセントカラー。選択状態・チェックボックス・スイッチ・スライダー・タブのアクティブ表示・ドロップターゲット色の基準など約50ファイル。[main.ts](src/main.ts) からJSでも参照 |
| `--primary-foreground` | `50 26% 97%` | `220.9 39.3% 11%` | primary 上の文字色。チェックボックス、changelog ダイアログ、マウントダイアログなど |
| `--secondary` | `45 18% 90%` | `222 10% 18%` | 第二背景色。ボタンの secondary バリアント、メニューアイテムのホバー背景、タブリスト、ステータスバーなど約25ファイル |
| `--secondary-foreground` | `20 18% 18%` | `0 0% 60%` | secondary 上の文字色。ボタン、メニューアイテム、フィルター系コンポーネント |
| `--destructive` | `0 84.2% 60.2%` | `0 62.8% 50%` | 危険操作・エラー色。削除ボタン、ウィンドウ閉じるボタン（[window-actions.vue](src/modules/window-toolbar/window-actions.vue)）、削除確認ダイアログ、エラー表示など約25ファイル |
| `--destructive-foreground` | `210 20% 98%` | `210 20% 98%` | destructive 上の文字色。[button.vue](src/components/ui/button/button.vue) のみ |
| `--ring` | `16 45% 44%` | `216 12.2% 83.9%` | フォーカスリング色。input / button / checkbox / switch / slider / tabs などフォーカス可能な全UIコンポーネント（約23ファイル） |
| `--success` | `174deg 100% 27%` | 同じ | 成功色（ティール）。クリップボードツールバー、ショートカット設定、グリッド/リストビューの状態表示 |
| `--warning` | `4deg 82% 58%` | 同じ | 警告色（赤）。トースト進捗、クリップボードツールバー、グリッド/リストビューの状態表示 |
| `--icon` | `18 18% 34%` | `0 0% 62%` | アイコン色（`color` / `stroke`）。ナビサイドバー、クイックアクセスパネル、設定アイテム・アクション、拡張機能ツールバー |
| `--light` | `0 0% 100%` | 同じ | **未使用**（定義のみ） |
| `--dark` | `0 0% 0%` | 同じ | **未使用**（定義のみ） |
| `--window-toolbar` | `42 22% 92%` | `220 11% 19%` | **未使用**（定義のみ） |

---

## ホバートランジション

| 変数 | 値 | 使用箇所 |
|---|---|---|
| `--hover-transition-duration-in` | `0s` | ホバー開始は即時。下記9ファイルで共通使用 |
| `--hover-transition-duration-out` | `0.15s` | ホバー解除はアニメーション。同上 |
| `--hover-transition-easing-out` | `ease-out` | 同上 |

使用ファイル: ダッシュボード（[dashboard.vue](src/modules/dashboard/pages/dashboard.vue)、[entry-card.vue](src/modules/dashboard/components/entry-card.vue)）、ホーム画面のカード類（drive-card / drives-section / user-directory-card / user-directories-section）、ファイルブラウザー（grid-card / list-view / address-bar-editor-suggestion-row）。

---

## ドロップターゲット（ドラッグ&ドロップ先の強調表示）

`--primary` を基準にした半透明色。

| 変数 | 値 | 使用箇所 |
|---|---|---|
| `--drop-target-background` | `hsl(var(--primary) / 15%)` | タブ、アドレスバー、グリッドカード、リストビュー、クイックアクセスパネル |
| `--drop-target-subtle-background` | `hsl(var(--primary) / 8%)` | [drop-target-card.vue](src/components/drop-target-card/drop-target-card.vue)、ダッシュボード、ホームのセクション類 |
| `--drop-target-outline` | `2px dashed hsl(var(--primary) / 60%)` | 上記すべて（計9ファイル） |
| `--drop-target-outline-offset` | `-2px` | 同上 |

---

## ドライブ使用量インジケーター

ホーム画面のドライブ容量表示専用。緑（余裕あり）/ 赤（残量少）。

| 変数 | 値 | 使用箇所 |
|---|---|---|
| `--drive-progress-color-green` | `174deg 100% 27%` | [circular-progress.vue](src/modules/home/components/indicators/circular-progress.vue) |
| `--drive-progress-color-red` | `4deg 82% 58%` | 同上 |
| `--drive-progress-bg-green` / `-red` | 上記の25% / 18%透過 | [linear-bar.vue](src/modules/home/components/indicators/linear-bar.vue)、[edge-indicator.vue](src/modules/home/components/indicators/edge-indicator.vue) |
| `--drive-progress-glow-green` / `-red` | グロー（box-shadow） | 同上 |

---

## サイズ

| 変数 | 値 | 使用箇所 |
|---|---|---|
| `--nav-sidebar-width` | `42px` | [nav-sidebar.vue](src/modules/nav-sidebar/nav-sidebar.vue) |
| `--quick-access-panel-width` | `260px` | [quick-access-panel.vue](src/modules/nav-sidebar/components/quick-access-panel.vue) |
| `--window-toolbar-height` | `48px` | ウィンドウツールバー、タブバー、ナビサイドバー、各ページの高さ計算（`calc(100vh - ...)`）、`--tab-height` の基準。計8ファイル |
| `--tab-height` | `calc(var(--window-toolbar-height) - 16px)` | [tab.vue](src/modules/tab-bar/tab/tab.vue)、[tab-draggable.vue](src/modules/tab-bar/tab-draggable/tab-draggable.vue) |
| `--navigator-list-view-entry-height` | `42px` | [file-browser-list-view.vue](src/modules/navigator/components/file-browser/file-browser-list-view.vue) |
| `--navigator-grid-view-dir-entry-height` | `52px` | [file-browser-grid-card.vue](src/modules/navigator/components/file-browser/file-browser-grid-card.vue) |
| `--navigator-grid-view-entry-height` | `120px` | 同上 |
| `--ring-outline-offset` | `0px` | フォーカスリングのオフセット。UIコンポーネント全般（input / button / checkbox / dialog / slider / switch / tabs / combobox 等、約20ファイル） |
| `--action-toolbar-height` | `42px` | **未使用** |
| `--workspace-toolbar-height` | `48px` | **未使用** |
| `--info-panel-width-value` / `--info-panel-width` | `280` / `calc(... * 1px)` | **未使用**（vars.css 内の相互参照のみ） |
| `--info-panel-preview-height` | `158px` | **未使用** |
| `--info-panel-header-height` | `32px` | **未使用** |
| `--info-panel-sub-header-height` | `16px` | **未使用** |
| `--info-panel-properties-header-height` | `36px` | **未使用** |
| `--navigator-sorting-header-height` | `36px` | **未使用** |
| `--control-button-width` | `46px` | **未使用** |
| `--dir-entry-transition` | `all 0.3s ease-in-out` | **未使用** |

---

## SIGMA-UI 汎用（角丸・影・フォント・ブラー）

| 変数 | 値 | 使用箇所 |
|---|---|---|
| `--radius` | `0.5rem` | 角丸の基準値。カード、ボタン、ダイアログ、トースト、設定アイテムなど約35ファイル。下記 radius 系の基準 |
| `--radius-xl` | `calc(var(--radius) + 4px)` | **未使用** |
| `--radius-lg` | `var(--radius)` | ダイアログ系（dialog-content / dialog-scroll-content / changelog-dialog） |
| `--radius-md` | `calc(var(--radius) - 2px)` | メニュー系コンテンツ（dropdown / context-menu / select / command）、tooltip、skeleton、アドレスバーなど約19ファイル |
| `--radius-sm` | `calc(var(--radius) - 4px)` | 最多使用の角丸（約40ファイル）。メニューアイテム、タブ、入力欄、リストヘッダー、ナビサイドバーなど小要素全般 |
| `--radius-xs` | `min(calc(var(--radius) / 2.5), 6px)` | [checkbox.vue](src/components/ui/checkbox/checkbox.vue)、[info-panel.vue](src/modules/navigator/components/info-panel/info-panel.vue) |
| `--radius-full` | `9999px` | 完全な丸。switch / slider / scroll-bar / drawer |
| `--backdrop-filter-blur` | `32px` | 背景ブラー量。ポップオーバー系コンテンツ全般（tooltip / select / dropdown / context-menu / popover / dialog / combobox）とグリッドビュー |
| `--font-mono` | 等幅フォントスタック | `markdown-content.css`、拡張機能カード・詳細、完全削除確認ダイアログ |
| `--shadow-md` | 多層 box-shadow（弱） | メニュー系コンテンツ、トーストカード、クイックアクセスパネル |
| `--shadow-lg` | 多層 box-shadow（強） | ダイアログ系（dialog / command-dialog / changelog-dialog） |

---

## 備考

- `color-scheme: light;` / `color-scheme: dark;` はブラウザネイティブUI（スクロールバー、フォームコントロール等）の配色をテーマに合わせるための宣言。
- テーマ切り替えは `<html>` 等への `.dark` クラス付与で行われ、変数値が上書きされる仕組み。
- **未使用**とマークした変数（`--light`、`--dark`、`--window-toolbar`、info-panel 系サイズ、`--action-toolbar-height`、`--workspace-toolbar-height`、`--navigator-sorting-header-height`、`--control-button-width`、`--dir-entry-transition`、`--radius-xl`）は `src` 内に参照が見つからなかったもの（2026-06-10 時点）。
