# フロントエンドの開発チュートリアル
Next.jsでの開発方法です。

## セットアップ
nvmをインストールし、nvmでNode.jsをインストールします。

### Node.js
> JavaScriptをブラウザ上ではなくOS上で実行するための実行環境。開発ツールやパッケージが必要になるwebアプリ開発ではNode.jsが必須。

### nvm(Node Version Manager)
> Node.jsをインストール・管理するためのツール。Node.jsをインストールしたり、バージョンを切り替えて複数のバージョンのNode.jsを利用したりすることができる。

### nvmのインストール(scoopを利用)
```bash
scoop install nvm
```

### Node.jsのインストール
今回はversion.18.20.3をインストール
```bash
nvm install 18.20.3
nvm use 18.20.3
```

Node.jsをインストールすると、`npm`や`npx`コマンドが利用できます。

### npm(Node Package Manager)
> Node.jsのパッケージ（ライブラリやツール）をインストール・管理するためのツール。


### npx(Node Package Execute)
> 一時的にパッケージを実行するためのツール。

名前が似ているのでまとめ。
| ツール | 役割 |
| ----- | ---- |
| `nvm` | Node.js(実行環境)のインストールと管理 |
| `npm` | ツールやパッケージのインストールと管理 |
| `npx` | `npm`でインストールしたパッケージ等の実行 |

## Next.jsプロジェクトの立ち上げ
プロジェクトを立ち上げたい場所まで移動し、以下のコマンドを実行。
```bash
npx create-next-app@latest
```

実行後、プロジェクトに関するいくつかの質問に答えていくとプロジェクトフォルダが作成されます。
質問の `No / Yes` は十字キーの`←`と`→`で選択して`Enter`で決定します。
```bash
# プロジェクト名を入力
? What is your project named? ... my-app
# TypeScript(静的型付けの言語)を利用するか？ [迷ったらYes 初心者はNoでもいいかも]
? Would you like to use TypeScript? ... No / Yes
# ESLint(構文エラーやコーディング規約の静的解析ツール)を利用するか？ [迷ったらYes]
? Would you like to use ESLint? ... No / Yes
# Tailwind CSS(CSSフレームワーク)を利用するか？ [迷ったらYes]
? Would you like to use Tailwind CSS? ... No / Yes
# ソースコードをsrc/ディレクトリ下に置くようにするか？ [YesかNoかは好み(個人的にはNo)]
? Would you like your code inside a `src/` directory? ... No / Yes
# Appルーターを利用するか？(以前はPageルーターが利用されていたがより便利なAppルーターが追加された) [迷ったらYes]
? Would you like to use App Router? (recommended) ... No / Yes
# Turbopack(バンドラ)を利用するか？ [迷ったらYes]
? Would you like to use Turbopack for `next dev`? ... No / Yes
# エイリアスをカスタマイズするか？(デフォルトは '@/*' ) [迷ったらNo]
? Would you like to customize the import alias (`@/*` by default)? ... No / Yes
```
質問の回答によって次の質問が若干変わったりします。

## 開発サーバーの立ち上げ

### プロジェクトフォルダへの移動
プロジェクトを作成したらプロジェクトフォルダに移動します。
```bash
cd .\my-app
```

### エディタの起動
ここではVSCodeを起動しています。
```bash
code .
```

### 開発サーバーの立ち上げ
以下のコマンドを実行します。
```bash
npm run dev
```

立ち上げに成功すると以下のような表示になると思います。
```bash
> pdf-editor@0.1.0 dev
> next dev

   ▲ Next.js 15.0.3
   - Local:        http://localhost:3000

 ✓ Starting...
 ✓ Ready in 4.2s
```

`http://localhost:3000`を Ctrl + クリック すると開発中のwebページをブラウザで閲覧することができます。
このとき、プロジェクト内のコードの内容を変更して保存するとリアルタイムでwebページの内容が更新されます。
開発中はこのwebページを見ながら開発していくことになると思います。

また、このwebページは同じネットワークにつながっているデバイスからなら基本的にはアクセス可能です。
開発サーバーを立ち上げているときにスマホなどのブラウザで`http://<自分のパソコンのIPアドレス>:3000`と検索するとwebページを閲覧することができます。
スマホ用のwebアプリを開発するときにはよく利用すると思います。

## フロント開発でおすすめのVSCode拡張機能
- [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)(**推奨**) : HTML, CSS, JavaScriptなどのフロント開発周りの言語対応のフォーマッターです。自動的にインデントや改行, 適切な空白を入れてくれます。
- [Tailwind CSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss)(**推奨**) : Tailwind CSSを利用する際にサジェストが利用できるようになります。
- [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme) : ファイルアイコンを追加します。フロント開発ではいろんな拡張子のファイルを扱うからあると便利かも。

Prettierでは上書き保存の際に自動的にフォーマッティングを行うように設定すると便利です。
1. ワーキングフォルダ直下に`.vscode/settings.json`を作成
1. 作成したフォルダ内に以下の内容を記述
```json
{
    "editor.tabSize": 2,
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
}
```

## git-czのインストール
このリポジトリでは`git cz`コマンドによるコミットが可能です。
`git cz`を利用するにはgit-czをインストールする必要があります。

git-czはJavaScriptで開発されたツールで、npmでインストールします。
```bash
npm i -g git-cz
```

インストール後は`git commit`の代わりに `git cz`コマンドでコミットできるようになります。
`git cz`の詳しい使い方は自分で調べてください。
