# PERA Experience 案内ページの作り方

社内外向けイベント「AIPC Experience Workshop」の案内ページを、外部ライブラリや画像を使わず、`index.html` の1ファイルで作成しています。

## 1. ページの基本構成を作る

`index.html` にHTML、CSS、JavaScriptをまとめます。

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>AIPC Experience Workshop | PERA Experience</title>
  <style>
    /* ページのデザイン */
  </style>
</head>
<body>
  <!-- 案内ページの内容 -->
  <script>
    // 参加ボタンと申込画面の動作
  </script>
</body>
</html>
```

`viewport` を指定することで、PCだけでなくスマートフォンでも適切な幅で表示されます。

## 2. イベント情報を配置する

ページの主要部分は、イベント名を表示するヒーローエリアと、開催概要を表示する情報カードの2カラム構成です。

- タイトル：AIPC Experience Workshop
- 日時：2026年10月23日 13:00〜15:00
- 内容：生成AI、データ分析、AIエージェントの体験
- 対象：社内外

HTMLでは、見出しに `<h1>`、概要に `<aside>`、体験内容にリストを使用し、情報の意味が分かりやすい構造にします。

## 3. 企業向けのデザインを設定する

CSSのカスタムプロパティに、ページ全体で使用する色を定義します。

```css
:root {
  --ink: #07182f;
  --navy: #0a2342;
  --blue: #176bff;
  --cyan: #47d7e8;
  --paper: #f4f8fc;
  --white: #ffffff;
}
```

信頼感のあるネイビーを基本色にし、ブルーとシアンをアクセントとして使用します。背景のグラデーション、半透明の情報カード、余白を広く取ったレイアウトによって、シンプルで先進的な印象にしています。

## 4. スマートフォン表示に対応する

メディアクエリを使い、画面幅が狭い場合は2カラムから1カラムへ切り替えます。

```css
@media (max-width: 820px) {
  main {
    grid-template-columns: 1fr;
  }
}
```

ボタンや文字サイズ、カード内の余白も画面幅に合わせて調整します。また、`prefers-reduced-motion` に対応し、動きを減らす設定を利用している環境ではアニメーションを抑えます。

## 5. 参加ボタンと申込画面を作る

申込画面にはHTMLの `<dialog>` 要素を使います。JavaScriptで参加ボタンを押したときにダイアログを開き、閉じるボタンや背景クリックで閉じられるようにします。

```javascript
const dialog = document.getElementById('registrationDialog');
const openButton = document.getElementById('openRegistration');

openButton.addEventListener('click', () => dialog.showModal());
```

フォームには、お名前、メールアドレス、参加区分の入力欄を設けます。送信時はページを再読み込みせず、受付完了メッセージへ切り替えます。

## 6. 内容を変更する

イベント名、日時、説明、体験内容は `index.html` 内の表示テキストを直接編集します。配色を変更する場合は、CSS冒頭の `:root` にあるカラーコードを変更します。

実際に申し込みを受け付ける場合は、`registrationForm` の送信処理を社内フォーム、予約サービス、またはAPIへ接続してください。現在の実装は画面上の動作を確認するためのもので、入力内容の保存や外部送信は行いません。
